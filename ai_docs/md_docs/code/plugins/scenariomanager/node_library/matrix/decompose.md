# Decompose TRS


![](../img/decompose_trs.png)

### Description

Takes a transformation matrix apart into the position, rotation and scale it was built from, so that each can be read or changed on its own - reading off where something stands, or altering its rotation while its position stays put.


[Compose TRS](../../../../../code/plugins/scenariomanager/node_library/matrix/compose.md) reverses the operation.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/mat4.png) | **A** | The transformation to take apart. |
| ![](../img/types/vec3.png) | **Translation** | The position. |
| ![](../img/types/quat.png) | **Rotation** | The rotation. |
| ![](../img/types/vec3.png) | **Scale** | The scale along each axis. |


## See Also


- [Compose TRS](../../../../../code/plugins/scenariomanager/node_library/matrix/compose.md)
- [Break DMat4](../../../../../code/plugins/scenariomanager/node_library/matrix/break/dmat4.md)
- [Quat to Euler](../../../../../code/plugins/scenariomanager/node_library/quaternion/to_euler.md)
