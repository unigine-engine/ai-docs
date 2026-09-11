# Transformation and Common Parameters


Transformation and common parameters are available on the *Node* tab of the *Parameters* window. These parameters are common for all types of nodes and always available for editing.


![](transformation_common_settings.png)

*Transformation and Common Parameters*


The topmost section of the *Parameters* windows includes common node description:


![](common_description.png)


- **Selection** flag toggles node selection on and off. If disabled, the node cannot be selected in the viewport.
- **Transformation** flag toggles node transformations on and off. If disabled, the node cannot be transformed.
- **Enabled** flag toggles the node on and off. If unchecked, the node will not be rendered.
- **Name** � the name of the node.
- **Type** � the type of the node, it defines the set of node-specific parameters.
- **ID** � the [ID](../../../api/library/nodes/class.node_cpp.md#getID_int) of the node.


> **Notice:** You can also rename and toggle the node flags on and off via the *[World Nodes](../../../editor2/organizing_nodes/index.md)* window.


## Transformation Parameters


The transformation parameters can be modified only when **Transformation** ![](../../organizing_nodes/transformation_on.png) of the node is unlocked. You can toggle this flag on and off in the *[World Nodes](../../../editor2/organizing_nodes/index.md)* or *[Parameters](../../../editor2/node_parameters/transformation_common/index.md)* window.


| Position | Specifies the position coordinates for the node. |
|---|---|
| Rotation | Specifies the rotation coordinates for the node. |
| Scale | Specifies the scale factor for X, Y, and Z axes. > **Warning:** Don't scale meshes that are going to participate in collision detection � physics doesn't work properly with scaled objects. To avoid scaling, reimport the mesh with the required [scale](../../../editor2/fbx/index.md#fbx_scale). |


The default values can be restored by clicking the ![](../default_value.png) icon next to the corresponding fields.


You can copy and paste the position, rotation, scale, or all transformation parameters together using the following context menu displayed by clicking the ![](../copy_paste.png) icon next to the fields with values.


![](copy_paste_reset.gif)

*Copying, resetting and pasting node transformation parameters*


> **Notice:** [Math operations](../../../editor2/interface/context/index.md#spinbox) are available for spinboxes.


## Common Parameters


| Triggers Interaction | Enables interaction of the node with [World Triggers](../../../objects/worlds/world_trigger/index.md). |
|---|---|
| Clutter Interaction | Enables interaction of the node (Object or Decal) with *[World Clutters](../../../objects/worlds/world_clutter/index.md#cutout_intersection)* and *[Mesh Clutters](../../../objects/objects/mesh_clutter/index.md#cutout_intersection)*. This option enables [cutting out clutter objects](../../../objects/objects/mesh_clutter/index.md#cutout_intersection) in the areas of intersection with an Object or a Decal (e.g., can be used to remove vegetation under houses or from the surface of roads projected using decals). > **Notice:** It is recommended to disable this option for better performance, when cutting node out of clutters is not necessary. Especially when the world contains a significant number of such nodes. |
| Mobility | When switched to **Immovable** the node is moved to a separate spatial tree for immovable (static) objects optimizing node management. Using this parameter can improve performance. **Immovable** is set by default. Switch the *Mobility* of the node to **Dynamic**, if you intend to move a node, assign a physical body to it (other than *[Dummy Body](../../../principles/physics/bodies/dummy/index.md)*) to make it physics-driven, or make any other changes affecting the spatial tree (see below). There are several restrictions on nodes considered immovable. Any action affecting the spatial tree is prohibited and causes a warning: you cannot change the node state (enabled/disabled), surfaces, bounds, transformation, visibility distance, as well as move the node, assign a non-dummy physical body or even change the *Mobility* state as it also leads to rebiulding of the spatial tree. > **Notice:** - You can disable these warnings via the `world_moving_immovable_node_mode` console command, if necessary. > - This parameter has effect only for [*objects*](../../../objects/objects/index.md) except for [*grass*](../../../objects/objects/grass/index.md) and *collider objects*. |
| Culled by Occlusion Query | Enables occlusion query for the objects. The objects are tested whether their bounding boxes are seen. It allows reducing the number of rendered triangles, which is beneficial by using heavy shaders. This option provides the substantial performance gain when enabled for water or meshes with reflections. > **Notice:** Enable this option only for a few nodes that use heavy shaders; otherwise, the performance will decrease instead of increasing. Culling will be performed if the [hardware occlusion query test](../../../principles/world_management/index.md#occlusion_culling) is enabled for the scene (the *Rendering -> Occlusion Culling -> Occlusion Query* flag is set). |
| Grass Interaction | Enables interaction of the node (Object or Decal) with *[Grass](../../../objects/objects/grass/index.md)*. This option enables [cutting out Grass](../../../objects/objects/grass/settings.md#cutout_intersection) in the areas of intersection with an Object or a Decal (e.g., can be used to remove vegetation under houses or from the surface of roads projected using decals). > **Notice:** It is recommended to disable this option for better performance, when cutting node out of grass is not necessary. Especially when the world contains a significant number of such nodes. |
