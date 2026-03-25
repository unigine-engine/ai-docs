# Switcher


**Switcher** is an object that disables or enables its child nodes at a specified distance from the camera. Possible use cases are:


- Enabling one object and disabling another at a specified distance
- Disabling an object while moving away
- Enabling an object while approaching


![](index.gif)

*Each object is composed ofSwitcherand two spheres of different colors*


### See Also


- The *[WorldSwitcher](../../../api/library/worlds/class.worldswitcher_cpp.md)* class to manage *Switcher* via API


## Adding a Switcher


To add *Switcher* to the scene via UnigineEditor, do the following:


1. [Run](../../../sdk/projects/index_cpp.md#run) the project with UnigineEditor.
2. On the Menu bar, click *Create -> Optimization -> Switcher*. ![](add.png)
3. Place the node somewhere in the world.
4. Make the node that will be controlled by *Switcher* a [child](../../../editor2/organizing_nodes/index.md#make_child_node) of the latter.
5. Specify the enabling and the disabling [distance](#editing) in the *Switcher* parameters.


## Switching between Two Objects


To switch between two object at the specified distance (like shown in the picture above), do the following:


1. Create a *[Node Dummy](../../../objects/nodes/dummy/index.md)* for convenient grouping.
2. Make the first *Switcher* the [child](../../../editor2/organizing_nodes/index.md#make_child_node) of the *Node Dummy*.
3. Make the first object the [child](../../../editor2/organizing_nodes/index.md#make_child_node) of the first *Switcher* and specify its [maximum visibility distance](#max_distance).
4. Make the second *Switcher* the [child](../../../editor2/organizing_nodes/index.md#make_child_node) of the *Node Dummy*.
5. Make the second object the [child](../../../editor2/organizing_nodes/index.md#make_child_node) of the second *Switcher* and specify its [minimum visibility distance](#min_distance).


![](hierarchy.png)


> **Notice:** To make objects switch at the same point, the maximum visibility distance of the first one and minimum visibility distance of the second one should match.


## Switcher Parameters


In the *Node* tab of the *[Parameters](../../../editor2/node_parameters/index.md)* window, you can adjust the following parameters of *Switcher*:


![](parameters.png)

*Nodetab of theWorldSwitchernode*


| Min Distance | The minimum distance of visibility, in units. If the camera is closer to a node than this minimum distance, the node is not visible. |
|---|---|
| Max distance | The maximum distance of visibility, in units. If the camera is further from a node than this maximum distance, the node is not visible. |
