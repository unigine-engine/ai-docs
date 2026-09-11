# Quat Inverse


![](../img/quat_inverse.png)

### Description

Outputs the rotation that undoes **A**: the same turn taken in the opposite direction. Combining a rotation with its inverse leaves an orientation unchanged.


This is what converts between frames of reference. Applying the inverse of an object's rotation to a world direction expresses that direction as the object sees it - which is how a bearing is found relative to where something is facing.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/quat.png) | **A** | The rotation to invert. |
| ![](../img/types/quat.png) | **Result** | The inverted rotation. |


## See Also


- [Quat Multiply](../../../../../code/plugins/scenariomanager/node_library/quaternion/multiply.md)
- [Rotate Vector](../../../../../code/plugins/scenariomanager/node_library/quaternion/rotate_vec.md)
- [Mat4 inverse](../../../../../code/plugins/scenariomanager/node_library/matrix/inverse.md)
