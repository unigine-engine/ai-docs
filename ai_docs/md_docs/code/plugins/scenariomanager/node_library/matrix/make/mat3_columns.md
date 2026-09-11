# Make Mat3 (columns)


![](../../img/make_mat3_columns.png)

### Description

Builds a Mat3 from three columns, each given as a Vec3.


The columns are where the X, Y and Z axes end up once the transformation is applied. Supplying three perpendicular directions of unit length this way builds a rotation from axes that have been computed rather than authored - the usual pattern being a forward direction, an up direction, and their [Cross](../../../../../../code/plugins/scenariomanager/node_library/vector/cross.md) product for the third.


Where the rotation is already available as a quaternion, [Make Mat3 (Quat)](../../../../../../code/plugins/scenariomanager/node_library/matrix/make/mat3_quat.md) is the direct route.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/vec3.png) | **col0** | The first column, where the X axis ends up. |
| ![](../../img/types/vec3.png) | **col1** | The second column, where the Y axis ends up. |
| ![](../../img/types/vec3.png) | **col2** | The third column, where the Z axis ends up. |
| ![](../../img/types/mat3.png) | **Result** | The assembled matrix. |


## See Also


- [Break Mat3](../../../../../../code/plugins/scenariomanager/node_library/matrix/break/mat3.md)
- [Make Mat3 (Quat)](../../../../../../code/plugins/scenariomanager/node_library/matrix/make/mat3_quat.md)
- [Cross](../../../../../../code/plugins/scenariomanager/node_library/vector/cross.md)
