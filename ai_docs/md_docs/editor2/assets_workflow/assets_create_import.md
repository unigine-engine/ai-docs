# Creating and Importing Assets


Not all content for your UNIGINE project can be created within [UnigineEditor](../../editor2/index.md). Most [assets](../../editor2/assets_workflow/index.md#asset_system) are created externally, using Digital Content Creation tools, such as *3ds Max, Maya, Photoshop*, and others.


In the table below you can see a very general breakdown of the types of assets that can be created in UnigineEditor and those that are created using external Digital Content Creation (DCC) tools.


| Assets created in UnigineEditor | Assets created using External Applications |
|---|---|
| - [Worlds](../../editor2/assets_workflow/asset_types.md#world) - [Nodes](../../editor2/assets_workflow/asset_types.md#node) - [Materials](../../editor2/assets_workflow/asset_types.md#materials) - [Properties](../../editor2/assets_workflow/asset_types.md#property) - [Scripts](../../editor2/assets_workflow/asset_types.md#scripts) - [Landscapes](../../editor2/assets_workflow/asset_types.md#sandworm) - [Tracks](../../editor2/assets_workflow/asset_types.md#track) (Cinematic Sequences) - [Render Settings](../../editor2/assets_workflow/asset_types.md#settings) - [Physics Settings](../../editor2/assets_workflow/asset_types.md#settings) - [Sound Settings](../../editor2/assets_workflow/asset_types.md#settings) | - [Textures](../../editor2/assets_workflow/asset_types.md#texture) - [Static and skeletal meshes and animations](../../editor2/assets_workflow/asset_types.md#geometry) - [Sounds](../../editor2/assets_workflow/asset_types.md#sound) - [Videos](../../editor2/assets_workflow/asset_types.md#video) - [Fonts](../../editor2/assets_workflow/asset_types.md#font) - [Paths](../../editor2/assets_workflow/asset_types.md#path) |


To use assets created in a third-party Digital Content Creation tool in your UNIGINE project you should export them in a way that would not alter their dimensions, transforms, etc. when you import them to UNIGINE.


## Exporting Assets from Content Creation Tools


Before exporting assets from Digital Content Creation tools, check the following **general recommendations**:


- Check the working units used in your tool because scales in your tool and in UNIGINE may differ, and adjust, if needed. In UNIGINE **1 unit = 1 meter**.
- Align your model along to the front axis and check that **Y+** points forward at the export.
- Reset all transformations to avoid any misplacement issues after the model import.
- Prepare materials. Keep in mind that surfaces and meshes of the imported model are named after the materials.


In addition to the general recommendations, there are guidelines for export from the most commonly used Digital Content Creation tools:


- [Exporting 3D Models From Blender](../../editor2/assets_workflow/export/export_from_blender.md)
- [Exporting 3D Models From Autodesk Maya](../../editor2/assets_workflow/export/export_from_maya.md)
- [Exporting 3D Models From Autodesk 3ds Max](../../editor2/assets_workflow/export/export_from_3dsmax.md)
- [Exporting 3D Models From Maxon Cinema 4D](../../editor2/assets_workflow/export/export_from_cinema4d.md)


If you export your model from any other tool, check the guidelines and try to follow the general recommendations.


## Importing Assets


You can import the content for your project in several ways:


- Drag the file(s) from the standard file browser of your operating system into the [Asset Browser](../../editor2/assets_workflow/index.md#asset_browser) window. In this case, the dragged file(s) will be copied to the `data` project folder. > **Notice:** To import composite assets (e.g. a material requiring a texture, or a node that requires several materials linked to plenty of textures) stored in Asset Packages (`*.upackage`), [follow this guide](../../editor2/assets_workflow/assets_migration.md).
- In the *Asset Browser*, go to the folder where you want to import the file(s) to, right-click and select **Import New Asset** in the context menu. ![](import_button.png) Choose a file (or several files) in the file browser window that appears. The selected files will be copied to the project folder. In case a single asset is imported, the [import settings](#import_settings) dialog window will be displayed (available for certain asset types). Otherwise, all assets will be imported with the last used import settings, that can be changed later, if necessary.
- Put your resources to the `data` folder of your project directly using the functions of your operating system. Then, as you open UnigineEditor, it will try to create all possible asset types with the last used import settings. You can change these settings later if necessary.


If your asset was imported successfully, a `*.meta` metafile will be created for it in the same folder and, if it is not a native asset, corresponding runtime file(s) will be generated in the [`data/.runtimes`](../../editor2/assets_workflow/project_files.md#data_runtimes_folder) folder of your project.


> **Notice:** You can modify your assets at any time after importing, UnigineEditor will notice when you save new changes to the file and will re-import it as necessary.


### Import Settings


Some types of assets supported by UNIGINE have a set of adjustable import settings, which determine the asset's appearance and behavior. These settings are displayed in a window that appears when you import a single asset.


For example, the import settings for an image will allow you to choose the type of texture, image format, size, etc. The import settings for an [FBX file](../../editor2/fbx/index.md) allow you to adjust the scale, decide whether you want to import materials and lights or use animation defined in the file.


You can change import settings for a particular asset when necessary. To do so, select it in the *Asset Browser*, the available settings will appear in the *Parameters* window. The options that are displayed will vary depending on the [type](../../editor2/assets_workflow/asset_types.md) of the selected asset.


Here you can also specify whether an asset will be used "as is" or a runtime file will be generated for it. This option is available only for some types of assets.


[![](import_settings.png)](import_settings.png)

*Clicking on an image asset in the Asset Browser shows the import settings in theParameterswindow.*


After changing the import settings click *Reimport* to reimport the asset with new settings or click *Cancel* to discard your changes.


## Real-Time Tracking of Changes


You can modify your assets at any time after importing, UnigineEditor will notice when you save new changes to the source file and will re-import it as necessary.


> **Notice:** The asset will be reimported automatically only when you modify its source file, stored inside the `data` folder of your project, either by direct editing or by replacing it with an updated version with the same name.


## Creating Assets in UnigineEditor


Any time you create a new [world](../../editor2/worlds/index.md#create_world), [save presets](../../editor2/settings/index.md#save_load_settings), inherit a new [material](../../editor2/materials_settings/organizing_materials/index.md#create_material) or a property, create a node reference or export a node to an FBX file in UnigineEditor an asset of the corresponding type is created.


You can also create assets of certain types (e.g., a material or a property) in the Asset Browser using the *Create* option. To do so, right-click in the Asset Browser to open the context menu, select *Create* and the desired type of asset from the list. A new asset will be created at the current folder of you project. You can [move the new asset to another location](../../editor2/assets_workflow/assets_organize.md#move) if necessary.


![](create_button.png)


> **Warning:** Do not create user folders with the following reserved names in the root of the `data/` or a mounted folder:
>
>
> - `.runtimes`
> - `.cache_textures`
> - `.editor2`
> - `core`
> - `editor2`
> - `scripts`
>
>
> If such a folder is created via Explorer, it won't be displayed in the Asset Browser. Inside subfolders of the data folder, no name restrictions are applied and such folders will be displayed by the Asset Browser properly.
