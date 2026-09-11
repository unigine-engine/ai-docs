# Mat3 to Quat


![](../../img/mat3_to_quat.png)

### Description

Extracts the rotation held by a Mat3 as a quaternion.


Quaternions are the form rotations are blended and combined in, so this is the step between a matrix that has been read from a transformation and a rotation that [Slerp](../../../../../../code/plugins/scenariomanager/node_library/quaternion/slerp.md) or [Quat Multiply](../../../../../../code/plugins/scenariomanager/node_library/quaternion/multiply.md) can work with.


> **Notice:** Only the orientation carries over. A scale held by the matrix is not represented in a quaternion and is lost in the conversion.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/mat3.png) | **Value** | The value to convert. |
| ![](../../img/types/quat.png) | **Result** | The converted value. |


## See Also


- [Quat to Mat3](../../../../../../code/plugins/scenariomanager/node_library/matrix/convert/quat_to_mat3.md)
- [Mat4 to Quat](../../../../../../code/plugins/scenariomanager/node_library/matrix/convert/mat4_to_quat.md)
- [Slerp](../../../../../../code/plugins/scenariomanager/node_library/quaternion/slerp.md)
