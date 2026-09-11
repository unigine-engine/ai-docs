# Assets Workflow


The **Asset System** aims to unify file management within the UNIGINE project and make it simple and intuitive. For this purpose the content of the project is represented as a collection of "building blocks" � assets, and the whole workflow is organized around them.


**Asset** is the "unit of work", it represents any item that can be used in your world or project. An asset may come from a file created using a third-party application, such as a 3D model, an audio file, an image, or any other type supported by the UNIGINE Engine. Assets can also be created using the UnigineEditor, e.g., a node, a material, or a property.


Each asset is represented by a pair: a file on disk, and a `*.meta` metadata file which stores auxiliary information for this asset including a *GUID (globally unique identifier)*. A GUID identifies a path to the asset (i.e., location of the asset in the project) and is used by the Asset System to keep all links and dependencies between the resources regardless of their name and location within the project. So, you don�t have to worry that your material will lose a texture when you change its name.


Another important feature of the Asset System is real-time tracking of changes. You can modify your assets at any time after importing, the Asset System will notice when you save new changes to the file and will re-import it as necessary.


All assets are stored in the [`data`](../../editor2/assets_workflow/project_files.md#data_folder) folder of your project. For all assets, that are in non-native format (e.g. *`.fbx`, `.obj`, `.hdr`*, etc.) the Editor automatically generates all resources to be used by the UNIGINE Engine at run time. Such files are called [**runtime files**](../../editor2/assets_workflow/assets_runtimes.md).


> **Notice:** Runtime files are generated automatically and stored in the [`data/.runtimes`](../../editor2/assets_workflow/project_files.md#data_runtimes_folder) folder of your project.


![](file_system.png)

*Relationship between the contents of thedatafolder in your project's root on your computer, and the Project folder in the Asset Browser window*


The entire workflow will revolve around the [Asset Browser](#asset_browser), and the regular file explorer should no longer be necessary when working on a UNIGINE project. In fact, the goal of this feature is for users of UNIGINE to ignore what lies on the disk completely and only interact with their project's content via the Editor.


## Asset Browser


The main front-end tool of the Asset System is the **Asset Browser**. It is used to organize content in your project: create, import, view, rename your assets, move them between the folders and manage their hierarchy.


> **Notice:** The simplest way to safely move or rename your assets is to **always** do it using the **Asset Browser**. In this case the Asset System will keep all links and dependencies between the resources.


Asset Browser is accessible from the **Window** menu.


![](asset_browser.png)

*Asset Browser elements*


Asset Browser consists of the Hierarchy View and the Thumbnail View. You can use them both, or move the dividing bar between them to either side, and use only one of them, as demonstrated below:


![](asset_browser_rearrangement.gif)

*Rearranging Asset Browser*


To facilitate managing assets, you can create multiple Asset Browser windows via the menu bar: ***Windows -> Add Asset Browser*** and stack them anywhere.


![](../interface/asset_browser_windows.png)


Each of the created windows is listed in the *Windows* menu and can be hidden, shown or removed, if required.


![](asset_browser_windows_menu.png)


Watch the tutorial below to learn how to manage assets with the Asset Browser:


### Hierarchy View


![](folder_view_panel.png)


**Hierarchy View** is located on the left side of the Asset Browser interface. It contains a list of all folders and assets within your project. The following root folders are available:


- `favorites` � contains the project assets, folders, and search requests selectively added by the user via the corresponding [item of the context menu](../../editor2/interface/context/index.md#favorites).
- `data` � contains the data stored in the `data` folder of the project root. It is the folder where all work with the project content is performed.
- `core` � contains the built-in core assets. These assets are available for every project by default. > **Notice:** Core assets are read-only.
- `configs` � stores all global engine-related and project-related settings represented as separate [configuration files](../../code/configuration_file_cpp.md).


When a folder is selected from the list by clicking, its contents will be shown in the [Thumbnail View](#thumbnail_view) to the right. You can use a small triangle next to the folder to expand or collapse it, displaying nested folders and assets.


The **buttons on the top** allow collapsing and expanding the asset list as well as selecting the representation mode: only folders or both folders and assets.


The content can be resized using the slider at the bottom of the panel.


The assets can be added to the scene by dragging directly from the Hierarchy View into the editor viewport.


### Thumbnail View


![](thumbnail_view.png)


**Thumbnail View** displays icons for all assets in the selected project folder after applying all selected filters. You can select the types of assets to be displayed using the **Filter** icon in the top right corner of the panel.


**Search** is performed within the currently selected folder, i.e. to search through the whole project you need to select the `data` folder and enter your search request. As you select the asset from the search result and delete the search request, the folder that stores this asset will be open in the Thumbnail View.


Search requests can be added to the *[favorites](#favorites)* folder by right-clicking in the search field with the entered request. In this case, the search will be performed across the whole project.


The assets available in the Thumbnail View can be dragged directly into the editor viewport.


You can create a new folder, material or property by right-clicking somewhere within the panel and choosing the desired item from the [context menu](../../editor2/interface/context/index.md#asset_browser). The list of assets can be navigated by using the scroll bar or rotating the mouse wheel.


The icons can be resized using the slider at the bottom of the panel; they will be replaced by a hierarchical list view if the slider is moved to the extreme left.


To show the asset file location in the standard file browser window, right-click on the asset and choose *Show in Explorer*.


The elements of the **path to file** are also clickable. This way you can quickly move to any of the parent folders.


### Preview and Details


**Preview and Details** are displayed in the *[Parameters](../../editor2/interface/index.md#parameters)* window on the right side of the Asset Browser interface. The information is available for the selected asset depending on its type.


| **3D Geometry** | **Material** | **Texture** |
|---|---|---|
| ![](preview_mesh.png) | ![](preview_material.png) | ![](preview_texture.png) |
| 3D geometry Asset (such as *`.mesh`, `.node`, `.fbx`*) is shown in a test environment with default *[mesh_base](../../content/materials/library/mesh_base/index.md)* base material applied. You can rotate the model with a mouse, holding the left button pressed, and scale it with the mouse wheel. | Material asset is shown as applied to a primitive (Sphere, Material Ball, Box, Capsule, Cylinder, Dodecahedron, or Icosahedron). You can rotate the primitive with a mouse, holding the left button pressed, and scale it with the mouse wheel. | A texture asset is shown as an image, with information and controls at the top of the panel. These controls are used to select Red, Green, Blue and Alpha channels and MipMapping level. You can move the image with a mouse, holding the left button pressed, and scale it with the mouse wheel. |


Audio player is displayed for an **audio asset**. Previews for other asset types are displayed as icons.
