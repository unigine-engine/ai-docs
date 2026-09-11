# Break Mat3


![](../../img/break_mat3.png)

### Description

Splits a Mat3 into its three columns, each as a Vec3.


The columns are where the X, Y and Z axes end up once the transformation is applied, so this is how the axes of an orientation are read out - taking the column that corresponds to the forward axis gives the direction an object faces.


> **Notice:** The columns are of unit length only when the matrix carries no scale. Normalize a column with [Vec3 Normalize](../../../../../../code/plugins/scenariomanager/node_library/vector/normalize.md) where a pure direction is needed.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/mat3.png) | **M** | The matrix to split. |
| ![](../../img/types/vec3.png) | **col0** | The first column, where the X axis ends up. |
| ![](../../img/types/vec3.png) | **col1** | The second column, where the Y axis ends up. |
| ![](../../img/types/vec3.png) | **col2** | The third column, where the Z axis ends up. |


## See Also


- [Make Mat3 (columns)](../../../../../../code/plugins/scenariomanager/node_library/matrix/make/mat3_columns.md)
- [Break Mat2](../../../../../../code/plugins/scenariomanager/node_library/matrix/break/mat2.md)
- [Vec3 Normalize](../../../../../../code/plugins/scenariomanager/node_library/vector/normalize.md)
