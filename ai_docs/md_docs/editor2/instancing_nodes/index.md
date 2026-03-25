# Instancing Nodes


![](instances.png)


The virtual world, that you're building, may contain a lot of identical objects, that should always look the same, such as electricity pylons, planes, wheels, boxes, etc.


When you clone these objects and place them in your world, multiple separate copies are created. Thus, if you decide to change something (e.g., the geometry or materials of some parts of the pylons) you'll have do that for each copy individually.


Instead of making copies of an object, it is recommended to make instances of a single one. Such approach ensures integrity when changing the parameters of the repeatedly used objects, especially if they are complex and sophisticated. To do so,  You can simply add several *[Node References](../../objects/nodes/reference/index.md)* referring to a single `*.node` file and then edit only one node reference in order to update all of them.


Below is the typical workflow for node instancing based on *Node References*.


## 1. Creating a Hierarchy of Nodes


First of all we should prepare the basic hierarchy, that will represent our object. Suppose we have [organized the nodes hierarchy](../../editor2/organizing_nodes/index.md) for a helicopter, that we are going to reuse several times in our world (see the picture below)


![](helicopter_hierarchy.png)


## 2. Converting the Hierarchy of Nodes


The second step is to convert the hierarchy of nodes to a *[Node Reference](../../objects/nodes/reference/index.md)*. You can do that by simply dragging the root node of the hierarchy to the desired folder in the [*Asset Browser*](../../editor2/assets_workflow/index.md#asset_browser). A corresponding `*.node` asset (source), containing the hierarchy, will be created in the folder. The node hierarchy will be replaced with a reference to this asset.


![](drag_hierarchy.gif)


You can also convert a single node or a group of selected nodes in the [*World Nodes Hierarchy*](../../editor2/interface/index.md#world_hierarchy) window via the context menu. To do so, select the desired node(s) in the *World Nodes Hierarchy* window, right-click on the selected node and choose *Create a Node Reference*. A corresponding `*.node` asset (source), containing the selected node (or a group of nodes as children with a *[Dummy Node](../../objects/nodes/dummy/index.md)* as the root), will be created in the current folder opened in the *Asset Browser*. Selected nodes will be replaced with a reference to this asset.


![](context_menu.png)


## 3. Placing Instances


So, we already have the first instance in the world. It's the one, that replaced the hierarchy, when we dragged it to the *Asset Browser*. To add other instances to the world, we can simply drag the desired `*.node` asset from the *Asset Browser* directly to the *Scene Viewport*.


> **Notice:** The new instance will be placed at the origin.


Or you can simply clone a node reference, as any other node, via the *Scene Viewport* by moving it with a manipulator while holding the **Shift** key. In this case a new instance will be placed exactly where you point to.


![](add_instance.gif)


## 4. Editing the Source Node from its Instances


If you decide to change something in the source node, you can do that by editing any of its instances. To do so, perform the following steps:


1. Select any instance in the world via the *Scene Viewport* or the *World Nodes Hierarchy* window. The parameters of the node reference will be displayed in the *Parameters* window. ![](edit_source.png)
2. Click *Edit*. The hierarchy of the source node will be displayed in the *World Nodes Hierarchy* window. ![](edit_hierarchy.png)
3. Edit the source node. You can make any changes: modify materials, add new nodes, remove existing ones, etc.
4. Click *Apply* to save changes made to the source node or *Cancel* to discard them. The changes will be applied to all instances at once. ![](apply_source.png) ![](instances_changed.png)


> **Notice:** Modifying (resetting) the path to the Node Reference's baked [lightmap](../../editor2/lighting/gi/lightmaps.md) will affect all instances of the Node Reference, and [automatic replacement](../../objects/nodes/reference/index.md#bake_light) of the unique baked texture for each individual Node Reference won't be available anymore. (You will have to replace baked textures manually for each instance.)


## Video Tutorial: Instancing Nodes


## Video Tutorial: Node References: Must-Knows
