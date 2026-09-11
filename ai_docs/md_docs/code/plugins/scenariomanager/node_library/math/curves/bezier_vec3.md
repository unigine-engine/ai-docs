# Bezier Vec3


![](../../img/bezier_vec3.png)

### Description

Evaluates a cubic Bezier curve through space at the position **T**, where 0 is the start of the curve and 1 its end. This is [Bezier](../../../../../../code/plugins/scenariomanager/node_library/math/curves/bezier.md) applied to points rather than to single numbers.


The path runs from **P0** to **P3**, bent toward the control points **P1** and **P2** without passing through them. Sweeping **T** from 0 to 1 traces a curved route between two places - a flight path, or a camera move that avoids a straight line.


> **Notice:** Equal steps in **T** do not cover equal distances along the curve, so movement driven directly by **T** varies in speed where the curve bends.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/vec3.png) | **P0** | The point at the start of the curve. |
| ![](../../img/types/vec3.png) | **P1** | The first control point. |
| ![](../../img/types/vec3.png) | **P2** | The second control point. |
| ![](../../img/types/vec3.png) | **P3** | The point at the end of the curve. |
| ![](../../img/types/float.png) | **T** | The position along the curve. |
| ![](../../img/types/vec3.png) | **Result** | The point on the curve at that position. |


## See Also


- [Bezier](../../../../../../code/plugins/scenariomanager/node_library/math/curves/bezier.md)
- [CatmullRom Vec3](../../../../../../code/plugins/scenariomanager/node_library/math/curves/catmullrom_vec3.md)
- [Lerp](../../../../../../code/plugins/scenariomanager/node_library/math/interpolation/lerp.md)
