# Make DMat4


![](../../img/make_dmat4.png)

### Description

Builds a DMat4 world transformation from a rotation and a position.


The position is kept at double precision, which is what allows a placement to stay accurate far from the world origin. The rotation is supplied as a Mat3 and needs no extra precision, since it describes only orientation and scale.


Use [Make Mat3 (Quat)](../../../../../../code/plugins/scenariomanager/node_library/matrix/make/mat3_quat.md) to supply the rotation from a quaternion.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/mat3.png) | **Rotation** | The rotation and scale. |
| ![](../../img/types/dvec3.png) | **Translation** | The position. |
| ![](../../img/types/dmat4.png) | **Result** | The assembled transformation. |


## See Also


- [Break DMat4](../../../../../../code/plugins/scenariomanager/node_library/matrix/break/dmat4.md)
- [Make Mat3 (Quat)](../../../../../../code/plugins/scenariomanager/node_library/matrix/make/mat3_quat.md)
- [Compose TRS](../../../../../../code/plugins/scenariomanager/node_library/matrix/compose.md)
