# Preparing Animation Assets


Character animation in UNIGINE relies on three asset types that are typically created in an external DCC tool (3ds Max, Maya, Blender, etc.) and imported as FBX, glTF, or USD files. During import, the UnigineEditor splits them into separate native assets:


- **Skeleton** (`*.skeleton`) - the joint hierarchy and bind pose.
- **Skinned Mesh** (`*.mesh_skinned`) - the 3D model with skinning weights.
- **Animation** (`*.anim`) - the animation clip with per-joint transforms for each frame.


These three assets work together: the skeleton defines the joint structure, animations move the joints, and the skinned mesh deforms visually based on joint positions.


## Skeleton


A **Skeleton** (`*.skeleton`) defines the joint hierarchy of a character. It stores:


![](skeleton_asset.png)

*A .skeleton asset in the Asset Browser*


- **Joint hierarchy** - joint names and parent-child relationships.
- **Bind pose** - the transforms of each joint in the pose where the mesh was bound to the skeleton (skinned). This is the only pose where the mesh has zero deformation.
- **Blend masks** - named masks that control per-joint blend weights, used for partial body blending (e.g., upper body only).
- **Retarget data** - per-joint retargeting mode and joint length, used for sharing animations between skeletons with different proportions.


### Skeleton Preview


When you select a `*.skeleton` asset in the Asset Browser, the preview panel displays the skeleton in its **bind pose**. The following display options are available:


- *Show Bones* - toggle visibility of lines connecting joints.
- *Show Joints* - toggle visibility of joint markers.
- *Show Joint Names* - toggle text labels for each joint.
- *Bone Size* - scale the visual size of bones and joints in the preview.


The preview also provides settings for **[Blend Masks](../../../content/animations/blend_masks/index.md)** and **[Retarget Data](../../../content/animations/retargeting/index.md)** - see the corresponding articles for details on configuring them.


## Skinned Mesh


A **Skinned Mesh** (`*.mesh_skinned`) is a 3D model whose vertices are bound to skeleton joints via skinning weights. When joints move, the mesh deforms accordingly - this is how character animation becomes visible on screen.


![](mesh_skinned_asset.png)

*A .mesh_skinned asset in the Asset Browser*


A skinned mesh is displayed in the scene via an **ObjectMeshSkinned** node, which is controlled by a **NodeSkeletonPose**. One **NodeSkeletonPose** can drive multiple skinned meshes simultaneously - for example, a character body and separate clothing meshes that share the same skeleton.


> **Notice:** UNIGINE also has an older **ObjectMeshSkinnedLegacy** ![](ObjectMeshSkinnedLegacy.png) node type that combines the mesh and animation playback into a single object (with built-in layers, IK chains, and playback controls). This is the legacy animation system. For new projects, use **ObjectMeshSkinned** ![](ObjectMeshSkinned.png) + **NodeSkeletonPose** ![](NodeSkeletonPose.png) with an animation graph instead.


### Skinned Mesh Preview


The skinned mesh preview enables you to inspect the mesh with an optional animation and switch between different skeleton poses using the *Render Pose* setting:


- **Default** - the skeleton is in the pose of the current animation frame. If no animation is assigned, the mesh is displayed in its bind pose.
- **Bind** - the skeleton is frozen in the bind pose (the pose where skinning weights were assigned). The mesh has zero deformation in this pose.
- **Rest** - the skeleton is frozen in the rest pose - the default joint positions from the source file at the time of export. The rest pose may differ from the bind pose if the artist adjusted joints after skinning (e.g., bound in T-pose but exported in A-pose).


The preview also provides *Render Skeleton* options to choose which skeleton hierarchy to display:


- **Shared** - displays the skeleton that will actually be used at runtime (the `*.skeleton` file referenced by the mesh).
- **Source** - displays the original skeleton hierarchy embedded in the `*.mesh_skinned` file from import.


## Animation


An **Animation** (`*.anim`) is a clip that stores per-joint transforms (translation, rotation, scale) for each frame.


![](anim_asset.png)

*An .anim asset in the Asset Browser*


### Animation Preview


The animation preview plays the selected clip on a skinned mesh. Use the *Preview Mesh Skinned* setting to choose which mesh to use for playback. A mesh is required to see the animation - without it, only the skeleton can be displayed.


The *Render Skeleton* dropdown controls which skeleton hierarchy is displayed in the preview:


- **Shared** (default) - displays the skeleton that will actually be used at runtime (the `*.skeleton` file referenced by the animation).
- **Source** - displays the original skeleton hierarchy embedded in the `*.anim` file from import.


The preview also provides controls for playback (play/pause, frame scrubbing, speed), and sections for editing **[Sync Markers](../../../content/animations/synchronization/index.md)** and **[Root Motion](../../../content/animations/root_motion/index.md)** settings.


## Shared and Source Skeletons


Each `*.anim` and `*.mesh_skinned` file keeps the original joint hierarchy from its source file - the **source skeleton**. It also stores a reference to a `*.skeleton` asset - the **shared skeleton**. On load, the Engine maps source joints to the shared skeleton by name, filtering out any joints that do not match. The asset then only works with the joints of its shared skeleton:


- **Animation** - curves for joints not in the shared skeleton are skipped.
- **Skinned Mesh** - joints not in the shared skeleton stay in their rest pose.


Usually, the source and shared skeletons are identical (they come from the same file), and you do not need to think about any of this. It only matters when you point an asset to a different shared skeleton (e.g., importing an animation with finger joints and assigning a shared skeleton without fingers - the finger curves are simply skipped). See **[Skeleton Retargeting](../../../content/animations/retargeting/index.md)** for details on using different skeletons together.


## Importing Animation Assets


When you import an `*.fbx, *.glb`, or `*.usd` file that contains a rigged and animated character, the UnigineEditor automatically extracts and creates separate `*.mesh_skinned, *.skeleton`, and `*.anim` assets. A single source file can produce multiple assets of each type - skeletons, meshes, and animation clips. See the **[FBX Import](../../../editor2/fbx/index.md)** article for import settings details.


After import, each asset is independent - you can modify skeleton settings (blend masks, retarget data) or animation settings (sync markers) without reimporting the source file.


## Putting It All Together: NodeSkeletonPose


**NodeSkeletonPose** ![](NodeSkeletonPose.png) is the scene node that brings everything together: you assign a skeleton, attach skinned meshes, and connect an **animation graph** (`*.agraph`). Each frame, the animation graph decides the current pose, and the **NodeSkeletonPose** applies it to the attached meshes.


The quickest way to set up a character is to drag a `*.mesh_skinned, *.fbx, *.glb`, or `*.usd` asset from the Asset Browser into the viewport and choose *Skeleton Pose + Skinned Mesh* in the popup menu. This automatically creates a **NodeSkeletonPose** with the correct skeleton and a child **ObjectMeshSkinned**. After that, assign an **animation graph** to start animating.


![](mesh_skinned_drag_and_drop.png)

*Dragging a skinned mesh into the viewport shows a menu to choose the node type*


You can also set things up manually:


1. Create a **NodeSkeletonPose** ![](NodeSkeletonPose.png) in the scene and assign a **skeleton** to it.
2. Create **ObjectMeshSkinned** ![](ObjectMeshSkinned.png) nodes and attach them as controlled objects.
3. Assign an **Animation Graph** that controls the animation logic.


With the character in place, you are all set to start building your animation logic - the other articles in this section will guide you through it.


## See Also


- [Animation Graph Overview](../../../content/animations/index.md)
- [Blend Masks](../../../content/animations/blend_masks/index.md)
- [Skeleton Retargeting](../../../content/animations/retargeting/index.md)
- [Animation Synchronization](../../../content/animations/synchronization/index.md)
