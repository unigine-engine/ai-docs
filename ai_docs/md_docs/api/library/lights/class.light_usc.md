# Unigine.Light Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Node


This base class is used to create light sources and shadows from them. The lights can be rendered as a simplified deferred lighting.


## Light Class

### Members

## void setShadowScreenSpaceSoftness ( float softness = 0.4 )

Sets a new softness value of the screen-space shadows for the light source. Higher values provide softer shadows.
> **Notice:** Screen-space shadows must be enabled, see the [setShadowScreenSpace()](#setShadowScreenSpace_int_void) method.


### Arguments

- *float* **softness** - The screen-space shadows softness.

## float getShadowScreenSpaceSoftness () const

Returns the current softness value of the screen-space shadows for the light source. Higher values provide softer shadows.
> **Notice:** Screen-space shadows must be enabled, see the [setShadowScreenSpace()](#setShadowScreenSpace_int_void) method.


### Return value

Current screen-space shadows softness.
## void setShadowScreenSpaceThresholdNear ( float near = 1.0 )

Sets a new threshold value used to calculate screen-space shadows for the light source ([close distance range](#setShadowScreenSpaceThresholdNearDistance_float_void)). You can set different Step Size and Threshold values for objects located near the camera and far away from it. Thus, full-scale shadows will be rendered for large objects located far away, while within the close distance range only shadows cast by small objects will be rendered. This feature is especially useful for locations where details are required for both short and long-distance ranges.
> **Notice:** Screen-space shadows must be enabled, see the [setShadowScreenSpace()](#setShadowScreenSpace_int_void) method.


### Arguments

- *float* **near** - The screen-space shadows [threshold for close distance range](../../../objects/lights/parameters/index.md#near_threshold).

## float getShadowScreenSpaceThresholdNear () const

Returns the current threshold value used to calculate screen-space shadows for the light source ([close distance range](#setShadowScreenSpaceThresholdNearDistance_float_void)). You can set different Step Size and Threshold values for objects located near the camera and far away from it. Thus, full-scale shadows will be rendered for large objects located far away, while within the close distance range only shadows cast by small objects will be rendered. This feature is especially useful for locations where details are required for both short and long-distance ranges.
> **Notice:** Screen-space shadows must be enabled, see the [setShadowScreenSpace()](#setShadowScreenSpace_int_void) method.


### Return value

Current screen-space shadows [threshold for close distance range](../../../objects/lights/parameters/index.md#near_threshold).
## void setShadowScreenSpaceStepSizeNear ( float near = 0.5 )

Sets a new size of the step used to calculate screen-space shadows for the light source ([close distance range](#setShadowScreenSpaceStepSizeNearDistance_float_void)). This parameter can be used to adjust calculation of shadows for specific sizes of objects. You can set different Step Size and Threshold values for objects located near the camera and far away from it. Thus, full-scale shadows will be rendered for large objects located far away, while within the close distance range only shadows cast by small objects will be rendered. This feature is especially useful for locations where details are required for both short and long-distance ranges.
> **Notice:** Screen-space shadows must be enabled, see the [setShadowScreenSpace()](#setShadowScreenSpace_int_void) method.


### Arguments

- *float* **near** - The screen-space [step size for close distance range](../../../objects/lights/parameters/index.md#near_step_size).

## float getShadowScreenSpaceStepSizeNear () const

Returns the current size of the step used to calculate screen-space shadows for the light source ([close distance range](#setShadowScreenSpaceStepSizeNearDistance_float_void)). This parameter can be used to adjust calculation of shadows for specific sizes of objects. You can set different Step Size and Threshold values for objects located near the camera and far away from it. Thus, full-scale shadows will be rendered for large objects located far away, while within the close distance range only shadows cast by small objects will be rendered. This feature is especially useful for locations where details are required for both short and long-distance ranges.
> **Notice:** Screen-space shadows must be enabled, see the [setShadowScreenSpace()](#setShadowScreenSpace_int_void) method.


### Return value

Current screen-space [step size for close distance range](../../../objects/lights/parameters/index.md#near_step_size).
## void setShadowScreenSpaceNoiseStep ( float step = 0.5 )

Sets a new intensity of the step noise used to calculate screen-space shadows for the light source. Higher values reduce the banding effect more. However, this option significantly affects performance.
> **Notice:** Screen-space shadows must be enabled, see the [setShadowScreenSpace()](#setShadowScreenSpace_int_void) method.


### Arguments

- *float* **step** - The step noise intensity.

## float getShadowScreenSpaceNoiseStep () const

Returns the current intensity of the step noise used to calculate screen-space shadows for the light source. Higher values reduce the banding effect more. However, this option significantly affects performance.
> **Notice:** Screen-space shadows must be enabled, see the [setShadowScreenSpace()](#setShadowScreenSpace_int_void) method.


### Return value

Current step noise intensity.
## void setShadowScreenSpaceNoiseRay ( )

Sets a new intensity of the ray noise used to calculate screen-space shadows for the light source. Higher values reduce the banding effect more. However, this option significantly affects performance.
> **Notice:** Screen-space shadows must be enabled, see the [setShadowScreenSpace()](#setShadowScreenSpace_int_void) method.


### Arguments

- **ray** - The ray noise intensity.

## getShadowScreenSpaceNoiseRay () const

Returns the current intensity of the ray noise used to calculate screen-space shadows for the light source. Higher values reduce the banding effect more. However, this option significantly affects performance.
> **Notice:** Screen-space shadows must be enabled, see the [setShadowScreenSpace()](#setShadowScreenSpace_int_void) method.


### Return value

Current ray noise intensity.
## void setShadowScreenSpaceNumSteps ( int steps = 8 )

Sets a new number of steps used to calculate screen-space shadows for the light source. Higher values, improve the quality of shadows more. However, this option significantly affects performance.
> **Notice:** Screen-space shadows must be enabled, see the [setShadowScreenSpace()](#setShadowScreenSpace_int_void) method.

### Arguments

- *int* **steps** - The number of steps.

## int getShadowScreenSpaceNumSteps () const

Returns the current number of steps used to calculate screen-space shadows for the light source. Higher values, improve the quality of shadows more. However, this option significantly affects performance.
> **Notice:** Screen-space shadows must be enabled, see the [setShadowScreenSpace()](#setShadowScreenSpace_int_void) method.

### Return value

Current number of steps.
## void setShadowScreenSpaceNumRays ( int rays = 8 )

Sets a new number of rays used to calculate screen-space shadows for the light source. Higher values, improve the quality of shadows more. However, this option significantly affects performance.
> **Notice:** Screen-space shadows must be enabled, see the [setShadowScreenSpace()](#setShadowScreenSpace_int_void) method.

### Arguments

- *int* **rays** - The number of rays.

## int getShadowScreenSpaceNumRays () const

Returns the current number of rays used to calculate screen-space shadows for the light source. Higher values, improve the quality of shadows more. However, this option significantly affects performance.
> **Notice:** Screen-space shadows must be enabled, see the [setShadowScreenSpace()](#setShadowScreenSpace_int_void) method.

### Return value

Current number of rays.
## void setShadowScreenSpace ( int space = false )

Sets a new value indicating if screen-space shadows for the light source are enabled. With this option enabled, penumbras from the light source are calculated using the ray tracing algorithm.
### Arguments

- *int* **space** - The screen-space shadows for the light source

## int isShadowScreenSpace () const

Returns the current value indicating if screen-space shadows for the light source are enabled. With this option enabled, penumbras from the light source are calculated using the ray tracing algorithm.
### Return value

Current screen-space shadows for the light source
## Texture getShadowTexture () const

Returns the current depth texture (shadow map) of the light source.
### Return value

Current depth texture (shadow map) of the light source.
## Texture getDynamicShadowColorTexture () const

Returns the current shadow texture of the light source used to render translucent shadows: G-channel stores depth values, R-channel - transparency values.
### Return value

Current shadow texture of the light source.
## Texture getBakedDepthTexture () const

Returns the current depth texture baked for the light source. this texture is available for [Static](#MODE_STATIC) light sources only.
> **Notice:** Static lights with [mixed shadow mode](#SHADOW_MODE_MIXED) enabled use a mixture of [dynamic](#getDynamicDepthTexture_Texture) and baked depth textures.


### Return value

Current baked depth texture for the light source.
## void setBakedDepthTextureFilePath ( string path )

Sets a new path to a baked depth texture file, which stores a shadow map generated for the light source, when its mode is set to [MODE_STATIC](#MODE_STATIC). [EnvironmentProbes](../../../api/library/lights/class.lightenvironmentprobe_usc.md) use this texture for [cutting out reflections for occluded areas](../../../api/library/lights/class.lightenvironmentprobe_usc.md#setCutoutByShadow_int_void), where they should not be visible. This texture is baked automatically via the Editor or using [bake()](../../../api/library/lights/class.bakelighting_usc.md#bake_VECLightVoxelProbe_VECLightEnvironmentProbe_VECLight_VECObjectMeshStatic_VECint_void) or [bakeAll()](../../../api/library/lights/class.bakelighting_usc.md#bakeAll_int_int_int_int_void) methods.
### Arguments

- *string* **path** - The path to a baked depth texture file to be used.

## const char * getBakedDepthTextureFilePath () const

Returns the current path to a baked depth texture file, which stores a shadow map generated for the light source, when its mode is set to [MODE_STATIC](#MODE_STATIC). [EnvironmentProbes](../../../api/library/lights/class.lightenvironmentprobe_usc.md) use this texture for [cutting out reflections for occluded areas](../../../api/library/lights/class.lightenvironmentprobe_usc.md#setCutoutByShadow_int_void), where they should not be visible. This texture is baked automatically via the Editor or using [bake()](../../../api/library/lights/class.bakelighting_usc.md#bake_VECLightVoxelProbe_VECLightEnvironmentProbe_VECLight_VECObjectMeshStatic_VECint_void) or [bakeAll()](../../../api/library/lights/class.bakelighting_usc.md#bakeAll_int_int_int_int_void) methods.
### Return value

Current path to a baked depth texture file to be used.
## Texture getDynamicDepthTexture () const

Returns the current dynamic depth texture for the light source. This texture is available for the following types of light sources:
- [Dynamic](#MODE_DYNAMIC) lights.
- [Static](#MODE_STATIC) lights with [mixed shadow mode](#SHADOW_MODE_MIXED) enabled, that use a mixture of dynamic and baked depth textures.


### Return value

Current depth texture to be used for the light source.
## void setShadowPenumbra ( float penumbra = 0.0 )

Sets a new intensity of penumbra for the selected mode.
> **Notice:** This value is ignored when [penumbra rendering mode](#setShadowPenumbraMode_int_void) is set to *disabled*.


### Arguments

- *float* **penumbra** - The intensity of penumbra for the selected mode:

  - *Low* values correspond to sharper shadow edges.
  - Higher values increase penumbra size.

## float getShadowPenumbra () const

Returns the current intensity of penumbra for the selected mode.
> **Notice:** This value is ignored when [penumbra rendering mode](#setShadowPenumbraMode_int_void) is set to *disabled*.


### Return value

Current intensity of penumbra for the selected mode:
- *Low* values correspond to sharper shadow edges.
- Higher values increase penumbra size.


## void setShadowPenumbraMode ( int mode = SHADOW_PENUMBRA_GLOBAL )

Sets a new global quality mode used for rendering penumbra from the light source. this mode enables simulation of real-world shadows by keeping sharp contact shadows closer to the base and softening the farther the shadow stretches away. *Higher* values produce *softer* shadows.
### Arguments

- *int* **mode** - The quality mode used for penumbra rendering, one of the [LIGHT_SHADOW_PENUMBRA_*](#SHADOW_PENUMBRA_ULTRA) variables.

## int getShadowPenumbraMode () const

Returns the current global quality mode used for rendering penumbra from the light source. this mode enables simulation of real-world shadows by keeping sharp contact shadows closer to the base and softening the farther the shadow stretches away. *Higher* values produce *softer* shadows.
### Return value

Current quality mode used for penumbra rendering, one of the [LIGHT_SHADOW_PENUMBRA_*](#SHADOW_PENUMBRA_ULTRA) variables.
## void setShadowFilter ( float filter )

Sets a new filtering intensity for the selected mode.
> **Notice:** This value is ignored when [filtering mode](#setShadowFilterMode_int_void) is set to *disabled*.


### Arguments

- *float* **filter** - The filtering intensity for the selected [mode](#setShadowFilterMode_int_void). The *higher* the value the less noticeable the stair-step effect at the edges of shadows will be. The default value is 1.0f.

## float getShadowFilter () const

Returns the current filtering intensity for the selected mode.
> **Notice:** This value is ignored when [filtering mode](#setShadowFilterMode_int_void) is set to *disabled*.


### Return value

Current filtering intensity for the selected [mode](#setShadowFilterMode_int_void). The *higher* the value the less noticeable the stair-step effect at the edges of shadows will be. The default value is 1.0f.
## void setShadowFilterMode ( int mode )

Sets a new filtering mode used to reduce the stair-step effect for soft shadows making the edges smoother.
### Arguments

- *int* **mode** - The filtering mode to be used for shadows rendering, one of the [LIGHT_SHADOW_FILTER_*](#SHADOW_FILTER_ULTRA) variables.

## int getShadowFilterMode () const

Returns the current filtering mode used to reduce the stair-step effect for soft shadows making the edges smoother.
### Return value

Current filtering mode to be used for shadows rendering, one of the [LIGHT_SHADOW_FILTER_*](#SHADOW_FILTER_ULTRA) variables.
## void setShadowMode ( int mode )

Sets a new shadow mode for the light source in static mode. this shadow mode should be [aligned](../../../content/optimization/lights/index.md#static_light) with the [shadow mode](../../../api/library/objects/class.object_usc.md#setShadowMode_int_int_void) of the object surface in order to make this surface cast a shadow from the light source.
### Arguments

- *int* **mode** - The shadow mode of the light in static mode, one of the [LIGHT_SHADOW_MODE_*](#SHADOW_MODE_STATIC) variables.

## int getShadowMode () const

Returns the current shadow mode for the light source in static mode. this shadow mode should be [aligned](../../../content/optimization/lights/index.md#static_light) with the [shadow mode](../../../api/library/objects/class.object_usc.md#setShadowMode_int_int_void) of the object surface in order to make this surface cast a shadow from the light source.
### Return value

Current shadow mode of the light in static mode, one of the [LIGHT_SHADOW_MODE_*](#SHADOW_MODE_STATIC) variables.
## void setMode ( int mode )

Sets a new rendering mode for the light source. This option determines whether the light is to be rendered as a dynamic or static one.
### Arguments

- *int* **mode** - The light mode, one of the [LIGHT_MODE_*](#MODE_DYNAMIC) variables.

## int getMode () const

Returns the current rendering mode for the light source. This option determines whether the light is to be rendered as a dynamic or static one.
### Return value

Current light mode, one of the [LIGHT_MODE_*](#MODE_DYNAMIC) variables.
## void setShadowNormalBias ( float bias )

Sets a new shadow bias that is achieved by shifting the surface on which the shadow falls. the surface is shifted along normals stored in the normal map. depending on the normal map of the surface, the shadow may differ for the same values of the normal bias.
### Arguments

- *float* **bias** - The normal bias. If a negative value is provided, 0 will be used instead.

## float getShadowNormalBias () const

Returns the current shadow bias that is achieved by shifting the surface on which the shadow falls. the surface is shifted along normals stored in the normal map. depending on the normal map of the surface, the shadow may differ for the same values of the normal bias.
### Return value

Current normal bias. If a negative value is provided, 0 will be used instead.
## void setShadowBias ( float bias )

Sets a new
### Arguments

- *float* **bias** - The constant depth offset. If a negative value is provided, 0 will be used instead.

## float getShadowBias () const

Returns the current
### Return value

Current constant depth offset. If a negative value is provided, 0 will be used instead.
## void setShadowResolution ( int resolution )

Sets a new size of the shadow map created for the light source.
- The higher the resolution, the smoother and true to life the result is.
- The lower the resolution, the more blocky and jagged the shadows outline appears.


### Arguments

- *int* **resolution** - The shadow map size, one of the [LIGHT_SHADOW_RESOLUTION_VALUE_](#SHADOW_RESOLUTION_VALUE_16384) variables.

## int getShadowResolution () const

Returns the current size of the shadow map created for the light source.
- The higher the resolution, the smoother and true to life the result is.
- The lower the resolution, the more blocky and jagged the shadows outline appears.


### Return value

Current shadow map size, one of the [LIGHT_SHADOW_RESOLUTION_VALUE_](#SHADOW_RESOLUTION_VALUE_16384) variables.
## void setShadow ( int shadow )

Sets a new value indicating if the light source casts shadows from surfaces with the [Cast Shadow](../../../api/library/rendering/class.material_usc.md#setCastShadow_int_void) material.
### Arguments

- *int* **shadow** - The shadow casting

## int getShadow () const

Returns the current value indicating if the light source casts shadows from surfaces with the [Cast Shadow](../../../api/library/rendering/class.material_usc.md#setCastShadow_int_void) material.
### Return value

Current shadow casting
## void setAttenuationPower ( float power = 1.0 )

Sets a new attenuation power of the light. This parameter determines how fast the intensity decreases up to the attenuation distance set for the light source. If the attenuation equals to zero or is close to it, the edge between illuminated and non-illuminated areas is sharp.
### Arguments

- *float* **power** - The light attenuation power.

## float getAttenuationPower () const

Returns the current attenuation power of the light. This parameter determines how fast the intensity decreases up to the attenuation distance set for the light source. If the attenuation equals to zero or is close to it, the edge between illuminated and non-illuminated areas is sharp.
### Return value

Current light attenuation power.
## void setColorFilter ( vec4 filter )

Sets a new color multiplier for the light source color (calculated using the [color temperature](#setColorTemperature_float_void) value). This is used to imitate colored glass. The method takes effect only when the color mode is set to *Temperature*.
### Arguments

- *vec4* **filter** - The color.

## vec4 getColorFilter () const

Returns the current color multiplier for the light source color (calculated using the [color temperature](#setColorTemperature_float_void) value). This is used to imitate colored glass. The method takes effect only when the color mode is set to *Temperature*.
### Return value

Current color.
## void setColorTemperature ( float temperature )

Sets a new light source temperature used for light color calculation.
### Arguments

- *float* **temperature** - The light source temperature in range [0;40000].

## float getColorTemperature () const

Returns the current light source temperature used for light color calculation.
### Return value

Current light source temperature in range [0;40000].
## void setLux ( float lux )

Sets a new intensity of the light color (as perceived by the human eye) in lux. in unigine, all light sources have the [intensity](#setIntensity_float_void) of 1 by default, which is equal to 100000 lux.
### Arguments

- *float* **lux** - The light color intensity.

## float getLux () const

Returns the current intensity of the light color (as perceived by the human eye) in lux. in unigine, all light sources have the [intensity](#setIntensity_float_void) of 1 by default, which is equal to 100000 lux.
### Return value

Current light color intensity.
## void setIntensity ( float intensity )

Sets a new multiplier of the light color used to control color intensity. the higher the value, the brighter the light is.
- The minimum value of 1 corresponds to the least saturated light color.
- The maximum value of 100 equals the most bright and intense color.


### Arguments

- *float* **intensity** - The color multiplier.

## float getIntensity () const

Returns the current multiplier of the light color used to control color intensity. the higher the value, the brighter the light is.
- The minimum value of 1 corresponds to the least saturated light color.
- The maximum value of 100 equals the most bright and intense color.


### Return value

Current color multiplier.
## void setColor ( vec4 color )

Sets a new color of the light source. The default is opaque white, **(1, 1, 1, 1)**. The method takes effect only when the *Classic* color mode is set.
### Arguments

- *vec4* **color** - The color in the RGBA format.

## vec4 getColor () const

Returns the current color of the light source. The default is opaque white, **(1, 1, 1, 1)**. The method takes effect only when the *Classic* color mode is set.
### Return value

Current color in the RGBA format.
## void setColorMode ( int mode )

Sets a new color calculation mode of the light source. Light source color can be defined by the [color](#setColor_vec4_void) value (classic mode) or by the [color temperature](#setColorTemperature_float_void) and [color filter](#setColorFilter_vec4_void) values (physically based mode).
### Arguments

- *int* **mode** - The color calculation mode, one of the following values:

  - [LIGHT_COLOR_MODE_CLASSIC](#COLOR_MODE_CLASSIC) - classic mode
  - [LIGHT_COLOR_MODE_TEMPERATURE](#COLOR_MODE_TEMPERATURE) - physically based mode

## int getColorMode () const

Returns the current color calculation mode of the light source. Light source color can be defined by the [color](#setColor_vec4_void) value (classic mode) or by the [color temperature](#setColorTemperature_float_void) and [color filter](#setColorFilter_vec4_void) values (physically based mode).
### Return value

Current color calculation mode, one of the following values:
- [LIGHT_COLOR_MODE_CLASSIC](#COLOR_MODE_CLASSIC) - classic mode
- [LIGHT_COLOR_MODE_TEMPERATURE](#COLOR_MODE_TEMPERATURE) - physically based mode


## void setViewportMask ( int mask )

Sets a new bit mask for rendering into the viewport. The light is rendered, if its mask matches the player's one.
### Arguments

- *int* **mask** - The bit mask - an integer, each bit of which is used to set a mask.

## int getViewportMask () const

Returns the current bit mask for rendering into the viewport. The light is rendered, if its mask matches the player's one.
### Return value

Current bit mask - an integer, each bit of which is used to set a mask.
## void setShadowMask ( int mask )

Sets a new light mask for the light source.
For the shadow from an object's surface to be rendered for the light source, this mask must match the following ones (one bit, at least):

- [Shadow mask of the surface](../../../api/library/objects/class.object_usc.md#setShadowMask_int_int_void) of the object
- [Shadow mask of the material](../../../api/library/rendering/class.material_usc.md#setShadowMask_int_void) assigned to this surface


### Arguments

- *int* **mask** - The bit mask - an integer, each bit of which is used to set a mask.

## int getShadowMask () const

Returns the current light mask for the light source.
For the shadow from an object's surface to be rendered for the light source, this mask must match the following ones (one bit, at least):

- [Shadow mask of the surface](../../../api/library/objects/class.object_usc.md#setShadowMask_int_int_void) of the object
- [Shadow mask of the material](../../../api/library/rendering/class.material_usc.md#setShadowMask_int_void) assigned to this surface


### Return value

Current bit mask - an integer, each bit of which is used to set a mask.
## void setRenderOnTransparent ( int transparent )

Sets a new value indicating if the light from the source is rendered on transparent objects.
### Arguments

- *int* **transparent** - The rendering the light from the source on transparent objects

## int isRenderOnTransparent () const

Returns the current value indicating if the light from the source is rendered on transparent objects.
### Return value

Current rendering the light from the source on transparent objects
## void setRenderOnWater ( int water )

Sets a new value indicating if the light from the source is rendered on water objects.
### Arguments

- *int* **water** - The rendering the light from the source on water objects

## int isRenderOnWater () const

Returns the current value indicating if the light from the source is rendered on water objects.
### Return value

Current rendering the light from the source on water objects
## void setFadeDistance ( float distance )

Sets a new distance, at which the light source gradually disappears. This parameter enables to render the light with decreasing radiance after the [Visible distance](#setVisibleDistance_float_void) is past.
### Arguments

- *float* **distance** - The distance in units.

## float getFadeDistance () const

Returns the current distance, at which the light source gradually disappears. This parameter enables to render the light with decreasing radiance after the [Visible distance](#setVisibleDistance_float_void) is past.
### Return value

Current distance in units.
## void setShadowDistance ( float distance )

Sets a new distance, at which shadow from the light source starts fading out to nonexistence.
### Arguments

- *float* **distance** - The distance in units.

## float getShadowDistance () const

Returns the current distance, at which shadow from the light source starts fading out to nonexistence.
### Return value

Current distance in units.
## void setVisibleDistance ( float distance )

Sets a new distance, at which the light source starts fading. If the distance is set to infinity, the source is always rendered.
### Arguments

- *float* **distance** - The distance in units.

## float getVisibleDistance () const

Returns the current distance, at which the light source starts fading. If the distance is set to infinity, the source is always rendered.
### Return value

Current distance in units.
## int getNumLensFlares () const

Returns the current total number of lens flares used for the per-light lens flare effect.
> **Notice:** The lens flare effect must be [enabled](#setLensFlaresEnabled_int_void) for the light source. This feature is available only for: [Omni Lights](../../../api/library/lights/class.lightomni_usc.md), [Projected Lights](../../../api/library/lights/class.lightproj_usc.md) and [World Lights](../../../api/library/lights/class.lightworld_usc.md).


### Return value

Current number of lens flares used for the per-light lens flare effect.
## void setLensFlaresUseLightColor ( int color )

Sets a new value indicating if light color modulation is enabled for per-light lens flares. when enabled, the lens flares will have the same color as the light source.
> **Notice:** The lens flare effect must be [enabled](#setLensFlaresEnabled_int_void) for the light source. This feature is available only for: [Omni Lights](../../../api/library/lights/class.lightomni_usc.md), [Projected Lights](../../../api/library/lights/class.lightproj_usc.md) and [World Lights](../../../api/library/lights/class.lightworld_usc.md).


### Arguments

- *int* **color** - The light color modulation for the per-light lens flare effect

## int isLensFlaresUseLightColor () const

Returns the current value indicating if light color modulation is enabled for per-light lens flares. when enabled, the lens flares will have the same color as the light source.
> **Notice:** The lens flare effect must be [enabled](#setLensFlaresEnabled_int_void) for the light source. This feature is available only for: [Omni Lights](../../../api/library/lights/class.lightomni_usc.md), [Projected Lights](../../../api/library/lights/class.lightproj_usc.md) and [World Lights](../../../api/library/lights/class.lightworld_usc.md).


### Return value

Current light color modulation for the per-light lens flare effect
## void setLensFlaresWorldPositionOffset ( vec3 offset )

Sets a new offset from the world position of the light source for the per-light lens flares. offset is not available for [World Lights](../../../api/library/lights/class.lightworld_usc.md).
> **Notice:** The lens flare effect must be [enabled](#setLensFlaresEnabled_int_void) for the light source. This feature is available only for: [Omni Lights](../../../api/library/lights/class.lightomni_usc.md), [Projected Lights](../../../api/library/lights/class.lightproj_usc.md) and [World Lights](../../../api/library/lights/class.lightworld_usc.md).


### Arguments

- *vec3* **offset** - The vector representing the offset of lens flares from the light source world position.

## vec3 getLensFlaresWorldPositionOffset () const

Returns the current offset from the world position of the light source for the per-light lens flares. offset is not available for [World Lights](../../../api/library/lights/class.lightworld_usc.md).
> **Notice:** The lens flare effect must be [enabled](#setLensFlaresEnabled_int_void) for the light source. This feature is available only for: [Omni Lights](../../../api/library/lights/class.lightomni_usc.md), [Projected Lights](../../../api/library/lights/class.lightproj_usc.md) and [World Lights](../../../api/library/lights/class.lightworld_usc.md).


### Return value

Current vector representing the offset of lens flares from the light source world position.
## void setLensFlaresOcclusionFadeBorder ( float border )

Sets a new lens flare occlusion fade border value for the cases when the light source becomes occluded by the edges of the screen.
> **Notice:** The lens flare effect must be [enabled](#setLensFlaresEnabled_int_void) for the light source. This feature is available only for: [Omni Lights](../../../api/library/lights/class.lightomni_usc.md), [Projected Lights](../../../api/library/lights/class.lightproj_usc.md) and [World Lights](../../../api/library/lights/class.lightworld_usc.md).


### Arguments

- *float* **border** - The lens flare occlusion fade border value in the range [0.0f; 1.0f]. By the value of 0.0f, lens flares disappear abruptly, as the light source becomes occluded by an object. If 1.0f is set, lens flares will fade out gradually.

## float getLensFlaresOcclusionFadeBorder () const

Returns the current lens flare occlusion fade border value for the cases when the light source becomes occluded by the edges of the screen.
> **Notice:** The lens flare effect must be [enabled](#setLensFlaresEnabled_int_void) for the light source. This feature is available only for: [Omni Lights](../../../api/library/lights/class.lightomni_usc.md), [Projected Lights](../../../api/library/lights/class.lightproj_usc.md) and [World Lights](../../../api/library/lights/class.lightworld_usc.md).


### Return value

Current lens flare occlusion fade border value in the range [0.0f; 1.0f]. By the value of 0.0f, lens flares disappear abruptly, as the light source becomes occluded by an object. If 1.0f is set, lens flares will fade out gradually.
## void setLensFlaresOcclusionFade ( float fade )

Sets a new lens flare occlusion fade value for the cases when the light source becomes occluded by an object.
> **Notice:** The lens flare effect must be [enabled](#setLensFlaresEnabled_int_void) for the light source. This feature is available only for: [Omni Lights](../../../api/library/lights/class.lightomni_usc.md), [Projected Lights](../../../api/library/lights/class.lightproj_usc.md) and [World Lights](../../../api/library/lights/class.lightworld_usc.md).


### Arguments

- *float* **fade** - The lens flare occlusion fade value in the range [0.0f; 1.0f]. By the value of 0.0f, lens flares disappear abruptly, as the light source becomes occluded by an object. If 1.0f is set, lens flares will fade out gradually.

## float getLensFlaresOcclusionFade () const

Returns the current lens flare occlusion fade value for the cases when the light source becomes occluded by an object.
> **Notice:** The lens flare effect must be [enabled](#setLensFlaresEnabled_int_void) for the light source. This feature is available only for: [Omni Lights](../../../api/library/lights/class.lightomni_usc.md), [Projected Lights](../../../api/library/lights/class.lightproj_usc.md) and [World Lights](../../../api/library/lights/class.lightworld_usc.md).


### Return value

Current lens flare occlusion fade value in the range [0.0f; 1.0f]. By the value of 0.0f, lens flares disappear abruptly, as the light source becomes occluded by an object. If 1.0f is set, lens flares will fade out gradually.
## void setLensFlaresIntensity ( float intensity )

Sets a new intensity of per-light lens flares.
> **Notice:** The lens flare effect must be [enabled](#setLensFlaresEnabled_int_void) for the light source. This feature is available only for: [Omni Lights](../../../api/library/lights/class.lightomni_usc.md), [Projected Lights](../../../api/library/lights/class.lightproj_usc.md) and [World Lights](../../../api/library/lights/class.lightworld_usc.md).


### Arguments

- *float* **intensity** - The intensity of per-light lens flares.*Higher* values make the effect more pronounced.

## float getLensFlaresIntensity () const

Returns the current intensity of per-light lens flares.
> **Notice:** The lens flare effect must be [enabled](#setLensFlaresEnabled_int_void) for the light source. This feature is available only for: [Omni Lights](../../../api/library/lights/class.lightomni_usc.md), [Projected Lights](../../../api/library/lights/class.lightproj_usc.md) and [World Lights](../../../api/library/lights/class.lightworld_usc.md).


### Return value

Current intensity of per-light lens flares.*Higher* values make the effect more pronounced.
## void setLensFlaresTextureName ( string name )

Sets a new name of the texture used for the per-light lens flare effect. This texture stores images for all lens flares used to render lens flares.
> **Notice:** The lens flare effect must be [enabled](#setLensFlaresEnabled_int_void) for the light source. This feature is available only for: [Omni Lights](../../../api/library/lights/class.lightomni_usc.md), [Projected Lights](../../../api/library/lights/class.lightproj_usc.md) and [World Lights](../../../api/library/lights/class.lightworld_usc.md).


### Arguments

- *string* **name** - The texture name.

## const char * getLensFlaresTextureName () const

Returns the current name of the texture used for the per-light lens flare effect. This texture stores images for all lens flares used to render lens flares.
> **Notice:** The lens flare effect must be [enabled](#setLensFlaresEnabled_int_void) for the light source. This feature is available only for: [Omni Lights](../../../api/library/lights/class.lightomni_usc.md), [Projected Lights](../../../api/library/lights/class.lightproj_usc.md) and [World Lights](../../../api/library/lights/class.lightworld_usc.md).


### Return value

Current texture name.
## void setLensFlaresEnabled ( int enabled )

Sets a new value indicating if the per-light lens flare effect is enabled for the light source.
> **Notice:** - This feature is available only for: [Omni Lights](../../../api/library/lights/class.lightomni_usc.md), [Projected Lights](../../../api/library/lights/class.lightproj_usc.md) and [World Lights](../../../api/library/lights/class.lightworld_usc.md).
> - The maximum number of per-light lens flares that can be rendered is 32.


### Arguments

- *int* **enabled** - The per-light lens flare effect for the light source

## int isLensFlaresEnabled () const

Returns the current value indicating if the per-light lens flare effect is enabled for the light source.
> **Notice:** - This feature is available only for: [Omni Lights](../../../api/library/lights/class.lightomni_usc.md), [Projected Lights](../../../api/library/lights/class.lightproj_usc.md) and [World Lights](../../../api/library/lights/class.lightworld_usc.md).
> - The maximum number of per-light lens flares that can be rendered is 32.


### Return value

Current per-light lens flare effect for the light source
## void setShadowScreenSpaceThresholdFar ( float far )

Sets a new threshold value used to calculate screen-space shadows for the light source ([long distance range](#setShadowScreenSpaceThresholdFarDistance_float_void)). You can set different Step Size and Threshold values for objects located near the camera and far away from it. Thus, full-scale shadows will be rendered for large objects located far away, while within the close distance range only shadows cast by small objects will be rendered. This feature is especially useful for locations where details are required for both short and long-distance ranges.
### Arguments

- *float* **far** - The screen-space shadows [threshold for long distance range](../../../objects/lights/parameters/index.md#far_threshold). The default value is 1.0. > **Notice:** Screen-space shadows must be enabled, see the [setShadowScreenSpace()](#setShadowScreenSpace_int_void) method.

## float getShadowScreenSpaceThresholdFar () const

Returns the current threshold value used to calculate screen-space shadows for the light source ([long distance range](#setShadowScreenSpaceThresholdFarDistance_float_void)). You can set different Step Size and Threshold values for objects located near the camera and far away from it. Thus, full-scale shadows will be rendered for large objects located far away, while within the close distance range only shadows cast by small objects will be rendered. This feature is especially useful for locations where details are required for both short and long-distance ranges.
### Return value

Current screen-space shadows [threshold for long distance range](../../../objects/lights/parameters/index.md#far_threshold). The default value is 1.0.
> **Notice:** Screen-space shadows must be enabled, see the [setShadowScreenSpace()](#setShadowScreenSpace_int_void) method.


## void setShadowScreenSpaceThresholdFarDistance ( float distance )

Sets a new distance from the camera after which the [Far Threshold](#setShadowScreenSpaceThresholdFar_float_void) is used for screen-space shadows calculation. You can set different Step Size and Threshold values for objects located near the camera and far away from it. Thus, full-scale shadows will be rendered for large objects located far away, while within the close distance range only shadows cast by small objects will be rendered. This feature is especially useful for locations where details are required for both short and long-distance ranges.
### Arguments

- *float* **distance** - The distance from the camera (in units) after which the [*Far Threshold*](#setShadowScreenSpaceThresholdFar_float_void) shall be used for screen-space shadows calculation. For the space between [*Near Threshold Distance*](#setShadowScreenSpaceThresholdFarDistance_float_void) and *Far Threshold Distance*, the threshold value is interpolated from [*Near Threshold*](#setShadowScreenSpaceThresholdNear_float_void) to [*Far Threshold*](#setShadowScreenSpaceThresholdFar_float_void).

## float getShadowScreenSpaceThresholdFarDistance () const

Returns the current distance from the camera after which the [Far Threshold](#setShadowScreenSpaceThresholdFar_float_void) is used for screen-space shadows calculation. You can set different Step Size and Threshold values for objects located near the camera and far away from it. Thus, full-scale shadows will be rendered for large objects located far away, while within the close distance range only shadows cast by small objects will be rendered. This feature is especially useful for locations where details are required for both short and long-distance ranges.
### Return value

Current distance from the camera (in units) after which the [*Far Threshold*](#setShadowScreenSpaceThresholdFar_float_void) shall be used for screen-space shadows calculation. For the space between [*Near Threshold Distance*](#setShadowScreenSpaceThresholdFarDistance_float_void) and *Far Threshold Distance*, the threshold value is interpolated from [*Near Threshold*](#setShadowScreenSpaceThresholdNear_float_void) to [*Far Threshold*](#setShadowScreenSpaceThresholdFar_float_void).
## void setShadowScreenSpaceThresholdNearDistance ( float distance )

Sets a new distance from the camera up to which the [Near Threshold](#setShadowScreenSpaceThresholdNear_float_void) is used for screen-space shadows calculation. You can set different Step Size and Threshold values for objects located near the camera and far away from it. Thus, full-scale shadows will be rendered for large objects located far away, while within the close distance range only shadows cast by small objects will be rendered. This feature is especially useful for locations where details are required for both short and long-distance ranges.
### Arguments

- *float* **distance** - The distance from the camera (in units) up to which the [Near Threshold](#setShadowScreenSpaceThresholdNear_float_void) shall be used for screen-space shadows calculation.

## float getShadowScreenSpaceThresholdNearDistance () const

Returns the current distance from the camera up to which the [Near Threshold](#setShadowScreenSpaceThresholdNear_float_void) is used for screen-space shadows calculation. You can set different Step Size and Threshold values for objects located near the camera and far away from it. Thus, full-scale shadows will be rendered for large objects located far away, while within the close distance range only shadows cast by small objects will be rendered. This feature is especially useful for locations where details are required for both short and long-distance ranges.
### Return value

Current distance from the camera (in units) up to which the [Near Threshold](#setShadowScreenSpaceThresholdNear_float_void) shall be used for screen-space shadows calculation.
## void setShadowScreenSpaceStepSizeFar ( float far )

Sets a new size of the step used to calculate screen-space shadows for the light source ([long distance range](#setShadowScreenSpaceStepSizeFarDistance_float_void)). This parameter can be used to adjust calculation of shadows for specific sizes of objects. You can set different Step Size and Threshold values for objects located near the camera and far away from it. Thus, full-scale shadows will be rendered for large objects located far away, while within the close distance range only shadows cast by small objects will be rendered. This feature is especially useful for locations where details are required for both short and long-distance ranges.
### Arguments

- *float* **far** - The screen-space [step size for long distance range](../../../objects/lights/parameters/index.md#far_step_size). The default value is 0.5. > **Notice:** Screen-space shadows must be enabled, see the [setShadowScreenSpace()](#setShadowScreenSpace_int_void) method.

## float getShadowScreenSpaceStepSizeFar () const

Returns the current size of the step used to calculate screen-space shadows for the light source ([long distance range](#setShadowScreenSpaceStepSizeFarDistance_float_void)). This parameter can be used to adjust calculation of shadows for specific sizes of objects. You can set different Step Size and Threshold values for objects located near the camera and far away from it. Thus, full-scale shadows will be rendered for large objects located far away, while within the close distance range only shadows cast by small objects will be rendered. This feature is especially useful for locations where details are required for both short and long-distance ranges.
### Return value

Current screen-space [step size for long distance range](../../../objects/lights/parameters/index.md#far_step_size). The default value is 0.5.
> **Notice:** Screen-space shadows must be enabled, see the [setShadowScreenSpace()](#setShadowScreenSpace_int_void) method.


## void setShadowScreenSpaceStepSizeNearDistance ( float distance )

Sets a new distance from the camera up to which the [Near Step Size](#setShadowScreenSpaceStepSizeNear_float_void) is used for screen-space shadows calculation. You can set different Step Size and Threshold values for objects located near the camera and far away from it. Thus, full-scale shadows will be rendered for large objects located far away, while within the close distance range only shadows cast by small objects will be rendered. This feature is especially useful for locations where details are required for both short and long-distance ranges.
### Arguments

- *float* **distance** - The distance from the camera (in units) up to which the [Near Step Size](#setShadowScreenSpaceStepSizeNear_float_void) shall be used for screen-space shadows calculation.

## float getShadowScreenSpaceStepSizeNearDistance () const

Returns the current distance from the camera up to which the [Near Step Size](#setShadowScreenSpaceStepSizeNear_float_void) is used for screen-space shadows calculation. You can set different Step Size and Threshold values for objects located near the camera and far away from it. Thus, full-scale shadows will be rendered for large objects located far away, while within the close distance range only shadows cast by small objects will be rendered. This feature is especially useful for locations where details are required for both short and long-distance ranges.
### Return value

Current distance from the camera (in units) up to which the [Near Step Size](#setShadowScreenSpaceStepSizeNear_float_void) shall be used for screen-space shadows calculation.
## void setShadowScreenSpaceStepSizeFarDistance ( float distance )

Sets a new distance from the camera after which the [Far Step Size](#setShadowScreenSpaceStepSizeFar_float_void) is used for screen-space shadows calculation. You can set different Step Size and Threshold values for objects located near the camera and far away from it. Thus, full-scale shadows will be rendered for large objects located far away, while within the close distance range only shadows cast by small objects will be rendered. This feature is especially useful for locations where details are required for both short and long-distance ranges.
### Arguments

- *float* **distance** - The distance from the camera (in units) after which the [Far Step Size](#setShadowScreenSpaceStepSizeFar_float_void) shall be used for screen-space shadows calculation. For the space between [*Near Step Size Distance*](#setShadowScreenSpaceStepSizeNearDistance_float_void) and *Far Step Size Distance*, the step size value is interpolated from [*Near Step Size*](#setShadowScreenSpaceStepSizeNear_float_void) to [*Far Step Size*](#setShadowScreenSpaceStepSizeFar_float_void).

## float getShadowScreenSpaceStepSizeFarDistance () const

Returns the current distance from the camera after which the [Far Step Size](#setShadowScreenSpaceStepSizeFar_float_void) is used for screen-space shadows calculation. You can set different Step Size and Threshold values for objects located near the camera and far away from it. Thus, full-scale shadows will be rendered for large objects located far away, while within the close distance range only shadows cast by small objects will be rendered. This feature is especially useful for locations where details are required for both short and long-distance ranges.
### Return value

Current distance from the camera (in units) after which the [Far Step Size](#setShadowScreenSpaceStepSizeFar_float_void) shall be used for screen-space shadows calculation. For the space between [*Near Step Size Distance*](#setShadowScreenSpaceStepSizeNearDistance_float_void) and *Far Step Size Distance*, the step size value is interpolated from [*Near Step Size*](#setShadowScreenSpaceStepSizeNear_float_void) to [*Far Step Size*](#setShadowScreenSpaceStepSizeFar_float_void).
## void setShadowColorTextureMode ( int mode )

Sets a new type of texture used to define light distribution.
> **Notice:** This feature is available only for Omni Lights and Projected Lights. See description of the modes in the corresponding articles for [Omni Lights](../../../objects/lights/omni/index.md#light_settings_mode) and [Projected Lights](../../../objects/lights/proj/index.md#light_settings_mode).


### Arguments

- *int* **mode** - The type of texture used to define light distribution. One of the following modes:

  - **0** - IES (Light distibution is defined by the IES profile).
  - **1** - SIMPLE (An arbitrary 2D texture is projected onto the scene).

## int getShadowColorTextureMode () const

Returns the current type of texture used to define light distribution.
> **Notice:** This feature is available only for Omni Lights and Projected Lights. See description of the modes in the corresponding articles for [Omni Lights](../../../objects/lights/omni/index.md#light_settings_mode) and [Projected Lights](../../../objects/lights/proj/index.md#light_settings_mode).


### Return value

Current type of texture used to define light distribution. One of the following modes:
- **0** - IES (Light distibution is defined by the IES profile).
- **1** - SIMPLE (An arbitrary 2D texture is projected onto the scene).


## void setShadowScreenSpaceTranslucentViewBias ( float bias )

Sets a new Sets a new *[View Bias](../../../objects/lights/parameters/index.md#sss_translucent_view_bias)* value for Screen-Space Shadows, that controls an effect of fuzziness for vegetation (e.g. simulating leaves of saintpaulia or providing a sponge-like look for tree crowns).
### Arguments

- *float* **bias** - The *View Bias* value to be set for Screen-Space Shadows:

  - By the value of 0 the effect is disabled
  - the value of 1 corresponds to the maximum effect.

## float getShadowScreenSpaceTranslucentViewBias () const

Returns the current Sets a new *[View Bias](../../../objects/lights/parameters/index.md#sss_translucent_view_bias)* value for Screen-Space Shadows, that controls an effect of fuzziness for vegetation (e.g. simulating leaves of saintpaulia or providing a sponge-like look for tree crowns).
### Return value

Current *View Bias* value to be set for Screen-Space Shadows:
- By the value of 0 the effect is disabled
- the value of 1 corresponds to the maximum effect.

## void setShadowScreenSpaceTranslucentDepthPerspectiveCompensation ( float compensation )

Sets a new *[Perspective Compensation](../../../objects/lights/parameters/index.md#sss_perspective_compensation)* value for Screen-Space Shadows, that defines whether the *[Translucent Depth](#setShadowScreenSpaceTranslucentDepth_float_void)* parameter depends on the distance from the camera to the surface or not. This effect is used to make tree crowns located far from the camera more translucent than the grass nearby.
### Arguments

- *float* **compensation** - The *Perspective Compensation* value to be set for the *[Translucent Depth](#setShadowScreenSpaceTranslucentDepth_float_void)* parameter of Screen-Space Shadows:

  - 0 - the *Translucent Depth* value does not depend on the distance from the camera to the surface.
  - 1 - the *Translucent Depth* value linearly depends on the distance from the camera to the surface.

## float getShadowScreenSpaceTranslucentDepthPerspectiveCompensation () const

Returns the current *[Perspective Compensation](../../../objects/lights/parameters/index.md#sss_perspective_compensation)* value for Screen-Space Shadows, that defines whether the *[Translucent Depth](#setShadowScreenSpaceTranslucentDepth_float_void)* parameter depends on the distance from the camera to the surface or not. This effect is used to make tree crowns located far from the camera more translucent than the grass nearby.
### Return value

Current *Perspective Compensation* value to be set for the *[Translucent Depth](#setShadowScreenSpaceTranslucentDepth_float_void)* parameter of Screen-Space Shadows:
- 0 - the *Translucent Depth* value does not depend on the distance from the camera to the surface.
- 1 - the *Translucent Depth* value linearly depends on the distance from the camera to the surface.

## void setShadowScreenSpaceTranslucentDepth ( float depth )

Sets a new *[Translucent Depth](../../../objects/lights/parameters/index.md#sss_translucent_depth)* value for Screen-Space Shadows indicating how much the light passes through screen-space shadows on translucent materials (with **Translucence** option enabled).
### Arguments

- *float* **depth** - The *Translucent Depth* value to be set for Screen-Space Shadows. Higher values ensure a deeper light penetration into translucent objects by shifting the shadow.

## float getShadowScreenSpaceTranslucentDepth () const

Returns the current *[Translucent Depth](../../../objects/lights/parameters/index.md#sss_translucent_depth)* value for Screen-Space Shadows indicating how much the light passes through screen-space shadows on translucent materials (with **Translucence** option enabled).
### Return value

Current *Translucent Depth* value to be set for Screen-Space Shadows. Higher values ensure a deeper light penetration into translucent objects by shifting the shadow.
## void setShadowFadeDistance ( float distance )

Sets a new distance from the camera after which the shadows gradually disappear.
### Arguments

- *float* **distance** - The distance from the camera after which the shadows start fading away.

## float getShadowFadeDistance () const

Returns the current distance from the camera after which the shadows gradually disappear.
### Return value

Current distance from the camera after which the shadows start fading away.
## void setOrder ( int order )

Sets a new light's [priority](../../../objects/lights/parameters/index.md#rendering_transparent_order) for rendering on transparent objects (glass, raindrops, etc.). Lower-priority lights may be randomly skipped for optimization purposes if the special globally-set [limit](../../../editor2/settings/render_settings/lights/index.md#forward_limits) is exceeded. A higher value means a higher priority.
### Arguments

- *int* **order** - The light's priority value for affecting transparent objects.

## int getOrder () const

Returns the current light's [priority](../../../objects/lights/parameters/index.md#rendering_transparent_order) for rendering on transparent objects (glass, raindrops, etc.). Lower-priority lights may be randomly skipped for optimization purposes if the special globally-set [limit](../../../editor2/settings/render_settings/lights/index.md#forward_limits) is exceeded. A higher value means a higher priority.
### Return value

Current light's priority value for affecting transparent objects.
## void setSpecularRoughnessOffset ( float offset )

Sets a new offset applied to the surface roughness when computing this light's specular contribution, in the [0; 1] range: the value acts as the minimum effective roughness for this light, making very glossy surfaces respond as if they were rougher. Raising it softens and spreads the light's specular highlights, which suppresses specular aliasing (bright specular flickering) caused by the light on glossy materials. The default value is 0.
### Arguments

- *float* **offset** - The roughness offset for the specular contribution of the light

## float getSpecularRoughnessOffset () const

Returns the current offset applied to the surface roughness when computing this light's specular contribution, in the [0; 1] range: the value acts as the minimum effective roughness for this light, making very glossy surfaces respond as if they were rougher. Raising it softens and spreads the light's specular highlights, which suppresses specular aliasing (bright specular flickering) caused by the light on glossy materials. The default value is 0.
### Return value

Current roughness offset for the specular contribution of the light
---

## void allocateLensFlares ( int num )

Allocate a buffer for a given number of lens flares to be created. With this function, memory can be allocated once rather than in chunks, making the creation faster.
> **Notice:** The lens flare effect must be [enabled](#setLensFlaresEnabled_int_void) for the light source. This feature is available only for: [Omni Lights](../../../api/library/lights/class.lightomni_usc.md), [Projected Lights](../../../api/library/lights/class.lightproj_usc.md) and [World Lights](../../../api/library/lights/class.lightworld_usc.md).


### Arguments

- *int* **num** - Number of lens flares to be created in the allocated buffer.

## void addLensFlare ( )

Add a new lens flare for the per-light lens flare effect.
> **Notice:** The lens flare effect must be [enabled](#setLensFlaresEnabled_int_void) for the light source. This feature is available only for: [Omni Lights](../../../api/library/lights/class.lightomni_usc.md), [Projected Lights](../../../api/library/lights/class.lightproj_usc.md) and [World Lights](../../../api/library/lights/class.lightworld_usc.md).


## LightLensFlare getLensFlare ( int num )

Returns the given lens flare from the list of the ones used for the per-light lens flare effect.
> **Notice:** The lens flare effect must be [enabled](#setLensFlaresEnabled_int_void) for the light source. This feature is available only for: [Omni Lights](../../../api/library/lights/class.lightomni_usc.md), [Projected Lights](../../../api/library/lights/class.lightproj_usc.md) and [World Lights](../../../api/library/lights/class.lightworld_usc.md).


### Arguments

- *int* **num** - Lens flare number.

### Return value

[Light lens flare](../../../api/library/lights/class.lightlensflare_usc.md) instance.
## void cloneLensFlare ( int num )

Creates a clone of the lens flare with a given number in the list of lens flares used for the per-light lens flare effect.
> **Notice:** The lens flare effect must be [enabled](#setLensFlaresEnabled_int_void) for the light source. This feature is available only for: [Omni Lights](../../../api/library/lights/class.lightomni_usc.md), [Projected Lights](../../../api/library/lights/class.lightproj_usc.md) and [World Lights](../../../api/library/lights/class.lightworld_usc.md).


### Arguments

- *int* **num** - Number of lens flare to be cloned.

## void removeLensFlare ( int num )

Removes the lens flare with a given number from the list of lens flares used for the per-light lens flare effect.
> **Notice:** The lens flare effect must be [enabled](#setLensFlaresEnabled_int_void) for the light source. This feature is available only for: [Omni Lights](../../../api/library/lights/class.lightomni_usc.md), [Projected Lights](../../../api/library/lights/class.lightproj_usc.md) and [World Lights](../../../api/library/lights/class.lightworld_usc.md).


### Arguments

- *int* **num** - Number of lens flare to be removed.

## void clearLensFlares ( )

Clears the list of lens flares used for the per-light lens flare effect.
> **Notice:** The lens flare effect must be [enabled](#setLensFlaresEnabled_int_void) for the light source. This feature is available only for: [Omni Lights](../../../api/library/lights/class.lightomni_usc.md), [Projected Lights](../../../api/library/lights/class.lightproj_usc.md) and [World Lights](../../../api/library/lights/class.lightworld_usc.md).


## vec4 calculateFinalColor ( )

Calculates the final color of the light source depending on the [calculation mode](#setColorMode_int_void) used.
### Return value

Resulting color of the light source.
## int saveStateLight ( Stream stream )

Saves the state of the light source to the specified stream.
**Example** using SaveStateLight() and [restoreStateLight()](#restoreStateLight_Stream_int) methods:


```cpp
// set the light state
light.setColorTemperature(15000.0f);

// save state
Blob blob_state = new Blob();
light.saveStateLight(blob_state);

// change state
light.setColorTemperature(27000.0f);

// restore state
blob_state.seekSet(0); // returning the carriage to the start of the blob
light.restoreStateLight(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - Stream instance.

### Return value

**1** if the state of the light source is saved successfully; otherwise, **0**.
## int restoreStateLight ( Stream stream )

Restores the state of the light source from the specified stream.
**Example** using [saveStateLight()](#saveStateLight_Stream_int) and restoreStateLight() methods:


```cpp
// set the light state
light.setColorTemperature(15000.0f);

// save state
Blob blob_state = new Blob();
light.saveStateLight(blob_state);

// change state
light.setColorTemperature(27000.0f);

// restore state
blob_state.seekSet(0); // returning the carriage to the start of the blob
light.restoreStateLight(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - Stream instance.

### Return value

**1** if the state of the light source is restored successfully; otherwise, **0**.
## int saveStateLensFlares ( Stream stream )

Saves the state of the per-light lens flare effect to the specified stream.
**Example** using saveStateLensFlares() and [restoreStateLensFlares()](#restoreStateLensFlares_Stream_int) methods:


```cpp
// set the lens flare state
lens_flare.setLensFlaresIntensity(0.75f);

// save state
Blob blob_state = new Blob();
lens_flare.saveStateLensFlares(blob_state);

// change state
lens_flare.setLensFlaresIntensity(0.25f);

// restore state
blob_state.seekSet(0); // returning the carriage to the start of the blob
lens_flare.restoreStateLensFlares(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - Stream instance.

### Return value

**1** if the state of the per-light lens flare effect is saved successfully; otherwise, **0**.
## int restoreStateLensFlares ( Stream stream )

Restores the state of the per-light lens flare effect from the specified stream.
**Example** using [saveStateLensFlares()](#saveStateLensFlares_Stream_int) and restoreStateLensFlares() methods:


```cpp
// set the lens flare state
lens_flare.setLensFlaresIntensity(0.75f);

// save state
Blob blob_state = new Blob();
lens_flare.saveStateLensFlares(blob_state);

// change state
lens_flare.setLensFlaresIntensity(0.25f);

// restore state
blob_state.seekSet(0); // returning the carriage to the start of the blob
lens_flare.restoreStateLensFlares(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - Stream instance.

### Return value

**1** if the state of the per-light lens flare effect is restored successfully; otherwise, **0**.
