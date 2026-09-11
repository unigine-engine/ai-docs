# Context Menus


UnigineEditor has context menus to facilitate various operations. In addition to commonly used operations, such as *Delete, Cut, Copy, Paste, Rename, Clear, Open*, there are specific operations that depend on the window or parameter.


## Asset Browser


Operations of the *Asset Browser* window context menu:


![](asset.png)


| Edit Graph | Opens the material graph editor to edit the selected graph. |
|---|---|
| Import New Asset | Import a selected file as a project asset. |
| Create Folder | Create a new folder. |
| Create Material | Create a new [Material Graph or Subgraph](../../../content/materials/graph/index.md#graph_create) or inherit a child from any of the base materials available in the Materials Hierarchy. |
| Create Code | Create a new shader, property, C# component, base material, or UnigineScript file. |
| Create Landscape Layer Map | Create a new landscape layer map. |
| Create World | Create a new world. |
| Create Mount Point | Create a new mount point. |
| Place as Node Reference | [Create a *Node Reference*](../../../editor2/create_import_nodes/index.md#assets) by placing a selected `*.node` asset in the scene. |
| Place as Node Layer | [Create a *Node Layer*](../../../editor2/create_import_nodes/index.md#assets) by placing a selected `*.node` asset in the scene. |
| Place as Node Content | [Create a node](../../../editor2/create_import_nodes/index.md#assets) by placing a selected `*.node` asset, which can be any node type or a hierarchy of nodes, in the scene. |
| Create Child | Create a child asset. Available for materials and properties. |
| Convert To Unique Graph | Convert a selected material to a unique material graph file. |
| Reimport | Reimport a previously [imported](#import) file. Used to implement updates that have been performed in a source file after the import. > **Notice:** If you reimport an FBX that is referenced by a *Node Reference*, check that the *Node Reference* has been [created](../../../objects/nodes/reference/index.md#exporting) correctly. Otherwise, all your modifications will be lost after the reimport. |
| Export As Package | Export a selected file as a UNIGINE package file. |
| Convert To | Converts a selected texture file to a specified format. |
| Open | Display the content of a [geometry container](../../../editor2/fbx/index.md#fbx_container). |
| Show in Explorer | Show a selected file in Explorer. |
| Show Runtime in Explorer | Show the [runtime file](../../../editor2/assets_workflow/assets_runtimes.md) of a selected file in Explorer. |
| Show Assets Using This One | List all assets (materials, textures, `.fbx` files, properties, etc.) that use the currently selected asset (or assets). |
| Show World Nodes Using This One | List all world nodes that use the currently selected asset (or assets). |
| Show Assets Used | List all assets (materials, textures, `.fbx` files, properties, etc.) that are used in the currently selected asset (or assets). |
| Show Assets Used Only In This World | List all the assets (materials, textures, `.fbx` files, properties, etc.) that are [unique for the currently selected world](../../../editor2/assets_optimize/unique_assets.md) and are not used in other worlds available in the project and selected for comparison. |
| Replace Asset Links | Replace all references to the right-clicked asset with references to the asset selected via the window that opens. |
| [Batch Rename](../../../editor2/tools/batch_rename/index.md) | Change the names of multiple objects according to the selected rule. |
| Add to Favorites | Add the selected asset, folder, or search request to the `favorites` folder, which is accessible via the [Hierarchy View](../../../editor2/assets_workflow/index.md#hierarchy_view) of the *Asset Browser*. |
| Remove from Favorites | Remove the selected asset, folder, or search request from the `favorites` folder, which is accessible via the [Hierarchy View](../../../editor2/assets_workflow/index.md#hierarchy_view) of the *Asset Browser*. |


## World Hierarchy


Operations of the *World Nodes* window context menu:


![](world.png)


| Select Child Nodes | Select all child nodes of a node without selecting the parent node itself. Available for parent nodes. |
|---|---|
| Focus | Make the scene camera focus on the node. |
| Move to Camera | Move the selected node into the scene camera's focus. |
| [Create a Node Reference](../../../editor2/exporting_nodes/index.md#export_to_noderef) | Create a *Node Reference* of a selected node and store it in the current folder of the *Asset Browser*. |
| [Create Mesh](../../../editor2/exporting_nodes/index.md#export_to_mesh) | Create a mesh of a selected node and store it in the current folder of the *Asset Browser*. |
| [Create FBX](../../../editor2/exporting_nodes/index.md#export_to_fbx) | Create an `*.fbx` file of a selected node and store it in the current folder of the *Asset Browser*. |
| [Create Mesh Clusters from Hierarchy](../../../objects/objects/mesh_cluster/index.md#cluster_node) | Create a *Mesh Cluster(s)* from a selected hierarchy. |
| [Group](../../../editor2/organizing_nodes/index.md#group_nodes) | Create a *Dummy Node* and make selected nodes its child nodes. |
| [Make Parent](../../../editor2/organizing_nodes/index.md#make_parent_node) | Select a group of nodes and make a right-clicked node a parent of the group. |
| [Unparent](../../../editor2/organizing_nodes/index.md#unparent_node) | Detach a node from its parent. A detached node is placed at the same level as the former parent. |
| [Clone](../../../editor2/organizing_nodes/index.md#clone_node) | Clone a selected node. |


## Materials Hierarchy, Properties Hierarchy


Context menus of the *Materials Hierarchy* and *Properties Hierarchy* windows are identical. In addition to the options available in Asset Browser, they contain the following options:


![](materials.png)


| [Create Clone](../../../editor2/materials_settings/organizing_materials/index.md#clone_material) | Clone an asset. |
|---|---|
| Show Asset | Show an asset in the *Asset Browser*. |
| [Rename](../../../editor2/materials_settings/organizing_materials/index.md#rename_material) | Rename an asset. |
| [Delete](../../../editor2/materials_settings/organizing_materials/index.md#delete_material) | Permanently delete an asset from the hierarchy and the asset folder. This action cannot be undone. |


## Viewport Window


The Viewport Window has two context menus depending on where you click: if you click a node, the context menu is the same as in the *[World Nodes](#world)* window, clicking outside any node (or **Shift + RMB**) opens the *[Create](../../../editor2/create_import_nodes/index.md#menu)* menu.


[![](viewport.jpg)](viewport.jpg)


## Parameters Tab


The *Parameters* Tab has several types of context menu depending on the parameter's type.


### Spinbox context menu


The context menu of spinboxes contains the following operations:


![](param_1.png)


| Step up | Add one (+1) to the current value. This operation can be also performed by scrolling, when the cursor is in the spinbox. Scrolling while holding the **Ctrl** key pressed adds 10 each step. |
|---|---|
| Step down | Subtract one (-1) from the current value. This operation can be also performed by scrolling, when the cursor is in the spinbox. Scrolling while holding the **Ctrl** key pressed subtracts 10 each step. |
| Maths | A list of math operations: - **Add** � add an entered value to the current value. - **Subtract** � subtract an entered value from the current value. - **Multiply** � multiply the current value by an entered value. - **Divide** � divide the current value by an entered value. - **Round To** � round to a multiple of a specified value entered by a user. This math operation can be used to avoid the accumulation of rounding errors. A rounded value is calculated as follows: 1. Current Value / Entered Value = Real Number. 2. Real Number is transformed to Natural Number by cutting off any digits after the decimal point. 3. Natural Number * Entered Value = Rounded Value. |


### Properties context menu


The context menu of node and surface properties is displayed by clicking ![](gear.png) right to the property field and contains the following operations:


![](param_3.png)


| Copy Values | Copy values of all parameters of a property. |
|---|---|
| Paste Values | Paste values to all destination parameters that have the same name and type as the parameters of the copied property. |
| Move Up | Move a property one line up in the list of properties. |
| Move Down | Move a property one line down in the list of properties. |
| Reset | Set all property values to default. |


### Surface context menu


The surface context menu is displayed by clicking ![](copy_paste.png) in the top-right corner of the surfaces section and contains the following operations that facilitate the [copy/paste procedure](../../../editor2/node_parameters/visual_representation/index.md#copy_paste):


![](param_4.png)


| Copy Parameters | Copy parameters of selected surfaces. |
|---|---|
| Paste Parameters Sequentially | Paste parameters copied from source surfaces to destination surfaces in the order they appear in the hierarchy. |
| Paste Parameters By Surface Names | Paste copied parameters if their surface names are the same as destination surface names. |
