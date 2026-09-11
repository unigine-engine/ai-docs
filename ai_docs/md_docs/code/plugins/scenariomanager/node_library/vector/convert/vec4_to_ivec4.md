# Vec4 to IVec4


![](../../img/vec4_to_ivec4.png)

### Description

Converts a Vec4 to an IVec4, turning each floating-point component into a whole one.


> **Notice:** The fractional part is discarded rather than rounded, so 1.9 becomes 1 and -1.9 becomes -1. Apply [Round](../../../../../../code/plugins/scenariomanager/node_library/math/round.md) first to round to the nearest whole number instead.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/vec4.png) | **Value** | The value to convert. |
| ![](../../img/types/ivec4.png) | **Result** | The converted value. |


## See Also


- [IVec4 to Vec4](../../../../../../code/plugins/scenariomanager/node_library/vector/convert/ivec4_to_vec4.md)
- [Vec4 to DVec4](../../../../../../code/plugins/scenariomanager/node_library/vector/convert/vec4_to_dvec4.md)
- [Vec4 to Vec3](../../../../../../code/plugins/scenariomanager/node_library/vector/convert/vec4_to_vec3.md)
