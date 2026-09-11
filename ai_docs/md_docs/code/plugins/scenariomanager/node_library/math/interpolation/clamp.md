# Clamp


![](../../img/clamp.png)

### Description

Keeps **Value** inside the range set by **Min** and **Max**: anything below the lower bound comes out as **Min**, anything above the upper bound as **Max**, and anything in between passes through unchanged.


Use it to keep a computed quantity within limits the rest of the graph can rely on - a fuel level that never reads below zero, or a speed capped at its maximum.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/float.png) | **Value** | The value to constrain. |
| ![](../../img/types/float.png) | **Min** | The lower bound. Defaults to 0. |
| ![](../../img/types/float.png) | **Max** | The upper bound. Defaults to 1. |
| ![](../../img/types/float.png) | **Result** | The constrained value. |


## See Also


- [Lerp](../../../../../../code/plugins/scenariomanager/node_library/math/interpolation/lerp.md)
- [Remap](../../../../../../code/plugins/scenariomanager/node_library/math/interpolation/remap.md)
- [SmoothStep](../../../../../../code/plugins/scenariomanager/node_library/math/interpolation/smoothstep.md)
