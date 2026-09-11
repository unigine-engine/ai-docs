# Importing Animations From Mixamo


**[Mixamo](https://www.mixamo.com/)** is a free online service by *Adobe* that provides a library of ready-to-use 3D characters and animations. You can upload your own character model, auto-rig it (automatically create a skeleton and assign skin weights), apply animations from the library, and download everything as FBX files ready for import into UNIGINE.


![](mixamo_preview.png)


## Overview


Mixamo provides two main features:


- **Auto-Rigger** - upload a static 3D model (`FBX` or `OBJ`) and Mixamo will automatically generate a skeleton and skin weights for it.
- **Animation Library** - a collection of motion-captured animations (locomotion, combat, gestures, etc.) that can be previewed and applied to any rigged character.


The typical workflow is: pick or upload a character, choose animations, download as `FBX`, and import into your UNIGINE project.


## 1. Download the Character


On the *Mixamo* website, choose a character from the built-in library or upload your own model and use the auto-rigger to create a skeleton for it. Before downloading, configure the following settings:


![](mixamo_download_character_settings.png)


| Setting | Value |
|---|---|
| Format | **FBX Binary (*.fbx)** |
| Pose | **T-Pose** |


This downloads the character mesh with a skeleton in T-pose, without any animation. Use this file as the base for your character in UNIGINE.


![](mixamo_download_character.png)

*Make sure no animation is selected before downloading. Downloading the character and animations separately allows for more flexible asset management in UNIGINE.*


## 2. Download Animations


Browse the animation library, preview animations on your character, and download each one separately. Use the following download settings:


![](mixamo_download_animation_settings.png)


| Setting | Value | Notes |
|---|---|---|
| Format | **FBX Binary (.fbx)** |  |
| Skin | **Without Skin** | Downloads only the animation and skeleton, without the mesh. Reduces file size since the mesh is already in the character file. |
| Frames per Second | **30** | Matches UNIGINE's default Animation FPS. |
| Keyframe Reduction | **none** | Preserves all keyframes for maximum accuracy. |


![](mixamo_download_animation.png)

*You can adjust animation parameters (speed, arm spacing, character proportions, etc.) directly on the Mixamo website before downloading.*


Repeat for each animation you need (e.g. idle, walk, run, jump). Name the downloaded files descriptively: *character_idle.fbx, character_walk.fbx*, etc.


> **Notice:** You can also download animations **With Skin** if you want each file to be self-contained. UNIGINE will import the mesh from whichever file you add to the scene, and use the skeleton from any of them as long as the bone names match.


## 3. Import into UNIGINE


Drag the downloaded FBX files into the *Asset Browser* in UnigineEditor and configure the import settings for each asset.

 Best PracticeImport the character first to create a shared [skeleton](../../../content/animations/animation_assets/index.md#shared_and_source_skeleton) asset, then import each animation using **Take Shared** to link it to that skeleton. This way you can add new animations from *Mixamo* at any time - just download, import with the same shared skeleton, and the animation is immediately available in your [animation graph](../../../content/animations/index.md).
### Importing Character


For the character file (T-pose with mesh):


![](mixamo_import_character.png)


| Setting | Value |
|---|---|
| Import Meshes | On |
| Import Skeletons | On |
| Import Skeleton Mode | Create |
| Import Animations | **Off** |


This creates the `*.mesh_skinned` and `*.skeleton` assets.


![](mixamo_imported_character.png)


For details on other FBX import settings, see the [FBX Import Guide](../../../editor2/fbx/index.md).


### Importing Animations


For each animation file (without skin):


![](mixamo_import_animations.png)


| Setting | Value |
|---|---|
| Import Meshes | Off |
| Import Skeletons | On |
| Import Skeleton Mode | **Take Shared** |
| Shared Skeleton | Select the `*.skeleton` from the character import |
| Import Animations | On |
| Animation FPS | 30 (or the value you chose when [downloading animations](#download_animations)) |


Many *Mixamo* animations include **root motion** - the character visibly moves through space during playback (e.g. walking forward, lunging during an attack). This movement is typically baked into the *mixamorig:Hips* bone. To extract it during import, configure the following settings:


- **Create Root Motion Joint** - On
- **Target Root Motion Joint** - *mixamorig:Hips*
- **Position Component** - XY (horizontal movement)
- **Rotation Component** - Only Vertical Axis (turning)
- **Root Motion Forward Axis** - Y


This separates the horizontal movement and turning from the animation pose, making it available as a [root motion delta](../../../content/animations/root_motion/index.md) that your game code can apply to the character's position. Vertical motion (jumping, bouncing) stays on the original bone.


> **Notice:** Not all *Mixamo* animations contain root motion. In-place animations (e.g. idle, waving) do not need these settings.


## 4. Add to the Scene


Drag the `*.mesh_skinned` asset into the viewport and choose **Skeleton Pose + Skinned Mesh** in the popup menu. This creates a **[NodeSkeletonPose](../../../objects/animations/nodeskeletonpose/index.md)** with a child **[ObjectMeshSkinned](../../../objects/objects/mesh_skinned/index.md)**.


![](mixamo_adding_to_the_scene.png)


Assign an [animation graph](../../../content/animations/index.md) to the **NodeSkeletonPose** to start playing the imported animations.


## Known Issues


### Non-Identity Transforms on Armature


Mixamo characters imported into *Blender* typically have **Rotation X = 90�** and **Scale = 0.01** on the armature. This is because Mixamo uses Y-up coordinate system and centimeters, while *Blender* uses Z-up and meters.


If you import the Mixamo FBX directly into UNIGINE (without going through *Blender*), this is not an issue - UNIGINE reads the axis and unit metadata from the FBX file and converts automatically.


If you do go through *Blender*, see the **Apply Transforms** section in [Exporting Animations From Blender](../../../editor2/assets_workflow/export/export_animations_from_blender.md#apply_transforms).


### Bone Name Prefix


Mixamo skeletons use the *mixamorig:* prefix on all bone names (e.g. *mixamorig:Hips, mixamorig:Spine*). This is consistent across all Mixamo characters, so animations are compatible between them. However, if you want to share animations with non-Mixamo characters, the bone names must match - you may need to rename bones in a third-party DCC tool before export.


## See Also


- [Exporting Animations From Blender](../../../editor2/assets_workflow/export/export_from_blender.md)
- [FBX Import Guide](../../../editor2/fbx/index.md)
- [Preparing Animation Assets](../../../content/animations/animation_assets/index.md)
- [Animation Graph Overview](../../../content/animations/index.md)
