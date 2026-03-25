# Adjusting Node Parameters


The multi-purpose *[Parameters](../../editor2/interface/index.md#parameters)* window provides access to parameters of the currently selected node.


![](parameters_window.png)

*Parameters Window with Node Settings*


> **Notice:** If the window isn't opened, choose *Windows -> Add Parameters* in the main menu.


Via this window, you can change a [name](../../editor2/node_parameters/transformation_common/index.md#name) of the selected node, [toggle](../../editor2/node_parameters/transformation_common/index.md#enabled) the node on and off, modify the node's [transformation parameters](../../editor2/node_parameters/transformation_common/index.md), its [visual representation](../../editor2/node_parameters/visual_representation/index.md), set up [physics](../../editor2/node_parameters/physics/index.md), and assign [properties](../../editor2/node_parameters/properties/index.md).


The node-related data is organized into two tabs:


- **Node** tab contains general and node-specific parameters. For example, settings for [object-related](../../objects/index.md) nodes include surface settings, such as rendering, LOD, intersection, collision, material, and property.
- **Physics** tab contains [settings](../../principles/physics/index.md) of the node's physical body.


The node parameters on each tab are grouped in separate panels, and each panel is expanded by default. You can collapse panels by clicking the arrow to the left of the panel name.


![](collapse_expand.gif)


### Multi-Selection Editing


UnigineEditor allows multi-selection editing of nodes: you can adjust parameters of several selected nodes at once by selecting nodes in one of the available ways and tweaking the required parameters. For example, you can [scale](../../editor2/node_parameters/transformation_common/index.md#transformation_params) nodes, disable [casting of world shadows](../../editor2/node_parameters/visual_representation/index.md#cast_world_shadows), or assign the same [material](../../editor2/node_parameters/visual_representation/index.md#surface_material) or [property](../../editor2/node_parameters/properties/index.md) to them.


Only parameters that are common for all selected nodes are visible in the *Parameters* window: if selected nodes are of the same type, the Node and Physics settings are available for editing; for the nodes of different types, only shared parameters on the *Node* tab are available.


[Per-surface settings](../../editor2/node_parameters/visual_representation/index.md) (such as material, rendering, or LOD settings) are available only if all selected nodes are of [object-related](../../objects/objects/index.md) types.


> **Notice:** If selected nodes have several different surfaces, per-surface settings will be applied to the entire node as if it has only one surface.
