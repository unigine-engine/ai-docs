# Exporting Nodes


Any part of the scene (both a single node or a group of nodes including all children) can be exported from UnigineEditor and saved to a `.node`, `.mesh` or `.fbx` file.


## Exporting Nodes to a NodeReference


Any node (or nodes) from the *World Hierarchy* can be exported to a *[Node Reference](../../objects/nodes/reference/index.md)*. Exporting a node to a *[Node Reference](../../objects/nodes/reference/index.md)* may be required, for example, if you want to implement [instancing of nodes](../../editor2/instancing_nodes/index.md) in your project.


To export a node to a `.node` file, right-click the target node in the *World Hierarchy* window and choose *Create a NodeReference* in the drop-down list.


![](export_noderef.gif)

*Exporting Node to NodeReference*


Another way to export a node (nodes) is to select it in any available way and choose *Edit -> Convert To NodeReference* in the Menu Bar. In both cases, the selected node will be converted to *NodeReference*, and the `.node` file named after the node will be created.


If you select several nodes, they will be exported to a single `.node` file as child nodes of the *[Dummy Node](../../objects/nodes/dummy/index.md)*.


The exported node will be saved in local coordinates (relative to the zero of coordinates or to the parent node, if any).


## Exporting Nodes to a Mesh


Exporting nodes to a mesh may be required, for example, when you have several mesh-based nodes, and you want to get them as a single mesh.


Nodes of the following object-related types can be exported to the `.mesh` file:


- [Static Mesh](../../objects/objects/mesh/index.md)
- [Skinned Mesh](../../objects/objects/mesh_skinned/index.md)
- [Dynamic Mesh](../../objects/objects/mesh_dynamic/index.md)
- [Mesh Cluster](../../objects/objects/mesh_cluster/index.md)
- [Mesh Clutter](../../objects/objects/mesh_clutter/index.md)
- [World Spline Graph](../../objects/worlds/world_spline_graph/index.md)


To export a node to a `.mesh` file, right-click the target node in the *World Hierarchy* window and choose *Export to -> UNIGINE Mesh file (.mesh)* in the drop-down list.


> **Notice:** The exported mesh will be saved in the world coordinates.


![](export_mesh.gif)

*Exporting Node to Mesh*


The exported mesh can be used, for example, to create a [mesh-based node](../../code/usage/mesh_class/index_cpp.md).


## Exporting Nodes to FBX


Exporting nodes to an `.fbx` file provides a wide range of use cases for artists: for example, after exporting the scene you can bake lightmaps with the 3rd-party tool (for example, *V-Ray*).


Nodes of the following types can be exported to the `.fbx` file:


- [Static Mesh](../../objects/objects/mesh/index.md)
- [Skinned Mesh](../../objects/objects/mesh_skinned/index.md)
- [Dynamic Mesh](../../objects/objects/mesh_dynamic/index.md)
- [Node Reference](../../objects/nodes/reference/index.md)
- [World Spline Graph](../../objects/worlds/world_spline_graph/index.md)
- [All players](../../objects/players/index.md)
- [All light sources](../../objects/lights/index.md) except *[Environment Probe](../../objects/lights/envprobe/index.md)* and *[Voxel Probe](../../objects/lights/voxelprobe/index.md)*


> **Notice:** If you export a node of any other type, an empty `.fbx` file will be created.


- When exporting a static or dynamic mesh that has more than one surface with the same material, a separate mesh for each surface will be created and saved in the [FBX container](../../editor2/fbx/index.md#fbx_container).
- When exporting a *[Node Reference](../../objects/nodes/reference/index.md)*, the node stored by the reference (in the `.node` file) will be exported.


To export a node to an `.fbx` file, right-click the target node in the *World Hierarchy* window and choose *Export to -> FBX* in the drop-down list.


![](export_fbx.gif)

*Exporting Node to FBX*


The following window will open:


![FBX export settings](fbx_export_settings.png)


| Name | Name of the target FBX file. |
|---|---|
| Destination | Destination folder for the generated FBX file. |
| Save root transform | Preserve current transformations, when exporting selection to FBX. Uncheck to have your FBX content located at the origin *(0,0,0)* with default orientation. > **Notice:** - When exporting a static or dynamic mesh that has more than one surface with the same material, transformation of each [created mesh](#export_details) is saved in the parent coordinates. In this case, the parent of the meshes is the static/dynamic mesh that is exported. > - When exporting a *[Node Reference](../../objects/nodes/reference/index.md)*, transformation of this *Node Reference* is saved rather than transformation of the node stored by the reference. |
| Embed textures | Embed currently assigned textures into the target FBX file together with the geometry. |
| Separate surfaces into meshes | Split all surfaces into separate meshes inside the target FBX container. |
| Overwrite file if name matches | Overwrite the target file having a name that matches the specified one. |


You can export both a single node or nodes hierarchy tree branch. However, exporting to FBX is available only if one node in the hierarchy is selected. To export the hierarchy tree branch, select and export the parent node: the child nodes will be exported as well. If you need to export the whole scene or its part, the nodes should be added as children to a *[Dummy](../../objects/nodes/dummy/index.md)* or *[Layer](../../objects/nodes/layer/index.md)* node in the hierarchy.


> **Notice:** If you export the hierarchy tree branch, only nodes that are on the list of the [supported types](#supported_nodes_fbx) will be exported.


## Exporting Nodes to USD


You can export the scene content (including models, light sources, etc.) to a [`*.usd / *.usda / *.usdc`](https://openusd.org/release/intro.html#usd-can-be-extended-customized) (*Universal Scene Description*) file.


Nodes of the following types can be exported to the `USD` file:


- [Static Mesh](../../objects/objects/mesh/index.md)
- [Skinned Mesh](../../objects/objects/mesh_skinned/index.md)
- [Dynamic Mesh](../../objects/objects/mesh_dynamic/index.md)
- [Node Reference](../../objects/nodes/reference/index.md)
- [Light Omni](../../objects/lights/omni/index.md), [Light World](../../objects/lights/world/index.md)


> **Notice:** If you export a node of any other type, an empty file will be created.


When exporting a *[Node Reference](../../objects/nodes/reference/index.md)*, the node stored by the reference (in the `*.node` file) will be exported.


To export a node to a `USD` file, right-click the target node in the *World Nodes* window and choose *Export To -> Universal Scene Description file (.usd .usdc .usda)* in the drop-down list.


![](usd_export_menu.png)

*Exporting Node to USD*


The following window will open:


![USD export settings](usd_export_window.jpg)


| Name | Name of the target USD file. |
|---|---|
| Extension | [Format](https://openusd.org/release/intro.html#usd-can-be-extended-customized) of the target USD file, either of the following: - `usda` - text - `usdc` - binary - `usd` - the default (binary usdc) |
| Destination | Destination folder for the generated USD file. |
| Save root transform | Preserve current transformations, when exporting selection to USD. Uncheck to have your USD content located at the origin (0,0,0) with default orientation. > **Notice:** - When exporting a static or dynamic mesh that has more than one surface with the same material, transformation of each created mesh is saved in the parent coordinates. In this case, the parent of the meshes is the static/dynamic mesh that is exported. > - When exporting a *[Node Reference](../../objects/nodes/reference/index.md)*, transformation of this *Node Reference* is saved rather than transformation of the node stored by the reference. |
| Embed textures | Embed currently assigned textures into the target USD file together with the geometry. |
| Separate surfaces into meshes | Split all surfaces into separate meshes inside the target USD file. |
| Overwrite file if name matches | Overwrite the target file having a name that matches the specified one. |


You can export both a single node or nodes hierarchy tree branch. However, exporting to USD is available only if one node in the hierarchy is selected. To export the hierarchy tree branch, select and export the parent node: the child nodes will be exported as well. If you need to export the whole scene or its part, the nodes should be added as children to a *[Dummy](../../objects/nodes/dummy/index.md)* or *[Layer](../../objects/nodes/layer/index.md)* node in the hierarchy.


> **Notice:** If you export the hierarchy tree branch, only nodes that are on the list of the [supported types](#supported_nodes_usd) will be exported.
