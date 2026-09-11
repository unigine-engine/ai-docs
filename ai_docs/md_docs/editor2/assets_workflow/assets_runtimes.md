# Assets and Runtime Files


Each time an asset is [created or imported](../../editor2/assets_workflow/assets_create_import.md), the [UnigineEditor](../../editor2/index.md) creates a corresponding file and a `*.meta` file in the `data` folder of your project, it can also generate so-called "runtime files" when necessary.


**Runtime files** are files in UNIGINE's native format (such as `.texture` textures, `.mesh` geometry, `.anim` animations, etc.) used by the Engine at run time.


In the context of runtime files, assets in UNIGINE can be divided into two groups:


- For a **native asset** (in UNIGINE's native format) no runtime files are generated normally, as such an asset itself is treated and used as a runtime file. > **Notice:** - Such assets are included in the final build "as is". > - A `*.mesh` or an image file can be treated as a non-native asset if the **Unchanged** option is disabled for it (a corresponding runtime file will be generated).
- For a **non-native asset** (e.g. `.fbx`, `.obj`, `.hdr`, etc.) corresponding runtime file(s) will be generated in the `data/.runtimes` folder. A particular case of a non-native asset is a **container-asset** � such assets have multiple runtime files generated for them (e.g. an FBX asset may produce `.node`, `.mesh`, `.mat`, etc. files). > **Notice:** A non-native asset may have no runtimes at all (e.g., a `.txt` file).


> **Notice:** You can choose to [use a non-native asset as a runtime file](../../editor2/assets_workflow/assets_create_import.md#unchanged), in this case the asset will be treated as a native one (no runtime file will be generated for it).


Asset type is defined by the extension of this file. Some of the asset types are associated with more than one extension (e.g. a texture asset is associated with `.png, .jpg, .psd, .hdr,` etc.).


![](assets_runtimes_folder.png)

*Assets and corresponding generated runtime files in thedata/.runtimesfolder*


The following table shows the types of runtime files generated for certain types of assets.


| Non-native Asset Type | Runtime(s) Produced |
|---|---|
| `*.fbx, *.dae, *.3ds` | Node (`*.node`) Static Meshes (`*.mesh`) Skinned Mesh Animations (`*.anim`) Materials (`*.mat`) Textures (`*.texture`) |
| `*.obj + *.mtl` | Node (`*.node`) Static Meshes (`*.mesh`) Materials (`*.mat`) Textures (`*.texture`) |
| `*.png, *.jpg, *.tiff, *.dds, *tgs, *.rgb, *.rgba, *.psd, *.hdr, *.pgm, *.ppm, *.sgi` | Texture (`*.texture`) |


You can use `assets_info` and `assets_list` console commands to view information on non-native assets and runtimes generated for them.


To find a runtime file generated for an asset, right-click the asset in the [Asset Browser](../../editor2/assets_workflow/index.md#asset_browser) and choose *[Show Runtime in Explorer](../../editor2/interface/context/index.md#show_runtime)* in the context menu.


![](show_runtime.png)


### See Also


- *[FileSystem article](../../principles/filesystem/index_cpp.md)* to learn more about accessing assets and runtime files.
- API classes:

  - *[FileSystem Class](../../api/library/filesystem/class.filesystem_cpp.md)*
  - *[FileSystemAssets Class](../../api/library/filesystem/class.filesystemassets_cpp.md)*
