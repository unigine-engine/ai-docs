# Node Dependencies


Sometimes it might be useful to track dependencies between **runtime-nodes** - nodes that currently exist in the world opened in UnigineEditor, including the ones that are stored only in RAM and have not been saved to a file (`*.world / *.node`) on the disk.


![](menu.png)


In UnigineEditor you can find all runtime-nodes, that use the selected node or group of nodes, to help avoid accidental removal of nodes [somehow used](#dependency_types) by others, as well as to analyze / validate the logic of node interactions (e.g., to check if the right nodes are used in componets etc.). Just select the desired node or group of nodes, right-click on any of them in the *World Nodes Hierarchy* window and choose **Show World Nodes Using This One**.


You'll see a table of dependencies between nodes, it has two columns: the left one contains the list of selected nodes, while the right one shows the nodes that use each of the nodes from the left.


![](dependencies.png)


> **Notice:** Dependencies between runtime-nodes are valid at the moment they are found. If some nodes have been removed or renamed after displaying the dependencies table, you should use the tool again to take all these changes into account.


To display the path to the node in the *World Nodes Hierarchy* check the *Full Node Hierarchy Path* box.


![](with_path.png)


## Types of Dependencies Tracked


The following types of dependencies between runtime-nodes are tracked:


- **Property** - a node can be used in the component logic assigned to other nodes (it is assigned to **Property / C# Component** in the corresponding field). ![](component.png)
- **PlayerPersecutor** - a node can be assigned to the *Target Node* field in the list of *PlayerPersecutor* camera parameters to allow the camera to follow the target node. ![](persecutor.png)
- **Skinned Mesh** - a node can be assigned to the *Bind Node* field of a *Skinned Mesh* object to control the transformations of the skeletal bone to which it is attached. ![](meshskinned.png)
- **Objects** having a physical **Body** can be connected via **Joints**. ![](joint.png)


## Tracking and Container Nodes


If the node of interest is used by another node that is a part of *NodeLayer* or *NodeReference* container, the dependency search will only trace down to the container displaying the hierarchy with *NodeLayer/NodeReference* nodes as atomic units. If you want to find the exact node inside the *NodeReference* container that uses your node of interest, open the container *NodeReference* via **Edit** and search again.
