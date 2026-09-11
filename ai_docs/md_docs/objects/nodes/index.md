# Nodes


In terms of Unigine, all of the objects added into the scene are called **nodes**. Nodes can be used both directly or as reference nodes to which the other nodes refer.


### Nodes and Node References


Nodes and *Node References* are fundamental objects that form the world:


- [![](node.png)](../../objects/nodes/node/index.md) � [**Node**](../../objects/nodes/node/index.md) is a generic entity representing any object that is positioned and stored in the world.
- [![](node_reference.png)](../../objects/nodes/reference/index.md) � **[Node Reference](../../objects/nodes/reference/index.md)** is a node that refers to an external file on the disk, which contains a pre-fabricated node (or a hierarchy of nodes) with all the materials and properties that are required for its rendering.


> **Notice:** A *Node Reference* should be used instead of the node if there are a lot of identical objects repeated in the world:  it helps avoid manual editing of each object in case you need to make the same changes in all of these objects. For more details, read the article on *[Node Reference](../../objects/nodes/reference/index.md)*.


There are also the following differences between nodes and *Node References*:


- To create a node, you need to simply add any object to the scene. To create a *Node Reference*, you will need to export a node from UnigineEditor into a `.node` file and then specify it to be a *Node Reference*.
- All changes made for the node are saved in the `.world` file and affect only one specific node. All changes made for the *Node Reference* are saved in the source `.node` file and affect all the nodes referenced to this file.


### Base Nodes


Base nodes are invisible and perform the following:


- [![](node_dummy.png)](../../objects/nodes/dummy/index.md) � **[Dummy Node](../../objects/nodes/dummy/index.md)** is used to organize other nodes into a hierarchy.
- [![](node_layer.png)](../../objects/nodes/layer/index.md) � **[Layer](../../objects/nodes/layer/index.md)** enables to save all its child nodes into a separate `.node` file.
- [![](node_trigger.png)](../../objects/nodes/trigger/index.md) � **[Trigger](../../objects/nodes/trigger/index.md)** fires callbacks when it is enabled/disabled or its transformation has been changed.
