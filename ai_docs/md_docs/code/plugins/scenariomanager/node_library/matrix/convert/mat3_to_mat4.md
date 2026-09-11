# Mat3 to Mat4


![](../../img/mat3_to_mat4.png)

### Description

Converts a Mat3 to a Mat4, keeping the rotation and scale and adding a position of zero.


The result places its object at the world origin, oriented as the original matrix describes. Combine it with a transformation that carries a position, or use [Compose TRS](../../../../../../code/plugins/scenariomanager/node_library/matrix/compose.md) to supply one directly.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/mat3.png) | **Value** | The value to convert. |
| ![](../../img/types/mat4.png) | **Result** | The converted value. |


## See Also


- [Mat4 to Mat3](../../../../../../code/plugins/scenariomanager/node_library/matrix/convert/mat4_to_mat3.md)
- [Compose TRS](../../../../../../code/plugins/scenariomanager/node_library/matrix/compose.md)
- [Mat4 Multiply](../../../../../../code/plugins/scenariomanager/node_library/matrix/multiply.md)
