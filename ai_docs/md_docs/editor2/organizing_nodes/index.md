# Organizing Nodes


In Unigine, nodes are organized in a [hierarchy](../../principles/world_structure/index.md#nodes_hierarchy) that can be managed via the *[World Nodes](../../editor2/interface/index.md#world_hierarchy)* window.


To open this window, choose *Windows → World Hierarchy* in the Menu.


![](world_hierarchy_detailed.png)

*World NodesWindow*


As you can see, this window allows filtering nodes by name and type, collapsing and expanding nodes hierarchy (i.e., showing only the parent nodes and hiding the child ones or showing all nodes added to the world), and changing nodes hierarchy - [rearranging](#rearrange_node), [reparenting](#reparent_node), [cloning](#clone_node), [renaming](#rename_node), [deleting](#delete_node), and [grouping](#group_nodes) the nodes.


> **Notice:** When building a hierarchy, take into account [multi-threaded update of dependent nodes](../../principles/world_management/index.md#multithreading).


The *World Nodes* window contains all nodes existing in the current world. Some nodes can be instances of the [asset files](../../editor2/assets_workflow/asset_types.md): meshes, sounds, terrains, instanced nodes, or nodes stored in the `*.node` files.


When you add a new node to the scene via the [Menu Bar](../../editor2/interface/index.md#menu_bar) (the *Create* menu) or by dragging it from the *[Asset Browser](../../editor2/assets_workflow/assets_create_import.md)*, it is automatically added to the nodes hierarchy and displayed in the *World Nodes* window.


In front of the name of each node, there is a set of icons:


- ![](property.png) � indicates that the node has [a property assigned](../../editor2/node_parameters/properties/index.md#node_property). > **Notice:** The property is considered assigned even if it is empty (i.e., no property name is specified).
- ![](selection_on.png) / ![](selection_off.png) � toggles [node selection](../../editor2/select_position_nodes/index.md#select_nodes) on and off.
- ![](transformation_on.png) / ![](transformation_off.png) � toggles [node transformation](../../editor2/node_parameters/transformation_common/index.md#transformation_params) on and off.
- ![](state_on.png) / ![](state_off.png) � toggles the node is [on or off](#toggle_node).


To manage these icons, click **Filter by node type** and specify the icons you want to show or hide in the *Show Columns* section. Note that the state icon ![](state_on.png) always stays visible.


![](manage_icons.png)


## Toggling Nodes


To toggle a node on and off, left-click the checkbox in front of it. If the flag is unchecked, the node will not be rendered.


![](toggling.gif)

*Toggling a node on and off*


You can also enable and disable a group of selected nodes:


![](multiselection_toggling.gif)

*Multi-selection toggling*


A node can also be disabled and enabled in the *[Parameters](../../editor2/node_parameters/transformation_common/index.md#enabled)* window.


## Renaming Nodes


To rename a node, select it in the *World Nodes* and left-click it once again (slow double-clicking) to enter a new name.


![](rename_node.gif)

*Renaming a Node*


You can also right-click a node, choose **Rename** in the drop-down list, and type a new name.


A node can also be renamed in the *[Parameters](../../editor2/node_parameters/transformation_common/index.md#name)* window:


![](rename_via_parameters.png)

*Renaming viaParametersWindow*


> **Notice:** Renaming a node doesn't lead to renaming the asset it is linked to (if any).


## Rearranging Nodes


To move a node to a specific position in the hierarchy, drag it with the **left mouse button** pressed.


![](rearrange.gif)

*Moving a Node in Hierarchy*


The position in the hierarchy, where the node will be placed, is highlighted with the *white line*:


![](move_node.png)

*Highlighted Position*


## Setting Up Nodes Inheritance


Nodes in the scene have hierarchical arrangement: each node (*parent node*) can have multiple children (*child nodes*). It allows you, for example, to change the transformation of several nodes only by transforming the parent node.


To collapse or expand the list of child nodes, click the *arrow* to the left of the parent node.
You can also collapse all child nodes in the *World Nodes* window by clicking ![](collapse_nodes.png), or expand the list to see all nodes in the *World Nodes* by clicking ![](expand_nodes.png).


By default, a new node added to the scene is positioned at the root level of the nodes hierarchy. You can set up its inheritance in one of the ways described below.


### Making a Parent Node


To make one node a parent for the other node (or several nodes), select both the parent and the desired child nodes, right-click the parent node, and choose **Make Parent** in the drop-down list:


![](make_parent.gif)

*Making a Parent Node*


By using this option, you can perform reparenting for the hierarchy tree branch: select the target branch, right-click the desired parent node and choose **Make Parent** in the drop-down list. It produces the following:


1. The new-made parent is always placed at the root level of the hierarchy.
2. The child nodes positioned at the different hierarchy levels are placed at the same level.


![](reparent.gif)

*Reparenting Nodes*


### Making a Child Node


To add one node as a child to the other in the hierarchy, or reparent a node, drag it holding the **left mouse button** to the desired parent node.


![](move_as_child.gif)

*Adding a Child Node*


The parent node to which the node will be added, is highlighted with the *white frame*:


![](move_as_child.png)

*Highlighted Parent Node*


You can also [move](#rearrange_node) a node to a specific position alongside the child nodes of the desired parent: the node will be added as a child to this parent node.


![](moved_as_child.png)

*Moving Node As a Child*


### Unparenting a Node


To detach a node from its parent, right-click it and choose **Unparent** in the drop-down list:


> **Notice:** The node is detached only from its direct parent and placed at the same level as the former parent.


![](unparent.gif)

*Detaching a Node from Its Parent*


To reset inheritance of a child node (i.e., detach it from all parents and place at the root level of the hierarchy), simply [drag](#rearrange_node) it to the corresponding position in the hierarchy.


## Cloning a Node


To clone a node, right-click it and choose **Clone** in the drop-down list:


![](clone_node.gif)

*Cloning a Node*


You can also select the node and press **Ctrl+D** to perform the same operation. The new node will be created at the same hierarchy level as the original one, and have the same transformation. If the original node has children, they will be cloned as well.


Another way to clone a node is to select it, press **Shift** and drag the node's arrow manipulator.


## Copying a Node


To copy a node, right-click it and choose **Copy** in the drop-down list:


![](copy_node.png)

*Copying a Node*


The node will be copied to the clipboard. To paste the copied node right-click anywhere in UNIGINE Editor and select **Paste** in the drop-down list.


You can also use the **Ctrl+C** and **Ctrl+V** hotkeys to perform the same operations.


**The copied node can be pasted in any world within the same project.**


## Deleting a Node


To delete a node from the hierarchy, right-click it and choose **Delete** in the drop-down list:


![](delete_node.gif)

*Deleting Node*


You can also select a node and press **DELETE** to perform the same operation.


> **Notice:** If you delete a parent node, all its child nodes will be deleted as well.


Deleting a node doesn't lead to deleting the asset it is linked to (if any).


## Filtering Nodes


Filtering nodes simplifies their management in a large world.


You can select which node types to display in the *World Nodes* window: click ![](filter_button.png) and choose the required node types. Here, you can also specify how to view the filtered nodes - as a flat list (*Flat List View*) or according to their hierarchy (*Hierarchy View*).


You can temporarily show all objects by clicking **Enable All**. At that, the current filter settings will be preserved.


![](filter_nodes.gif)

*Filtering Nodes*


Nodes can be filtered by name or by ID. Type the node name or ID in the corresponding field.


![](filter_by_name.gif)

*Filtering Nodes by Name*


> **Notice:** The ID should be typed in full.


![](filter_by_id.gif)

*Filtering Nodes by ID*


## Grouping Nodes


Grouping nodes allows managing several nodes simultaneously. The grouped nodes can be transformed as a single node relative to a [pivot point](../../editor2/select_position_nodes/index.md#pivot_point)


When grouping nodes, a new *[Dummy Node](../../objects/nodes/dummy/index.md)* is created, and all selected nodes become its children. At that, the hierarchy of grouped nodes persists.


To group nodes, [select](../../editor2/select_position_nodes/index.md#select_nodes) them, right-click, and choose **Group** in the drop-down list or press **Ctrl+G**:


![](group_nodes.gif)

*Grouping Nodes*


The grouped nodes can be selected and transformed as a single node:


![](nodedummy_group.png)

*Grouped Nodes*
