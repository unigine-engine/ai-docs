# Vec2 to IVec2


![](../../img/vec2_to_ivec2.png)

### Description

Converts a Vec2 to an IVec2, turning each floating-point component into a whole one.


> **Notice:** The fractional part is discarded rather than rounded, so 1.9 becomes 1 and -1.9 becomes -1. Apply [Round](../../../../../../code/plugins/scenariomanager/node_library/math/round.md) first to round to the nearest whole number instead.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/vec2.png) | **Value** | The value to convert. |
| ![](../../img/types/ivec2.png) | **Result** | The converted value. |


## See Also


- [IVec2 to Vec2](../../../../../../code/plugins/scenariomanager/node_library/vector/convert/ivec2_to_vec2.md)
- [Vec2 to DVec2](../../../../../../code/plugins/scenariomanager/node_library/vector/convert/vec2_to_dvec2.md)
- [Vec2 to Vec3](../../../../../../code/plugins/scenariomanager/node_library/vector/convert/vec2_to_vec3.md)
