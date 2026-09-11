# Rotation Space


![](../img/rotation_space.png)

### Description

Re-expresses a **rotation** in another coordinate space. The node composes the source and target frames and outputs the quaternion that produces the same orientation in the space set by the **To** property.


A common use is taking a joint rotation read in object space, adjusting it, and converting it back to the local frame of another joint before writing it with [Set Joint Transform](../../../../../content/animations/graph/node_library/transform/set_joint_transform.md).


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/quat.png) | **In** | The rotation to convert, expressed in the **From** space. |
| ![](../img/types/anim_pose.png) | **Pose** | The pose the joint frames are taken from. It is required only when **From** or **To** is set to Local; for a World-to-Object conversion the input may be left unconnected. |
| ![](../img/types/quat.png) | **Out** | The same rotation expressed in the **To** space. |


## Properties


| From | Space the incoming value is currently expressed in: World, Object (relative to the skeleton root), or Local (relative to the parent of the joint picked in **From Joint**). The default value is World. |
|---|---|
| To | Space the value is converted to. The same three options as **From**. The default value is Object. |
| From Joint | Joint whose local frame the incoming value is expressed in. Shown only when **From** is set to Local. |
| To Joint | Joint whose local frame the value is converted to. Shown only when **To** is set to Local. |


## See Also


- [Position Space](../../../../../content/animations/graph/node_library/transform/position_space.md) for points.
- [Direction Space](../../../../../content/animations/graph/node_library/transform/direction_space.md) for vectors that carry a direction only.
- [Euler to Quat](../../../../../content/animations/graph/node_library/math/euler_to_quat.md) to build a rotation from degrees.
