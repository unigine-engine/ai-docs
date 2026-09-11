# DVec4 to Vec4


![](../../img/dvec4_to_vec4.png)

### Description

Converts a DVec4 to a Vec4, narrowing each component from double to single precision.


> **Notice:** Precision is lost. A world position far from the origin can shift noticeably when narrowed, so convert only where the reduced range is acceptable - typically once a position has already been turned into a local offset.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/dvec4.png) | **Value** | The value to convert. |
| ![](../../img/types/vec4.png) | **Result** | The converted value. |


## See Also


- [Vec4 to DVec4](../../../../../../code/plugins/scenariomanager/node_library/vector/convert/vec4_to_dvec4.md)
- [IVec4 to Vec4](../../../../../../code/plugins/scenariomanager/node_library/vector/convert/ivec4_to_vec4.md)
- [Vec3 to Vec4](../../../../../../code/plugins/scenariomanager/node_library/vector/convert/vec3_to_vec4.md)
