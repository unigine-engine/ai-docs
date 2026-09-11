# Break Mat2


![](../../img/break_mat2.png)

### Description

Splits a Mat2 into its two columns, each as a Vec2.


Each column is where one of the two axes ends up once the transformation is applied, so reading them back shows the directions and lengths the matrix gives those axes.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/mat2.png) | **M** | The matrix to split. |
| ![](../../img/types/vec2.png) | **col0** | The first column. |
| ![](../../img/types/vec2.png) | **col1** | The second column. |


## See Also


- [Make Mat2](../../../../../../code/plugins/scenariomanager/node_library/matrix/make/mat2.md)
- [Break Mat3](../../../../../../code/plugins/scenariomanager/node_library/matrix/break/mat3.md)
- [Break Vec2](../../../../../../code/plugins/scenariomanager/node_library/vector/break/vec2.md)
