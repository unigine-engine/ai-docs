# CatmullRom Vec3


![](../../img/catmullrom_vec3.png)

### Description

Evaluates a Catmull-Rom spline through space at the position **T**, moving from **P1** to **P2**. This is [CatmullRom](../../../../../../code/plugins/scenariomanager/node_library/math/curves/catmullrom.md) applied to points rather than to single numbers.


The neighbouring points **P0** and **P3** shape the direction of travel at each end without being visited. Running consecutive segments over a list of waypoints produces a route that passes through every waypoint with no corner at the joins, which is the usual way to make a patrol or camera path follow marked positions smoothly.


> **Notice:** Equal steps in **T** do not cover equal distances along the curve, so movement driven directly by **T** varies in speed where the curve bends.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/vec3.png) | **P0** | The point before the segment, which sets the starting direction. |
| ![](../../img/types/vec3.png) | **P1** | The point at the start of the segment. |
| ![](../../img/types/vec3.png) | **P2** | The point at the end of the segment. |
| ![](../../img/types/vec3.png) | **P3** | The point after the segment, which sets the ending direction. |
| ![](../../img/types/float.png) | **T** | The position within the segment. |
| ![](../../img/types/vec3.png) | **Result** | The point on the spline at that position. |


## See Also


- [CatmullRom](../../../../../../code/plugins/scenariomanager/node_library/math/curves/catmullrom.md)
- [Bezier Vec3](../../../../../../code/plugins/scenariomanager/node_library/math/curves/bezier_vec3.md)
- [Lerp](../../../../../../code/plugins/scenariomanager/node_library/math/interpolation/lerp.md)
