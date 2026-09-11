# SmoothStep


![](../../img/smoothstep.png)

### Description

Produces a gradual transition from 0 to 1 as **X** moves from **Edge0** to **Edge1**. The curve leaves and arrives flat, so the change starts and ends gently instead of abruptly.


Unlike [Lerp](../../../../../../code/plugins/scenariomanager/node_library/math/interpolation/lerp.md), the result is held within 0 to 1: below the first edge it stays 0 and above the second it stays 1.


This shaping is what makes a fade or a camera move read as natural rather than mechanical - feed the result to a Lerp as its blend factor.


> **Notice:** When both edges are equal the node outputs 0.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/float.png) | **Edge0** | The value of **X** at which the transition begins. |
| ![](../../img/types/float.png) | **Edge1** | The value of **X** at which the transition completes. Defaults to 1. |
| ![](../../img/types/float.png) | **X** | The value to evaluate. |
| ![](../../img/types/float.png) | **Result** | The smoothed factor, between 0 and 1. |


## See Also


- [Lerp](../../../../../../code/plugins/scenariomanager/node_library/math/interpolation/lerp.md)
- [SmoothDamp](../../../../../../code/plugins/scenariomanager/node_library/math/interpolation/smoothdamp.md)
- [Clamp](../../../../../../code/plugins/scenariomanager/node_library/math/interpolation/clamp.md)
