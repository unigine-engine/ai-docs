# Surface ID Rendering Mode Node


![](../img/surface_id_rendering_mode.png)

### Description

Reports which [Surface ID Buffers](../../../../../content/materials/custom_parameters/ids_and_buffers.md#modes) the current configuration provides, so that a graph can adapt to it instead of assuming.


Only two of the four outputs actually vary: they follow the *Multilayered* setting. The other two are constants.


The answer is about the configuration, not about the frame: a buffer that exists but received nothing reads as empty at every pixel, exactly like a buffer that does not exist at all. The per-pixel check is **isValidSurfaceParameters()**.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/bool.png) | **Transparent Buffer Available** | Transparent geometry has a buffer of its own, which happens while *Multilayered* is enabled. |
| ![](../img/types/bool.png) | **Decal Buffer Available** | Always true: a decal reads and writes the Surface ID in the same pass, so it gets a target of its own in either mode. |
| ![](../img/types/bool.png) | **Water Buffer Available** | Water has a buffer of its own, which happens while *Multilayered* is enabled. |
| ![](../img/types/bool.png) | **Scene Buffer Available** | Always true: the composed Scene Buffer exists in either mode. |
