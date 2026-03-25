# Node


A **node** is a generic entity representing any object that is presented in the world and specifically positioned and oriented. The node is created and stored in the world hierarchy. All changes made to the node are saved in the `.world` file. You can also export any subset of the world hierarchy (a node or a hierarchy of nodes) to an external `.node` asset and then import it into the world when necessary or create a [reference](../../../objects/nodes/reference/index.md) to it. However, all changes made for the original node via UnigineEditor will still be saved into the `.world` file.


### See Also


- The *[Node](../../../api/library/nodes/class.node_cpp.md)* class to edit nodes via API


## Creating a New Node


To create a new node via UnigineEditor, click *Create* on the Menu bar, choose a required node type and add it to the scene. The new node will appear in the [*World Nodes*](../../../editor2/interface/index.md#world_hierarchy) list. For example, you can add a static mesh which will be a node in terms of Unigine:


[![](create_node_sm.jpg)](create_node.png)

*Creating a new node*


## Editing a Node


The node can be edited via the *[Parameters](../../../editor2/node_parameters/index.md)* window of UnigineEditor. All nodes have [common settings](../../../editor2/node_parameters/transformation_common/index.md) which are presented in the *Node* tab. Also each node has special settings, which vary depending on the type of the node.


Editing the node also includes editing [materials](../../../editor2/materials_settings/index.md) and [properties](../../../editor2/properties_settings/index.md) assigned to the node.


## Importing a Node


Besides creating a new node, you can import the existing node which was previously [exported](../../../editor2/exporting_nodes/index.md#export_to_noderef) into an external `.node` file.


To import the content of a `.node` asset into the current world, click *Create -> Node -> Reference Contents*. In the *Select Node* dialog window that opens, choose the required `.node` asset.


You can also do it by means of the [Asset Browser](../../../editor2/create_import_nodes/index.md#assets).


> **Notice:** Once imported, the node content isn't linked to the source `.node` file anymore. So, if you edit the imported node via UnigineEditor, changes will be saved only in the `.world` file.


## Deleting a Node


To delete a node from the world, select it and press **Delete**. The node will be removed from the `.world` file after saving the world via UnigineEditor.


> **Notice:** Deleting the node doesn't affect the `.node` file.
