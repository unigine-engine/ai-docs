# Blend Space 2D Sync


![](../img/blendspace_2d_sync.png)

### Description

A variant of **[BlendSpace 2D](../../../../../content/animations/graph/node_library/blend_space/blend_space_2d.md)** designed for synchronized animation playback. Instead of subgraphs, each blend point references a single animation asset with its own playback speed. All animations in the blend space play in sync, maintaining consistent timing - for example, keeping footsteps aligned across walk and run animations at different speeds. Use this node when you need smooth blending between animations that must stay in phase.


See **[Blend Spaces](../../../../../content/animations/blend_spaces/index.md)** and **[Animation Synchronization](../../../../../content/animations/synchronization/index.md)** articles for details.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/float.png) | **X** | Position along the X axis of the blend space. Default: 0.0. |
| ![](../img/types/float.png) | **Y** | Position along the Y axis of the blend space. Default: 0.0. |
| ![](../img/types/anim_pose.png) | **Pose** | The interpolated pose based on the current **X** and **Y** position. |


## Properties


| Name | Display name of the blend space node. Must be unique within the graph. |
|---|---|
| Axis X | Display name for the X axis. Also updates the **X** input label on the node. |
| Axis Y | Display name for the Y axis. Also updates the **Y** input label on the node. |
| Grid X | Number of grid cells along the X axis, for visual reference only. Range: 1 to 20. |
| Grid Y | Number of grid cells along the Y axis, for visual reference only. Range: 1 to 20. |
| Axis Min | Minimum value for both axes. Default: -1.0. |
| Axis Max | Maximum value for both axes. Default: 1.0. |
| Mode | Interpolation mode: Cartesian or Polar. Default: Cartesian. |
| Smooth Weights | When enabled, blend weights transition smoothly over time instead of snapping instantly. |
| Smoothing Speed | Controls how quickly weights change when **Smooth Weights** is enabled. Minimum: 0.01. |
| Sync Group | Name of the synchronization group. Nodes in the same group synchronize their playback. |
| Sync Role | Role in the sync group: Leader, Follower, or Weighted Leader. |
| Sync Method | How playback is synchronized: Normalized Time or Marker Sync. |


## See Also


- [Blend Spaces](../../../../../content/animations/blend_spaces/index.md)
- [Animation Synchronization](../../../../../content/animations/synchronization/index.md)
- [BlendSpace 2D](../../../../../content/animations/graph/node_library/blend_space/blend_space_2d.md)
