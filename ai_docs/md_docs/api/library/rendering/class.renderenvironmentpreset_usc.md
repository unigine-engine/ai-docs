# Unigine.RenderEnvironmentPreset Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


The class represents an [environment preset](../../../editor2/settings/render_settings/environment/index.md#presets). Each preset has settings that can be get/set by using methods of the class.


To get an instance of the class, use the *[engine.render.getEnvironmentPreset()](../../../api/library/rendering/class.render_usc.md#getEnvironmentPreset_int_RenderEnvironmentPreset)* function:


```cpp
// get the second environment preset
RenderEnvironmentPreset preset = engine.render.getEnvironmentPreset(1);

```


## RenderEnvironmentPreset Class

### Members

---

## int getNum ( )

Returns the number of the preset.
### Return value

Preset number. Available values: **0**, **1**, **2**.
## void setIntensity ( float intensity )


Sets the intensity of the given preset. The preset intensity is used to blend the given environment preset with the other ones.


> **Notice:** Presets overlay each other: the first preset overlays the zero one, the second overlays the first and the zero ones.


### Arguments

- *float* **intensity** - Intensity of the preset.

## float getIntensity ( )


Returns the intensity of the preset. The preset intensity is used to blend the environment preset with the other ones.


> **Notice:** Presets overlay each other: the first preset overlays the zero one, the second overlays the first and the zero ones.


### Return value

Intensity of the preset.
## void setScatteringMieLUTName ( string name )

Sets the path to the [Mie LUT texture](../../../editor2/settings/render_settings/environment/index.md#mie_lut) (the texture for setting the color of the light round the sun) for the preset. The Mie texture is used for both sun and moon.
### Arguments

- *string* **name** - Path to the texture.

## string getScatteringMieLUTName ( )

Returns the path to the [Mie LUT texture](../../../editor2/settings/render_settings/environment/index.md#mie_lut) (the texture for setting the color of the light round the sun) set for the preset. The Mie texture is used for both sun and moon.
### Return value

Path to the texture.
## void setScatteringLightColorLUTName ( string name )

Sets the path to the [light color texture](../../../editor2/settings/render_settings/environment/index.md#light_lut) (the texture defining the color of the LightWorld for different times of the day) for the preset.
### Arguments

- *string* **name** - Path to the texture.

## string getScatteringLightColorLUTName ( )

Returns the path to the [light color texture](../../../editor2/settings/render_settings/environment/index.md#light_lut) (the texture defining the color of the LightWorld for different times of the day).
### Return value

Path to the texture.
## void setScatteringBaseLUTName ( string name )

Sets the path to the [base LUT texture](../../../editor2/settings/render_settings/environment/index.md#base_lut) (the texture defining the base color of the sky) for the preset.
### Arguments

- *string* **name** - Path to the texture.

## string getScatteringBaseLUTName ( )

Returns the path to the [base LUT texture](../../../editor2/settings/render_settings/environment/index.md#base_lut) (the texture defining the base color of the sky) set for the preset.
### Return value

Path to the texture.
## void setHazeMaxDistance ( float distance )

Sets the [distance](../../../editor2/settings/render_settings/environment/index.md#haze_max_distance) starting at which the haze becomes completely solid, so nothing will be seen behind. For large terrains it is recommended to the this parameter equal to your camera's [Far](../../../api/library/rendering/class.camera_usc.md#getZFar_float) parameter. This is required for distant objects to fade into the distance instead of being cut sharply.
### Arguments

- *float* **distance** - Haze maximum visibility distance.

## float getHazeMaxDistance ( )

Returns the distance starting at which the haze becomes completely solid, so nothing will be seen behind.
### Return value

Haze maximum visibility distance.
## void setHazeColor ( vec4 color )

Sets the [color of the haze](../../../editor2/settings/render_settings/environment/index.md#haze_color) for the preset. This function will take effect only if the *[HAZE_SOLID](../../../api/library/rendering/class.render_usc.md#HAZE_SOLID)* mode is set via *[setEnvironmentHazeMode()](../../../api/library/rendering/class.render_usc.md#setEnvironmentHazeMode_int_void)*.
### Arguments

- *vec4* **color** - Haze color.

## vec4 getHazeColor ( )


Returns the [haze color](../../../editor2/settings/render_settings/environment/index.md#haze_color) for the preset.


> **Notice:** This function will return color only if the [RENDER_HAZE_SOLID](../../../api/library/rendering/class.render_usc.md#HAZE_SOLID) mode is set via *[setEnvironmentHazeMode()](../../../api/library/rendering/class.render_usc.md#setEnvironmentHazeMode_int_void)*.


### Return value

Haze color.
## void setHazeDensity ( float density )

Sets the [density of the haze](../../../editor2/settings/render_settings/environment/index.md#haze_density) for the preset.
### Arguments

- *float* **density** - Haze density.

## float getHazeDensity ( )

Returns the [haze density](../../../editor2/settings/render_settings/environment/index.md#haze_density) set for the preset.
### Return value

Haze density.
## void setReflectionIntensity ( float intensity )


Sets intensity of the environment reflection for the preset. **0** value means no environment reflection for the preset.


> **Notice:** It is recommended to use the default value of the parameter to keep the image realistic.


### Arguments

- *float* **intensity** - Intensity value of the environment reflection.

## float getReflectionIntensity ( )

Returns the intensity of the environment reflections for the preset. **0** value means no environment reflections for the preset.
### Return value

The intensity value of the environment reflections.
## void setSkyIntensity ( float intensity )


Sets intensity of the environment sky for the preset. **0.0f** value means no environment sky for the preset.


> **Notice:** It is recommended to use the default value of the parameter to keep the image realistic. If, for example, the sky looks too dark in contrast with lighting from it, you should check exposure and tone mapping settings before changing the environment intensity.


### Arguments

- *float* **intensity** - Intensity value of the environment sky.

## float getSkyIntensity ( )

Returns the intensity of the environment sky set for the preset.
### Return value

Intensity value of the environment sky.
## void setAmbientIntensity ( float intensity )


Sets the intensity of the environment ambient lighting for the preset. **0** value means no environment ambient lighting for the preset. The higher the value, the more ambient lighting affects environment.


> **Notice:** It is recommended to use the default value of the parameter to keep the image realistic.


### Arguments

- *float* **intensity** - Intensity value of the environment ambient lighting. The value can be greater than 1.0f (useful for dark scenes).

## float getAmbientIntensity ( )

Returns the intensity of the environment ambient lighting for the preset. **0** value means no environment ambient lighting for the preset. The higher the value, the more ambient lighting affects environment.
### Return value

The intensity value of environment ambient lighting. The value can be greater than 1.0f.
## void setTexture ( Texture texture )

Sets the [cubemap defining the environment color](../../../editor2/settings/render_settings/environment/index.md#env_texture) for the preset. This texture is used for imitating landscape reflections and lighting in accordance with the ground mask.
### Arguments

- *[Texture](../../../api/library/rendering/class.texture_usc.md)* **texture** - Cubemap defining the environment color.

## Texture getTexture ( )

Returns the [cubemap defining the environment color](../../../editor2/settings/render_settings/environment/index.md#env_texture) set for the preset. This texture is used for imitating landscape reflections and lighting in accordance with the ground mask.
### Return value

Cubemap defining the environment color.
## void setTextureName ( string name )

Sets the path to the [cubemap defining the environment color](../../../editor2/settings/render_settings/environment/index.md#env_texture) for the preset. This texture is used for imitating landscape reflections and lighting in accordance with the ground mask.
### Arguments

- *string* **name** - Path to the cubemap defining the environment color.

## string getTextureName ( )

Returns the path to the [cubemap defining the environment color](../../../editor2/settings/render_settings/environment/index.md#env_texture) set for the preset. This texture is used for imitating landscape reflections and lighting in accordance with the ground mask.
### Return value

Path to the cubemap defining the environment color.
## void setTextureColor ( vec4 color )

Sets the [environment color multiplier](../../../editor2/settings/render_settings/environment/index.md#env_texture_color) for the preset. The alpha channel defines visibility of the environment cubemap above scattering. The color multiplier is required when you need to display a sky with a photo texture and dynamic gradients at the same time.
### Arguments

- *vec4* **color** - The environment color multiplier.

## vec4 getTextureColor ( )

Returns the [environment color multiplier](../../../editor2/settings/render_settings/environment/index.md#env_texture_color) set for the preset. The alpha channel defines visibility of the environment cubemap above scattering. The color multiplier is required when you need to display a sky with a photo texture and dynamic gradients at the same time.
### Return value

The environment color multiplier.
## void setTextureRotation ( vec3 rotation )

Sets rotation of the environment texture along three axes.
### Arguments

- *vec3* **rotation** - Rotation of the texture along X, Y, Z axes, in degrees.

## vec3 getTextureRotation ( )

Returns rotation of the environment texture along three axes, in degrees.
### Return value

Rotation of the texture along X, Y, Z axes, in degrees.
## void setTextureBlur ( float blur )


Sets the blur intensity for the environment texture. This value can be used to make blurred panorama at the background.


> **Notice:** Reflections and ambient lighting aren't blurred.


### Arguments

- *float* **blur** - Blur intensity.

## float getTextureBlur ( )


Returns the blur intensity for the environment texture.


> **Notice:** Reflections and ambient lighting aren't blurred.


### Return value

Blur intensity.
## float getMoonTextureIntensity ( )

Returns the [intensity multiplier](../../../editor2/settings/render_settings/environment/index.md#moon_intensity) of the Moon texture. It allows increasing/reducing brightness of the Moon.
### Return value

Intensity of the Moon texture.
## void setMoonTextureIntensity ( float intensity )

Sets the [intensity multiplier](../../../editor2/settings/render_settings/environment/index.md#moon_intensity) of the Moon texture. It allows increasing/reducing brightness of the Moon.
### Arguments

- *float* **intensity** - Intensity of the Moon texture.

## void setSunTextureColor ( vec4 color )

Sets the [color multiplier](../../../editor2/settings/render_settings/environment/index.md#sun_color) for the current Sun texture. By default, it is (1,1,1,1).
### Arguments

- *vec4* **color** - Color multiplier.

## float getMoonAngularSize ( )

Returns the current [angular size](../../../editor2/settings/render_settings/environment/index.md#moon_size) of the Moon in degrees as seen from the Earth. By default, the size of the Moon is 0.5 degrees.
### Return value

Angular size of the Moon.
## float getSunTextureIntensity ( )

Returns the [intensity multiplier](../../../editor2/settings/render_settings/environment/index.md#sun_intensity) of the Sun texture. It allows increasing/reducing brightness of the Sun.
### Return value

Intensity of the sun texture.
## vec4 getMoonTextureColor ( )

Returns the [color multiplier](../../../editor2/settings/render_settings/environment/index.md#moon_color) of the Moon texture.
### Return value

Color multiplier.
## void setSunTextureName ( string name )

Sets the [Sun texture](../../../editor2/settings/render_settings/environment/index.md#sun) with the given name.
### Arguments

- *string* **name** - Name of the Sun texture.

## void setMoonTextureColor ( vec4 color )

Sets the [color multiplier](../../../editor2/settings/render_settings/environment/index.md#moon_color) for the current Moon texture. By default, it is (1,1,1,1).
### Arguments

- *vec4* **color** - Color multiplier.

## void setSunTextureIntensity ( float intensity )

Sets the [intensity multiplier](../../../editor2/settings/render_settings/environment/index.md#sun_intensity) of the Sun texture. It allows increasing/reducing brightness of the Sun.
### Arguments

- *float* **intensity** - Intensity of the Sun texture.

## void setMoonAngularSize ( float size )

Sets the [angular size](../../../editor2/settings/render_settings/environment/index.md#moon_size) of the Moon in degrees. The value is set for an observer on the Earth. By default, the size of the Moon is 0.5 degrees as seen from the Earth..
### Arguments

- *float* **size** - Angular size of the Moon.

## vec4 getSunTextureColor ( )

Returns the [color multiplier](../../../editor2/settings/render_settings/environment/index.md#sun_color) of the Sun texture. By default, it is (1,1,1,1).
### Return value

Color multiplier.
## void setMoonTextureName ( string name )

Sets a name of the [Moon texture](../../../editor2/settings/render_settings/environment/index.md#moon).
### Arguments

- *string* **name** - Name of the Moon texture.

## void setSunAngularSize ( float size )

Sets the [angular size](../../../editor2/settings/render_settings/environment/index.md#sun_size) of the Sun in degrees. The value is set for an observer on the Earth. By default, the size of the Sun is 0.5 degrees as seen from the Earth.
### Arguments

- *float* **size** - Angular size of the Sun.

## float getSunAngularSize ( )

Returns the [angular size](../../../editor2/settings/render_settings/environment/index.md#sun_size) of the Sun in degrees as seen from the Earth. By default, the size of the Sun is 0.5 degrees.
### Return value

Angular size of the Sun.
## string getSunTextureName ( )

Returns the name of the [Sun texture](../../../editor2/settings/render_settings/environment/index.md#sun).
### Return value

Name of the Sun texture.
## string getMoonTextureName ( )

Returns the name of the [Moon texture](../../../editor2/settings/render_settings/environment/index.md#moon).
### Return value

Name of the Moon texure.
## void setHazePhysicalStartHeight ( float height )

Sets a new reference height value for the two parameters ([Half Visibility Distance](#setHazePhysicalHalfVisibilityDistance_float_void) and [Half Faloff Height](#setHazePhysicalHalfFalloffHeight_float_void)).
### Arguments

- *float* **height** - New reference height value to be set, in units.

## float getHazePhysicalStartHeight ( )

Returns the current reference height value for the two parameters ([Half Visibility Distance](#setHazePhysicalHalfVisibilityDistance_float_void) and [Half Faloff Height](#setHazePhysicalHalfFalloffHeight_float_void)).
### Return value

Current reference height value, in units.
## void setHazePhysicalHalfVisibilityDistance ( float distance )

Sets the distance to the boundary at which the visibility comprises 50%. There is no zero-visibility in the real world, so the half-visibility boundary is used to adjust haze distance.
### Arguments

- *float* **distance** - New distance value to be set, in units.

## float getHazePhysicalHalfVisibilityDistance ( )

Returns the current distance to the boundary at which the visibility comprises 50%. There is no zero-visibility in the real world, so the half-visibility boundary is used to adjust haze distance.
### Return value

Current distance to the boundary at which the visibility comprises 50%, in units.
## void setHazePhysicalHalfFalloffHeight ( float height )

Sets the height of the haze density gradient. The *higher* the value, the *longer* the haze desity reduces as the height grows, making the transition between the clear sky and haze smoother.
### Arguments

- *float* **height** - New height of the haze density gradient to be set.

## float getHazePhysicalHalfFalloffHeight ( )

Returns the current height of the haze density gradient. The *higher* the value, the *longer* the haze desity reduces as the height grows, making the transition between the clear sky and haze smoother.
### Return value

Current height of the haze density gradient.
## void setHazePhysicalAmbientLightIntensity ( float intensity )

Sets the new intensity of the impact of the ambient lighting on haze (how much the ambient lighting affects the haze).
### Arguments

- *float* **intensity** - New value of intensity of the ambient lighting impact to be set.

## float getHazePhysicalAmbientLightIntensity ( )

Returns the current intensity of the impact of the ambient lighting on haze (how much the ambient lighting affects the haze).
### Return value

Current value of intensity of the ambient lighting impact.
## void setHazePhysicalAmbientColorSaturation ( float saturation )

Sets the new intensity of the ambient color's contribution to the haze (how much the sunlight affects the haze).
### Arguments

- *float* **saturation** - New value of intensity of the ambient color's contribution to the haze to be set.

## float getHazePhysicalAmbientColorSaturation ( )

Returns the current intensity of the ambient color's contribution to the haze (how much the sunlight affects the haze).
### Return value

Current value of intensity of the ambient color's contribution to the haze.
## void setHazePhysicalSunLightIntensity ( float intensity )

Sets the new intensity of the impact of the sunlight on haze (how much the sunlight affects the haze).
### Arguments

- *float* **intensity** - New value of intensity of the sunlight impact to be set.

## float getHazePhysicalSunLightIntensity ( )

Returns the current intensity of the impact of the sunlight on haze defining how much the sunlight affects the haze.
### Return value

Current value of intensity of the sunlight impact.
## void setHazePhysicalSunColorSaturation ( float saturation )


Sets the new intensity of the impact of the sunlight on haze (how much the sunlight affects the haze).


> **Notice:** "Sunlight color" here does not simply mean the color multiplier of the [*WorldLight*](../../../api/library/lights/class.lightworld_usc.md) source, but rather the [*Scattering LUT Light Color*](#setScatteringLightColorLUTName_cstr_void).


### Arguments

- *float* **saturation** - New value of intensity of the sunlight color's contribution to the haze to be set.

## float getHazePhysicalSunColorSaturation ( )

Returns the current intensity of the impact of the sunlight on haze (how much the sunlight affects the haze).
### Return value

Current intensity of the sunlight color's contribution to the haze.
## void setHazeScatteringMieIntensity ( float intensity )

Sets the minimum Mie intensity value for geometry-occluded areas. This value specifies the fraction of Mie intensity visible when the surface is viewed from straight on. Setting this value to 1 disables the Fresnel effect. You can use this parameter together with *Mie Frontside Intensity**[setHazeScatteringMieFrontSideIntensity()](../../...md#setHazeScatteringMieFrontSideIntensity_float_void)* and *Mie Fresnel Power**[setHazeScatteringMieFresnelPower()](../../...md#setHazeScatteringMieFresnelPower_float_void)* to control light occlusion from *World* light sources. Works for both, opaque and transparent objects.
### Arguments

- *float* **intensity** - New minimum Mie intensity value for geometry-occluded areas to be set in the [0.0f, 1.0f] range.

## float getHazeScatteringMieIntensity ( )

Returns the current minimum Mie intensity value for geometry-occluded areas. This value specifies the fraction of Mie intensity visible when the surface is viewed from straight on. Setting this value to 1 disables the Fresnel effect. You can use this parameter together with *Mie Frontside Intensity**[setHazeScatteringMieFrontSideIntensity()](../../...md#setHazeScatteringMieFrontSideIntensity_float_void)* and *Mie Fresnel Power**[setHazeScatteringMieFresnelPower()](../../...md#setHazeScatteringMieFresnelPower_float_void)* to control light occlusion from *World* light sources. Works for both, opaque and transparent objects.
### Return value

Current minimum Mie intensity value for geometry-occluded areas in the [0.0f, 1.0f] range.
## void setHazeScatteringMieFrontSideIntensity ( float intensity )

Sets the falloff of the Fresnel effect for Mie intensity. This value is used to control occlusion of light from a World light source by the geometry.
### Arguments

- *float* **intensity** - Falloff of the Fresnel effect for Mie intensity.

## float getHazeScatteringMieFrontSideIntensity ( )

Returns the falloff of the Fresnel effect for Mie intensity. This value is used to control occlusion of light from a World light source by the geometry.
### Return value

Falloff of the Fresnel effect for Mie intensity.
## void setHazeScatteringMieFresnelPower ( float power )

Sets the power of the Fresnel effect for Mie visibility. *Higher* values will tighten up the areas affected, while *lower* ones will allow more areas to be affected by the Fresnel effect.
### Arguments

- *float* **power** - New power of the Fresnel effect to be set.

## float getHazeScatteringMieFresnelPower ( )

Returns the current power of the Fresnel effect for Mie visibility. *Higher* values will tighten up the areas affected, while *lower* ones will allow more areas to be affected by the Fresnel effect.
### Return value

Current power of the Fresnel effect.
