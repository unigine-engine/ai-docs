# Dot


![](../img/dot.png)

### Description

Outputs the dot product of **A** and **B**, a single number that tells how much the two vectors point the same way.


For directions of unit length the result runs from 1 when they coincide, through 0 when they are perpendicular, to -1 when they are opposite. This makes the sign alone a cheap test of whether something lies ahead or behind, and the value itself the cosine of the angle between them, which [Acos](../../../../../code/plugins/scenariomanager/node_library/math/trig/acos.md) turns into the angle.


When the inputs are not normalized the result is also scaled by both lengths, so normalize them first with [Vec3 Normalize](../../../../../code/plugins/scenariomanager/node_library/vector/normalize.md) if only the direction matters.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/vec3.png) | **A** | The first vector. |
| ![](../img/types/vec3.png) | **B** | The second vector. |
| ![](../img/types/float.png) | **Result** | The dot product. |


## See Also


- [Cross](../../../../../code/plugins/scenariomanager/node_library/vector/cross.md)
- [Vec3 Normalize](../../../../../code/plugins/scenariomanager/node_library/vector/normalize.md)
- [Length](../../../../../code/plugins/scenariomanager/node_library/vector/length.md)
