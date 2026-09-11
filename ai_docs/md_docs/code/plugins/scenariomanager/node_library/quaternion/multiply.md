# Quat Multiply


![](../img/quat_multiply.png)

### Description

Combines the rotations **A** and **B** into the single rotation that performs both, which is how an offset is added to an existing orientation - a turret angle applied on top of the hull it sits on.


> **Notice:** Rotations do not commute: swapping the inputs generally gives a different result, because each rotation is applied relative to the orientation the previous one left behind.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/quat.png) | **A** | The first rotation. |
| ![](../img/types/quat.png) | **B** | The second rotation. |
| ![](../img/types/quat.png) | **Result** | The combined rotation. |


## See Also


- [Quat Inverse](../../../../../code/plugins/scenariomanager/node_library/quaternion/inverse.md)
- [Rotate Vector](../../../../../code/plugins/scenariomanager/node_library/quaternion/rotate_vec.md)
- [Slerp](../../../../../code/plugins/scenariomanager/node_library/quaternion/slerp.md)
