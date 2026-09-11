# Exporting Animated Models From Blender


To bring an animated character from *Blender* into UNIGINE, you need to export the mesh, skeleton, and animation data in a format the Engine can read. This article covers the recommended export and import settings to get the best results.


> **Notice:** This guide is based on **Blender 5.1** and **UNIGINE SDK 2.21**. The general workflow applies to other recent versions; however, UI details may vary.


For static model export (with no animation), see [Exporting 3D Models From Blender](../../../editor2/assets_workflow/export/export_from_blender.md).


## What UNIGINE Creates on Import


When you import an FBX file with a rigged and animated character, UnigineEditor splits it into three native assets:


- **[Skeleton](../../../content/animations/animation_assets/index.md#skeleton)** (`*.skeleton`) - joint hierarchy and bind pose.
- **[Skinned Mesh](../../../content/animations/animation_assets/index.md#skinned_mesh)** (`*.mesh_skinned`) - 3D model with skinning weights.
- **[Animation](../../../content/animations/animation_assets/index.md#animation)** (`*.anim`) - animation clips with per-joint transforms for each frame.


These assets are independent after import and can be modified without reimporting the source file. For more details, see [Preparing Animation Assets](../../../content/animations/animation_assets/index.md).


## 1. Prepare the Scene in Blender


Before configuring the export settings, make sure your scene is set up correctly in *Blender*.


### Set Units


Make sure *Unit Scale* is set to **1.0** in *Scene Properties -> Units*. Both *Blender* and UNIGINE use 1 unit = 1 meter by default.


![](blender_units.png)


> **Notice:** If you are importing third-party FBX files that use centimeters (e.g. from *Mixamo, Unreal Engine*, or *Autodesk* tools), the armature may get a scale of 0.01 in *Blender*. In *Blender* 4.4 and earlier, setting *Unit Scale* to 0.01 before import would avoid this. In *Blender* 5.0+, the new FBX importer always applies the unit conversion regardless of scene settings - use *All Transforms to Deltas* to clean up the scale after import.


### Orient the Model


The character should face towards you in *Blender*'s **Front View** (**Numpad 1**), i.e. look in the **-Y** direction.


![](blender_character_axis.png)


### Apply Transforms


Before rigging and skinning, make sure both the mesh and armature have no offset, no rotation, and a scale of 1.0. Apply transforms with **Ctrl+A** -> *All Transforms*.


![](blender_apply_transforms.png)


If you are working with an already rigged character that has non-identity Scale or Rotation on the armature (common with models imported from external sources), applying transforms may shift the model. In this case, use *Object -> Apply -> All Transforms to Deltas* instead - it moves the transforms into *Delta* channels, cleaning up the main transform values without affecting the rig or skinning.


> **Notice:** The FBX exporter's *Apply Transform* checkbox is marked as experimental by *Blender*. It may produce unexpected results with complex armatures - use with caution.


## 2. Set Up the Armature


These guidelines apply when creating a rig from scratch. If you are working with an already rigged character (e.g. from *Mixamo*), the rig is typically ready for export and you can skip to [3. Export as FBX](#export_fbx).


### Bone Naming


UNIGINE maps joints between skeletons, animations, and meshes **by name**. If a joint name in the animation does not match any joint in the skeleton, that joint will not be animated - without any warning. This matters when you use a separate skeleton asset or import animations from external sources.


Consistent naming allows you to reuse animations across different characters via [skeleton retargeting](../../../content/animations/retargeting/index.md).


### Bone Count


The skeleton itself can have any number of bones. However, each mesh surface can reference a **maximum of 128 bones** through its vertex weights (a GPU rendering limitation). If a surface exceeds this limit, UNIGINE will log a warning during import.


To reduce the bone count per surface, use the **Only Deform Bones** export option to exclude non-deforming control bones (IK targets, pole targets, etc.), or split the mesh into multiple surfaces.


### Rest Pose


Export the character in a **T-pose** or **A-pose**. A clean, symmetrical rest pose provides the best deformation results and makes it easier to reuse animations across characters via [skeleton retargeting](../../../content/animations/retargeting/index.md) (which uses bone lengths from the bind pose).


To set the current pose as rest: in Pose Mode, select all bones, *Pose -> Apply -> Apply Pose as Rest Pose*.


> **Notice:** UNIGINE distinguishes between the **bind pose** (where skinning weights were assigned - zero deformation) and the **rest pose** (default joint positions from the source file at export time). These are often the same but may differ if you adjusted joints after skinning.


### Constraints, IK, and Drivers


Constraints and drivers are **not** stored in FBX. Only the resulting bone transforms are exported.


When animation export is enabled, *Blender* bakes constraint results into keyframes automatically. If complex setups (especially **Spline IK**) produce inaccurate results, bake manually:


1. Select the armature and enter Pose Mode.
2. Navigate to *Pose -> Animation -> Bake Action*.
3. Disable **Only Selected Bones**, enable **Visual Keying** and **Clear Local Constraints**.


![](blender_bake_action.png)


## 3. Export as FBX


Select the armature and the mesh, then go to *File -> Export -> FBX (.fbx)*. Below are the recommended export settings for animated characters.


### Include Tab


Select the mesh and armature before export. Enable **Selected Objects** and set **Object Types** to *Armature* and *Mesh*.


![](blender_armature_and_mesh.png)


### Transform Tab


These settings control how *Blender* converts units and coordinate axes when writing the FBX file. UNIGINE reads the embedded metadata and handles the conversion automatically.


| \| Setting \| Value \| \|---\|---\| \| Scale \| **1.0** \| \| Apply Scalings \| **FBX Units Scale** \| \| Forward / Up \| **Y Forward**, **Z Up** \| \| Apply Unit \| **On** \| \| Use Space Transform \| **On** \| \| Apply Transform \| **Off** \| | Setting | Value | Scale | **1.0** | Apply Scalings | **FBX Units Scale** | Forward / Up | **Y Forward**, **Z Up** | Apply Unit | **On** | Use Space Transform | **On** | Apply Transform | **Off** | ![](blender_transform_tab.png) |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Setting | Value |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Scale | **1.0** |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Apply Scalings | **FBX Units Scale** |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Forward / Up | **Y Forward**, **Z Up** |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Apply Unit | **On** |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Use Space Transform | **On** |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Apply Transform | **Off** |  |  |  |  |  |  |  |  |  |  |  |  |  |  |


> **Notice:** The **Apply Transform** option is marked as experimental by *Blender* and may produce unexpected results with complex armatures - use with caution.


### Armature Tab


| \| Setting \| Value \| \|---\|---\| \| Primary / Secondary Bone Axis \| **Y / X** \| \| Only Deform Bones \| **On** \| \| Add Leaf Bones \| **Off** \| | Setting | Value | Primary / Secondary Bone Axis | **Y / X** | Only Deform Bones | **On** | Add Leaf Bones | **Off** | ![](blender_armature_tab.png) |
|---|---|---|---|---|---|---|---|---|---|
| Setting | Value |  |  |  |  |  |  |  |  |
| Primary / Secondary Bone Axis | **Y / X** |  |  |  |  |  |  |  |  |
| Only Deform Bones | **On** |  |  |  |  |  |  |  |  |
| Add Leaf Bones | **Off** |  |  |  |  |  |  |  |  |


> **Notice:** Disable **Add Leaf Bones**. This option adds a dummy joint at the tip of every end bone to preserve bone length for re-import into *Blender*. UNIGINE imports these as regular joints - they serve no purpose but increase the bone count.


### Animation Tab


Enable the **Animation** checkbox to include animation data in the export.


| \| Setting \| Value \| \|---\|---\| \| Animation \| **On** \| \| Key All Bones \| **On** \| \| NLA Strips \| **Off** \| \| All Actions \| **Off** \| \| Sampling Rate \| 1.0 \| \| Simplify \| 1.0 \| | Setting | Value | Animation | **On** | Key All Bones | **On** | NLA Strips | **Off** | All Actions | **Off** | Sampling Rate | 1.0 | Simplify | 1.0 | ![](blender_animation_tab.png) |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Setting | Value |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Animation | **On** |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Key All Bones | **On** |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| NLA Strips | **Off** |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| All Actions | **Off** |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Sampling Rate | 1.0 |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Simplify | 1.0 |  |  |  |  |  |  |  |  |  |  |  |  |  |  |


With these settings, only the top action in the NLA stack is exported. To export **multiple animations**, enable **NLA Strips** to export stashed NLA tracks, or **All Actions** to export every action in the file. Each action becomes a separate FBX take, and UNIGINE imports each take as a separate `.anim` asset.


![](blender_nla_tracks.png)

*Give your NLA tracks descriptive names (e.g.idle, walk, run) - these names will be used for the exported.animassets. Enable NLA Strips to export only the stashed tracks, orAll Actionsto export everything.*


## 4. Import in UNIGINE


Drag the exported file into the *Asset Browser*, or right-click and select *Import New Asset*. For full details on all options, see the [FBX Import Guide](../../../editor2/fbx/index.md).


### Recommended Settings


| \| Setting \| Value \| Notes \| \|---\|---\|---\| \| Import Meshes \| **On** \| Disable if you are importing animation-only files without a character mesh. \| \| Import Skeletons \| **On** \|  \| \| Import Skeleton Mode \| **Create** \| Use *Take Shared* to reuse an existing skeleton. \| \| Import Animations \| **On** \|  \| \| Import Bones Without Skin \| **On** \| Includes accessory bones (weapon attachment points, etc.). \| \| Animation FPS \| 30 \| UNIGINE default. Match to the frame rate of your *Blender* project. \| \| Import Morph Targets \| **On** \| Enable if your mesh has [morph targets](../../../content/tutorials/morph/index_cpp.md) (shape keys) in *Blender* (e.g. for facial animation). \| \| Force Loop \| **Off** \| Enable for looping animations (idle, walk cycles). Smooths the playback at the loop boundary by blending the first and last frames. Set *Looped Frames* to control the number of blended frames (maximum: 30). \| | Setting | Value | Notes | Import Meshes | **On** | Disable if you are importing animation-only files without a character mesh. | Import Skeletons | **On** |  | Import Skeleton Mode | **Create** | Use *Take Shared* to reuse an existing skeleton. | Import Animations | **On** |  | Import Bones Without Skin | **On** | Includes accessory bones (weapon attachment points, etc.). | Animation FPS | 30 | UNIGINE default. Match to the frame rate of your *Blender* project. | Import Morph Targets | **On** | Enable if your mesh has [morph targets](../../../content/tutorials/morph/index_cpp.md) (shape keys) in *Blender* (e.g. for facial animation). | Force Loop | **Off** | Enable for looping animations (idle, walk cycles). Smooths the playback at the loop boundary by blending the first and last frames. Set *Looped Frames* to control the number of blended frames (maximum: 30). | ![](blender_import_to_unigine_settings.png) *The highlighted settings are the most important ones for animation import. Other settings can be left at their defaults.* |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Setting | Value | Notes |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Import Meshes | **On** | Disable if you are importing animation-only files without a character mesh. |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Import Skeletons | **On** |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Import Skeleton Mode | **Create** | Use *Take Shared* to reuse an existing skeleton. |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Import Animations | **On** |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Import Bones Without Skin | **On** | Includes accessory bones (weapon attachment points, etc.). |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Animation FPS | 30 | UNIGINE default. Match to the frame rate of your *Blender* project. |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Import Morph Targets | **On** | Enable if your mesh has [morph targets](../../../content/tutorials/morph/index_cpp.md) (shape keys) in *Blender* (e.g. for facial animation). |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Force Loop | **Off** | Enable for looping animations (idle, walk cycles). Smooths the playback at the loop boundary by blending the first and last frames. Set *Looped Frames* to control the number of blended frames (maximum: 30). |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |


### Root Motion


Root motion is a technique where character movement is driven by the animation itself rather than by game code. Instead of moving the character via scripts, the animator bakes the movement directly into the root bone - for example, the exact distance and timing of each step in a walk cycle, or the lunge of an attack.


If your animation contains such movement (the character visibly travels through space during playback), you can extract it during import using the following settings:


| Setting | Notes |
|---|---|
| Create Root Motion Joint | Creates an additional joint that captures the root bone's movement. The extracted motion is separated from the skeleton pose, so the character stays in place and the movement becomes available as a per-frame delta for your game code to apply. |
| Target Root Motion Joint | Name of the bone that carries the movement (e.g. *Root, Hips*). |
| Position Component | Which translation axes to extract: *ALL, XY* (horizontal movement only, leaving vertical bounce on the original bone), *Z* (vertical only), etc. |
| Rotation Component | Which rotation to extract: *ALL, Only Vertical Axis* (turning/yaw only, leaving body tilts on the original bone), or *NONE*. |


For details on enabling and using root motion in the animation graph, see the [Root Motion](../../../content/animations/root_motion/index.md) article.


### Adding the Character to the Scene


Click on the imported FBX asset in the *Asset Browser* to preview the model and adjust import settings. Double-click to open the asset and explore each of the contained assets individually (`*.skeleton, *.mesh_skinned, *.anim`).


![](unigine_fbx_preview.png)


Drag the `*.mesh_skinned` (or the original `*.fbx`) into the viewport and choose **Skeleton Pose + Skinned Mesh** in the popup menu. This creates a **[NodeSkeletonPose](../../../objects/animations/nodeskeletonpose/index.md)** with a child **[ObjectMeshSkinned](../../../objects/objects/mesh_skinned/index.md)**. Assign an [animation graph](../../../content/animations/index.md) to start animating.


![](../../../content/animations/animation_assets/mesh_skinned_drag_and_drop.png)


> **Notice:** Use the **NodeSkeletonPose + ObjectMeshSkinned + Animation Graph** workflow. The older **ObjectMeshSkinnedLegacy** is the legacy system and not recommended for new projects.


## See Also


- [Exporting 3D Models From Blender](../../../editor2/assets_workflow/export/export_from_blender.md)
- [FBX Import Guide](../../../editor2/fbx/index.md)
- [Preparing Animation Assets](../../../content/animations/animation_assets/index.md)
