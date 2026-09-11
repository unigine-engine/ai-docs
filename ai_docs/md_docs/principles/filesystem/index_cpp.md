# File System (CPP)


UNIGINE has its own file system module used to access files and folders. It has a few peculiarities you should be aware of, when loading resources or organizing the structure of your UNIGINE-based project.


## GUIDs


In UNIGINE's file system, each file has a *GUID* (Globally Unique Identifier), which defines a [virtual path](#scanning) to this file (not a file on a disk). Using GUIDs provides more flexible file management: you can abstract from file names (which can be the same in different folders of the project). For example, you can change a path to the file while keeping the same GUID.


The Engine generates GUIDs for all files of the [virtual file system](#scanning).


Files of UNIGINE's file system can be accessed by using both **names** or **GUIDs**: you can [obtain](../../api/library/filesystem/class.filesystem_cpp.md#getGUID_cstr_UGUID) a GUID for the specific file, [change](../../api/library/filesystem/class.filesystem_cpp.md#setGUID_cstr_UGUID_bool) the file GUID, [add](../../api/library/filesystem/class.filesystem_cpp.md#addCacheFile_UGUID_bool)/[remove](../../api/library/filesystem/class.filesystem_cpp.md#removeCacheFile_UGUID_bool) the file with the certain name or GUID to/from a blob or a cached file, and so on.


> **Notice:** To manage GUIDs via API use the *[UGUID](../../api/library/filesystem/class.uguid_cpp.md)* class.


If UnigineEditor is loaded, it saves generated GUIDs to the `data/guids.db` file automatically. Otherwise, you can implement the logic of [updating](../../api/library/filesystem/class.filesystem_cpp.md#saveGUIDs_cstr_bool_bool) `guids.db` via code. The `guids.db` file stores a pair: a GUID of a file and a path to this file relative to the `data` folder.


As UNIGINE's file system provides **[mount points](#mount_points)** to extend the project, there can be several `guids.db` files within a single project. Each mount point can store its own `guids.db`: GUIDs for external files aren't written to `data/guids.db`. For each mount point you can also define [wildcard-based ignore filters](#guidsdb_ignore_filters) (e.g., *"*.tmp", "cache_*/", "dir*/*1*.world", "editor_[1-9]*.log"* etc. - [read more about wildcards](../../principles/filesystem/wildcards.md)), to prevent unnecessary or temporary files from being tracked or assigned GUIDs, keeping your `guids.db` file organized and relevant, without unnecessary bloating.


Deleting the `guids.db` file won't cause any issues: if there is no `guids.db` file, the Engine will search among `.meta` files. However, `guids.db` might be necessary for the final release build of the project, if you aren't going to include the `.meta` files.


### Ignore Option for guids.db


Sometimes in case of teamwork development, an invalid `guids.db` file may be committed to the repository (due to an incorrect merge or otherwise) causing errors when working with [UnigineEditor](../../editor2/index.md). You can make the Engine ignore the `guids.db` file via the [`-skip_guidsdb`](../../code/command_line.md#skip_guidsdb) startup command line option. In this case, the Engine searches for GUIDs among all `.meta` files inside the `data` folder and all [mounted](#mount_points) external directories and packages. UnigineEditor uses this argument by default to avoid errors, and always re-generates the `guids.db` file to ensure its validity.


## File System Update


### Dynamic Scanning


Dynamic scanning allows the Engine to form a *virtual file system* for all files within the `data` folder (including the ones inside [mount points](#mount_points)). Dynamic scanning is performed on the Engine start-up. For files physically stored inside the `data` folder, file changes tracking is enabled in real time using [relative](#relative_absolute) paths to address files.


If changes to the file system are made not by means of UnigineScript, you may need to call the *[filesystem_reload](../../code/console/index.md#filesystem_reload)* console command.


### Automatic Resource Reloading


When UnigineEditor is loaded, it tracks changes made in files at run time: it checks [the time of the last modification](../../api/library/filesystem/class.filesystem_cpp.md#getMTime_cstr_llong) of such files and updates them in the memory. If UnigineEditor isn't loaded, the changed files are reloaded after [reloading the world](../../code/console/index.md#world_reload).


> **Notice:** However, it is possible only if files are [added to the virtual file system](#scanning) (dynamic scanning has been performed on the start-up).


### Known vs Unknown Files


If you add new files at run time, the Engine won't know anything about such files (as the virtual file system has been [formed](#scanning) on the start-up). Re-scanning the file system is resource-consuming, therefore, you can add new files to the virtual file system via API by using *[addVirtualFile()](../../api/library/filesystem/class.filesystem_cpp.md)*.


## Data Directory


All files used by the Engine at run time are stored in the `data` folder specified via the *[-data_path](../../code/command_line.md#data_path)* start-up option. By default, this is the `data` folder created automatically on project creation via [UNIGINE SDK Browser](../../sdk/projects/index_cpp.md#creation).


> **Notice:** The path to the data folder can be specified relatively to the binary executable or as an absolute path.


When the file system resolves paths, it tries to concatenate [data paths](#data_dir) with the specified path and perform a lookup. In case of absolute paths, the file system will use them "as is" without any checks.


> **Notice:** When the path to the `data` folder is relative, the engine switches the [current folder](#current_dir) to the folder with the binary executable.


For example, if the project folder has the following structure:


- ![](folder.png) **unigine_project**

  - ![](folder.png) **bin**
  - ![](folder.png) **data**


The data path will be `unigine_project/data` after the application start-up:


```bash
bin\main_x64d.exe -data_path "../"
```


> **Notice:** A path specified in the *-data_path* option won't be written into the configuration file.


### Current Directory


When the specified *-data_path* is absolute, the current working directory may differ from the directory with the binary executable. However, when the path to the data directory is relative, the Engine switches the current directory to the one with the binary executable.


When accessing a file outside the `data` directory via API, the path to such file should be specified relative to the current directory. For example:


```cpp
// cbox.mesh is stored outside the data directory, so the path is specified relative to the current directory
ObjectMeshStaticPtr cbox = ObjectMeshStatic::create("../../data/cbox.mesh");

```


### Root Mount File


The building block of the virtual file system is a **mount**: the file system is created as a root mount and can be easily extended by using additional **mount points**. This approach allows [extending](#mount_points) the virtual file system of your project by adding any external folders and packages to the data directory.


At project creation, the `root_mount.umount` file is created in the `data` folder. This is a file in the JSON format that represents the root mount point. It stores the version of UNIGINE SDK, in which the root mount has been created, ignore filters (**ignore_filters**) i.e., indication to **folders** that should be ignored, and GUIDs database ignore filters (**guidsdb_ignore_filters**) preventing certain files or directories (unnecessary or temporary) from being stored in the GUIDs database, keeping your guids.db file organized and relevant, without unnecessary bloating:


```text
{
	"ignore_filters": [
		".svn/*",
		".git/*",
		".teamcity/*",
	],
	"guidsdb_ignore_filters": [
		"*.gpu_cache",
		"*.meta"
	]
}

```


The `root_mount.umount` file already contains default ignore filters and the list can be extended as necessary using wildcards (e.g., *"*.jpg", "some_folder_*/", "dir*/*1*.world", "editor_[1-9]*.log"* etc. - [read more about wildcards](../../principles/filesystem/wildcards.md)).


The path is set relative to the `data` folder. If a folder that should be ignored is located inside any other folder (for example `data/folder_1/.svn`), the relative path to that folder should be set as an ignore filter (`folder_1/.svn/`).


> **Notice:** Folder filters must end with a slash symbol (**"/"**).


If a project does not contain the `root_mount.umount` file (the project was created with a previous version of UNIGINE SDK or the file has been deleted), the project runs without ignoring any folders in `data`.


The `root_mount.umount` file can be created manually or via code using [API](../../api/library/filesystem/class.filesystemmount_cpp.md).


## File Packages


### Types


UNIGINE supports the following types of file archives to save space or pack the production version of resources:


- **UNG** (a UNIGINE-native format for archives created with *[Archiver](../../tools/archiver/index.md)* tool)
- **ZIP**
- Custom **[C++ packages](../../api/library/filesystem/class.package_cpp.md)** created via UNIGINE API


Besides saving space, archives also speed up resource loading, as files in an archive are read linearly.


UNG and ZIP archives are loaded automatically if they are located within the `data` folder. Files are added to the [virtual file system](#scanning) the same way as non-archived files.


> **Notice:** A package cannot store another package. Also a [mount point](#mount_points) cannot be packed. However, it can refer to a package.


### Content Access


Archives are completely transparent to the Engine. There is no need to explicitly unpack the archives, as their content is automatically handled as not packed. Archived files are addressed as if they are non-archived. For example, if you have `data/project/archive.ung` and want to address `directory/file.txt` within it, simply specify the following path: `project/directory/file.txt`.


Inside the archive, files can be organized in any way. However, in the root of the archive only files with unique names should be placed. Otherwise, the file search will return incorrect results.


> **Notice:** Using GUIDs allows you to avoid the need to control uniqueness of names when working with archived files.


Here is an example of an **incorrect file tree** for an archive:


- ![](folder.png) `my_archive.ung`

  - ![](folder.png) `my_folder`

    - ![](file.png) `file_2.txt`
  - ![](file.png) `file_1.txt`
  - ![](file.png) `file_2.txt`


In this case, there is no problem with `file_1.txt`, since its name is unique. `file_2.txt`, on the other hand, will cause problems: it does not guarantee that a non-root file will be returned.


The correct archive structure can be specified as follows:


- ![](folder.png) `my_archive.ung`

  - ![](folder.png) `my_folder`

    - ![](file.png) `file_2.txt`
  - ![](folder.png) `another_folder`

    - ![](file.png) `file_2.txt`
  - ![](file.png) `file_1.txt`


In this case, the files with the same names are stored in different directories, so the file search will be perfectly correct.


If there is a name collision between an archived file and a non-archived one, the first matching file is returned. The search is performed in the following order:


1. Non-archived files
2. Files in UNG archives
3. Files in ZIP archives


From UNIGINE API, archives are handled using the *[FileSystem](../../api/library/filesystem/class.filesystem_cpp.md)* functions as well.


## Extending File System


The virtual file system can be easily extended by using the **mount point** feature. It allows you to extend the virtual file system of your project by adding any external folders and packages to the data directory.


Using the mount points in your project allows you to use content stored:


- In a single folder or repository for several projects.
- In several folders for one project. You can create as many mount points as required for the project.


A UNIGINE-based project has a single `data` directory. Here all project assets and runtime files are stored. In addition, the `data` folder can store mount points created via the Asset Browser (*Create Mount Point*) or [API](../../api/library/filesystem/class.filesystem_cpp.md).


A mount point is represented on the disk as a `*.umount` file: a file in the JSON format that stores a reference to an external directory or package as an absolute path or a path relative to the current directory. Also the `*.umount` file stores information on whether the mount is read-only or not.


By default, **all files and folders** in your UNIGINE-project are considered to be **in the whitelist**. To exclude certain files or directories, you can define **ignore_filters** (blacklist). When you need to override ignore rules and make specific exceptions, you can use **exclusive_filters** (exceptions from the blacklist), which un-ignore listed files or directories. These filters can be specified using wildcards (e.g., *"*.jpg", "some_folder_*/", "dir*/*1*.world", "editor_[1-9]*.log"* etc. - [read more about wildcards](../../principles/filesystem/wildcards.md)) to selectively add files of certain types or contents of folders with certain names, or on the contrary, to ignore the ones specified).


> **Notice:** Wildcard patterns can be **relative** (no leading slash) or **absolute** (starting with `'/'`).
>
>
> - A pattern without a leading slash may match at any directory depth.
> - A pattern with a slash at the beginning or middle is relative to the directory level of the mount point configuration (the `*.umount`file).


You can also use GUIDs database ignore filters (**guidsdb_ignore_filters**) preventing certain files or directories (unnecessary or temporary) from being stored in the [GUIDs database](#guids), keeping your `guids.db` file organized and relevant, without unnecessary bloating. For example:


```text
{
    "data_path": "D:/mount_test",
    "readonly": false,
	"ignore_filters": ["*.jpg","*.prop"],
	"guidsdb_ignore_filters": [
		"*.gpu_cache",
		"*.meta"
	]
}

```


> **Notice:** Use only **forward slashes for paths** (Unix convention) as backslashes in JSON files are used as escape characters.


Each mount point has its own independent set of rules (filters). Rules are not inherited � a **nested mount point does not reuse the rules from its parent mount point**.


All folders inside the mount point are treated by the file system as usual folders with assets inside the `data` directory.


Inside each mount point, there is a `.runtimes` folder that stores runtime files generated for assets of the external directory. Note that they aren�t added to the runtimes stored inside the `data/.runtimes` folder. If you move an asset from one mount point to another, its runtime will be moved as well.


GUIDs for external files aren't written to `data/guids.db`.


If several team members work with a single mount point, it should be **read-only** to avoid issues.


The **read-only** mount point doesn�t allow any changes in the folder or package it is referenced to. It means that such folder must store assets with already generated `.meta` files and runtimes. Otherwise, they won�t be available in the Asset Browser. The workflow here should be as follows:


1. The `.meta` and runtime files for assets are generated once and saved/committed to the folder/repository (if any).
2. In each project that uses the assets from this folder/repository, the read-only mount point is created. The assets are used "as is", without opportunity to somehow modify them.


> **Notice:** All `.meta` files and runtimes in the mounted directory/package **must be valid and up-to-date**. All assets that were not properly migrated, as well as the ones having outdated `.meta` or runtime files will be unavailable and won't be displayed.


When working with mount points, there are rules to be followed:


- Mount points can be embedded: a folder referenced by a `*.umount` file can store another `*.umount` file, etc. However, looped mount points are not allowed: you cannot create the `2.umount` inside the `1.umount` that refers to `1.umount`.
- `*.umount` files cannot be packed, as well as packages cannot store another packages. However, the `*.umount` file can refer to a package.
- `*.umount` file should have a unique name. If the `data` folder contains a folder with the same name as the mount point, this mount point will be ignored.


When UnigineEditor is loaded, [automatic resource reloading](#reloading) isn�t available for mount points. Each mount point is updated manually on demand: in the Asset Browser, right-click the mount point and choose *Refresh Mount Point*. When UnigineEditor isn't loaded, the Engine reloads all resources, **including the ones stored inside mount points**, after [reloading the world](../../code/console/index.md#world_reload) if resources are added to the virtual file system.


## Paths


The Engine accepts the [relative, absolute](#relative_absolute), [network](#network_paths), and [virtual](#virtual_paths) paths.


> **Notice:** UNIGINE's file system features path normalization: it automatically converts Windows paths to UNIX paths.


### Virtual Paths


UNIGINE's file system is *strict*. It means that the virtual file system always checks the exact file location instead of searching somewhere inside the `data` directory. Such approach makes working with project files clear and transparent.


The virtual file system operates with *virtual paths* to files. A virtual path is a path to a file inside the `data` folder (including files in [mount points](#mount_points)). The Engine always tries to convert any path to a virtual one. There are several types of virtual paths:


- Full virtual path - a path to a file inside the `data` folder
- [Partial](#partial) virtual path
- Virtual path specified as an [absolute](#absolute_virtual) one


When specifying a virtual path to a file inside the mount point, it always includes the name of the mount point. For example, if you have a `data/external_images.umount` mount point, that refers to `D:\external_content`, you should access any file in this folder as follows:


```text
external_images/1.tga

```


#### Partial


Using partial paths means that the file system performs a non-strict file search. In this case, only a file name can be provided without a path. Partial paths are allowed for cases where the user can enter a path manually, such as:


- World loading operations. You can specify only a world name and it will be found and loaded.
- Including paths in the source code.
- Paths in [UI files](../../code/gui/ui/index.md).
- Paths in [manual material files](../../content/materials/index.md#manual_internal_materials).
- Paths to textures in [base material files](../../code/formats/materials_formats/ulon_base_material_format.md).
- Paths to font files.


> **Notice:** If a name is not unique, the first found file with such name is loaded.


It is also possible to provide a sub-path that uniquely specifies a file. For example, to load `data/project/my_world/my_world.world`, you can use `my_world.world` (if a name is unique) or `my_world/my_world.world`.


Also you can refer files by [GUIDs](#guids) to uniquely specify a file.


> **Notice:** A partial path can be resolved via the *resolvePartialVirtualPath()* method of the FileSystem class. It converts the given partial virtual path to the full virtual one, and then it can be processed as required.


#### Virtual Path Specified as Absolute


The Engine can resolve paths that are specified as absolute, but actually are virtual. It means that the path to a file can look like absolute, but physically there is no such file by this path.


For example, there is a project stored in the `D:/projects/unigine_project/` folder. In the data folder of this project, there is a `test.umount` that refers to a `D:/content/test/` folder with the `1.tga` texture. You can specify the path to this texture as absolute as follows and the Engine will be able to return a virtual path for it.


```cpp
getVirtualPath("D:/projects/unigine_project/test/1.tga"); // returned: test/1.tga

```


If you try to get an absolute path, the absolute path `D:/content/test/1.tga` will be returned.


```cpp
getAbsolutePath("D:/projects/unigine_project/test/1.tga"); // returned D:/content/test/1.tga

```


To get more usage examples on the *getVirtualPath() / getAbsolutePath()* methods, check the article on the *[FileSystem](../../api/library/filesystem/class.filesystem_cpp.md)* class.


### Network Paths


A lot of heavy content used in a project is usually stored on a network drive. To access such content, a *network path* should be specified in the following format:


```text
//share/content/1.tga

```


The network paths are successfully resolved by the file system.


You can create a mount point that refers to a network folder. It allows you to avoid unnecessary copying of assets to a local computer and, therefore, saves the disk space.


### Relative vs Absolute


A *relative path* is a path specified relative to the current directory. It should be used when, for example, you need to write some file in the same folder with the binary executable. If you specify a virtual path, it will be written into the `data` directory by default.


When relative paths are used, you can relocate your UNIGINE-based application or copy it onto another machine, and all resources will be properly loaded. There is no loading speed penalty as well: it is as fast as loading files by an absolute path due to the [virtual file system](#scanning). It is possible to use absolute paths to load resources outside the `data` folder, but such project will not be portable.


As file names are added to the [virtual file system](#scanning), usually the same name and path should be used to load and remove the file when accessing from your source code by using [FileSystem](../../api/library/filesystem/class.filesystem_cpp.md) functions:


- For default resources, functions return full paths relative to the `data` folder.
- If you load a file and specify a relative path, use a relative path to delete the resource.
- If you load a file using an absolute path, use an absolute path to delete the resource.


> **Notice:** Using GUIDs allows you to avoid the necessity to control paths when working with files.


You can check whether a path is absolute or relative via the *[isAbsolute()](../../api/library/filesystem/class.dir_cpp.md#isAbsolute_cstr_int)* function.


The file system also allows you to get a path to a file relative to the `data` folder by using the *[getVirtualPath()](../../api/library/filesystem/class.filesystem_cpp.md#getVirtualPath_cstr_String)* function.


## Loading Priorities


The Engine resolves any path as follows:


1. It tries to convert the path to a full virtual one.
2. It tries to get the current mount point by this path.


By using the obtained information on the path, the Engine can get a real path to the file on the disk (or blob/package/cache).


A virtual path can represent up to four entities at the same time: it can be a file on the disk, a file stored in a [package](../../api/library/filesystem/class.filesystem_cpp.md#isPackageFile_cstr_bool), a file added to a [cache](../../api/library/filesystem/class.filesystem_cpp.md#isCacheFile_UGUID_bool) and to a [blob](../../api/library/filesystem/class.filesystem_cpp.md#isBlobFile_UGUID_bool).


> **Notice:** A [GUID](#guids) is generated for a virtual path: neither a file on the disk, a package file, a cached or a blobbed file can have a GUID.


For example, the `textures/white.texture` path has only one GUID, however, it can represent the following at the same time:


- Within the project folder, you can have both `core/textures/white.texture` and `core.ung/textures/white.texture`.
- In addition, in code, you can have both: ```cpp // the file loaded into a cache FileSystem::addCacheFile("core/textures/white.texture"); // the file loaded into a blob FileSystem::addBlobFile("core/textures/white.texture"); ```


> **Notice:** You can check whether a virtual path or a GUID represents a certain entity via the [corresponding API methods](../../api/library/filesystem/class.filesystem_cpp.md#isPackageFile_cstr_bool).


During *read / write* operations, the Engine will load the first found entity for such virtual path. The entities are checked in the following order:


- For *read* operations:

  1. The file loaded into a blob.
  2. The file added into a cache.
  3. The read-only file stored on the disk.
  4. The file stored in a package.
- For *write* operations: > **Notice:** Cached and packed files aren't checked as *write* operations aren't allowed for them.

  1. The file loaded into a blob.
  2. The file stored on the disk.


## Accessing Assets and Runtime Files


Working with assets via UnigineEditor is clear and simple, but in order to access your project files properly you should have a clear understanding of the concept of [asset and runtime files](../../editor2/assets_workflow/assets_runtimes.md).


Generated runtime files have constant GUIDs and are named as follows:
 `<GUID>.<extension>` (e.g., `ab23be4cd7832478edaaab23be4cd7832478edaa.texture`).


These files are stored in sub-folders of the [`data/.runtimes`](../../editor2/assets_workflow/project_files.md#data_runtimes_folder) folder. The structure of this folder is optimized for the file system.


> **Notice:** Inside each **mount point**, there is also a `.runtimes` folder that stores runtime files generated for assets of the external directory. These runtimes aren�t added to the runtimes stored inside the `data/.runtimes` folder. If you move an asset from one mount point to another, its runtime will be moved as well.


A runtime file generated for a non-native asset with a certain [GUID](#guids) is placed in a folder that has a name equal to the first two bytes of this GUID.


> **Notice:** A sub-folder of the `data/.runtimes` folder may contain runtime files generated for different assets (if these assets have matching first two bytes in their GUIDs).


E.g., your non-native asset `data/my_textures/1.tga` will have runtime file (with a name corresponding to runtime's GUID) generated for it in a folder: `./runtimes/ae/aeb53b44cdbbbbbbbbaaabccc1c1c1c1c1c1c1c1.texture`


Therefore each runtime file has an **alias** - a human-readable form of a path used to refer to this file.


Full aliases are constructed as follows: *`<source_asset_path>`/<runtime_alias>*


E.g.:

- `1.tga`/1.texture
- **1.fbx**/1.mesh


In order to simplify access to runtime files, we also use a concept of the **primary runtime** - a runtime file uniquely assoсiated with the asset. It acts like an implied reference to a runtime file: *when we say "model.fbx", we actually mean "model.node"*. So, that we could write:


```cpp
NodeReferencePtr node = NodeReference::create("model.fbx");
```


> **Notice:** Primary runtime is actually used instead of a non-native asset, when you refer to it by path.


There are two ways you can access your assets and runtime files:


- [Using a GUID](#access_guid)
- [Using a path](#access_path)


The file system includes a subsystem for managing assets and runtime files. This subsystem is implemented as a separate class named *[FileSystemAssets](../../api/library/filesystem/class.filesystemassets_cpp.md)*.


You can use `assets_info` and `assets_list` console commands to view information on non-native assets and runtimes generated for them.


### Accessing by Path


The way of accessing a certain asset by path is determined by its type:


- [**Native assets**](../../editor2/assets_workflow/assets_runtimes.md) are accessed simply by their name: ```cpp ImagePtr image = Image::create("image.texture"); ```
- All [**non-native assets**](../../editor2/assets_workflow/assets_runtimes.md) have a [primary runtime](#primary_runtime) file. So, when you refer to the asset by its name, this primary runtime file will be actually used. For example, if you specify: ```cpp ImagePtr image = Image::create("image.png"); ``` The `image.texture` generated primary runtime file will actually be used. You can also directly access any asset source file (not a runtime file). For example, if you need to specify a `.png` texture, you should write the following: ```cpp ImagePtr image = Image::create("asset://image.png"); ``` In this case, the runtime `.texture` file will be ignored, `.png` source file will be used.
- Each [**container asset**](../../editor2/assets_workflow/assets_runtimes.md) also has a primary runtime, in case of an FBX asset it is a generated `.node` file. So, you can use the following reference: ```cpp NodeReferencePtr node = NodeReference::create("teapot.fbx"); ``` The `teapot.node` generated runtime file will be used in this case. You can access each runtime file of a container asset. For example, an FBX file has `.node` and `.mesh` runtime files generated for it. You can access the generated `.mesh` file in the following way: ```cpp MeshPtr mesh = Mesh::create("teapot.fbx/teapot.mesh"); ```


### Accessing by GUID


You can also access any runtime or asset in your project using [GUIDs](#guids). If a GUID of a file is specified, the exact path corresponding to this GUID is used:


```cpp
UGUID asset_guid; // GUID of the asset named "1.tga"
const char *asset_path = "1.tga";

ImagePtr image = Image::create(asset_guid); // -> 1.tga
ImagePtr image = Image::create(asset_path); // -> 1.texture

```


## Modifiers


File modifiers serve to automatically choose which resources to load when a UNIGINE project is run on different platforms or with different localizations. Instead of keeping multiple versions of the same project and copying shared data between them, you can add a custom postfix to file or folder names, and load only required resources on demand.


> **Warning:** This feature is run-time only, and is not supported by UnigineEditor.


Modifiers are added to file or folder names as a postfix (only one can be specified). Any custom postfix can be used. For example, it could be:


- File name modifier: ***file.small.node*** or ***texture.eng.texture***
- Folder name modifier: ***textures.lowres*** > **Notice:** If a folder has a modifier, files inside it should not have their own modifiers. Otherwise, file modifiers will be ignored.


Register necessary modifiers in code via *[addModifier()](../../api/library/filesystem/class.filesystem_cpp.md#addModifier_cstr_void)*. When the project is running, resources with the registered modifiers are loaded automatically. Files without modifiers have the lowest priority (can be used for default resources).


### Usage Example


For example, three localization languages are supported in the project: English (by default), German and French. Depending on the language, different splash textures should be loaded on the start-up.


To organize your resources, name them using the following file modifiers:


- ![](folder.png) **data**

  - ![](folder.png) **splashes**

    - ![](file.png) **splash.png** (this is a default version of the texture. In our case, a texture with an English title)
    - ![](file.png) **splash.de.png** (a German title)
    - ![](file.png) **splash.fr.png** (a French title)


After that, you need to specify in code which modifier to use via *[addModifier()](../../api/library/filesystem/class.filesystem_cpp.md#addModifier_cstr_void)*. This function is called in the [system script](../../code/fundamentals/execution_sequence/app_logic_system.md#systemlogic) since a modifier needs to be registered before the world and its resources start to be loaded. For example, to load a German splash screen and the low resolution textures interface:


```cpp
// unigine.cpp

int init() {
	...

	// Register modifier
	engine.filesystem.addModifier("de");

	// Set a splash texture
	engine.splash.setWorld("textures/splash.png");   // splash.de.png will be automatically used
	...

	return 1;
}

```


Also you can use *[-extern_define](../../code/command_line.md#extern_define)* CLI option to pass the language (for example, if a user chooses a language in the launcher).

```bash
bin\main_x64d.exe -extern_define "LANG_DE"
```


And here is how passed defines can be handled in the code.


```cpp
// unigine.cpp
string lang = "";

int init() {
	...

	// Parse EXTERN_DEFINE
	#ifdef LANG_DE
		lang = "de";
	#elif LANG_FR
		lang = "fr";
	#endif

	if(lang != "") {
		engine.filesystem.addModifier(lang);
	}

	// Set a splash texture: splash.de.png or splash.fr.png will be used if the language is passed
	engine.splash.setWorld("textures/splash.png");	// otherwise, splash.png
	...

	return 1;
}

```


## Asynchronous Loading


UNIGINE Engine allows you to control asynchronous loading of files by means of the *[AsyncQueue](../../api/library/filesystem/class.asyncqueue_cpp.md)* class. All file-related methods of this class will load a file and add it to the file system as a cached one.
