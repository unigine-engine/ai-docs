# Runtime Files in Detail


The [Assets and Runtime Files](../../editor2/assets_workflow/assets_runtimes.md) article introduces runtime files: UNIGINE-native files generated from non-native assets and consumed by the Engine at run time. This article goes deeper: how runtime files and their GUIDs are organized on disk, why references in materials and other files point at runtime GUIDs rather than at source assets, what `guids.db` does and does not contain, when the Editor regenerates runtime files, and how to handle runtimes in version control and automated builds.


> **Notice:** A runtime file is always in a UNIGINE native format, but that format is not necessarily binary: for example, `.node` and `.prop` runtime files are XML-based text files.


## Where Runtime Files Live


Runtime files are stored in a `.runtimes` folder at the root of the [mount point](../../principles/filesystem/index_cpp.md#mount_points) that contains their source asset: for regular project content that is `data/.runtimes`, and for content added via a mount point it is the `.runtimes` folder of the mounted folder itself. A runtime file is always generated in the same mount as its source asset, never in another one.


Inside `.runtimes`, files are laid out in subfolders named by the first two characters of the runtime's GUID, and each runtime file is accompanied by its own meta file:


```text
.runtimes/
	d1/
		d161d566696f0cb86a8bff171e76e4ebca319a94.texture
		d161d566696f0cb86a8bff171e76e4ebca319a94.texture.meta
```


**The file name of a runtime file is its GUID.** This is the reverse of the rule for source assets, where the GUID is stored next to the file: for a runtime file the Engine derives the GUID directly from the name, with no database lookup involved. For the same reason, runtime files must never be moved out of the `.runtimes` folder or renamed by hand.


Do not confuse runtime files with cache files. Runtime files are generated content: they are products of their source assets, meant to be stored and shipped (see [below](../../editor2/assets_workflow/runtimes_in_depth.md#versioning)). Cache folders and files � such as the `data/.cache_textures` folder and `*.cache` / `*.gpu_cache` files � are machine-local acceleration data: they can be deleted and regenerated freely and belong in the [version control ignore list](../../editor2/assets_workflow/version_control/index.md), not in the repository.


## GUIDs and Meta Files


The GUID of an asset does not depend on its path or file name: it is randomly generated when the asset is registered, and if the generated value collides with an already known GUID, another value is simply generated instead. Once assigned, the GUID does not change: renaming or moving an asset (together with its `*.meta` file) keeps its GUID and all references to it intact.


### Source Asset Meta Files


The `*.meta` file of a source asset is an XML file. For an imported texture asset with a generated runtime it looks like this:


```text
<?xml version="1.0" encoding="utf-8"?>
<asset version="2.22.0.0">
	<guid>7bee413711bf15dd4127235ed304c9cd150f83c8</guid>
	<type>texture</type>
	<hash>ba09bfcb</hash>
	<runtimes>
		<runtime id="7bee413711bf15dd4127235ed304c9cd150f83c8" name="brick_black_04_b_alb.png" link="0" type="6"/>
		<runtime id="538a62d5301d81933ba640fae299f39c5b425487" name="brick_black_04_b_alb.texture" link="1" type="6"/>
	</runtimes>
</asset>
```


The **<runtimes>** section lists the files the asset resolves to:


- The mandatory entry with **link="0"** represents the source file itself: its **id** is the asset's GUID. This is the entry the Engine reads to learn the GUID of the file when no `guids.db` record is available. A native asset that needs no runtime files has only this entry.
- Optional entries with **link="1"** represent generated runtime files stored in the `.runtimes` folder; the **id** of such an entry is the runtime's GUID, i.e. its file name. These GUIDs are file IDs from the Engine's file system. The numeric **type** attribute is an internal asset-type code mirroring the **<type>** element; the Engine does not read it.


**Materials and properties are an exception.** When a runtime entry points to a `.mat` or a `.prop` file, its **id** is the ID of the material or the property itself � the **guid** stored inside that file � rather than a file system ID. For such an entry the **id** does not match the runtime's file name, and this is the normal state, not a defect: when tracing such a reference, look for the GUID inside the `.mat` / `.prop` file. This is what lets a material keep its identity when its file is regenerated.


For an imported (non-native) asset the meta file additionally stores a hash covering the source file and its import settings (the **<hash>** element above), and the import parameters themselves. The hash is what the Editor checks to decide whether the runtimes are still up to date (see [below](../../editor2/assets_workflow/runtimes_in_depth.md#generation)).


### Runtime Meta Files


The meta file that accompanies a runtime file is a JSON file, not XML:


```text
{
	"asset": "7bee413711bf15dd4127235ed304c9cd150f83c8",
	"alias": "brick_black_04_b_alb.texture",
	"primary": 1,
	"version": "2.22.0.0",
    "parameters": {
        "UnigineEditor.AssetHash": "8fc56dce"
    }
}
```


It stores:


- the GUID of the source asset the runtime belongs to (this link, together with the runtime's file name, is all the Engine needs � which is why runtime files are not listed in `guids.db`);
- the runtime's name ([alias](../../principles/filesystem/index_cpp.md#alias)) relative to the asset;
- a flag marking the [**primary** runtime](../../principles/filesystem/index_cpp.md#primary_runtime) � the one the asset resolves to when it is referenced by a plain path or GUID;
- the SDK version the runtime was generated with � a diagnostic marker: it tells which SDK actually generated the file, letting you verify that an expected reimport really took place;
- a copy of the hash from the source asset's meta file, stored here by the Editor so that validity can be checked without hashing the (potentially large) runtime file itself;
- optional generation parameters.


To sum up the two kinds of meta files:


|  | Asset Meta File | Runtime Meta File |
|---|---|---|
| Format | XML | JSON |
| Location | Next to the source asset, named `<asset>.<ext>.meta` | Next to the runtime file in `.runtimes`, named `<guid>.<ext>.meta` |
| Contents | Asset GUID and type, hash calculated for the (*source file + import settings*) combination, the list of runtime entries, import parameters themselves | GUID of the source asset, runtime name (alias), primary flag, SDK version, a copy of the asset hash, optional generation parameters |


## Why References Point at Runtime GUIDs


When you inspect a material in the Editor, texture references in it may show the GUID of a runtime file (displayed in red) rather than the GUID of the source asset. **The red color here does not indicate an error:** for a reference that points at an existing runtime file this is the expected state, and it is the result of a deliberate GUID exchange the Editor performs when it creates a runtime:


1. Initially the source asset owns some GUID **A**, and everything that uses the asset references **A**.
2. When a runtime file is generated for the asset, the Editor assigns a new GUID **B** to the source asset and hands the original GUID **A** over to the runtime file.
3. All existing references to **A** now point at the runtime file � which is exactly what the Engine should load at run time, so no reference needs rewriting.
4. If the runtime file is later removed (for example, the asset is switched back to the [Unchanged](../../editor2/assets_workflow/assets_create_import.md#unchanged) mode), the GUID **A** is returned to the source asset, and the references stay valid again.


At run time the Engine resolves references in both directions: a plain path or GUID is transparently resolved to the primary runtime file, while a path prefixed with `asset://` resolves to the source asset instead (see [Accessing by Path](../../principles/filesystem/index_cpp.md#access_path)). A reference is actually broken only when its GUID resolves to nothing � neither a runtime file nor a source asset (see [Finding and Fixing Runtime Issues](../../editor2/assets_workflow/runtimes_in_depth.md#troubleshooting)).


## guids.db


The `guids.db` file maps GUIDs to the paths of **source assets** in its mount point; every mount point can carry a `guids.db` of its own, and these databases are loaded before any other file of the mount. The database deliberately omits:


- runtime files � the GUID of a runtime file is its file name, so the Engine always knows it without any database, and the link to the source asset is stored in the runtime's meta file, which is read anyway;
- meta files and the `guids.db` file itself;
- anything matched by the mount's [guids.db ignore filters](../../principles/filesystem/index_cpp.md#guidsdb_ignore_filters).


If `guids.db` is missing or skipped (the `-skip_guidsdb` [command-line option](../../principles/filesystem/index_cpp.md#guids)), the Engine falls back to reading the GUID of each file from its `*.meta` file.


## Generation and Reimport


Runtime files are produced by the Editor's import pipeline. On every start (and whenever a new mount point is added) the Editor validates the existing runtimes against their source assets instead of blindly regenerating them: it compares the hash stored in the source asset's meta file with the copy of that hash stored in the runtime's meta file. If the hashes do not match � the source file or its import settings have changed � the **reimport stage** starts and the runtimes of the asset are regenerated. The same happens when you press *[Reimport](../../editor2/assets_workflow/assets_create_import.md#import_settings_change)* manually. A running Editor does notice when the source file of an asset is modified or replaced, and reimports that asset (see [real-time tracking of changes](../../editor2/assets_workflow/assets_create_import.md#tracking)). What is not performed while the Editor is running is the full validation pass over the existing runtime files: re-checking them on the fly is not supported. So, it's recommended to close the Editor before any bulk external changes (for example, switching a branch in your version control system), make those changes, and then open the Editor again to revalidate them.


Hash-based validation has a limit: a runtime file that is present but corrupted (for example, by a faulty merge or an interrupted transfer) still passes the check � the hashes in the two meta files match � and manifests only as a load error. Such a runtime is not detected or repaired automatically; it is fixed only by reimporting the asset.


Moving an asset has the following effects on its runtimes:


- Moving an asset (with its `*.meta`) to another folder **within the same mount point** requires no regeneration: GUIDs do not depend on paths.
- Moving an asset **to another mount point** (when the Editor is closed) removes its runtime files from the old mount and regenerates them in the new one on the next Editor start (runtimes always live in the same mount as their asset).
- Moving an asset **outside of any mount point** (when the Editor is closed) leaves its runtime files orphaned; the [Cleaner](../../editor2/cleaner/index.md) either removes such a runtime, if nothing references it, or reports it as lost.


> **Notice:** Moving an asset from/to any mount point **when the Editor is opened** moves its runtimes together as well, **no regeneration required**.


Texture runtimes are generated on the GPU where possible � this only makes the import faster. The result is expected to be the same, although hardware- and driver-specific factors may affect it, so a runtime regenerated on different hardware is not guaranteed to be byte-identical. Keep in mind also that on a machine without GPU access (a typical virtual build server) the same import falls back to the CPU and can take dramatically longer.


When a GPU-ready format such as `.dds` is imported, the data is fully re-encoded into the `.texture` runtime � there is no path that takes the ready-made compressed blocks as is, which is why the first import of a large legacy texture set is expensive. Keeping `.dds` files as native assets via the [Unchanged](../../editor2/assets_workflow/assets_create_import.md#unchanged) option is not recommended: at the very least, mipmap streaming is not supported for `.dds` files.


> **Notice:** The `.runtimes` folder is a mandatory part of a UNIGINE-based project: if you delete it (or check out a repository that does not include it), the Editor will regenerate all runtime files on the next start, which may take a lot of time.


## Runtimes on Read-Only Mounts


A [mount point](../../principles/filesystem/index_cpp.md#mount_points) is read-only unless its `*.umount` file explicitly sets **"readonly": false**. The file system only reads from such a mount, so the Editor cannot create runtime files there at all. Prepare the runtimes in advance: generate them while the folder is still mounted as writable (or in the source project the mounted content comes from), publish them together with the content, and only then consume the mount as read-only.


If a non-native asset on a read-only mount has no runtime files, the Editor considers such an asset invalid and does not allow working with it in the Editor UI. The Engine, however, simply loads files from a read-only mount point as they are: if a file references a source asset or a runtime file from this mount point, rendering and logic will work fine.


## Version Control and CI


Store runtime files in your version control system and commit them together with their assets � this is how UNIGINE's own content repositories are managed (see the recommended [version control setup](../../editor2/assets_workflow/version_control/index.md)). Committed runtimes do not have to be trusted blindly: the Editor [compares the stored hashes](../../editor2/assets_workflow/runtimes_in_depth.md#generation) on every start, so even if an asset and its runtime files get out of sync in the repository, the outdated runtime files are simply regenerated.


Committing runtimes increases the repository size, but it pays off:


- a fresh checkout opens without the (potentially very long) initial generation of all runtime files;
- build machines without GPU access do not have to regenerate texture runtimes on the CPU � a stronger workstation generates them once, and every other machine reuses the committed result;
- content on read-only mounts stays usable, since runtimes cannot be generated there on the fly.


One thing no mechanism resolves for you is a concurrent import: when two people import the same new asset independently, each machine generates its own GUIDs, meta files, and runtime files, and merging the two results is always an ordinary version-control conflict. There is no automatic reconciliation � the team decides whose changes to keep, taking that side's asset, meta, and runtime files together.


Other conflicts are easier. A conflicting or corrupted runtime file can always be resolved by deleting the runtime together with its meta file � the Editor regenerates them on the next start, at the cost of the import time. As for `guids.db`, whether to commit it is up to the project; UNIGINE's own projects always commit it, because a packaged application launched from `bin/` needs this file to start without problems. Conflicts on it are frequent and are routinely resolved by taking the most recent version: UnigineEditor always re-generates the file to ensure its validity, and an invalid `guids.db` committed as a result of an incorrect merge can be [ignored and rebuilt](../../principles/filesystem/index_cpp.md#ignore_guidsdb).


For pipelines that cannot run the Editor, runtime files can be generated by the console [Runtimes Generator](../../tools/runtimes_generator/index.md) tool, and project assembly is automated via the [command-line build](../../editor2/projects/build_ci.md).


## Runtime Files in Final Builds


A [final build](../../editor2/projects/build_project.md) ships the runtime files together with their meta files and `guids.db`; source assets that have runtimes can be excluded from the build. In this case `guids.db` still lists the source assets with their GUIDs: the Engine's virtual file system keeps treating them as present, so they remain visible to file iteration and resolvable by GUID, even though physically only the runtime files exist. A reference to such an asset is resolved to its runtime through the GUID mechanism described above.


## Finding and Fixing Runtime Issues


To find the runtime files of an asset, right-click the asset in the Asset Browser and choose *[Show Runtime in Explorer](../../editor2/interface/context/index.md#show_runtime)*. The `assets_info` and `assets_list` console commands print statistics and the full asset-to-runtime list (file path and alias) at run time.


To find the asset a runtime file belongs to, open the runtime's `*.meta` file and take the source asset GUID from its **asset** field; then resolve that GUID to a path via `guids.db` (a plain GUID-to-path map, stored as JSON or in an equivalent binary form) or by searching the asset `*.meta` files, or simply look the GUID up in the `assets_list` output.


If a reference is genuinely broken (its GUID resolves to nothing), check the following: a runtime file that is missing from `.runtimes` is regenerated on the next Editor start; runtime files whose asset is gone are reported by the [Cleaner](../../editor2/cleaner/index.md) as lost; and if `guids.db` itself is invalid (for example, after an incorrect merge), it can be [skipped and re-generated](../../principles/filesystem/index_cpp.md#ignore_guidsdb). A runtime file that is present but corrupted passes the hash validation and shows up only as a load error � reimport the asset (or delete the runtime together with its meta file) to regenerate it.


## See Also


- *[Assets and Runtime Files](../../editor2/assets_workflow/assets_runtimes.md)* � the overview of runtime files and the asset-to-runtime type table.
- *[File System](../../principles/filesystem/index_cpp.md)* � GUIDs, mount points, and accessing assets and runtime files from code.
- *[Creating and Importing Assets](../../editor2/assets_workflow/assets_create_import.md)* � import options, the Unchanged mode, and reimport.
- *[Version Control](../../editor2/assets_workflow/version_control/index.md)* � what to commit and what to ignore.
- *[Project Files](../../editor2/assets_workflow/project_files.md)* � the reference of project folders, including `.runtimes` and the cache folders.
- *[Runtimes Generator](../../tools/runtimes_generator/index.md)* � generating runtime files without the Editor.
- API classes:

  - *[FileSystem Class](../../api/library/filesystem/class.filesystem_cpp.md)*
  - *[FileSystemAssets Class](../../api/library/filesystem/class.filesystemassets_cpp.md)*
