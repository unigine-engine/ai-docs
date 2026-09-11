# Exporting Animated Models From Autodesk 3ds Max


To bring an animated character from *Autodesk 3ds Max* into UNIGINE, you need to export the mesh, skeleton, and animation data as an FBX file. This article covers the recommended export and import settings to get the best results.


> **Notice:** This guide is based on **Autodesk 3ds Max 2025** and **UNIGINE SDK 2.21**. The general workflow applies to other recent versions; however, UI details may vary.


For static model export (with no animation), see [Exporting 3D Models From Autodesk 3ds Max](../../../editor2/assets_workflow/export/export_from_3dsmax.md).


## What UNIGINE Creates on Import


When you import an FBX file with a rigged and animated character, UnigineEditor splits it into three native assets:


- **[Skeleton](../../../content/animations/animation_assets/index.md#skeleton)** (`*.skeleton`) - joint hierarchy and bind pose.
- **[Skinned Mesh](../../../content/animations/animation_assets/index.md#skinned_mesh)** (`*.mesh_skinned`) - 3D model with skinning weights.
- **[Animation](../../../content/animations/animation_assets/index.md#animation)** (`*.anim`) - animation clips with per-joint transforms for each frame.


These assets are independent after import and can be modified without reimporting the source file. For more details, see [Preparing Animation Assets](../../../content/animations/animation_assets/index.md).


## 1. Prepare the Scene in 3ds Max


Before configuring the export settings, make sure your scene is set up correctly in *3ds Max*.


### Set Units


Verify that **Centimeters** are set as system units in *Customize -> Units Setup -> System Unit Setup*. This matches the FBX standard and avoids scale mismatches on import.


![](3dsmax_unit_setup.png)


### Orient the Model


Orient the character so it faces the negative Y axis (the front direction in *3ds Max*). UNIGINE reads the axis metadata from the FBX file and handles all conversions automatically.


![](3dsmax_axis_setup.png)


### Reset XForm


Before skinning, apply *Reset XForm* (*Utilities -> Reset XForm*) to the mesh to bake all transforms into the vertex data. Then collapse the resulting *XForm* modifier. This ensures the mesh has a clean identity transform at the object level.


![](3dsmax_reset_transform.png)


> **Notice:** Apply *Reset XForm* **before** adding the *Skin* modifier. Applying it after skinning will break the deformation.


## 2. Set Up the Skeleton


These guidelines apply when creating a rig from scratch. If you are working with an already rigged character, the skeleton is typically ready for export and you can skip to [Export as FBX](#export_fbx).


*3ds Max* offers three skeleton systems. All three export to FBX, but with different behavior:


- **Standard Bones** (*Create -> Systems -> Bones*) - the most flexible option with the cleanest FBX export path. Standard animation controllers export directly without conversion.
- **Biped** (*Character Studio*) - a predefined humanoid skeleton. Uses proprietary controllers that are automatically baked to standard keyframes during FBX export.
- **CAT** (*Character Animation Toolkit*) - supports non-humanoid rigs and animation layers. Layer data is flattened into a single track during FBX export.


### Bone Naming


UNIGINE maps joints between skeletons, animations, and meshes **by name**. If a bone name in the animation does not match any joint in the skeleton, that joint will not be animated - without any warning. This matters when you use a separate skeleton asset or import animations from external sources.


Consistent naming allows you to reuse animations across different characters via [skeleton retargeting](../../../content/animations/retargeting/index.md).


> **Notice:** Avoid spaces and special characters in bone names. Use alphanumeric characters and underscores (e.g. *L_UpperArm*).


### Bone Count


The skeleton itself can have any number of bones. However, each mesh surface can reference a **maximum of 128 bones** through its vertex weights (a GPU rendering limitation). If a surface exceeds this limit, UNIGINE will log a warning during import.


### Skin Modifier


Use the *Skin* modifier (not *Physique*) to bind the mesh to the skeleton. Set the **Bone Affect Limit** to **4** in the Skin modifier properties - this matches UNIGINE's maximum of 4 weights per vertex and lets you preview the actual in-engine deformation.


Make sure all vertices are weighted (no zero-weight vertices) and that weights are normalized (sum to 1.0 per vertex).


### Constraints, IK, and Controllers


IK solvers, constraints, wire parameters, expressions, and script controllers are **not** stored in FBX. Only the resulting bone transforms are exported.


Enable **Bake Animation** in the FBX export dialog to automatically sample the final bone transforms at every frame. Without baking, bones driven by IK or constraints will export in their rest position.


## 3. Export as FBX


Go to *File -> Export*, choose **Autodesk (*.FBX)** as the file type, and click *Save*. The FBX Export dialog will appear with the following sections.


### Geometry


![](3dsmax_fbx_geometry.png)


If you are exporting animation only (without the character mesh), enable **Animation Only (Do Not Export Geometry)** and skip to [Animation](#fbx_animation). Otherwise, keep the default geometry settings.


### Animation and Deformations


| \| Setting \| Value \| \|---\|---\| \| Animation \| **On** \| \| Bake Animation \| **On** \| \| Start / End \| Your animation range \| \| Step \| 1 \| \| Skins \| **On** \| \| Morphs \| **On** \| | Setting | Value | Animation | **On** | Bake Animation | **On** | Start / End | Your animation range | Step | 1 | Skins | **On** | Morphs | **On** | ![](3dsmax_fbx_animation.png) |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Setting | Value |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Animation | **On** |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Bake Animation | **On** |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Start / End | Your animation range |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Step | 1 |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Skins | **On** |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Morphs | **On** |  |  |  |  |  |  |  |  |  |  |  |  |  |  |


Enable **Bake Animation** to convert all controllers, IK solvers, and constraints into per-frame keyframes. *Biped* and *CAT* controllers are baked automatically during export.


Enable **Skins** to export *Skin* modifier data. Enable **Morphs** to export *Morpher* modifier channels as morph targets.


> **Notice:** The *Morpher* modifier must be **above** the *Skin* modifier in the modifier stack.


To export **multiple animations**, set the timeline to the desired frame range, export, rename the file (e.g. *character_idle.fbx, character_walk.fbx*), and repeat for each animation.


### Advanced Options


| \| Setting \| Value \| \|---\|---\| \| Scale Factor \| **Automatic** \| \| Up Axis \| **Z-up** \| \| FBX File Format \| **Binary** \| | Setting | Value | Scale Factor | **Automatic** | Up Axis | **Z-up** | FBX File Format | **Binary** | ![](3dsmax_fbx_advanced.png) |
|---|---|---|---|---|---|---|---|---|---|
| Setting | Value |  |  |  |  |  |  |  |  |
| Scale Factor | **Automatic** |  |  |  |  |  |  |  |  |
| Up Axis | **Z-up** |  |  |  |  |  |  |  |  |
| FBX File Format | **Binary** |  |  |  |  |  |  |  |  |


UNIGINE reads the unit and axis metadata from the FBX file and handles conversions automatically.


## 4. Import in UNIGINE


Drag the exported FBX file into the *Asset Browser*, or right-click and select *Import New Asset*. For full details on all options, see the [FBX Import Guide](../../../editor2/fbx/index.md).


### Recommended Settings


| Setting | Value | Notes |
|---|---|---|
| Import Meshes | **On** | Disable if importing animation-only files. |
| Import Skeletons | **On** |  |
| Import Animations | **On** |  |
| Animation FPS | 30 | Match to the frame rate of your *3ds Max* scene. |
| Import Morph Targets | **On** | Enable if your mesh has a Morpher modifier. |


![](blender_import_to_unigine_settings.png)


### Adding the Character to the Scene


Click on the imported FBX asset in the *Asset Browser* to preview the model and adjust import settings. Double-click to open the asset and explore each of the contained assets individually (`*.skeleton`, `*.mesh_skinned`, `*.anim`).


Drag the `*.mesh_skinned` (or the original `*.fbx`) into the viewport and choose **Skeleton Pose + Skinned Mesh** in the popup menu. This creates a **[NodeSkeletonPose](../../../objects/animations/nodeskeletonpose/index.md)** with a child **[ObjectMeshSkinned](../../../objects/objects/mesh_skinned/index.md)**. Assign an [animation graph](../../../content/animations/index.md) to start animating.


![](../../../content/animations/animation_assets/mesh_skinned_drag_and_drop.png)


## See Also


- [Exporting 3D Models From Autodesk 3ds Max](../../../editor2/assets_workflow/export/export_from_3dsmax.md)
- [FBX Import Guide](../../../editor2/fbx/index.md)
- [Preparing Animation Assets](../../../content/animations/animation_assets/index.md)
- [Animation Graph Overview](../../../content/animations/index.md)
