# DVec2 to Vec2


![](../../img/dvec2_to_vec2.png)

### Description

Converts a DVec2 to a Vec2, narrowing each component from double to single precision.


> **Notice:** Precision is lost. A world position far from the origin can shift noticeably when narrowed, so convert only where the reduced range is acceptable - typically once a position has already been turned into a local offset.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/dvec2.png) | **Value** | The value to convert. |
| ![](../../img/types/vec2.png) | **Result** | The converted value. |


## See Also


- [Vec2 to DVec2](../../../../../../code/plugins/scenariomanager/node_library/vector/convert/vec2_to_dvec2.md)
- [IVec2 to Vec2](../../../../../../code/plugins/scenariomanager/node_library/vector/convert/ivec2_to_vec2.md)
- [Vec3 to Vec2](../../../../../../code/plugins/scenariomanager/node_library/vector/convert/vec3_to_vec2.md)
