# Animation Pose


![](../img/animation_pose.png)

### Description

Samples a static pose at a specific frame from an animation. Unlike **[Animation Player](../../../../../content/animations/graph/node_library/animation/animation_player.md)**, this node does not advance playback over time - it always outputs the pose at the given frame number. Useful for pose-driven blending or previewing specific frames.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/anim_asset.png) | **Anim** | The animation (`.anim`) to sample. You can either connect an **[Animation Asset](../../../../../content/animations/graph/node_library/animation/animation_asset.md)** node or pick the animation directly via the inline asset picker on the node. |
| ![](../img/types/float.png) | **Frame** | The frame number to extract the pose from. Default: 0.0. |
| ![](../img/types/anim_pose.png) | **Pose** | The pose at the specified frame. |


## See Also


- [Animation Asset](../../../../../content/animations/graph/node_library/animation/animation_asset.md)
- [Animation Player](../../../../../content/animations/graph/node_library/animation/animation_player.md)
