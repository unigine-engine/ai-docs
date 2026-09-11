# Direction Space


![](../img/direction_space.png)

### Description

Re-expresses a **direction** in another coordinate space. Unlike [Position Space](../../../../../content/animations/graph/node_library/transform/position_space.md), only the rotation of the frame is applied - the translation is ignored, so a direction keeps its length and is not shifted by the origin of the target space.


Use it for aim vectors, velocity directions and axes: anything that answers "which way", not "where".


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/vec3.png) | **In** | The direction to convert, expressed in the **From** space. |
| ![](../img/types/anim_pose.png) | **Pose** | The pose the joint frames are taken from. It is required only when **From** or **To** is set to Local; for a World-to-Object conversion the input may be left unconnected. |
| ![](../img/types/vec3.png) | **Out** | The same direction expressed in the **To** space. |


## Properties


| From | Space the incoming value is currently expressed in: World, Object (relative to the skeleton root), or Local (relative to the parent of the joint picked in **From Joint**). The default value is World. |
|---|---|
| To | Space the value is converted to. The same three options as **From**. The default value is Object. |
| From Joint | Joint whose local frame the incoming value is expressed in. Shown only when **From** is set to Local. |
| To Joint | Joint whose local frame the value is converted to. Shown only when **To** is set to Local. |


## See Also


- [Position Space](../../../../../content/animations/graph/node_library/transform/position_space.md) for points.
- [Rotation Space](../../../../../content/animations/graph/node_library/transform/rotation_space.md) for quaternions.
