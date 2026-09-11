# Unigine.RenderEnvironmentPreset Class (CS)


The class represents an [environment preset](../../../editor2/settings/render_settings/environment/index.md#presets). Each preset has settings that can be get/set by using methods of the class.


To get an instance of the class, use the *[Render.getEnvironmentPreset()](../../../api/library/rendering/class.render_cs.md#getEnvironmentPreset_int_RenderEnvironmentPreset)* method:


```csharp
// get the second environment preset
RenderEnvironmentPreset preset = Render.GetEnvironmentPreset(1);

```


## RenderEnvironmentPreset Class

### Properties

## float SkyIntensity

The intensity of the environment sky set for the preset.
## float ReflectionIntensity

The intensity of the environment reflections for the preset. **0** value means no environment reflections for the preset.
## float AmbientIntensity

The intensity of the environment ambient lighting for the preset. **0** value means no environment ambient lighting for the preset. The higher the value, the more ambient lighting affects environment.
## string TextureName

The path to the [cubemap defining the environment color](../../../editor2/settings/render_settings/environment/index.md#env_texture) set for the preset. This texture is used for imitating landscape reflections and lighting in accordance with the ground mask.
## float TextureBlur

The blur intensity for the environment texture.
> **Notice:** Reflections and ambient lighting aren't blurred.


## vec3 TextureRotation

The Rotation of the environment texture along three axes, in degrees.
## vec4 TextureColor

The [environment color multiplier](../../../editor2/settings/render_settings/environment/index.md#env_texture_color) set for the preset. The alpha channel defines visibility of the environment cubemap above scattering. The color multiplier is required when you need to display a sky with a photo texture and dynamic gradients at the same time.
## float MoonTextureIntensity

The [intensity multiplier](../../../editor2/settings/render_settings/environment/index.md#moon_intensity) of the Moon texture. It allows increasing/reducing brightness of the Moon.
## vec4 MoonTextureColor

The [color multiplier](../../../editor2/settings/render_settings/environment/index.md#moon_color) of the Moon texture.
## float MoonAngularSize

The current [angular size](../../../editor2/settings/render_settings/environment/index.md#moon_size) of the Moon in degrees as seen from the Earth. By default, the size of the Moon is 0.5 degrees.
## string MoonTextureName

The name of the [Moon texture](../../../editor2/settings/render_settings/environment/index.md#moon).
## float SunTextureIntensity

The [intensity multiplier](../../../editor2/settings/render_settings/environment/index.md#sun_intensity) of the Sun texture. It allows increasing/reducing brightness of the Sun.
## vec4 SunTextureColor

The [color multiplier](../../../editor2/settings/render_settings/environment/index.md#sun_color) of the Sun texture. By default, it is (1,1,1,1).
## float SunAngularSize

The [angular size](../../../editor2/settings/render_settings/environment/index.md#sun_size) of the Sun in degrees as seen from the Earth. By default, the size of the Sun is 0.5 degrees.
## string SunTextureName

The name of the [Sun texture](../../../editor2/settings/render_settings/environment/index.md#sun).
## string ScatteringLightColorLUTName

The path to the [light color texture](../../../editor2/settings/render_settings/environment/index.md#light_lut) (the texture defining the color of the LightWorld for different times of the day).
## string ScatteringMieLUTName

The path to the [Mie LUT texture](../../../editor2/settings/render_settings/environment/index.md#mie_lut) (the texture for setting the color of the light round the sun) set for the preset. The Mie texture is used for both sun and moon.
## string ScatteringBaseLUTName

The path to the [base LUT texture](../../../editor2/settings/render_settings/environment/index.md#base_lut) (the texture defining the base color of the sky) set for the preset.
## float HazeMaxDistance

The distance starting at which the haze becomes completely solid, so nothing will be seen behind.
## float HazeDensity

The [haze density](../../../editor2/settings/render_settings/environment/index.md#haze_density) set for the preset.
## vec4 HazeColor

The [haze color](../../../editor2/settings/render_settings/environment/index.md#haze_color) for the preset.
> **Notice:** This function will return color only if the [HAZE_SOLID](../../../api/library/rendering/class.render_cs.md#HAZE_SOLID) mode is set via *[setEnvironmentHazeMode()](../../../api/library/rendering/class.render_cs.md#setEnvironmentHazeMode_int_void)*.


## float Intensity

The intensity of the preset. the preset intensity is used to blend the environment preset with the other ones.
> **Notice:** Presets overlay each other: the first preset overlays the zero one, the second overlays the first and the zero ones.


## 🔒︎ int Num

The number of the preset.
## float HazePhysicalSunColorSaturation

The Current intensity of the sunlight color's contribution to the haze.
## float HazePhysicalSunLightIntensity

The Current value of intensity of the sunlight impact.
## float HazePhysicalAmbientColorSaturation

The Current value of intensity of the ambient color's contribution to the haze.
## float HazePhysicalAmbientLightIntensity

The Current value of intensity of the ambient lighting impact.
## float HazePhysicalHalfFalloffHeight

The Current height of the haze density gradient.
## float HazePhysicalHalfVisibilityDistance

The Current distance to the boundary at which the visibility comprises 50%, in units.
## float HazePhysicalStartHeight

The Current reference height value, in units.
## Texture Texture

The [cubemap defining the environment color](../../../editor2/settings/render_settings/environment/index.md#env_texture) set for the preset. This texture is used for imitating landscape reflections and lighting in accordance with the ground mask.
## float HazeScatteringMieFresnelPower

The Current power of the Fresnel effect.
## float HazeScatteringMieFrontSideIntensity

The Falloff of the Fresnel effect for Mie intensity.
## float HazeScatteringMieIntensity

The Current minimum Mie intensity value for geometry-occluded areas in the [0.0f, 1.0f] range.
## float HazePhysicalVisibilityThreshold

The threshold for the physical haze visibility factor: visibility is normalized by this value, so lower thresholds make the haze reach its full density sooner. The default value is 1.
### Members

---
