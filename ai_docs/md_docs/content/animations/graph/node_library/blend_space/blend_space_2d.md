# Blend Space 2D


![](../img/blendspace_2d.png)

### Description

Blends between multiple animation subgraphs arranged in a 2D space. Each blend point contains its own subgraph that produces a pose. The **X** and **Y** inputs determine the current position in the blend space, and the output pose is interpolated from the nearest points using triangulation. The interpolation mode can be set to Cartesian or Polar.


Double-click this node to open the blend space editor, where you can add, remove, and position blend points. Each point opens its own subgraph where you build the animation logic for that point.


See **[Blend Spaces](../../../../../content/animations/blend_spaces/index.md)** article for details.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/float.png) | **X** | Position along the X axis of the blend space. |
| ![](../img/types/float.png) | **Y** | Position along the Y axis of the blend space. |
| ![](../img/types/anim_pose.png) | **Pose** | The interpolated pose based on the current **X** and **Y** position. |


## Properties


| Name | Display name of the blend space node. Must be unique within the graph. |
|---|---|
| Axis X | Display name for the X axis (e.g., Speed). Also updates the **X** input label on the node. |
| Axis Y | Display name for the Y axis (e.g., Direction). Also updates the **Y** input label on the node. |
| Grid X | Number of grid cells along the X axis, for visual reference only. Range: 1 to 20. |
| Grid Y | Number of grid cells along the Y axis, for visual reference only. Range: 1 to 20. |
| Axis Min | Minimum value for both axes. |
| Axis Max | Maximum value for both axes. |
| Mode | Interpolation mode: Cartesian (standard 2D distance) or Polar (angle-based, useful for directional blending). |
| Smooth Weights | When enabled, blend weights transition smoothly over time instead of snapping instantly. |
| Smoothing Speed | Controls how quickly weights change when **Smooth Weights** is enabled. Higher values mean faster transitions. |


## See Also


- [Blend Spaces](../../../../../content/animations/blend_spaces/index.md)
- [BlendSpace 2D Sync](../../../../../content/animations/graph/node_library/blend_space/blend_space_2d_sync.md)
