# Make Additive


![](../img/make_additive.png)

### Description

Creates an additive pose by computing the difference between **Base** and **Reference** poses.


For example, if you have a breathing animation made from an idle pose, connect the breathing as **Base** and the idle as **Reference** - the node will extract just the breathing motion. This delta can then be layered on top of any other animation (walk, run, etc.) using **[Apply Additive](../../../../../content/animations/graph/node_library/blend/apply_additive.md)**. Without this node, you would need to create a separate additive animation in your DCC tool.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/anim_pose.png) | **Base** | The target pose. |
| ![](../img/types/anim_pose.png) | **Reference** | The reference pose to subtract from the base. |
| ![](../img/types/anim_pose.png) | **Additive** | The computed additive (delta) pose: **Base** minus **Reference**. |


## See Also


- [Apply Additive](../../../../../content/animations/graph/node_library/blend/apply_additive.md)
- [Blend Poses](../../../../../content/animations/graph/node_library/blend/blend_poses.md)
