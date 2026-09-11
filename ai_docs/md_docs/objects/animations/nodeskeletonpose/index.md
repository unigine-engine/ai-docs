# Skeleton Pose


A **Skeleton Pose** node drives skeletal animation for one or more *[Skinned Mesh](../../../objects/objects/mesh_skinned/index.md)* objects. It holds a skeleton, computes the final blended pose each frame, and applies it to all controlled meshes.


This node replaces the built-in animation player that was part of *[Skinned Mesh (Legacy)](../../../objects/objects/mesh_skinned_legacy/index.md)*, providing a cleaner separation between rendering and animation control.


### See Also


- The *[NodeSkeletonPose](../../../api/library/nodes/class.nodeskeletonpose_cpp.md)* class.
- The *[Animation](../../../content/animations/index.md)* content section for details on building animations in UNIGINE.


## Adding a Skeleton Pose


To add a *Skeleton Pose* to the scene via UnigineEditor:


1. On the Menu bar, click *Create -> Animation -> Skeleton Pose*.
2. In the dialog window that opens, choose the path to a `.skeleton` file.
3. Place the node in the world.


![](create_nodeskeletonpose.png)


The *[Skinned Mesh](../../../objects/objects/mesh_skinned/index.md)* objects to be animated should be placed as children of this node, or added to the controlled objects list.


## Skeleton


A `.skeleton` file must be assigned to define the bone structure. The skeleton provides joint names, hierarchy, bind pose transforms, and optionally retargeting data and animation masks.


![](skeleton.png)


## Animation Modes


Skeleton Pose supports two modes of operation:


- **Anim Script** - animation logic is driven by a visual [animation graph](../../../content/animations/index.md) with state machines, blend spaces, and transitions.
- **Anim Layers** - manual layer-based blending. You create layers, assign `.anim` files to them, set weights, and control blending via API.


![](anim_mode.png)


## Control Type


The control type defines how the *Skeleton Pose* node finds the *Skinned Mesh* objects it should animate:


- **Hierarchy** - automatically controls all *[Skinned Mesh](../../../objects/objects/mesh_skinned/index.md)* child nodes in the hierarchy.
- **List** - controls only the meshes explicitly added to the controlled objects list.


![](anim_control_type.png)


## Animation Settings


Depending on the selected mode, the *Parameters* window displays different settings:


- In **Anim Script** mode - an animation graph file (`.agraph`) is assigned. The graph controls all animation logic internally.
- In **Anim Layers** mode - a preview animation file (`.anim`) can be assigned for previewing in the Editor.


| ![](using_graph.png) *Anim Script mode* | ![](using_layers.png) *Anim Layers mode* |
|---|---|
