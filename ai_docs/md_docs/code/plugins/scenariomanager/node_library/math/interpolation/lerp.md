# Lerp


![](../../img/lerp.png)

### Description

Blends between **A** and **B** by the factor **T**, so that 0 gives **A**, 1 gives **B**, and 0.5 gives the midpoint.


The factor is not restricted to the 0 to 1 range - values outside it continue the line past either end, which is useful for extrapolating a trend but will overshoot if that is not intended. Feed the factor through [Clamp](../../../../../../code/plugins/scenariomanager/node_library/math/interpolation/clamp.md) to rule that out.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/float.png) | **A** | The value returned when **T** is 0. |
| ![](../../img/types/float.png) | **B** | The value returned when **T** is 1. Defaults to 1. |
| ![](../../img/types/float.png) | **T** | The blend factor. |
| ![](../../img/types/float.png) | **Result** | The blended value. |


## See Also


- [Inverse Lerp](../../../../../../code/plugins/scenariomanager/node_library/math/interpolation/inverse_lerp.md)
- [Remap](../../../../../../code/plugins/scenariomanager/node_library/math/interpolation/remap.md)
- [SmoothStep](../../../../../../code/plugins/scenariomanager/node_library/math/interpolation/smoothstep.md)
