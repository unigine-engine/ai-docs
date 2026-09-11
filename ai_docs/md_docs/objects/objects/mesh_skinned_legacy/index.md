# Skinned Mesh (Legacy)


A ![](mesh.png)�**skinned mesh (legacy)** is a monolithic object that contains both mesh geometry and a built-in animation player. It is usually used for rendering characters with a bone-based animation or a morph target animation (also known as blend shapes).


> **Notice:** For new projects, use the modern approach: a [Skinned Mesh](../../../objects/objects/mesh_skinned/index.md) for rendering and a [Skeleton Pose](../../../objects/animations/nodeskeletonpose/index.md) node for animation control. The modern setup separates rendering from animation logic, supports [animation graphs](../../../content/animations/index.md), and provides a cleaner architecture. The *Skinned Mesh (Legacy)* is kept for backward compatibility with existing projects.


The mesh geometry is stored in a `.mesh_skinned` file, while animation data is stored in separate `.anim` files.


![](skinned_1.png)


A *skinned mesh* is created in third-party graphics programs (such as 3ds Max, Maya, etc.)


Most operations with the *skinned mesh (legacy)* are performed via scripts, but you can do some of them via UnigineEditor:


- [Add](#adding) a *Skinned Mesh (Legacy)*.
- [Load](#loading) a *Skinned Mesh (Legacy)* and animation.
- [Adjust](#setting) animation settings.


The **mesh limitations** set in UNIGINE:


| Maximum number of **vertices** per mesh | 4,294,967,295 |
|---|---|
| Maximum number of **surfaces** per mesh | 32,768 |
| Maximum amount of **weights** per vertex | 4 |


### See Also


- The *[Adding Morph Targets](../../../content/tutorials/morph/index_cpp.md)* tutorial to know how to add morph targets in Unigine
- The *[Mesh File Format](../../../code/formats/file_formats.md)* article to know more about `.mesh` and `.mesh_skinned` formats
- *[Animation](../../../sdk/api_samples/cs/animation.md)* sample in *C# Component Samples* suite
- The *[ObjectMeshSkinnedLegacy](../../../api/library/objects/class.objectmeshskinnedlegacy_cpp.md)* class to edit skinned meshes via API


## Adding a Skinned Mesh (Legacy)


To add a *skinned mesh (legacy)* to the scene via UnigineEditor, do the following:


1. [Run](../../../editor2/index.md#run) UnigineEditor.
2. On the Menu bar, click *Create -> Mesh -> Skinned (Legacy)*. ![](skinned_create.png)
3. In the dialog window that opens, choose the path to the `.mesh_skinned` file.
4. Place the mesh somewhere in the world.


> **Notice:** You can change the path to the mesh at any time in the *Mesh Skinned Legacy* tab.


## Loading a Skinned Mesh (Legacy) and Animation


To replace a loaded *skinned mesh (legacy)* with a new one, do the following:


1. Choose the mesh in the *[World Hierarchy](../../../editor2/organizing_nodes/index.md)* window and go to the *Node* tab of the *[Parameters](../../../editor2/node_parameters/index.md)* window.
2. In the *Mesh Skinned Legacy* section, choose the path to the new `.mesh_skinned` file in the *Mesh* field.


![](loading.png)


To add animation or replace the existing with a new one via UnigineEditor, do the following:


1. Choose the mesh in the *[World Hierarchy](../../../editor2/organizing_nodes/index.md)* window and go to the *Node* tab of the *[Parameters](../../../editor2/node_parameters/index.md)* window.
2. In the *[Mesh Skinned Legacy](#preview_anim)* section, choose the path to a new `.anim` file in the *Preview Animation* field.


## Setting Up Animation


You can perform the following operations with the *skinned mesh (legacy)* animation via UnigineEditor:


![](setting.png)

*Mesh Skinned Legacy tab*


| Loop | Play an animation in a loop. |
|---|---|
| Quaternion | Toggles the dual-quaternion skinning mode on and off. The dual-quaternion model is an accurate, computationally efficient, robust, and flexible method of representing rigid transforms and it is used in skeletal animation. |
| Controlled | Set the flag identifying that the mesh animation is controlled by a parent skinned mesh. |
| Time | Set the animation time, in animation frames. The time count starts from the zero frame. If the time is set to be between frames, animation is blended. If the time is set outside the animation frame range, the animation is looped. |
| Playback Speed | The multiplier of the animation playback [time](#time). |
| Preview Animation | Path to a file with animation (`.anim`) to be played. |
| Play | Start the animation playback. |
| Stop | Stop the animation playback. |


## Setting Up Bones


Bone hierarchy of your *skinned mesh (legacy)* is displayed in the *Bones* section of the *Parameters* window.


Each bone of a *skinned mesh (legacy)* can be bound to a separate node to control its transformation giving you a lot of flexibility. For example, you can animate these nodes via the Tracker tool or enable physics-based control over *skinned mesh (legacy)* bones binding them to nodes driven by physics.


![](skinned_bones.png)

*Mesh Skinned Legacy tab*


| Visualize Bones | Enable visualizer for bones and their basis vectors to monitor your settings while adjusting them. The visualizer is rendered even when a *skinned mesh (legacy)* is not selected in the *World Nodes* hierarchy, making it possible to show positions of bones for multiple meshes simultaneously. > **Notice:** The global Visualizer is enabled automatically, when you check this option. ![](bone_visualizer.png) |
|---|---|
| Create Dummy Hierarchy | Creates a hierarchy of [dummy nodes](../../../objects/nodes/dummy/index.md) for the *skinned mesh (legacy)*, where each node has the same name and transform as the corresponding bone and is bound to it with default settings. > **Notice:** The hierarchy can also be generated for selected bones only. |
| Bind Node | Node whose transformation is used to control the transformation of the bone. |
| Node Transform Basis | Defines which transformation of the bound node (*World* or *Local*) is to be used to override the transformation of the selected bone. |
| Bone Transform Basis | Defines which transformation of the selected bone is to be overridden by the [node's](#bind_node) transformation: - World coordinates - Coordinates relative to the *skinned mesh (legacy)* object - Coordinates of the parent bone |
| Bind Mode | Defines the type of blending of node's and bone's transformations: - **Override** � replace bone's transformation with the transformation of the node. - **Additive** � node's transformation is added to the current transformation of the bone. |
| Position Offset | *Translation* part of the additional transformation matrix applied to the node's transformation before applying it to bone's transformation. This parameter serves for the purpose of additional correction of the node's transform for the bone's basis. |
| Rotation Offset | *Rotation* part of the additional transformation matrix applied to the node's transformation before applying it to bone's transformation. This parameter serves for the purpose of additional correction of the node's transform for the bone's basis. |
| Scale Offset | *Scaling* part of the additional transformation matrix applied to the node's transformation before applying it to bone's transformation. This parameter serves for the purpose of additional correction of the node's transform for the bone's basis. |
| Reset Node Transform | Resets initial node transformation. |
| Reset Bone Transform | Reset bone transformation. This button is used to restore initial transformation of the bone after modifying it via a [bound node](#bind_node). |


## Optimizing Animation Playback


Updating each frame a huge number of objects located far away from the camera that are hardly distinguishable or observed as a mass is a waste of resources.


To improve performance and avoid the excessive load, animation playback can be [updated with a reduced framerate](../../../principles/world_management/index.md#periodic_update). When the player is out of the area specified by **Update Distance Limit**, the animation stops to be updated and freezes statically.


The set of frame rates enables you to specify how often the animation playback should be updated when the object is visible, when only the shadow of the Skinned Mesh (Legacy) is visible, or when it is not visible at all.


![](../../../principles/world_management/periodic_update.png)

*Parameterstab ->Periodic Updatesection*


| FPS When Object Is Rendered To Viewport | Update rate value for the case when the object is rendered to viewport. |
|---|---|
| FPS When Only Object Shadows Are Rendered | Update rate value when the object itself is outside the viewing frustum, and only its shadow is rendered to viewport. |
| FPS When Object Is Not Rendered At All | Update rate value when both the object and its shadow are not rendered to the viewport. |
| Update Distance Limit | Distance from the camera up to which the object should be updated. |


> **Notice:** These values are not fixed and can be adjusted by the Engine at any time to ensure best performance.


This feature is enabled with default settings ensuring optimum performance and can be adjusted per-object in the UnigineEditor or via API at run time.


> **Warning:** Please be aware that using reduced update frame rate for an object should be carefully considered in your application's logic, as it may lead to various issues with rendering *Skinned / Dynamic Meshes* (flickering due to misalignment, e.g. in case of attaching a cloth to a *skinned mesh (legacy)*).


## Controlling Morph Targets


For meshes containing morph targets, the *Morph Targets Preview* list is available in the *Parameters* window. This set of parameters in the Editor allows visualizing what the model looks like with one or more morph targets applied. Actual application of morph targets and their weights is done via [code](../../../api/library/objects/class.objectmeshskinnedlegacy_cpp.md#setSurfaceTargetEnabled_int_int_int_void).


![](morph_targets_preview.png)


Each target has a slider that allows configuring its weight � the extent of the morph target's effect on the resulting view of the model.


***Basis*** represents the original position of all vertices of the mesh, and its slider is shown for reference.
