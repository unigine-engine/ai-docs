# Make Mat2


![](../../img/make_mat2.png)

### Description

Builds a Mat2 from two columns, each given as a Vec2.


A two-by-two matrix describes a rotation, scale or shear in a plane. Its columns are where the two axes end up once the transformation is applied, which is the direct way to specify one: give each axis its new direction and length.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/vec2.png) | **col0** | The first column. |
| ![](../../img/types/vec2.png) | **col1** | The second column. |
| ![](../../img/types/mat2.png) | **Result** | The assembled matrix. |


## See Also


- [Break Mat2](../../../../../../code/plugins/scenariomanager/node_library/matrix/break/mat2.md)
- [Make Mat3 (columns)](../../../../../../code/plugins/scenariomanager/node_library/matrix/make/mat3_columns.md)
- [Mat2 Identity](../../../../../../code/plugins/scenariomanager/node_library/constants/mat2.md)
