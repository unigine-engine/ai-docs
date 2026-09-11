# Break DMat4


![](../../img/break_dmat4.png)

### Description

Splits a DMat4 world transformation into its rotation and its position.


The position comes out at double precision, so a world placement can be read without losing the accuracy that the type exists to preserve. The rotation comes out as a Mat3, which [Mat3 to Quat](../../../../../../code/plugins/scenariomanager/node_library/matrix/convert/mat3_to_quat.md) turns into a quaternion.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/dmat4.png) | **M** | The transformation to split. |
| ![](../../img/types/mat3.png) | **Rotation** | The rotation and scale. |
| ![](../../img/types/dvec3.png) | **Translation** | The position. |


## See Also


- [Make DMat4](../../../../../../code/plugins/scenariomanager/node_library/matrix/make/dmat4.md)
- [Mat3 to Quat](../../../../../../code/plugins/scenariomanager/node_library/matrix/convert/mat3_to_quat.md)
- [Decompose TRS](../../../../../../code/plugins/scenariomanager/node_library/matrix/decompose.md)
