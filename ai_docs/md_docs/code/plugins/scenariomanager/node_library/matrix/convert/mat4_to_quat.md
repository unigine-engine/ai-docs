# Mat4 to Quat


![](../../img/mat4_to_quat.png)

### Description

Extracts the rotation held by a Mat4 as a quaternion, discarding its position and scale.


This is the short route from a full transformation to the orientation alone, where [Decompose TRS](../../../../../../code/plugins/scenariomanager/node_library/matrix/decompose.md) would also return parts that are not needed.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/mat4.png) | **Value** | The value to convert. |
| ![](../../img/types/quat.png) | **Result** | The converted value. |


## See Also


- [Mat3 to Quat](../../../../../../code/plugins/scenariomanager/node_library/matrix/convert/mat3_to_quat.md)
- [Decompose TRS](../../../../../../code/plugins/scenariomanager/node_library/matrix/decompose.md)
- [Quat to Euler](../../../../../../code/plugins/scenariomanager/node_library/quaternion/to_euler.md)
