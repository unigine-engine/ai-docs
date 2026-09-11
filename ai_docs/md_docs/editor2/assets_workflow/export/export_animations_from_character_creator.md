# Exporting Animated Characters From Character Creator


**[Character Creator](https://www.reallusion.com/character-creator/)** by *Reallusion* is a tool for designing 3D characters with detailed facial morphs, skin shading, and clothing. Combined with *iClone* for animation, it provides a complete pipeline for creating animated characters and exporting them as FBX files for use in UNIGINE.


> **Notice:** This guide is based on **Character Creator 5** and **UNIGINE SDK 2.21**.


## What UNIGINE Creates on Import


When you import an FBX file with a rigged and animated character, UnigineEditor splits it into three native assets:


- **[Skeleton](../../../content/animations/animation_assets/index.md#skeleton)** (`*.skeleton`) - joint hierarchy and bind pose.
- **[Skinned Mesh](../../../content/animations/animation_assets/index.md#skinned_mesh)** (`*.mesh_skinned`) - 3D model with skinning weights.
- **[Animation](../../../content/animations/animation_assets/index.md#animation)** (`*.anim`) - animation clips with per-joint transforms for each frame.


These assets are independent after import and can be modified without reimporting the source file. For more details, see [Preparing Animation Assets](../../../content/animations/animation_assets/index.md).


## 1. Export From Character Creator


In *Character Creator*, go to *File -> Export -> FBX* and configure the following settings.


![](character_creator_export_settings.png)


| Setting | Value |
|---|---|
| Target Tool Preset | **Blender** |
| FBX Options | **Mesh and Motion** |
| Current Animation | **All** or **Range** |
| Frame Rate | 30 or 60 |
| First Frame Pose Type | **TPose** |


Set *Target Tool Preset* to **Blender** - there is no dedicated UNIGINE preset, but the *Blender* preset produces a standard FBX that UNIGINE can import. Choose **Mesh and Motion** to export the character with animation in a single file. Set **TPose** as the first frame pose type if you plan to use [skeleton retargeting](../../../content/animations/retargeting/index.md).


> **Notice:** Remember the *Frame Rate* value you set here - you will need to match it with *Animation FPS* when importing into UNIGINE.


> **Notice:** *Character Creator* characters include 60+ facial morph targets (expressions, visemes). These are exported automatically and significantly increase the file size. Enable **Import Morph Targets** in UNIGINE to use them.


For more advanced animation (body motion, facial capture, lip sync), use *[iClone](https://www.reallusion.com/iclone/)* to animate the character before exporting.


## 2. Import in UNIGINE


Drag the exported FBX file into the *Asset Browser*, or right-click and select *Import New Asset*. For full details on all options, see the [FBX Import Guide](../../../editor2/fbx/index.md).


### Recommended Settings


| Setting | Value | Notes |
|---|---|---|
| Import Meshes | **On** |  |
| Import Skeletons | **On** |  |
| Import Skeleton Mode | **Create** |  |
| Import Animations | **On** | Disable if the FBX contains only the character (no motion). |
| Import Morph Targets | **On** | Imports facial expressions as morph targets. |


![](blender_import_to_unigine_settings.png)


### Adding the Character to the Scene


Click on the imported FBX asset in the *Asset Browser* to preview the model and adjust import settings. Double-click to open the asset and explore each of the contained assets individually (`*.skeleton`, `*.mesh_skinned`, `*.anim`).


Drag the `*.mesh_skinned` (or the original `*.fbx`) into the viewport and choose **Skeleton Pose + Skinned Mesh** in the popup menu. This creates a **[NodeSkeletonPose](../../../objects/animations/nodeskeletonpose/index.md)** with a child **[ObjectMeshSkinned](../../../objects/objects/mesh_skinned/index.md)**. Assign an [animation graph](../../../content/animations/index.md) to start animating.


![](../../../content/animations/animation_assets/mesh_skinned_drag_and_drop.png)


## See Also


- [FBX Import Guide](../../../editor2/fbx/index.md)
- [Preparing Animation Assets](../../../content/animations/animation_assets/index.md)
- [Animation Graph Overview](../../../content/animations/index.md)
- [Skeleton Retargeting](../../../content/animations/retargeting/index.md)
