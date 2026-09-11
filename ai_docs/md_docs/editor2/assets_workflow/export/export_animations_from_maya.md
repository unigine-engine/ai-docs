# Exporting Animated Models From Autodesk Maya


To bring an animated character from *Autodesk Maya* into UNIGINE, you need to export the mesh, skeleton, and animation data as an FBX file. This article covers the recommended export and import settings to get the best results.


> **Notice:** This guide is based on **Autodesk Maya 2025** and **UNIGINE SDK 2.21**. The general workflow applies to other recent versions; however, UI details may vary.


For static model export (with no animation), see [Exporting 3D Models From Autodesk Maya](../../../editor2/assets_workflow/export/export_from_maya.md).


## What UNIGINE Creates on Import


When you import an FBX file with a rigged and animated character, UnigineEditor splits it into three native assets:


- **[Skeleton](../../../content/animations/animation_assets/index.md#skeleton)** (`*.skeleton`) - joint hierarchy and bind pose.
- **[Skinned Mesh](../../../content/animations/animation_assets/index.md#skinned_mesh)** (`*.mesh_skinned`) - 3D model with skinning weights.
- **[Animation](../../../content/animations/animation_assets/index.md#animation)** (`*.anim`) - animation clips with per-joint transforms for each frame.


These assets are independent after import and can be modified without reimporting the source file. For more details, see [Preparing Animation Assets](../../../content/animations/animation_assets/index.md).


## 1. Prepare the Scene in Maya


Before configuring the export settings, make sure your scene is set up correctly in *Maya*.


### Orient the Model


Orient the character so it faces the positive Z axis in *Maya* (towards the camera in the default perspective view). UNIGINE reads the unit and axis metadata from the FBX file and handles all conversions automatically.


![](maya_orient_model.png)


### Freeze Transformations


Before skinning, freeze transformations on the **mesh** (*Modify -> Freeze Transformations*) to reset translate, rotate, and scale to identity values.


> **Notice:** Do **not** freeze transformations on **joints**. This will overwrite *jointOrient* values and break the skeleton orientation.


![](maya_freeze_transformations.png)


### Delete History


Before export, clean up the construction history on your meshes. For skinned meshes, use *Edit -> Delete All by Type -> Non-Deformer History* to remove modeling history while preserving skin clusters and blend shapes.


![](maya_delete_non_deformer_history.png)


> **Notice:** Do not use *Delete All History* on skinned meshes - this will remove the skin cluster and break the deformation.


## 2. Set Up the Skeleton


These guidelines apply when creating a rig from scratch. If you are working with an already rigged character, the skeleton is typically ready for export and you can skip to [Export as FBX](#export_fbx).


### Joint Naming


UNIGINE maps joints between skeletons, animations, and meshes **by name**. If a joint name in the animation does not match any joint in the skeleton, that joint will not be animated - without any warning. This matters when you use a separate skeleton asset or import animations from external sources.


Consistent naming allows you to reuse animations across different characters via [skeleton retargeting](../../../content/animations/retargeting/index.md).


### Joint Count


The skeleton itself can have any number of joints. However, each mesh surface can reference a **maximum of 128 bones** through its vertex weights (a GPU rendering limitation). If a surface exceeds this limit, UNIGINE will log a warning during import.


### Bind Pose


Export the character in a clean **T-pose** or **A-pose**. Joints should have (0, 0, 0) rotation at bind pose, with orientation stored in *jointOrient*. Verify the bind pose with *Skeleton -> Go to Bind Pose*.


![](maya_goto_bind_pose.png)


### Constraints, IK, and Expressions


IK handles, constraints, expressions, set driven keys, and other procedural animation systems are **not** stored in FBX. Only the resulting joint transforms are exported.


Enable **Bake Animation** in the FBX export dialog to automatically sample the final joint transforms at every frame, including the effects of all constraints and IK. Without baking, constrained joints will export in their rest position.


## 3. Export Using Game Exporter


The easiest and recommended way to export animated characters from *Maya* is the **Game Exporter** (*File -> Game Exporter*). It provides separate tabs for exporting the model and animation clips, with all FBX settings in one place.


### Model Tab


Use the *Model* tab to export the character mesh and skeleton. The key settings are:


| \| Setting \| Value \| \|---\|---\| \| Smoothing Groups \| **On** \| \| Tangents & Binormals \| **On** \| \| Skinning \| **On** \| \| Blendshapes \| **On** \| \| Animation \| **Off** \| \| File Type \| **Binary** \| | Setting | Value | Smoothing Groups | **On** | Tangents & Binormals | **On** | Skinning | **On** | Blendshapes | **On** | Animation | **Off** | File Type | **Binary** | ![](maya_game_exporter_model_tab.png) |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Setting | Value |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Smoothing Groups | **On** |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Tangents & Binormals | **On** |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Skinning | **On** |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Blendshapes | **On** |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Animation | **Off** |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| File Type | **Binary** |  |  |  |  |  |  |  |  |  |  |  |  |  |  |


Enable **Skinning** and **Blendshapes** to include skin weights and morph targets (called **blend shapes** in *Maya*). UNIGINE handles axis conversion automatically regardless of the *Up Axis* setting.


### Animation Clips Tab


Use the *Animation Clips* tab to export animation. Click the **+** button to add a clip, then set its name and frame range. With **Export All** selected, the mesh and skeleton are included alongside the animation data.


| \| Setting \| Value \| \|---\|---\| \| Export \| **Export All** \| \| Bake Animation \| **On** \| \| File Type \| **Binary** \| | Setting | Value | Export | **Export All** | Bake Animation | **On** | File Type | **Binary** | ![](maya_game_exporter_animation_tab.png) |
|---|---|---|---|---|---|---|---|---|---|
| Setting | Value |  |  |  |  |  |  |  |  |
| Export | **Export All** |  |  |  |  |  |  |  |  |
| Bake Animation | **On** |  |  |  |  |  |  |  |  |
| File Type | **Binary** |  |  |  |  |  |  |  |  |


> **Notice:** Define animation clips with descriptive names and frame ranges. Give each clip a clear name - it will be used for the exported `*.anim` asset in UNIGINE.


Enable **Bake Animation** to convert IK, constraints, and expressions into per-frame keyframes.


You can define multiple clips and choose how to save them:


- **Save Clips to Single File** - all clips are saved as FBX takes within a single file. UNIGINE imports each take as a separate `*.anim` asset.
- **Save Multiple Clip Files** - each clip is saved as its own FBX file.


## 4. Import in UNIGINE


Drag the exported FBX file into the *Asset Browser*, or right-click and select *Import New Asset*. For full details on all options, see the [FBX Import Guide](../../../editor2/fbx/index.md).


### Recommended Settings


| Setting | Value | Notes |
|---|---|---|
| Import Meshes | **On** | Disable if importing animation-only files. |
| Import Skeletons | **On** |  |
| Import Animations | **On** |  |
| Animation FPS | 30 | Match to the frame rate of your *Maya* scene. |
| Import Morph Targets | **On** | Enable if your mesh has blend shapes. |


![](blender_import_to_unigine_settings.png)


### Adding the Character to the Scene


Click on the imported FBX asset in the *Asset Browser* to preview the model and adjust import settings. Double-click to open the asset and explore each of the contained assets individually (`*.skeleton`, `*.mesh_skinned`, `*.anim`).


Drag the `*.mesh_skinned` (or the original `*.fbx`) into the viewport and choose **Skeleton Pose + Skinned Mesh** in the popup menu. This creates a **[NodeSkeletonPose](../../../objects/animations/nodeskeletonpose/index.md)** with a child **[ObjectMeshSkinned](../../../objects/objects/mesh_skinned/index.md)**. Assign an [animation graph](../../../content/animations/index.md) to start animating.


![](../../../content/animations/animation_assets/mesh_skinned_drag_and_drop.png)


## See Also


- [Exporting 3D Models From Autodesk Maya](../../../editor2/assets_workflow/export/export_from_maya.md)
- [FBX Import Guide](../../../editor2/fbx/index.md)
- [Preparing Animation Assets](../../../content/animations/animation_assets/index.md)
- [Animation Graph Overview](../../../content/animations/index.md)
