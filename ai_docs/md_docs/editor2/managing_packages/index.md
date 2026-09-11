# Managing Packages


**Package** is a collection of files and data for UNIGINE projects stored in a single `*.upackage` file. A Package compresses data while preserving the original directory structure. Packages can be used to conveniently transfer files between your projects or exchange data with other users, be it content (a single model or a scene with a set of objects driven by logic implemented via [C# components](../../principles/component_system/index.md)) or files (plugins, libraries, execution files, etc.).


## Creating a Package


UnigineEditor allows exporting into a Package file both assets from the *Asset Browser* and external files (i.e. files stored outside the `data_path` directory).


In general, the pipeline is similar for both cases, however, there are some differences.


### Exporting Assets From Asset Browser


To export assets from the *Asset Browser* into a Package file:


1. In the *Asset Browser* select the desired asset(s) or folder(s) and choose *Export As Package* option in the context menu. And proceed to **Step 2** ![](select_export.png) ***Alternatively***: <details> <summary>Click to see alternative | Close</summary> In the Menu bar, you can choose *Packages -> Export Package*. ![](export_package.png) Click the *Add Files From Asset Browser* button in the *Export Package* window that opens. ![](add_assets.png) Then select the assets that you want to add to the Package in the *Select Assets* window and click *OK*. You can even select the folder containing the whole project, and then deselect the data you don't require on the next step. ![](select_assets.png) </details>
2. Now you can add assets to be exported in the *Export Package* window using a checkbox for each asset. ![](assets_selection.gif)
3. You can automatically add all dependent assets to the package (a texture used by a material, materials assigned to an object, etc.) via the *Include Dependencies* checkbox (dependent assets are marked green in the list). ![](assets_dependencies.gif)
4. After selecting assets click *Export Package* to pack them into a new `*.upackage` file. ![](export_package_button.png) > **Notice:** At least one asset must be selected to activate the *Export Package* button.
5. In the dialog window that opens, define the name and path to your package and click *Save*.


As soon as your Asset Package is successfully created, the location of your `*.upackage` file will be shown in your file manager.


### Exporting External Files


To copy external files (i.e. project files stored outside the `data_path` directory) to a Package file:


1. Open the *Export Package* window: in the Menu bar, choose *Packages -> Export Package*. If you have already added assets from the *Asset Browser*, you may skip this step as the window is open. ![](export_package.png)
2. Сlick the *Add External Files* button, choose files or folders in the dialog window that opens and click *Open*. Note that the external folders are colored red, while the folders from the *Asset Browser* are blue. ![](add_assets.png) > **Notice:** You can't add files stored outside the project folder.
3. Select files and/or folders to be exported, click *Export Package*, specify the name and path to a new `*.upackage` file and click *Save*.


## Importing a Package


To import contents of an existing package to your project you need to:


1. Drag it from the File Explorer directly into the *Asset Browser* or choose *Packages -> Import Package* in the Menu bar and select the `*.upackage` file. You can also right-click in the *Asset Browser*, choose *Import New Asset* in the context menu and select the package. If you have already added the `*.upackage` file to your targed project, double-click on it. > **Notice:** Do not use a file manager of your OS to copy a package to your project's folder, as in this case the package will be displayed in the *Asset Browser*, but its contents won't be extracted. The following window will open: ![](import_package.png)
2. Check the assets that are going to be imported. Assets in the package can be colored white, red, and yellow: ![](asset_colors.png) > **Notice:** To import all dependent assets for the ones that are selected, check *Force Import Dependencies*. Such assets will be colored green. For example, if you uncheck a texture used by a selected material, the texture will be imported anyway.

  - White-colored assets can be imported without any changes.
  - Yellow-colored assets are imported with a postfix to resolve the name collision.
  - Red-colored assets cannot be imported due to one of the following reasons:

    - The same asset is found in the project.
    - Asset with the same Source Runtime GUID is found in the project.
    - Asset with the same Runtime GUID is found in the project.
    - The specified target mount point is read-only.
3. After selecting all assets required for import, click the *Import Package* button.
4. Wait for the extraction process. Extraction time depends on the size of the assets selected for the import. ![](import_process.png)


Except assets, you can also import **files** stored in a package. If such file already exists in the project, it will be colored red with no import option.


![](import_file.png)


Upon successful package import, a new folder with the corresponding contents will be available in the *Asset Browser* and the following message will be displayed:


![](import_successful.png)


### Resolving Duplicates During Asset Import


When importing assets, some of them may already exist in the project. If duplicates are found:


- Duplicate files are highlighted in yellow.
- The import list shows a message describing the issue, including the path to the existing asset or file in the project.
- The duplicate path is also available as a tooltip when hovering over the problematic item.
- Below the import list there is a summary with the number of duplicated assets and files.
- Dropdowns are available for selecting how duplicates should be resolved.


![](import_duplicates.jpg)


| Resolve Asset Duplicates |  |
|---|---|
| Keep Existing | Existing assets in the project are preserved. New assets are not imported. |
| Import New Asset (Preserve Existing Path) | The existing asset in the project is replaced with the imported one, while keeping the original project path. |
| Import New Asset (Use New Path) | The existing asset is replaced, and the imported asset�s path from the package is used. |
| Resolve File Duplicates |  |
| Keep Existing | Existing files are preserved. New files are not copied. |
| Replace With New Files | Existing files are replaced with the imported ones. |


**Notes and limitations:**


> **Warning:** If you select any option other than **Keep Existing**, you initiate a replacement that cannot be undone.


- Duplicate detection is based on asset and runtime GUIDs, not on file names or content. Assets with different GUIDs are treated as separate, even if their content or names are identical.
- If a file has a different GUID but the same name as an existing file, it is automatically renamed during import (for example, `folder/child_1.mat` will be renamed to `folder/child_1_0.mat`).
- If a world file is replaced during import, it will be automatically closed.
- During import, temporary error messages (for example, missing textures or node references) may appear in the console. This is expected behavior and usually resolves automatically after the import completes successfully.
- In rare cases, duplicates cannot be resolved due to compatibility or safety reasons, and such assets will not be imported.


## Managing a Package


Packages provided on Add-On Store may be updated by the package creator from time to time. In this case, you'll need to delete the previously added files and add the new package version. The *Add-On Store Package History* window shows all added packages downloaded from Add-On Store and helps deleting the package files in one click.


To open the *Add-On Store Package History* window, select *Packages -> Add-On Store Package History* in the menu.


![Opening the Add-On Store Package History window](package_history_open.png)


The following window will open:


![Add-On Store Package History window](package_history_window.png)


This window provides the following details and options:


| Imported Packages | The list of packages from Add-On Store that have been imported to this project. |
|---|---|
| File Hierarchy | The hierarchy of files available in the selected package. If some package files have not been imported, they still be displayed in the *File Hierarchy* list but in grey color, as they are unavailable. The following options are available on this tab: ![](file_hierarchy_tab.png) 1. **Unlink Files From Package** � removes all links from assets to the package. Assets remain in the project, however cannot be managed via the *Add-On Store Package History* window anymore. This process cannot be reverted. To restore the package file hierarchy, import the package once again. 2. **Delete Package With Files** � removes all assets listed in *File Hierarchy* from the project. This process cannot be reverted. To restore the files, import the package once again. 3. **Show In Editor Plugin Manager** � the button that opens the plugin in *[Editor Plugin Manager](../../editor2/extensions/index.md#locating_plugins)*. It is available in *File Hierarchy* if the imported package contains the Editor plugin. |
| Description | Displays the description of the package as provided by the package creator on Add-On Store including the package version. |

 Best PracticeWhen performing any operations via the *Add-On Store Package History* window, check the Editor Console window.
