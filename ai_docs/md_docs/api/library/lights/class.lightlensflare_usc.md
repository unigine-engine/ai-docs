# Unigine.LightLensFlare Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is used to manage billboards used for the per-light lens flares effect.

> **Notice:** The lens flare effect must be [enabled](../../../api/library/lights/class.light_usc.md#setLensFlaresEnabled_int_void) for the light source. This feature is available only for: [Omni Lights](../../../api/library/lights/class.lightomni_usc.md), [Projected Lights](../../../api/library/lights/class.lightproj_usc.md) and [World Lights](../../../api/library/lights/class.lightworld_usc.md).


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
## void setColor ( vec4 color )

Sets a new color of the lens flare billboard.
### Arguments

- *vec4* **color** - The billboard color.

## vec4 getColor () const

Returns the current color of the lens flare billboard.
### Return value

Current billboard color.
## void setRotate ( int rotate = false )

Sets a new value indicating if rotation of the lens flare billboard is enabled. when enabled the top of the billboard will always face the center of the screen.
### Arguments

- *int* **rotate** - The rotation of the lens flare billboard

## int isRotate () const

Returns the current value indicating if rotation of the lens flare billboard is enabled. when enabled the top of the billboard will always face the center of the screen.
### Return value

Current rotation of the lens flare billboard
## void setUVUpperRight ( vec2 right )

Sets a new UV [texture](../../../api/library/lights/class.light_usc.md#setLensFlaresTextureName_cstr_void) coordinates of the the upper right corner of the lens flare billboard.
### Arguments

- *vec2* **right** - The UV [texture](../../../api/library/lights/class.light_usc.md#setLensFlaresTextureName_cstr_void) coordinates of the the upper right corner of the lens flare billboard.

## vec2 getUVUpperRight () const

Returns the current UV [texture](../../../api/library/lights/class.light_usc.md#setLensFlaresTextureName_cstr_void) coordinates of the the upper right corner of the lens flare billboard.
### Return value

Current UV [texture](../../../api/library/lights/class.light_usc.md#setLensFlaresTextureName_cstr_void) coordinates of the the upper right corner of the lens flare billboard.
## void setUVLowerLeft ( vec2 left )

Sets a new UV [texture](../../../api/library/lights/class.light_usc.md#setLensFlaresTextureName_cstr_void) coordinates of the lower left corner of the lens flare billboard.
### Arguments

- *vec2* **left** - The UV [texture](../../../api/library/lights/class.light_usc.md#setLensFlaresTextureName_cstr_void) coordinates of the lower left corner of the lens flare billboard.

## vec2 getUVLowerLeft () const

Returns the current UV [texture](../../../api/library/lights/class.light_usc.md#setLensFlaresTextureName_cstr_void) coordinates of the lower left corner of the lens flare billboard.
### Return value

Current UV [texture](../../../api/library/lights/class.light_usc.md#setLensFlaresTextureName_cstr_void) coordinates of the lower left corner of the lens flare billboard.
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
## void setName ( string name )

Sets a new name of the lens flare billboard.
### Arguments

- *string* **name** - The name of the lens flare billboard.

## const char * getName () const

Returns the current name of the lens flare billboard.
### Return value

Current name of the lens flare billboard.
