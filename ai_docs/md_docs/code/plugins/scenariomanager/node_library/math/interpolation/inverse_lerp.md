# Inverse Lerp


![](../../img/inverse_lerp.png)

### Description

Reports where **Value** falls between **A** and **B**, as a factor that reads 0 at **A** and 1 at **B**. This is the reverse of [Lerp](../../../../../../code/plugins/scenariomanager/node_library/math/interpolation/lerp.md): it recovers the blend factor rather than applying one.


Turning a measured quantity into such a factor is the usual way to drive a progress bar or feed another interpolation - a tank level between empty and full becomes the fraction filled.


A value outside the range yields a factor outside 0 to 1 rather than being cut off.


> **Notice:** When **A** and **B** are equal the range has no width and the node outputs 0.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/float.png) | **A** | The value that corresponds to a factor of 0. |
| ![](../../img/types/float.png) | **B** | The value that corresponds to a factor of 1. Defaults to 1. |
| ![](../../img/types/float.png) | **Value** | The value to locate within the range. |
| ![](../../img/types/float.png) | **T** | The resulting factor. |


## See Also


- [Lerp](../../../../../../code/plugins/scenariomanager/node_library/math/interpolation/lerp.md)
- [Remap](../../../../../../code/plugins/scenariomanager/node_library/math/interpolation/remap.md)
- [Clamp](../../../../../../code/plugins/scenariomanager/node_library/math/interpolation/clamp.md)
