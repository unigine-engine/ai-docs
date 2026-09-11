# Skeleton Retargeting


Skeleton retargeting enables sharing animations between characters with different skeleton proportions. Without it, playing an animation made for a tall adult on a small child causes visible artifacts: limbs stretch, feet slide, and proportions look wrong. Retargeting solves this by scaling joint translations (bone positions relative to their parent) to match the target character's body.


## Animation Pipeline


Before explaining retargeting itself, it helps to understand the full path animation data takes from the animation asset to the visual result on the mesh:


![](retargeting_funnel.png)

*The animation pipeline: data flows from source files through shared skeletons and the NodeSkeletonPose down to the mesh*


1. **Animation Auto-Mapping.** The animation asset references a `*.skeleton` (its **shared skeleton**). The Engine matches joints by name. Curves for joints not in the shared skeleton are skipped.
2. **Retargeting.** If the skeletons differ at either boundary (animation -> **NodeSkeletonPose**, or **NodeSkeletonPose** -> mesh), the Engine creates a retargeter automatically and adjusts the pose. If all skeletons are the same, no retargeting is needed. This is the step you can configure, see [Retargeting Modes](#retargeting_modes) below.
3. **Mesh Auto-Mapping.** The skinned mesh also references a `*.skeleton` (its **shared skeleton**). The Engine matches joints by name. Joints not in the shared skeleton stay in their rest pose.


> **Notice:** If you use one skeleton file for everything, **all these steps just work automatically** - the Engine matches joints by name and copies transforms.
>
>
> You only need to configure retargeting when different characters with different body proportions share animations. In that case, enable **proportional retargeting** on both skeletons to scale translations correctly.


## Retargeting Modes


When two different skeletons meet, the Engine always retargets by matching joint names and copying transforms. This works automatically without any configuration. To control **how translations are handled** for each joint, turn on *Enable Retarget* on the `*.skeleton` asset. This unlocks per-joint mode selection. Rotation and scale are always copied as-is regardless of the mode.


![](skeleton_retargeting_settings.png)


- **Pose** - the animation plays exactly as authored, but the character may look stretched or compressed if proportions differ. Use for facial bones where small translation offsets should stay the same regardless of body size.
- **Bind** - translations are locked to the target character's own bind pose, so proportions are always correct. However, any translation-based movement (including root motion) is lost. Use for twist/roll helpers or as a quick way to get a reasonable result without manual tuning.
- **Proportion** - both proportions and movement are correct. The Engine scales translations by the ratio of bone lengths (distance from joint to its parent in the bind pose) between the target and source skeletons. Bone lengths are calculated automatically; you can override them manually if needed. Use for root, hips, spine, legs, arms - the recommended mode for most body joints.


> **Notice:** *Enable Retarget* must be active on **both skeletons** for proportional retargeting to work. The modes you set apply to the skeleton that receives the animation.


## Retargeting Example


A tall adult and a small child. The goal: the child plays the adult's idle animation, with movements scaled to the child's smaller body.


![](wrong_retargeting.png)

*Without retargeting: the child plays the adult's animation as-is, causing stretched limbs and incorrect proportions*


1. Suppose you have an adult and a child with the following assets. Both skeletons use the same joint names. **Adult:** **Child:**

  - `adult.skeleton` - joint hierarchy and bind pose (bone lengths are here).
  - `adult.mesh_skinned` - the adult's mesh, references `adult.skeleton`.
  - `adult_idle.anim` - idle animation with baked joint transforms, references `adult.skeleton`.

  - `child.skeleton` - joint hierarchy and bind pose (shorter bone lengths).
  - `child.mesh_skinned` - the child's mesh, references `child.skeleton`.
2. Check *Enable Retarget* **on both** `adult.skeleton` and `child.skeleton`. On the child's skeleton, switch joints to Proportion mode - this is the skeleton that receives the animation.
3. In the child's animation graph, assign `adult_idle.anim` to a playback node. The Engine detects that the animation's shared skeleton (`adult.skeleton`) differs from the child's **NodeSkeletonPose** skeleton (`child.skeleton`) and creates a proportional retargeter automatically.


![](correct_retargeting.png)

*With proportional retargeting: the same animation is scaled to the child's body, preserving correct proportions*


When [Root Motion](../../../content/animations/root_motion/index.md) is enabled, the root motion delta is also scaled by the retargeting ratio, so a smaller character moves a shorter distance per step. In **Bind** mode, root motion is zeroed out entirely since translations are discarded.


## See Also


- C++ Sample:
- [Preparing Animation Assets](../../../content/animations/animation_assets/index.md)
- [Blend Masks](../../../content/animations/blend_masks/index.md)
- [Root Motion](../../../content/animations/root_motion/index.md)
