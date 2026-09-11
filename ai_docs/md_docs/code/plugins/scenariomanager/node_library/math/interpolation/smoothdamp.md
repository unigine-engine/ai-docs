# SmoothDamp


![](../../img/smoothdamp.png)

### Description

Moves **Current** a step closer to **Target**, easing in as it approaches instead of jumping there. Feeding the result back as the next frame's **Current** produces a value that chases a moving target smoothly.


**SmoothTime** sets roughly how long the approach takes, in seconds: larger values follow more slowly and lag further behind, smaller values catch up quickly.


The step is scaled by frame time, so the motion looks the same regardless of frame rate. This makes the node the usual choice for following a target that keeps changing - a camera trailing a vehicle, or a gauge easing toward a new reading - where [Lerp](../../../../../../code/plugins/scenariomanager/node_library/math/interpolation/lerp.md) would need its factor recomputed every frame.


> **Notice:** The node produces a value only while the graph is updating; on a frame with no elapsed time it passes **Current** through unchanged.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/float.png) | **Current** | The present value, normally the result of the previous frame. |
| ![](../../img/types/float.png) | **Target** | The value to approach. |
| ![](../../img/types/float.png) | **SmoothTime** | The approximate time the approach takes, in seconds. Defaults to 0.3. |
| ![](../../img/types/float.png) | **Result** | The value after this frame's step. |


## See Also


- [SmoothStep](../../../../../../code/plugins/scenariomanager/node_library/math/interpolation/smoothstep.md)
- [Lerp](../../../../../../code/plugins/scenariomanager/node_library/math/interpolation/lerp.md)
- [Delta Time](../../../../../../code/plugins/scenariomanager/node_library/time/dt.md)
