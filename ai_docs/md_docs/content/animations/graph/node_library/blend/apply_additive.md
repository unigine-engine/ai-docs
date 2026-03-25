# Apply Additive


![](../img/apply_additive.png)

### Description

Applies an additive pose on top of a **Base** pose using multiplicative blending. Connect a delta pose (created by **[Make Additive](../../../../../content/animations/graph/node_library/blend/make_additive.md)**) to the **Additive** input, and it will be layered onto the **Base** with the given **Weight**. When **Weight** is 0, the output equals the **Base** pose unchanged.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/anim_pose.png) | **Base** | The base pose to apply the additive on top of. |
| ![](../img/types/anim_pose.png) | **Additive** | The additive (delta) pose to layer onto the base. Typically created by **[Make Additive](../../../../../content/animations/graph/node_library/blend/make_additive.md)**. |
| ![](../img/types/float.png) | **Weight** | Strength of the additive effect. Clamped to [0, 1] range. |
| ![](../img/types/anim_pose.png) | **Pose** | The resulting pose with the additive applied. |


## See Also


- [Make Additive](../../../../../content/animations/graph/node_library/blend/make_additive.md)
- [Blend Poses](../../../../../content/animations/graph/node_library/blend/blend_poses.md)
