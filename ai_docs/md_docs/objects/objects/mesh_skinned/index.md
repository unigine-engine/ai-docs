# Skinned Mesh


A ![](mesh.png)�**skinned mesh** is an object that contains mesh geometry with skeletal deformation support. It is usually used for rendering characters with a bone-based animation or a morph target animation (also known as blend shapes).


Unlike [Skinned Mesh (Legacy)](../../../objects/objects/mesh_skinned_legacy/index.md), the new skinned mesh does not have a built-in animation player. Animation is controlled externally via [NodeSkeletonPose](../../../objects/animations/nodeskeletonpose/index.md) and [Animation Graphs](../../../content/animations/index.md).


![](skinned_1.png)


A *skinned mesh* is created in third-party graphics programs (such as 3ds Max, Maya, etc.)


The **mesh limitations** set in UNIGINE:


| Maximum number of **vertices** per mesh | 4,294,967,295 |
|---|---|
| Maximum number of **surfaces** per mesh | 32,768 |
| Maximum amount of **weights** per vertex | 4 |


### See Also


- The *[Adding Morph Targets](../../../content/tutorials/morph/index_cpp.md)* tutorial to know how to add morph targets in Unigine
- The *[Mesh File Format](../../../code/formats/file_formats.md)* article to know more about `.mesh` and `.mesh_skinned` formats
- The *[ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_cpp.md)* class to edit skinned meshes via API


## Adding a Skinned Mesh


To add a *skinned mesh* to the scene via UnigineEditor, do the following:


![](skinned_create.png)


1. On the Menu bar, click *Create -> Mesh -> Skinned*.
2. In the dialog window that opens, choose the path to the `.mesh` file.
3. Place the mesh somewhere in the world.


## Dual-Quaternion Skinning


Toggles the dual-quaternion skinning mode on and off. The dual-quaternion model is an accurate, computationally efficient, robust, and flexible method of representing rigid transforms and it is used in skeletal animation.


![](mesh_skinned.png)


## Controlling Morph Targets


For meshes containing morph targets, the *Morph Targets Preview* list is available in the *Parameters* window. This set of parameters in the Editor allows visualizing what the model looks like with one or more morph targets applied. Actual application of morph targets and their weights is done via [code](../../../api/library/objects/class.objectmeshskinned_cpp.md#setSurfaceTargetEnabled_int_int_int_void).


![](morph_targets_preview.png)


Each target has a slider that allows configuring its weight � the extent of the morph target's effect on the resulting view of the model.


***Basis*** represents the original position of all vertices of the mesh, and its slider is shown for reference.


## Optimizing Animation Playback


Updating each frame a huge number of objects located far away from the camera that are hardly distinguishable or observed as a mass is a waste of resources.


To improve performance and avoid the excessive load, animation playback can be [updated with a reduced framerate](../../../principles/world_management/index.md#periodic_update). When the player is out of the area specified by **Update Distance Limit**, the animation stops to be updated and freezes statically.


The set of frame rates enables you to specify how often the animation playback should be updated when the object is visible, when only the shadow of the Skinned Mesh is visible, or when it is not visible at all.


![](../../../principles/world_management/periodic_update.png)

*Parameterstab ->Periodic Updatesection*


| FPS When Object Is Rendered To Viewport | Update rate value for the case when the object is rendered to viewport. |
|---|---|
| FPS When Only Object Shadows Are Rendered | Update rate value when the object itself is outside the viewing frustum, and only its shadow is rendered to viewport. |
| FPS When Object Is Not Rendered At All | Update rate value when both the object and its shadow are not rendered to the viewport. |
| Update Distance Limit | Distance from the camera up to which the object should be updated. |


> **Notice:** These values are not fixed and can be adjusted by the Engine at any time to ensure best performance.


This feature is enabled with default settings ensuring optimum performance and can be adjusted per-object in the UnigineEditor or via API at run time.


> **Warning:** Please be aware that using reduced update frame rate for an object should be carefully considered in your application's logic, as it may lead to various issues with rendering *Skinned / Dynamic Meshes* (flickering due to misalignment, e.g. in case of attaching a cloth to a *skinned mesh*).
