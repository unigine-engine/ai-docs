# Node Reference


![](../node_reference.png) **Node Reference** is a node that refers to a `.node` file in the project directory, which is obtained by [exporting a node](../../../editor2/exporting_nodes/index.md) from the world.


> **Notice:** The world can contain several *Node References* referring to the same `.node` file.


The `.node` file usually contains a pre-fabricated node (or a hierarchy of nodes) with links to all materials and properties and configured physical bodies that are required for its rendering and behaviour. All changes made for the *Node Reference* content via UnigineEditor are saved into this file.


*Node References* should be used if a lot of identical objects are placed in the world: unlike regular nodes, *Node Reference* are loaded into the world faster because of the [internal cache](../../../principles/world_management/index.md#node_cache) usage.


Using *Node Reference* enables to avoid manual editing each identical object if you need to make the same changes in all of them. You can simply add several *Node References* that point to one `.node` file and then edit only one *Node Reference* in order to update them all. Such approach enables to hold to integrity of instanced objects, especially if they are complex and sophisticated.


> **Notice:** Each *Node References* has its internal copy of nodes loaded from the `.node` asset, therefore all node references are updated only when saving changes to the asset.


For example, the *Node Reference* can be used to add identical vehicles, characters, or buildings that should have the same look and behaviour and be updated at once, if necessary.


[![](node_reference_usage_sm.jpg)](node_reference_usage.png)

*Boats added as Node References*


*Node References* support nesting, i.e. a *Node Reference* can include other *Node References* which is helpful for implementing complex [instancing](../../../editor2/instancing_nodes/index.md) solutions.


Watch the following tutorial to learn the important things about *Node Reference*:


### Important Notes


> **Notice:** A *Node Reference* can contain only one root node.


#### Referencing Content Outside


A *Node Reference* should be thought of as a container for a self-sufficient hierarchy of nodes. When designing your world in UnigineEditor, avoid referencing nodes that are stored in a *Node Reference* directly from the outside (e.g. when manipulating nodes via [Tracker](../../../editor2/tools/tracker/index.md), creating physical [joints](../../../principles/physics/joints/index.md), specifying nodes in [component parameters](../../../principles/component_system/component_system_cs/index.md#structure_parameters) or the *target node* of a [Player Persecutor](../../../objects/players/persecutor/index.md)) as such references will be lost as soon as the world is reloaded.


#### Transformations


The transformation of a *Node Reference* is not affected by the transformation of the nodes stored by it. Thus, logic-driven and physics-driven nodes inside a *Node Reference* will make no influence on its direct children.


In the following example, the moving grouped *Node_1* and *Node_2* nodes (e.g. driven by physics) contained by a *Node Reference* will not modify the transformation of the *Node Reference* and, therefore, the *DirectChild* node will not be affected as well.


![](unpack_on.png)

*Schematic representation of aNode Referencecontent.*


So, it is recommended to enclose all interconnected nodes in a single *Node Reference* to ensure logical and hierarchical integrity.


### See Also


- The *[Instancing Nodes](../../../editor2/instancing_nodes/index.md)* article to learn more about using *Node References* to create identical objects.
- The *[NodeReference](../../../api/library/nodes/class.nodereference_cpp.md)* class to edit *Node References* via API
- The *[Randomizer](../../../editor2/tools/randomizer/index.md)* plugin to work with multiple *Node References*
- [Node References: Must-Knows](../../../videotutorials/essentials/node_reference.md) demonstrating the specifics of *Node Reference*


## Creating a Node Reference


There are two ways to create a *Node Reference* via UnigineEditor:


- Create a Node Reference from a previously created `.node` asset. In this case, you should export a node into a `.node` file first.
- [Convert a node](../../../editor2/instancing_nodes/index.md#save) with all its child nodes present in the nodes hierarchy list into a *Node Reference*. In this case, the source node will change its type to a *Node Reference*.


### By Using a Node Asset


1. [Export a node into a `.node` file](../../../editor2/exporting_nodes/index.md#export_to_noderef) or [import](../../../editor2/assets_workflow/assets_create_import.md#import) the desired **node** file to the project.
2. Add the *Node Reference* to the world by either of the following ways: ![](added_node_reference.png)

  - On the Menu bar, click *Create -> Node -> Reference* and select the desired `.node` asset in the window that opens: ![](create_node_reference.png) > **Warning:** It is not recommended to select a [geometry container](../../../editor2/fbx/index.md#fbx_container) (*.fbx, .dae, .gtlf*, etc.) as the changes made to its node runtime will not be saved when reimporting the asset.
  - Drag the `.node` asset [from the *Asset Browser* window](../../../editor2/create_import_nodes/index.md#assets).


You can repeat Step 2 in order to add the required number of *Node References*. Or you can simply [clone](../../../editor2/select_position_nodes/index.md#clone_delete) the added node.


![](node_ref_example.png)

*Several Node References with the red material applied*


### By Converting an Existing Node


1. Select a node in the *[World Nodes Hierarchy](../../../editor2/organizing_nodes/index.md)* window (or directly [in the scene](../../../editor2/select_position_nodes/index.md#select_nodes)).
2. On the Menu bar, click *Edit -> Convert to NodeReference* (or press **Ctrl+Shift+G**). ![](convert_to_nodereference.png)


As a result, a new `.node` asset is created at the current folder and the source node is converted into the *Node Reference*:


| ![](source_node.png) | ![](converted_node.png) |
|---|---|
| *Source node to be converted* | *Converted node* |


You can also [clone](../../../editor2/organizing_nodes/index.md#clone_node) the converted node in order to get the required number of *Node References*.


> **Notice:** If you select several nodes and convert them into a *Node Reference*, they are saved into a `.node` file as child nodes of a *[Dummy Node](../../../objects/nodes/dummy/index.md)*.


| ![](source_nodes.png) | ![](converted_nodes.png) |
|---|---|
| *Source nodes to be converted* | *Nodes grouped under aDummy Nodeto which Node Reference refers* |


## Editing a Node Reference


In the *Reference* section of the *Node* tab, you can change the asset of the source node or open the *ReferenceNode Editor* used to edit the source node:


![](path_reference.jpg)

*A node asset*


To edit the source node, to which the *Node Reference* points:


1. Select the *Node Reference* in the *[World Nodes Hierarchy](../../../editor2/organizing_nodes/index.md)* window.
2. Click **Edit** in the *Node* tab of the *[Parameters](../../../editor2/node_parameters/index.md)* window. ![](edit_reference.jpg) The source node becomes available in the *World Nodes Hierarchy* window as a child of the Node Reference and can be edited via the *Parameters* window. ![](source_node_edit.png) *World Nodes Hierarchywindow: source node in the edit mode*
3. Edit the source node. For example, you can change the material applied to it: | ![](node_ref_example.png) *Node References with the red material applied* | ![](node_ref_example_edit.png) *Node References with the changed material* | |---|---| You can also [reorganize hierarchy](../../../editor2/organizing_nodes/index.md) and replace the source nodes, but keep note that only the first child will be saved in the Node Reference as ***Node Reference* can contain only one root node**.
4. After all changes are made, select the parent node in the *World Nodes Hierarchy* window and click **Apply** to save changes to the source node or **Cancel changes** to keep nodes unchanged. ![](editor_reference.jpg) *Referencesection in theNodetab of the parent Node Reference*


It is also possible to quick-replace the source node with another one stored in the same folder. To do that, select a *Node Reference* in the *World Nodes Hierarchy* window or the Viewport, hold **Shift** and use the mouse wheel or **Page Up** and **Page Down** buttons.


![](node_ref_switch.gif)


## Baking Light and Shadows for a Node Reference


Instances of a Node Reference may be illuminated differently. Thus, when [light is baked](../../../editor2/lighting/gi/bake_lighting/index.md) for each of them, they will have individual [lightmaps](../../../editor2/lighting/gi/lightmaps.md) and depth textures (shadow maps). If you modify the Node Reference (change its hierarchy, replace the referenced asset, etc), these textures will be rebaked automatically after the *Apply* button is clicked. In code, the textures are updated by using [the corresponding method](../../../api/library/nodes/class.node_cpp.md#applyReplacePaths_void).


However, modifying (resetting) the path to the Node Reference's baked texture will affect all instances of the Node Reference, and automatic replacement of the unique baked texture for each individual Node Reference won't be available anymore. (You will have to replace baked textures manually for each instance.)


## Deleting a Node Reference


You can delete the *Node Reference* the same way as any other [node](../../../objects/nodes/node/index.md#delete_node).
