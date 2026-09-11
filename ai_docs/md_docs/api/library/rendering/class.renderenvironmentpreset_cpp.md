# Unigine.RenderEnvironmentPreset Class (CPP)

**Header:** #include <UnigineRender.h>


The class represents an [environment preset](../../../editor2/settings/render_settings/environment/index.md#presets). Each preset has settings that can be get/set by using methods of the class.


To get an instance of the class, use the *[Render::getEnvironmentPreset()](../../../api/library/rendering/class.render_cpp.md#getEnvironmentPreset_int_RenderEnvironmentPreset)* method:


```cpp
// get the second environment preset
RenderEnvironmentPresetPtr preset = Render::getEnvironmentPreset(1);

```


## RenderEnvironmentPreset Class

### Members

---

## int getNum ( ) const

Returns the number of the preset.
### Return value

Preset number. Available values: **0**, **1**, **2**.
## void setIntensity ( float intensity )


Sets the intensity of the given preset. The preset intensity is used to blend the given environment preset with the other ones.


> **Notice:** Presets overlay each other: the first preset overlays the zero one, the second overlays the first and the zero ones.


### Arguments

- *float* **intensity** - Intensity of the preset.

## float getIntensity ( ) const


Returns the intensity of the preset. The preset intensity is used to blend the environment preset with the other ones.


> **Notice:** Presets overlay each other: the first preset overlays the zero one, the second overlays the first and the zero ones.


### Return value

Intensity of the preset.
## void setScatteringMieLUTName ( const char * name )

Sets the path to the [Mie LUT texture](../../../editor2/settings/render_settings/environment/index.md#mie_lut) (the texture for setting the color of the light round the sun) for the preset. The Mie texture is used for both sun and moon.
### Arguments

- *const char ** **name** - Path to the texture.

## const char * getScatteringMieLUTName ( ) const

Returns the path to the [Mie LUT texture](../../../editor2/settings/render_settings/environment/index.md#mie_lut) (the texture for setting the color of the light round the sun) set for the preset. The Mie texture is used for both sun and moon.
### Return value

Path to the texture.
## void setScatteringLightColorLUTName ( const char * name )

Sets the path to the [light color texture](../../../editor2/settings/render_settings/environment/index.md#light_lut) (the texture defining the color of the LightWorld for different times of the day) for the preset.
### Arguments

- *const char ** **name** - Path to the texture.

## const char * getScatteringLightColorLUTName ( ) const

Returns the path to the [light color texture](../../../editor2/settings/render_settings/environment/index.md#light_lut) (the texture defining the color of the LightWorld for different times of the day).
### Return value

Path to the texture.
## void setScatteringBaseLUTName ( const char * name )

Sets the path to the [base LUT texture](../../../editor2/settings/render_settings/environment/index.md#base_lut) (the texture defining the base color of the sky) for the preset.
### Arguments

- *const char ** **name** - Path to the texture.

## const char * getScatteringBaseLUTName ( ) const

Returns the path to the [base LUT texture](../../../editor2/settings/render_settings/environment/index.md#base_lut) (the texture defining the base color of the sky) set for the preset.
### Return value

Path to the texture.
## void setHazeMaxDistance ( float distance )

Sets the [distance](../../../editor2/settings/render_settings/environment/index.md#haze_max_distance) starting at which the haze becomes completely solid, so nothing will be seen behind. For large terrains it is recommended to the this parameter equal to your camera's [Far](../../../api/library/rendering/class.camera_cpp.md#getZFar_float) parameter. This is required for distant objects to fade into the distance instead of being cut sharply.
### Arguments

- *float* **distance** - Haze maximum visibility distance.

## float getHazeMaxDistance ( ) const

Returns the distance starting at which the haze becomes completely solid, so nothing will be seen behind.
### Return value

Haze maximum visibility distance.
## void setHazeColor ( const Math:: vec4 & color )

Sets the [color of the haze](../../../editor2/settings/render_settings/environment/index.md#haze_color) for the preset. This function will take effect only if the *[HAZE_SOLID](../../../api/library/rendering/class.render_cpp.md#HAZE_SOLID)* mode is set via *[setEnvironmentHazeMode()](../../../api/library/rendering/class.render_cpp.md#setEnvironmentHazeMode_int_void)*.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Haze color.

## Math:: vec4 getHazeColor ( ) const


Returns the [haze color](../../../editor2/settings/render_settings/environment/index.md#haze_color) for the preset.


> **Notice:** This function will return color only if the [HAZE_SOLID](../../../api/library/rendering/class.render_cpp.md#HAZE_SOLID) mode is set via *[setEnvironmentHazeMode()](../../../api/library/rendering/class.render_cpp.md#setEnvironmentHazeMode_int_void)*.


### Return value

Haze color.
## void setHazeDensity ( float density )

Sets the [density of the haze](../../../editor2/settings/render_settings/environment/index.md#haze_density) for the preset.
### Arguments

- *float* **density** - Haze density.

## float getHazeDensity ( ) const

Returns the [haze density](../../../editor2/settings/render_settings/environment/index.md#haze_density) set for the preset.
### Return value

Haze density.
## void setReflectionIntensity ( float intensity )


Sets intensity of the environment reflection for the preset. **0** value means no environment reflection for the preset.


> **Notice:** It is recommended to use the default value of the parameter to keep the image realistic.


### Arguments

- *float* **intensity** - Intensity value of the environment reflection.

## float getReflectionIntensity ( ) const

Returns the intensity of the environment reflections for the preset. **0** value means no environment reflections for the preset.
### Return value

The intensity value of the environment reflections.
## void setSkyIntensity ( float intensity )


Sets intensity of the environment sky for the preset. **0.0f** value means no environment sky for the preset.


> **Notice:** It is recommended to use the default value of the parameter to keep the image realistic. If, for example, the sky looks too dark in contrast with lighting from it, you should check exposure and tone mapping settings before changing the environment intensity.


### Arguments

- *float* **intensity** - Intensity value of the environment sky.

## float getSkyIntensity ( ) const

Returns the intensity of the environment sky set for the preset.
### Return value

Intensity value of the environment sky.
## void setAmbientIntensity ( float intensity )


Sets the intensity of the environment ambient lighting for the preset. **0** value means no environment ambient lighting for the preset. The higher the value, the more ambient lighting affects environment.


> **Notice:** It is recommended to use the default value of the parameter to keep the image realistic.


### Arguments

- *float* **intensity** - Intensity value of the environment ambient lighting. The value can be greater than 1.0f (useful for dark scenes).

## float getAmbientIntensity ( ) const

Returns the intensity of the environment ambient lighting for the preset. **0** value means no environment ambient lighting for the preset. The higher the value, the more ambient lighting affects environment.
### Return value

The intensity value of environment ambient lighting. The value can be greater than 1.0f.
## void setTexture ( const Ptr < Texture > & texture )

Sets the [cubemap defining the environment color](../../../editor2/settings/render_settings/environment/index.md#env_texture) for the preset. This texture is used for imitating landscape reflections and lighting in accordance with the ground mask.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Texture](../../../api/library/rendering/class.texture_cpp.md)> &* **texture** - Cubemap defining the environment color.

## Ptr < Texture > getTexture ( ) const

Returns the [cubemap defining the environment color](../../../editor2/settings/render_settings/environment/index.md#env_texture) set for the preset. This texture is used for imitating landscape reflections and lighting in accordance with the ground mask.
### Return value

Cubemap defining the environment color.
## void setTextureName ( const char * name )

Sets the path to the [cubemap defining the environment color](../../../editor2/settings/render_settings/environment/index.md#env_texture) for the preset. This texture is used for imitating landscape reflections and lighting in accordance with the ground mask.
### Arguments

- *const char ** **name** - Path to the cubemap defining the environment color.

## const char * getTextureName ( ) const

Returns the path to the [cubemap defining the environment color](../../../editor2/settings/render_settings/environment/index.md#env_texture) set for the preset. This texture is used for imitating landscape reflections and lighting in accordance with the ground mask.
### Return value

Path to the cubemap defining the environment color.
## void setTextureColor ( const Math:: vec4 & color )

Sets the [environment color multiplier](../../../editor2/settings/render_settings/environment/index.md#env_texture_color) for the preset. The alpha channel defines visibility of the environment cubemap above scattering. The color multiplier is required when you need to display a sky with a photo texture and dynamic gradients at the same time.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - The environment color multiplier.

## Math:: vec4 getTextureColor ( ) const

Returns the [environment color multiplier](../../../editor2/settings/render_settings/environment/index.md#env_texture_color) set for the preset. The alpha channel defines visibility of the environment cubemap above scattering. The color multiplier is required when you need to display a sky with a photo texture and dynamic gradients at the same time.
### Return value

The environment color multiplier.
## void setTextureRotation ( const Math:: vec3 & rotation )

Sets rotation of the environment texture along three axes.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **rotation** - Rotation of the texture along X, Y, Z axes, in degrees.

## Math:: vec3 getTextureRotation ( ) const

Returns rotation of the environment texture along three axes, in degrees.
### Return value

Rotation of the texture along X, Y, Z axes, in degrees.
## void setTextureBlur ( float blur )


Sets the blur intensity for the environment texture. This value can be used to make blurred panorama at the background.


> **Notice:** Reflections and ambient lighting aren't blurred.


### Arguments

- *float* **blur** - Blur intensity.

## float getTextureBlur ( ) const


Returns the blur intensity for the environment texture.


> **Notice:** Reflections and ambient lighting aren't blurred.


### Return value

Blur intensity.
## float getMoonTextureIntensity ( ) const

Returns the [intensity multiplier](../../../editor2/settings/render_settings/environment/index.md#moon_intensity) of the Moon texture. It allows increasing/reducing brightness of the Moon.
### Return value

Intensity of the Moon texture.
## void setMoonTextureIntensity ( float intensity )

Sets the [intensity multiplier](../../../editor2/settings/render_settings/environment/index.md#moon_intensity) of the Moon texture. It allows increasing/reducing brightness of the Moon.
### Arguments

- *float* **intensity** - Intensity of the Moon texture.

## void setSunTextureColor ( const Math:: vec4 & color )

Sets the [color multiplier](../../../editor2/settings/render_settings/environment/index.md#sun_color) for the current Sun texture. By default, it is (1,1,1,1).
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color multiplier.

## float getMoonAngularSize ( ) const

Returns the current [angular size](../../../editor2/settings/render_settings/environment/index.md#moon_size) of the Moon in degrees as seen from the Earth. By default, the size of the Moon is 0.5 degrees.
### Return value

Angular size of the Moon.
## float getSunTextureIntensity ( ) const

Returns the [intensity multiplier](../../../editor2/settings/render_settings/environment/index.md#sun_intensity) of the Sun texture. It allows increasing/reducing brightness of the Sun.
### Return value

Intensity of the sun texture.
## Math:: vec4 getMoonTextureColor ( ) const

Returns the [color multiplier](../../../editor2/settings/render_settings/environment/index.md#moon_color) of the Moon texture.
### Return value

Color multiplier.
## void setSunTextureName ( const char * name )

Sets the [Sun texture](../../../editor2/settings/render_settings/environment/index.md#sun) with the given name.
### Arguments

- *const char ** **name** - Name of the Sun texture.

## void setMoonTextureColor ( const Math:: vec4 & color )

Sets the [color multiplier](../../../editor2/settings/render_settings/environment/index.md#moon_color) for the current Moon texture. By default, it is (1,1,1,1).
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color multiplier.

## void setSunTextureIntensity ( float intensity )

Sets the [intensity multiplier](../../../editor2/settings/render_settings/environment/index.md#sun_intensity) of the Sun texture. It allows increasing/reducing brightness of the Sun.
### Arguments

- *float* **intensity** - Intensity of the Sun texture.

## void setMoonAngularSize ( float size )

Sets the [angular size](../../../editor2/settings/render_settings/environment/index.md#moon_size) of the Moon in degrees. The value is set for an observer on the Earth. By default, the size of the Moon is 0.5 degrees as seen from the Earth..
### Arguments

- *float* **size** - Angular size of the Moon.

## Math:: vec4 getSunTextureColor ( ) const

Returns the [color multiplier](../../../editor2/settings/render_settings/environment/index.md#sun_color) of the Sun texture. By default, it is (1,1,1,1).
### Return value

Color multiplier.
## void setMoonTextureName ( const char * name )

Sets a name of the [Moon texture](../../../editor2/settings/render_settings/environment/index.md#moon).
### Arguments

- *const char ** **name** - Name of the Moon texture.

## void setSunAngularSize ( float size )

Sets the [angular size](../../../editor2/settings/render_settings/environment/index.md#sun_size) of the Sun in degrees. The value is set for an observer on the Earth. By default, the size of the Sun is 0.5 degrees as seen from the Earth.
### Arguments

- *float* **size** - Angular size of the Sun.

## float getSunAngularSize ( ) const

Returns the [angular size](../../../editor2/settings/render_settings/environment/index.md#sun_size) of the Sun in degrees as seen from the Earth. By default, the size of the Sun is 0.5 degrees.
### Return value

Angular size of the Sun.
## const char * getSunTextureName ( ) const

Returns the name of the [Sun texture](../../../editor2/settings/render_settings/environment/index.md#sun).
### Return value

Name of the Sun texture.
## const char * getMoonTextureName ( ) const

Returns the name of the [Moon texture](../../../editor2/settings/render_settings/environment/index.md#moon).
### Return value

Name of the Moon texure.
## void setHazePhysicalStartHeight ( float height )

Sets a new reference height value for the two parameters ([Half Visibility Distance](#setHazePhysicalHalfVisibilityDistance_float_void) and [Half Faloff Height](#setHazePhysicalHalfFalloffHeight_float_void)).
### Arguments

- *float* **height** - New reference height value to be set, in units.

## float getHazePhysicalStartHeight ( ) const

Returns the current reference height value for the two parameters ([Half Visibility Distance](#setHazePhysicalHalfVisibilityDistance_float_void) and [Half Faloff Height](#setHazePhysicalHalfFalloffHeight_float_void)).
### Return value

Current reference height value, in units.
## void setHazePhysicalHalfVisibilityDistance ( float distance )

Sets the distance to the boundary at which the visibility comprises 50%. There is no zero-visibility in the real world, so the half-visibility boundary is used to adjust haze distance.
### Arguments

- *float* **distance** - New distance value to be set, in units.

## float getHazePhysicalHalfVisibilityDistance ( ) const

Returns the current distance to the boundary at which the visibility comprises 50%. There is no zero-visibility in the real world, so the half-visibility boundary is used to adjust haze distance.
### Return value

Current distance to the boundary at which the visibility comprises 50%, in units.
## void setHazePhysicalHalfFalloffHeight ( float height )

Sets the height of the haze density gradient. The *higher* the value, the *longer* the haze desity reduces as the height grows, making the transition between the clear sky and haze smoother.
### Arguments

- *float* **height** - New height of the haze density gradient to be set.

## float getHazePhysicalHalfFalloffHeight ( ) const

Returns the current height of the haze density gradient. The *higher* the value, the *longer* the haze desity reduces as the height grows, making the transition between the clear sky and haze smoother.
### Return value

Current height of the haze density gradient.
## void setHazePhysicalAmbientLightIntensity ( float intensity )

Sets the new intensity of the impact of the ambient lighting on haze (how much the ambient lighting affects the haze).
### Arguments

- *float* **intensity** - New value of intensity of the ambient lighting impact to be set.

## float getHazePhysicalAmbientLightIntensity ( ) const

Returns the current intensity of the impact of the ambient lighting on haze (how much the ambient lighting affects the haze).
### Return value

Current value of intensity of the ambient lighting impact.
## void setHazePhysicalAmbientColorSaturation ( float saturation )

Sets the new intensity of the ambient color's contribution to the haze (how much the sunlight affects the haze).
### Arguments

- *float* **saturation** - New value of intensity of the ambient color's contribution to the haze to be set.

## float getHazePhysicalAmbientColorSaturation ( ) const

Returns the current intensity of the ambient color's contribution to the haze (how much the sunlight affects the haze).
### Return value

Current value of intensity of the ambient color's contribution to the haze.
## void setHazePhysicalSunLightIntensity ( float intensity )

Sets the new intensity of the impact of the sunlight on haze (how much the sunlight affects the haze).
### Arguments

- *float* **intensity** - New value of intensity of the sunlight impact to be set.

## float getHazePhysicalSunLightIntensity ( ) const

Returns the current intensity of the impact of the sunlight on haze defining how much the sunlight affects the haze.
### Return value

Current value of intensity of the sunlight impact.
## void setHazePhysicalSunColorSaturation ( float saturation )


Sets the new intensity of the impact of the sunlight on haze (how much the sunlight affects the haze).


> **Notice:** "Sunlight color" here does not simply mean the color multiplier of the [*WorldLight*](../../../api/library/lights/class.lightworld_cpp.md) source, but rather the [*Scattering LUT Light Color*](#setScatteringLightColorLUTName_cstr_void).


### Arguments

- *float* **saturation** - New value of intensity of the sunlight color's contribution to the haze to be set.

## float getHazePhysicalSunColorSaturation ( ) const

Returns the current intensity of the impact of the sunlight on haze (how much the sunlight affects the haze).
### Return value

Current intensity of the sunlight color's contribution to the haze.
## void setHazeScatteringMieIntensity ( float intensity )

Sets the minimum Mie intensity value for geometry-occluded areas. This value specifies the fraction of Mie intensity visible when the surface is viewed from straight on. Setting this value to 1 disables the Fresnel effect. You can use this parameter together with *Mie Frontside Intensity**[setHazeScatteringMieFrontSideIntensity](../../...md#setHazeScatteringMieFrontSideIntensity_float_void)* and *Mie Fresnel Power**[setHazeScatteringMieFresnelPower](../../...md#setHazeScatteringMieFresnelPower_float_void)* to control light occlusion from *World* light sources. Works for both, opaque and transparent objects.
### Arguments

- *float* **intensity** - New minimum Mie intensity value for geometry-occluded areas to be set in the [0.0f, 1.0f] range.

## float getHazeScatteringMieIntensity ( ) const

Returns the current minimum Mie intensity value for geometry-occluded areas. This value specifies the fraction of Mie intensity visible when the surface is viewed from straight on. Setting this value to 1 disables the Fresnel effect. You can use this parameter together with *Mie Frontside Intensity**[setHazeScatteringMieFrontSideIntensity](../../...md#setHazeScatteringMieFrontSideIntensity_float_void)* and *Mie Fresnel Power**[setHazeScatteringMieFresnelPower](../../...md#setHazeScatteringMieFresnelPower_float_void)* to control light occlusion from *World* light sources. Works for both, opaque and transparent objects.
### Return value

Current minimum Mie intensity value for geometry-occluded areas in the [0.0f, 1.0f] range.
## void setHazeScatteringMieFrontSideIntensity ( float intensity )

Sets the falloff of the Fresnel effect for Mie intensity. This value is used to control occlusion of light from a World light source by the geometry.
### Arguments

- *float* **intensity** - Falloff of the Fresnel effect for Mie intensity.

## float getHazeScatteringMieFrontSideIntensity ( ) const

Returns the falloff of the Fresnel effect for Mie intensity. This value is used to control occlusion of light from a World light source by the geometry.
### Return value

Falloff of the Fresnel effect for Mie intensity.
## void setHazeScatteringMieFresnelPower ( float power )

Sets the power of the Fresnel effect for Mie visibility. *Higher* values will tighten up the areas affected, while *lower* ones will allow more areas to be affected by the Fresnel effect.
### Arguments

- *float* **power** - New power of the Fresnel effect to be set.

## float getHazeScatteringMieFresnelPower ( ) const

Returns the current power of the Fresnel effect for Mie visibility. *Higher* values will tighten up the areas affected, while *lower* ones will allow more areas to be affected by the Fresnel effect.
### Return value

Current power of the Fresnel effect.
