# Vegetation Parameters


Vegetation such as trees and grass can be generated via the *Sandworm* tool based on available landcover data added as a *[Mask](../../../../editor2/sandworm/sources/mask/index.md)*.


![](../../workflow/vegetation/example.jpg)


An example of creating vegetation is provided [here](../../../../editor2/sandworm/workflow/vegetation/index.md).


## Parameters


![Vegetation Parameters](parameters.png)


| Object Name | The name of the object created in *Sandworm*, displayed in the *Objects* list and in the World Hierarchy. It can be edited either here (in the *Parameters* panel), or in the *Objects* list by double-clicking the object you want to rename. |
|---|---|
| Mask | [Mask](../../../../editor2/sandworm/sources/mask/index.md) used to distribute the specified vegetation node across the landscape. The drop-down list contains all added masks. |
| Node | [Primary object](../../../../editor2/sandworm/workflow/vegetation/index.md#create_primary_object) used to generate vegetation: a group of trees or grass. It is taken from a `*.node` asset � the file produced by [exporting a node](../../../../editor2/exporting_nodes/index.md) from the world, the same one a *[Node Reference](../../../../objects/nodes/reference/index.md)* points to. A single file may hold one such object or a whole group of them. The following types of primary objects are supported: - *[Grass](../../../../objects/objects/grass/index.md)* object - *[Mesh Clutter](../../../../objects/objects/mesh_clutter/index.md)* object - *[World Clutter](../../../../objects/worlds/world_clutter/index.md)* object (generated only if ***Object Terrain Global*** is selected as the [Terrain Type](../../../../editor2/sandworm/interface/index.md#terrain_type)) - A **group** of the objects above in one file � several nodes [exported to a single Node Reference](../../../../editor2/exporting_nodes/index.md#export_to_noderef) become children of a *[Dummy Node](../../../../objects/nodes/dummy/index.md)*. Every object found in the file is planted, and all of them cover the same area > **Notice:** Vegetation is generated only from the objects that lie in the selected file itself. If the file contains other *[Node References](../../../../objects/nodes/reference/index.md)*, nothing is generated from them: Sandworm does not look inside a nested reference, and writes a warning to the log. Unpack such a reference in the node file to have its objects generated. The process of creating a primary object is described [here](../../../../editor2/sandworm/workflow/vegetation/index.md#create_primary_object). > **Notice:** Intersections should be enabled for any type of the primary object. |
| Split Length (m) | Side length of the grid cell into which the generated vegetation area is split, in meters. Splitting into subsegments is recommended to restrict the size of the generated area ([Size X and Size Y](../../../../objects/objects/mesh_clutter/index.md#size) of the generated *[Mesh Clutter](../../../../objects/objects/mesh_clutter/index.md)*) to 10,000 m. Due to the nature of the mesh, there will be visual artifacts connected with the float precision, if a very big *Mesh Clutter* object is generated (with the side length of around 16,000 m and more). We recommend splitting such big objects to smaller ones. > **Notice:** Splitting a segment into too many subsegments (i. e. using very small values) affects the generation time and memory consumption. |
