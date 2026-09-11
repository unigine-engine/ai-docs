# Vec3 Lerp


![](../img/vec3_lerp.png)

### Description

Blends between the points **A** and **B** by the factor **C**, so that 0 gives **A**, 1 gives **B**, and 0.5 gives the point halfway between them.


Sweeping the factor from 0 to 1 traces the straight line between the two points, which is the simplest way to move something from one place to another. For a curved route use [Bezier Vec3](../../../../../code/plugins/scenariomanager/node_library/math/curves/bezier_vec3.md) or [CatmullRom Vec3](../../../../../code/plugins/scenariomanager/node_library/math/curves/catmullrom_vec3.md).


The factor is not restricted to the 0 to 1 range - values outside it continue past either end.


> **Notice:** Interpolating two directions this way shortens the result as it passes between them, so normalize it afterwards if a direction is needed. To blend rotations, use [Slerp](../../../../../code/plugins/scenariomanager/node_library/quaternion/slerp.md) instead.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/vec3.png) | **A** | The vector returned when **C** is 0. |
| ![](../img/types/vec3.png) | **B** | The vector returned when **C** is 1. |
| ![](../img/types/float.png) | **C** | The blend factor. |
| ![](../img/types/vec3.png) | **Result** | The blended vector. |


## See Also


- [Lerp](../../../../../code/plugins/scenariomanager/node_library/math/interpolation/lerp.md)
- [Slerp](../../../../../code/plugins/scenariomanager/node_library/quaternion/slerp.md)
- [CatmullRom Vec3](../../../../../code/plugins/scenariomanager/node_library/math/curves/catmullrom_vec3.md)
