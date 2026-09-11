# Blend Poses


![](../img/blend_poses.png)

### Description

Linearly blends (lerp) between two animation poses. When the **Weight** is 0, the output equals pose **A**; when the **Weight** is 1, the output equals pose **B**. Values in between produce a smooth mix of both poses. You can optionally apply a blend mask to limit blending to specific joints.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/anim_pose.png) | **A** | The first pose (returned when **Weight** is 0). |
| ![](../img/types/anim_pose.png) | **B** | The second pose (returned when **Weight** is 1). |
| ![](../img/types/float.png) | **Weight** | Blend weight between the two poses. Clamped to [0, 1] range. |
| ![](../img/types/anim_pose.png) | **Pose** | The blended result. |


## Properties


| Mask Mode | How the blend mask is defined: None (no mask), Skeleton Mask (a named mask from the skeleton asset with per-joint influence), Joint List (an explicit list of joints), or Joint Subtree (a joint and all its descendants). Depending on the mode, an additional field appears for the mask name, the joint list, or the subtree root. See the [Blend Masks](../../../../../content/animations/blend_masks/index.md) article for details. |
|---|---|
| Blend Mask | Name of the mask stored on the skeleton asset. Shown only when **Mask Mode** is set to Skeleton Mask; the drop-down lists the masks defined on the skeleton assigned to the graph. |
| Joints | Explicit list of joint names taking part in the blend. Shown only when **Mask Mode** is set to Joint List. |
| Subtree Root | Top joint of the region: it and all of its descendants take part in the blend. Shown only when **Mask Mode** is set to Joint Subtree. |


## See Also


- [Make Additive](../../../../../content/animations/graph/node_library/blend/make_additive.md)
- [Apply Additive](../../../../../content/animations/graph/node_library/blend/apply_additive.md)
