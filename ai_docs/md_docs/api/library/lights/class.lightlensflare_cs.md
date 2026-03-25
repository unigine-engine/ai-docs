# Unigine.LightLensFlare Class (CS)


This class is used to manage billboards used for the per-light lens flares effect.

> **Notice:** The lens flare effect must be [enabled](../../../api/library/lights/class.light_cs.md#setLensFlaresEnabled_int_void) for the light source. This feature is available only for: [Omni Lights](../../../api/library/lights/class.lightomni_cs.md), [Projected Lights](../../../api/library/lights/class.lightproj_cs.md) and [World Lights](../../../api/library/lights/class.lightworld_cs.md).


### See Also


Description of [lens flare settings](../../../objects/lights/parameters/index.md#lens_flares_settings).


## LightLensFlare Class

### Properties

## float Intensity

The intensity of the lens flare billboard.
## vec4 Color

The color of the lens flare billboard.
## bool Rotate

The value indicating if rotation of the lens flare billboard is enabled. when enabled the top of the billboard will always face the center of the screen.
## vec2 UVUpperRight

The UV [texture](../../../api/library/lights/class.light_cs.md#setLensFlaresTextureName_cstr_void) coordinates of the the upper right corner of the lens flare billboard.
## vec2 UVLowerLeft

The UV [texture](../../../api/library/lights/class.light_cs.md#setLensFlaresTextureName_cstr_void) coordinates of the lower left corner of the lens flare billboard.
## float OffsetScale

The [offset](#setOffset_float_void)-dependent scale factor for the lens flare billboard.
## float Offset

The offset value for the lens flare billboard. This is the offset from the light source along the direction of the light ray.
## float Size

The size of the lens flare billboard.
## string Name

The name of the lens flare billboard.
