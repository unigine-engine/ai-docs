# Layer


A ![](../node_layer.png) � **layer** is a zero-sized node that has no visual representation and enables to save all its child nodes into a separate `.node` file. Layer nodes should be used as containers for editing the other nodes in the world: you can split the world into several logical parts and save each of them in a `.node` file. It will enable to facilitate collaborative work on one project by eliminating conflicts arising from simultaneous editing of this world by several people.


> **Warning:** DO NOT use multiple layer nodes referring to the same `.node` file! This leads to conflicts when saving changes. If you want to have several instances of `.node` file contents, please use *[Node References](../../../objects/nodes/reference/index.md)*.


![](layer_nodes.png)

*World Nodes Grouped into Several Layers*


> **Notice:** All changes made in child nodes of a layer node will not affect the source `.world` file.


The contents of a layer depend on the hierarchy structure: to become part of a layer, a node should be assigned to it as a child. In the [World Nodes Hierarchy](../../../editor2/organizing_nodes/index.md) window, a layer node is displayed as a usual node that can be transformed, cloned and so on.


Layer nodes are especially convenient when using the VCS, because by merging the project modifications there will be no need to match the conflicted files.


> **Notice:** Using layer nodes won't prevent conflicts if the same layer is simultaneously edited by several people.


Unlike a *[Node Reference](../../../objects/nodes/reference/index.md)*, a layer node can contain more than 1 node of the same level in the hierarchy.


### See also


- The *[NodeLayer](../../../api/library/nodes/class.nodelayer_cpp.md)* class to edit layers via API


## Adding a Layer Node


To add a new layer via UnigineEditor do the following:


1. [Run](../../../editor2/index.md#run) UnigineEditor.
2. On the Menu bar, click *Create -> Node -> Layer*. ![](layer_create.png)
3. In the *Save Node* file dialog window that opens, specify a name for the `.node` file into which child nodes of the layer will be saved.
4. Place the layer node in the world. ![](add_layer_node.png)
5. Add child nodes to the layer node: select the required nodes and [drag](../../../editor2/organizing_nodes/index.md#reparent_node) the nodes inside the layer node: ![](move_as_child.gif)


## Editing a Layer Node


Changes made in the child nodes of the layer node are saved on the disk when:


- Clicking **Save** in the *Node* tab of the *[Parameters](../../../editor2/node_parameters/index.md)* window.
- Saving the world via *File -> Save World* or by pressing **Ctrl+S**.


In both cases only the `.node` file will be updated.


![](edit_layer_node.png)

*Node Tab*


The `.node` file contains all child nodes of the layer node. All changes made in child nodes of the layer node do not affect the source `.world` file.


> **Notice:** The layer node itself is not stored in the `.node` file.
