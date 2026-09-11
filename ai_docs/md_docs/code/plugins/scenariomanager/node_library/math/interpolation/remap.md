# Remap


![](../../img/remap.png)

### Description

Rescales **Value** from the input range set by **InMin** and **InMax** to the output range set by **OutMin** and **OutMax**, keeping its relative position within the range.


This is the combination of [Inverse Lerp](../../../../../../code/plugins/scenariomanager/node_library/math/interpolation/inverse_lerp.md) and [Lerp](../../../../../../code/plugins/scenariomanager/node_library/math/interpolation/lerp.md) in a single node, and it is the direct way to convert between units a scenario mixes - a sensor reading into a percentage, or a normalized factor into an angle.


Values outside the input range map outside the output range rather than being cut off. Swapping **OutMin** and **OutMax** reverses the direction of the mapping.


> **Notice:** When **InMin** and **InMax** are equal the input range has no width and the node outputs **OutMin**.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/float.png) | **Value** | The value to rescale. |
| ![](../../img/types/float.png) | **InMin** | The lower end of the input range. |
| ![](../../img/types/float.png) | **InMax** | The upper end of the input range. Defaults to 1. |
| ![](../../img/types/float.png) | **OutMin** | The lower end of the output range. |
| ![](../../img/types/float.png) | **OutMax** | The upper end of the output range. Defaults to 1. |
| ![](../../img/types/float.png) | **Result** | The rescaled value. |


## See Also


- [Lerp](../../../../../../code/plugins/scenariomanager/node_library/math/interpolation/lerp.md)
- [Inverse Lerp](../../../../../../code/plugins/scenariomanager/node_library/math/interpolation/inverse_lerp.md)
- [Clamp](../../../../../../code/plugins/scenariomanager/node_library/math/interpolation/clamp.md)
