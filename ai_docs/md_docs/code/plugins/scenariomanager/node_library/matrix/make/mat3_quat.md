# Make Mat3 (Quat)


![](../../img/make_mat3_quat.png)

### Description

Builds a Mat3 that performs the rotation held by the quaternion **Q**.


The two forms describe the same rotation; the matrix is the one that combines with other matrices, which is what makes this the step between a rotation that has been computed or blended as a quaternion and a transformation built from it.


[Mat3 to Quat](../../../../../../code/plugins/scenariomanager/node_library/matrix/convert/mat3_to_quat.md) converts back.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/quat.png) | **Q** | The rotation to express as a matrix. |
| ![](../../img/types/mat3.png) | **Result** | The resulting matrix. |


## See Also


- [Mat3 to Quat](../../../../../../code/plugins/scenariomanager/node_library/matrix/convert/mat3_to_quat.md)
- [Make Mat3 (columns)](../../../../../../code/plugins/scenariomanager/node_library/matrix/make/mat3_columns.md)
- [Make DMat4](../../../../../../code/plugins/scenariomanager/node_library/matrix/make/dmat4.md)
