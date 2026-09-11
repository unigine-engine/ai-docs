# Bezier


![](../../img/bezier.png)

### Description

Evaluates a cubic Bezier curve at the position **T**, where 0 is the start of the curve and 1 its end.


The curve runs from **P0** to **P3**. The two middle points pull it toward themselves without being touched, so **P1** shapes the departure from the start and **P2** the arrival at the end. This is the usual way to define an eased progression whose exact shape matters - an acceleration profile, or a value that overshoots before settling.


Values of **T** outside 0 to 1 continue the curve's formula beyond its ends and diverge quickly.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/float.png) | **P0** | The value at the start of the curve. |
| ![](../../img/types/float.png) | **P1** | The first control point. |
| ![](../../img/types/float.png) | **P2** | The second control point. |
| ![](../../img/types/float.png) | **P3** | The value at the end of the curve. Defaults to 1. |
| ![](../../img/types/float.png) | **T** | The position along the curve. |
| ![](../../img/types/float.png) | **Result** | The value of the curve at that position. |


## See Also


- [Bezier Vec3](../../../../../../code/plugins/scenariomanager/node_library/math/curves/bezier_vec3.md)
- [CatmullRom](../../../../../../code/plugins/scenariomanager/node_library/math/curves/catmullrom.md)
- [SmoothStep](../../../../../../code/plugins/scenariomanager/node_library/math/interpolation/smoothstep.md)
