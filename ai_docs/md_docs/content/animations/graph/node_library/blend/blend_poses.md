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


| Blend Mask | Optional mask that controls blending intensity per joint. See [Blend Masks](../../../../../content/animations/blend_masks/index.md) article for details. |
|---|---|


## See Also


- [Make Additive](../../../../../content/animations/graph/node_library/blend/make_additive.md)
- [Apply Additive](../../../../../content/animations/graph/node_library/blend/apply_additive.md)
