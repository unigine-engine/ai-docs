# Vec3 to IVec3


![](../../img/vec3_to_ivec3.png)

### Description

Converts a Vec3 to an IVec3, turning each floating-point component into a whole one.


> **Notice:** The fractional part is discarded rather than rounded, so 1.9 becomes 1 and -1.9 becomes -1. Apply [Round](../../../../../../code/plugins/scenariomanager/node_library/math/round.md) first to round to the nearest whole number instead.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/vec3.png) | **Value** | The value to convert. |
| ![](../../img/types/ivec3.png) | **Result** | The converted value. |


## See Also


- [IVec3 to Vec3](../../../../../../code/plugins/scenariomanager/node_library/vector/convert/ivec3_to_vec3.md)
- [Vec3 to DVec3](../../../../../../code/plugins/scenariomanager/node_library/vector/convert/vec3_to_dvec3.md)
- [Vec3 to Vec2](../../../../../../code/plugins/scenariomanager/node_library/vector/convert/vec3_to_vec2.md)
