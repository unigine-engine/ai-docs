# CatmullRom


![](../../img/catmullrom.png)

### Description

Evaluates a Catmull-Rom spline at the position **T**, interpolating between **P1** and **P2**, where 0 gives **P1** and 1 gives **P2**.


The outer points **P0** and **P3** are not reached; they set the slope at each end so the segment leaves and arrives in line with its neighbours. Chaining segments over a list of values in this way gives a single smooth curve that passes through all of them.


This is the difference from [Bezier](../../../../../../code/plugins/scenariomanager/node_library/math/curves/bezier.md), whose middle points are pulled toward rather than passed through: here the curve hits the values it is given, which suits a series of samples that must be honoured exactly.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/float.png) | **P0** | The value before the segment, which sets the starting slope. |
| ![](../../img/types/float.png) | **P1** | The value at the start of the segment. |
| ![](../../img/types/float.png) | **P2** | The value at the end of the segment. |
| ![](../../img/types/float.png) | **P3** | The value after the segment, which sets the ending slope. |
| ![](../../img/types/float.png) | **T** | The position within the segment. |
| ![](../../img/types/float.png) | **Result** | The value of the spline at that position. |


## See Also


- [CatmullRom Vec3](../../../../../../code/plugins/scenariomanager/node_library/math/curves/catmullrom_vec3.md)
- [Bezier](../../../../../../code/plugins/scenariomanager/node_library/math/curves/bezier.md)
- [Lerp](../../../../../../code/plugins/scenariomanager/node_library/math/interpolation/lerp.md)
