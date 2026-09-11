# Unigine.LightLensFlare Class (CPP)

**Header:** #include <UnigineLights.h>


This class is used to manage billboards used for the per-light lens flares effect.

> **Notice:** The lens flare effect must be [enabled](../../../api/library/lights/class.light_cpp.md#setLensFlaresEnabled_int_void) for the light source. This feature is available only for: [Omni Lights](../../../api/library/lights/class.lightomni_cpp.md), [Projected Lights](../../../api/library/lights/class.lightproj_cpp.md) and [World Lights](../../../api/library/lights/class.lightworld_cpp.md).


### See Also


Description of [lens flare settings](../../../objects/lights/parameters/index.md#lens_flares_settings).


## LightLensFlare Class

### Members

## void setIntensity ( float intensity )

Sets a new intensity of the lens flare billboard.
### Arguments

- *float* **intensity** - The intensity of the lens flare billboard. The [color](#setColor_vec4_void) of the billboard is multiplied by this value. The higher the value, the brighter the flare will be.

## float getIntensity () const

Returns the current intensity of the lens flare billboard.
### Return value

Current intensity of the lens flare billboard. The [color](#setColor_vec4_void) of the billboard is multiplied by this value. The higher the value, the brighter the flare will be.
## void setColor ( const Math:: vec4 & color )

Sets a new color of the lens flare billboard.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **color** - The billboard color.

## Math:: vec4 getColor () const

Returns the current color of the lens flare billboard.
### Return value

Current billboard color.
## void setRotate ( bool rotate = false )

Sets a new value indicating if rotation of the lens flare billboard is enabled. when enabled the top of the billboard will always face the center of the screen.
### Arguments

- *bool* **rotate** - Set **true** to enable rotation of the lens flare billboard; **false** - to disable it.

## bool isRotate () const

Returns the current value indicating if rotation of the lens flare billboard is enabled. when enabled the top of the billboard will always face the center of the screen.
### Return value

**true** if rotation of the lens flare billboard is enabled ; otherwise **false**.
## void setUVUpperRight ( const Math:: vec2 & right )

Sets a new UV [texture](../../../api/library/lights/class.light_cpp.md#setLensFlaresTextureName_cstr_void) coordinates of the the upper right corner of the lens flare billboard.
### Arguments

- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md)&* **right** - The UV [texture](../../../api/library/lights/class.light_cpp.md#setLensFlaresTextureName_cstr_void) coordinates of the the upper right corner of the lens flare billboard.

## Math:: vec2 getUVUpperRight () const

Returns the current UV [texture](../../../api/library/lights/class.light_cpp.md#setLensFlaresTextureName_cstr_void) coordinates of the the upper right corner of the lens flare billboard.
### Return value

Current UV [texture](../../../api/library/lights/class.light_cpp.md#setLensFlaresTextureName_cstr_void) coordinates of the the upper right corner of the lens flare billboard.
## void setUVLowerLeft ( const Math:: vec2 & left )

Sets a new UV [texture](../../../api/library/lights/class.light_cpp.md#setLensFlaresTextureName_cstr_void) coordinates of the lower left corner of the lens flare billboard.
### Arguments

- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md)&* **left** - The UV [texture](../../../api/library/lights/class.light_cpp.md#setLensFlaresTextureName_cstr_void) coordinates of the lower left corner of the lens flare billboard.

## Math:: vec2 getUVLowerLeft () const

Returns the current UV [texture](../../../api/library/lights/class.light_cpp.md#setLensFlaresTextureName_cstr_void) coordinates of the lower left corner of the lens flare billboard.
### Return value

Current UV [texture](../../../api/library/lights/class.light_cpp.md#setLensFlaresTextureName_cstr_void) coordinates of the lower left corner of the lens flare billboard.
## void setOffsetScale ( float scale )

Sets a new [offset](#setOffset_float_void)-dependent scale factor for the lens flare billboard.
### Arguments

- *float* **scale** - The scale factor. As the [offset](#setOffset_float_void) from the light source increases:

  - values **less** than 1.0f will make the billboard shrink.
  - values **greater** than 1.0f will make the billboard grow.

## float getOffsetScale () const

Returns the current [offset](#setOffset_float_void)-dependent scale factor for the lens flare billboard.
### Return value

Current scale factor. As the [offset](#setOffset_float_void) from the light source increases:
- values **less** than 1.0f will make the billboard shrink.
- values **greater** than 1.0f will make the billboard grow.


## void setOffset ( float offset )

Sets a new offset value for the lens flare billboard. This is the offset from the light source along the direction of the light ray.
### Arguments

- *float* **offset** - The billboard offset value. The lower the absolute value is, the closer to the light source the billboard will be. Negative values indicate that the distance is measured in the opposite direction.

## float getOffset () const

Returns the current offset value for the lens flare billboard. This is the offset from the light source along the direction of the light ray.
### Return value

Current billboard offset value. The lower the absolute value is, the closer to the light source the billboard will be. Negative values indicate that the distance is measured in the opposite direction.
## void setSize ( float size )

Sets a new size of the lens flare billboard.
### Arguments

- *float* **size** - The size of the lens flare billboard.

## float getSize () const

Returns the current size of the lens flare billboard.
### Return value

Current size of the lens flare billboard.
## void setName ( const char * name )

Sets a new name of the lens flare billboard.
### Arguments

- *const char ** **name** - The name of the lens flare billboard.

## const char * getName () const

Returns the current name of the lens flare billboard.
### Return value

Current name of the lens flare billboard.
