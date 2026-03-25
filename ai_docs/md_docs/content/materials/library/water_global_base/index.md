# water_global_base


The *water_global_base* material simulates [water](../../../../objects/objects/water/index.md) and other liquids and is applied to the [Water Global](../../../../objects/objects/water/water_object.md) object.


[![](index.jpg)](index.jpg)


## Parameters


### Common


![](common.png)


Parameters specifying the masks for the material.


| Material Mask | The [decal](../../../../objects/decals/index.md) will be projected onto the water surface if the material mask of the decal material matches this mask. |
|---|---|
| Material Backface Mask | Material Mask for the back face of the water surface. |
| Physics Field Mask | The [field mask](../../../../principles/bit_masking/index.md#field_mask) that controls CPU-related operations with fields. For example, intersection with a wave created by Field Height can be detected, if a relevant Field Mask is enabled. |
| Visual Field Mask | The [field mask](../../../../principles/bit_masking/index.md#field_mask) that controls GPU-related (visually perceptible) effects of fields. |


### Post Processing and Post Processing (Backface)


![](post_processing.png)


**Post processing** options activate post processing effects for the material. The effects are available both for front and back faces of the water surface.


| DOF | Enables the depth of field effect. |
|---|---|
| Motion blur | Enables the motion blur effect. |
