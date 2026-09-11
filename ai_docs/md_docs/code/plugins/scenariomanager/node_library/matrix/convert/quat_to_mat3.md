# Quat to Mat3


![](../../img/quat_to_mat3.png)

### Description

Expresses the rotation held by a quaternion as a Mat3.


The matrix form is the one that combines with other matrices, which is what this conversion is for once a rotation has been computed or blended as a quaternion. [Make Mat3 (Quat)](../../../../../../code/plugins/scenariomanager/node_library/matrix/make/mat3_quat.md) performs the same conversion.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/quat.png) | **Value** | The value to convert. |
| ![](../../img/types/mat3.png) | **Result** | The converted value. |


## See Also


- [Mat3 to Quat](../../../../../../code/plugins/scenariomanager/node_library/matrix/convert/mat3_to_quat.md)
- [Make Mat3 (Quat)](../../../../../../code/plugins/scenariomanager/node_library/matrix/make/mat3_quat.md)
- [Mat3 to Mat4](../../../../../../code/plugins/scenariomanager/node_library/matrix/convert/mat3_to_mat4.md)
