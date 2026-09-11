# Mat4 to Mat3


![](../../img/mat4_to_mat3.png)

### Description

Converts a Mat4 to a Mat3, keeping the rotation and scale and discarding the position.


Dropping the position is what leaves a transformation suitable for directions: a heading should turn with an object but not be displaced by where it stands.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/mat4.png) | **Value** | The value to convert. |
| ![](../../img/types/mat3.png) | **Result** | The converted value. |


## See Also


- [Mat3 to Mat4](../../../../../../code/plugins/scenariomanager/node_library/matrix/convert/mat3_to_mat4.md)
- [Mat4 to Quat](../../../../../../code/plugins/scenariomanager/node_library/matrix/convert/mat4_to_quat.md)
- [Decompose TRS](../../../../../../code/plugins/scenariomanager/node_library/matrix/decompose.md)
