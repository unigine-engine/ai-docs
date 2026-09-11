# Cross


![](../img/cross.png)

### Description

Outputs the cross product of **A** and **B**: a vector perpendicular to both of them. This is the usual way to obtain an axis to rotate around, or the normal of a surface described by two edges.


The order of the inputs decides which of the two perpendicular directions comes out - swapping them reverses the result.


The length of the result grows with the angle between the inputs and reaches its maximum when they are perpendicular. Vectors that point the same way, or exactly opposite ways, have no single perpendicular direction between them and give a zero-length result.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/vec3.png) | **A** | The first vector. |
| ![](../img/types/vec3.png) | **B** | The second vector. |
| ![](../img/types/vec3.png) | **Result** | The vector perpendicular to both inputs. |


## See Also


- [Dot](../../../../../code/plugins/scenariomanager/node_library/vector/dot.md)
- [Vec3 Normalize](../../../../../code/plugins/scenariomanager/node_library/vector/normalize.md)
- [Reflect](../../../../../code/plugins/scenariomanager/node_library/vector/reflect.md)
