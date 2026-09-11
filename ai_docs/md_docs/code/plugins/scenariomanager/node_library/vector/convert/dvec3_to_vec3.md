# DVec3 to Vec3


![](../../img/dvec3_to_vec3.png)

### Description

Converts a DVec3 to a Vec3, narrowing each component from double to single precision.


> **Notice:** Precision is lost. A world position far from the origin can shift noticeably when narrowed, so convert only where the reduced range is acceptable - typically once a position has already been turned into a local offset.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/dvec3.png) | **Value** | The value to convert. |
| ![](../../img/types/vec3.png) | **Result** | The converted value. |


## See Also


- [Vec3 to DVec3](../../../../../../code/plugins/scenariomanager/node_library/vector/convert/vec3_to_dvec3.md)
- [IVec3 to Vec3](../../../../../../code/plugins/scenariomanager/node_library/vector/convert/ivec3_to_vec3.md)
- [Vec2 to Vec3](../../../../../../code/plugins/scenariomanager/node_library/vector/convert/vec2_to_vec3.md)
