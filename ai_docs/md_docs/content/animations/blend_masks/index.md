# Blend Masks


A blend mask restricts a **[Blend Poses](../../../content/animations/graph/node_library/blend/blend_poses.md)** blend to a subset of joints, so some parts of the skeleton follow the blend while others pass through from pose **A** unchanged. This enables partial blending - for example, playing an upper-body aiming or waving animation only on the spine, arms, and head, while the legs stay fully controlled by the locomotion animation.

   Sorry, your browser does not support embedded videos.
*A state machine drives three locomotion animations (idle, walk, run). A blend mask lets the waving animation play on the upper body without affecting the legs, so the character keeps moving normally.*


## How Blend Masks Work


A blend mask is applied to a **Blend Poses** node. It determines which joints take part in the blend: a joint covered by the mask is blended, and a joint outside the mask is not blended at all - it keeps pose **A**. The mask covers every joint, including the root bone, so it also controls how [root motion](../../../content/animations/root_motion/index.md) is blended.


How the affected joints are chosen is set by the **Mask Mode** of the node:


- None - no mask; all joints blend with the same weight.
- **Skeleton Mask** - a named mask stored on the skeleton, with a custom influence value per joint.
- **Joint List** - an explicit list of joints defined on the node.
- **Joint Subtree** - a joint and all of its descendants, defined on the node.


Blending is always applied in each joint's local space (relative to its parent), so a masked joint stays attached to its parent and the mesh is never torn apart, no matter which joints the mask covers.


## Skeleton Mask


A **Skeleton Mask** is a named mask stored on the skeleton asset, where each joint has its own influence value from 0.0 to 1.0 that scales the blend weight for that joint individually. The final blend weight for each joint is calculated as:


Final Weight = Weight � Influence


Where:


- **Weight** is the blend weight input on the **Blend Poses** node (a single value for the whole blend).
- **Influence** is the per-joint value from the blend mask (0.0 to 1.0).


For example, if the **Weight** input is 0.8 and a joint's blend mask influence is 0.5, that joint blends at 0.4 (0.8 x 0.5). Joints with influence 0.0 are not blended at all - they pass through from pose **A** unchanged. Joints with influence 1.0 blend at the full **Weight** value.


The blend mask applies to all joints, including the root bone. If [root motion](../../../content/animations/root_motion/index.md) is enabled, the root bone's influence value affects how root motion is blended - setting it to 0.0 means root motion comes entirely from pose **A**.


### Creating a Skeleton Mask


Skeleton masks are created and stored on the skeleton asset. Each skeleton can have multiple named blend masks.


To create a blend mask:


1. Select a skeleton asset in the *Asset Browser*.
2. In the *Blend Masks* section, click *+* to add a new mask.
3. Enter a name for the mask (e.g., UpperBody, LeftArm).
4. For each joint in the skeleton hierarchy, set the influence value from 0.0 (not affected) to 1.0 (fully affected).


| ![](blend_masks_option.png) | ![](upper_body_example.png) |
|---|---|


The joint hierarchy is displayed as a tree. Set high influence values on joints you want to be affected by the blend, and low or zero values on joints you want to pass through unchanged.


You can use intermediate values for smooth transitions between body regions - for example, setting the lower spine to 0.3 and upper spine to 0.7 creates a gradual falloff instead of a hard cut.


## Joint List and Joint Subtree


These two modes define the mask directly on the **Blend Poses** node, without editing the skeleton asset. They are handy when you just need to select a region of the skeleton and do not need a per-joint influence curve - and when you do not want to modify the shared skeleton asset (for example, a mask specific to one graph).


- **Joint List** - an explicit list of joint names. Only the listed joints are affected. Use it when you want to pick out individual joints.
- **Joint Subtree** - a root joint and all of its descendants. Naming a single top joint selects a whole region of the body, such as an entire arm, the upper body, or a tail chain. Use it when the region you need matches a branch of the skeleton hierarchy.


In both modes every selected joint is blended at the full **Weight**, and every other joint passes through from pose **A**. There is no per-joint influence, so the transition between the affected and unaffected regions is abrupt rather than smooth. This is usually fine when the boundary sits at a natural break in the body (for example, masking a whole arm from the shoulder down). If you need a gradual falloff across the boundary - such as fading the blend along the spine - use a [Skeleton Mask](#skeleton_mask) with intermediate influence values instead.


Joint names that do not exist in the skeleton are ignored. An empty list or an empty subtree root means no mask, and the node performs a full-body blend.


## Choosing a Mask Mode in the Animation Graph


Select a **[Blend Poses](../../../content/animations/graph/node_library/blend/blend_poses.md)** node and choose how the mask is defined in the **Mask Mode** dropdown of the *Selected Item* panel. Depending on the selected mode, an additional field appears below it:


| None | No mask. All joints blend with the same **Weight**. |
|---|---|
| Skeleton Mask | Choose the mask from the **Blend Mask** dropdown, which lists all masks defined on the skeleton assigned to the graph. |
| Joint List | Add joint names in the **Joints** list. |
| Joint Subtree | Pick the top joint of the region in the **Subtree Root** field. |


![](choosing_blend_mask.png)


## See Also


- [Blend Poses](../../../content/animations/graph/node_library/blend/blend_poses.md)
- [Animation Graph Overview](../../../content/animations/index.md)
