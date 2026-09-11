# Compose TRS


![](../img/compose_trs.png)

### Description

Builds a transformation matrix from a position, a rotation and a scale, combining the three into the single value that places an object in space.


The parts are applied in the order the name gives: the scale first, then the rotation, then the position. That order is what makes the rotation turn the object about its own origin rather than sweeping it around the world origin.


[Decompose TRS](../../../../../code/plugins/scenariomanager/node_library/matrix/decompose.md) reverses the operation.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/vec3.png) | **A** | The position. |
| ![](../img/types/quat.png) | **B** | The rotation. |
| ![](../img/types/vec3.png) | **C** | The scale along each axis. |
| ![](../img/types/mat4.png) | **Result** | The resulting transformation. |


## See Also


- [Decompose TRS](../../../../../code/plugins/scenariomanager/node_library/matrix/decompose.md)
- [Mat4 Multiply](../../../../../code/plugins/scenariomanager/node_library/matrix/multiply.md)
- [Make DMat4](../../../../../code/plugins/scenariomanager/node_library/matrix/make/dmat4.md)
