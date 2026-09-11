# Unigine.Light Class (CS)

**Inherits from:** Node


This base class is used to create light sources and shadows from them. The lights can be rendered as a simplified deferred lighting.


## Light Class

### Enums

## SHADOW_RESOLUTION

Resolution of the shadow map created for the light source. The higher the resolution, the smoother and more true to life the shadows, at the cost of higher memory consumption.
| Name | Description |
|---|---|
| **MODE_DEFAULT** = -1 | Default shadow map resolution (512�512). |
| **MODE_64** = MODE_DEFAULT + 1 | Shadow map resolution equals 64�64. |
| **MODE_128** = MODE_64 + 1 | Shadow map resolution equals 128�128. |
| **MODE_256** = MODE_128 + 1 | Shadow map resolution equals 256�256. |
| **MODE_512** = MODE_256 + 1 | Shadow map resolution equals 512�512. |
| **MODE_1024** = MODE_512 + 1 | Shadow map resolution equals 1024�1024. |
| **MODE_2048** = MODE_1024 + 1 | Shadow map resolution equals 2048�2048. |
| **MODE_4096** = MODE_2048 + 1 | Shadow map resolution equals 4096�4096. |
| **MODE_8192** = MODE_4096 + 1 | Shadow map resolution equals 8192�8192. |
| **MODE_16384** = MODE_8192 + 1 | Shadow map resolution equals 16384�16384. |

## SHADOW_PENUMBRA

Quality mode of the penumbra rendered for the light source. A penumbra simulates real-world shadows by keeping sharp contact shadows closer to the base and softening the farther the shadow stretches away; higher modes produce softer shadows.
| Name | Description |
|---|---|
| **GLOBAL** = -1 | Quality mode of shadow penumbra that is [set globally](../../../api/library/rendering/class.render_cs.md#setShadowsPenumbraMode_int_void) for all light sources is applied. |
| **DISABLED** = GLOBAL + 1 | Shadow penumbra is disabled. |
| **LOW** = DISABLED + 1 | Low quality of shadow penumbra. |
| **MEDIUM** = LOW + 1 | Medium quality of shadow penumbra. |
| **HIGH** = MEDIUM + 1 | High quality of shadow penumbra. |
| **ULTRA** = HIGH + 1 | Ultra quality of shadow penumbra. |

## SHADOW_FILTER

Quality mode of the filtering used for shadows from the light source. Filtering reduces the stair-step effect at the edges of shadows; higher modes produce smoother edges.
| Name | Description |
|---|---|
| **GLOBAL** = -1 | Quality mode of shadow filtering that is [set globally](../../../api/library/rendering/class.render_cs.md#setShadowsFilterMode_int_void) is applied. |
| **DISABLED** = GLOBAL + 1 | Shadow filtering is disabled. |
| **LOW** = DISABLED + 1 | Low quality of shadow filtering. |
| **MEDIUM** = LOW + 1 | Medium quality of shadow filtering. |
| **HIGH** = MEDIUM + 1 | High quality of shadow filtering. |
| **ULTRA** = HIGH + 1 | Ultra quality of shadow filtering. |

## COLOR_MODE

Color calculation mode of the light source: the color is either set directly, or computed from the color temperature and multiplied by the color filter.
| Name | Description |
|---|---|
| **CLASSIC** = 0 | Classic color calculation mode, resulting color is defined by [Color](#setColor_vec4_void). |
| **TEMPERATURE** = 1 | Physically based color calculation mode, resulting color is calculated as: [ColorFilter](#setColorFilter_vec4_void) * (color obtained using the [ColorTemperature](#setColorTemperature_float_void) value). |

## SHADOW_MODE

Shadow casting mode for a light source with the static light mode enabled: either only baked shadows are rendered, or baked shadows from static surfaces are combined with a real-time shadow map for dynamic ones.
| Name | Description |
|---|---|
| **MIXED** = 0 | Shadow mode for omni and projected light sources with the static light mode enabled to render both static and dynamic shadows. |
| **STATIC** = 1 | Static shadow mode for omni and projected light sources with the static light mode enabled. |

## SHADOW_COLOR_MODE

Mode defining how the texture of an omni or projected light source is interpreted: either as an IES photometric profile defining the light distribution, or as a plain texture.
| Name | Description |
|---|---|
| **IES** = 0 | Light distibution is defined by the IES profile. |
| **SIMPLE** = 1 | An arbitrary 2D texture is projected onto the scene. |

## MODE

Mode of the light source defining its role in light baking: a dynamic light provides direct real-time lighting only and is turned off while light baking is being calculated, while a static light contributes to light baking and remains enabled all the time. For a static light, the types of shadows to be rendered are defined by the shadow mode.
| Name | Description |
|---|---|
| **DYNAMIC** = 0 | Real-time light rendering mode. The light source with this mode enabled is turned off while light baking is being calculated. Objects lit by such light cast only dynamic shadows. |
| **STATIC** = 1 | Mixed light rendering mode. The light source with this light mode enabled contributes to light baking and remains enabled all the time providing direct realtime lighting. Objects lit by such light can cast static or dynamic shadows depending on the shadow mode set for the source and the object surface. |

## SHAPE

Shape of the emitter of an omni or projected light source. A non-point shape turns the source into an area light that illuminates objects in different directions at once and provides a physically correct highlight on illuminated surfaces.
| Name | Description |
|---|---|
| **DEFAULT** = -1 | A point light source (light is emitted by an infinitely small point) set by default. |
| **POINT** = DEFAULT + 1 | A point light source (light is emitted by an infinitely small point). |
| **SPHERE** = POINT + 1 | A sphere-shaped light source. |
| **CAPSULE** = SPHERE + 1 | A capsule-shaped light source. |
| **RECTANGLE** = CAPSULE + 1 | A rectangular light source. Such light source produces the light and the speck in a form of a rounded rectangle. |

### Properties

## float ShadowScreenSpaceSoftness

The softness value of the screen-space shadows for the light source. Higher values provide softer shadows.
> **Notice:** Screen-space shadows must be enabled, see the [setShadowScreenSpace()](#setShadowScreenSpace_int_void) method.


## float ShadowScreenSpaceThresholdNear

The threshold value used to calculate screen-space shadows for the light source ([close distance range](#setShadowScreenSpaceThresholdNearDistance_float_void)). You can set different Step Size and Threshold values for objects located near the camera and far away from it. Thus, full-scale shadows will be rendered for large objects located far away, while within the close distance range only shadows cast by small objects will be rendered. This feature is especially useful for locations where details are required for both short and long-distance ranges.
> **Notice:** Screen-space shadows must be enabled, see the [setShadowScreenSpace()](#setShadowScreenSpace_int_void) method.


## float ShadowScreenSpaceStepSizeNear

The size of the step used to calculate screen-space shadows for the light source ([close distance range](#setShadowScreenSpaceStepSizeNearDistance_float_void)). This parameter can be used to adjust calculation of shadows for specific sizes of objects. You can set different Step Size and Threshold values for objects located near the camera and far away from it. Thus, full-scale shadows will be rendered for large objects located far away, while within the close distance range only shadows cast by small objects will be rendered. This feature is especially useful for locations where details are required for both short and long-distance ranges.
> **Notice:** Screen-space shadows must be enabled, see the [setShadowScreenSpace()](#setShadowScreenSpace_int_void) method.


## float ShadowScreenSpaceNoiseStep

The intensity of the step noise used to calculate screen-space shadows for the light source. Higher values reduce the banding effect more. However, this option significantly affects performance.
> **Notice:** Screen-space shadows must be enabled, see the [setShadowScreenSpace()](#setShadowScreenSpace_int_void) method.


## float ShadowScreenSpaceNoiseRay

The intensity of the ray noise used to calculate screen-space shadows for the light source. Higher values reduce the banding effect more. However, this option significantly affects performance.
> **Notice:** Screen-space shadows must be enabled, see the [setShadowScreenSpace()](#setShadowScreenSpace_int_void) method.


## int ShadowScreenSpaceNumSteps

The number of steps used to calculate screen-space shadows for the light source. Higher values, improve the quality of shadows more. However, this option significantly affects performance.
> **Notice:** Screen-space shadows must be enabled, see the [setShadowScreenSpace()](#setShadowScreenSpace_int_void) method.

## int ShadowScreenSpaceNumRays

The number of rays used to calculate screen-space shadows for the light source. Higher values, improve the quality of shadows more. However, this option significantly affects performance.
> **Notice:** Screen-space shadows must be enabled, see the [setShadowScreenSpace()](#setShadowScreenSpace_int_void) method.

## bool ShadowScreenSpace

The value indicating if screen-space shadows for the light source are enabled. With this option enabled, penumbras from the light source are calculated using the ray tracing algorithm.
## 🔒︎ Texture ShadowTexture

The depth texture (shadow map) of the light source.
## 🔒︎ Texture DynamicShadowColorTexture

The shadow texture of the light source used to render translucent shadows: G-channel stores depth values, R-channel - transparency values.
## 🔒︎ Texture BakedDepthTexture

The depth texture baked for the light source. this texture is available for [Static](#MODE_STATIC) light sources only.
> **Notice:** Static lights with [mixed shadow mode](#SHADOW_MODE_MIXED) enabled use a mixture of [dynamic](#getDynamicDepthTexture_Texture) and baked depth textures.


## string BakedDepthTextureFilePath

The path to a baked depth texture file, which stores a shadow map generated for the light source, when its mode is set to [MODE_STATIC](#MODE_STATIC). [EnvironmentProbes](../../../api/library/lights/class.lightenvironmentprobe_cs.md) use this texture for [cutting out reflections for occluded areas](../../../api/library/lights/class.lightenvironmentprobe_cs.md#setCutoutByShadow_int_void), where they should not be visible. This texture is baked automatically via the Editor or using [bake()](../../../api/library/lights/class.bakelighting_cs.md#bake_VECLightVoxelProbe_VECLightEnvironmentProbe_VECLight_VECObjectMeshStatic_VECint_void) or [bakeAll()](../../../api/library/lights/class.bakelighting_cs.md#bakeAll_int_int_int_int_void) methods.
## 🔒︎ Texture DynamicDepthTexture

The dynamic depth texture for the light source. This texture is available for the following types of light sources:
- [Dynamic](#MODE_DYNAMIC) lights.
- [Static](#MODE_STATIC) lights with [mixed shadow mode](#SHADOW_MODE_MIXED) enabled, that use a mixture of dynamic and baked depth textures.


## float ShadowPenumbra

The intensity of penumbra for the selected mode.
> **Notice:** This value is ignored when [penumbra rendering mode](#setShadowPenumbraMode_int_void) is set to *disabled*.


## Light.SHADOW_PENUMBRA ShadowPenumbraMode

The global quality mode used for rendering penumbra from the light source. this mode enables simulation of real-world shadows by keeping sharp contact shadows closer to the base and softening the farther the shadow stretches away. *Higher* values produce *softer* shadows.
## float ShadowFilter

The filtering intensity for the selected mode.
> **Notice:** This value is ignored when [filtering mode](#setShadowFilterMode_int_void) is set to *disabled*.


## Light.SHADOW_FILTER ShadowFilterMode

The filtering mode used to reduce the stair-step effect for soft shadows making the edges smoother.
## Light.SHADOW_MODE ShadowMode

The shadow mode for the light source in static mode. this shadow mode should be [aligned](../../../content/optimization/lights/index.md#static_light) with the [shadow mode](../../../api/library/objects/class.object_cs.md#setShadowMode_int_int_void) of the object surface in order to make this surface cast a shadow from the light source.
## Light.MODE Mode

The rendering mode for the light source. This option determines whether the light is to be rendered as a dynamic or static one.
## float ShadowNormalBias

The shadow bias that is achieved by shifting the surface on which the shadow falls. the surface is shifted along normals stored in the normal map. depending on the normal map of the surface, the shadow may differ for the same values of the normal bias.
## float ShadowBias

The constant offset of depth values in a shadow map.
- If the shadow acne appears, the bias value should be increased. This procedure eliminates the self-shadowing effect, as the points will appear closer to light source when compared to the map depth value.
- If the bias value is set too high, the shadow will look detached from the object casting it.


## Light.SHADOW_RESOLUTION ShadowResolution

The size of the shadow map created for the light source.
- The higher the resolution, the smoother and true to life the result is.
- The lower the resolution, the more blocky and jagged the shadows outline appears.


## bool Shadow

The value indicating if the light source casts shadows from surfaces with the [Cast Shadow](../../../api/library/rendering/class.material_cs.md#setCastShadow_int_void) material.
## float AttenuationPower

The attenuation power of the light. This parameter determines how fast the intensity decreases up to the attenuation distance set for the light source. If the attenuation equals to zero or is close to it, the edge between illuminated and non-illuminated areas is sharp.
## vec4 ColorFilter

The color multiplier for the light source color (calculated using the [color temperature](#setColorTemperature_float_void) value). This is used to imitate colored glass. The method takes effect only when the color mode is set to *Temperature*.
## float ColorTemperature

The light source temperature used for light color calculation.
## float Lux

The intensity of the light color (as perceived by the human eye) in lux. in unigine, all light sources have the [intensity](#setIntensity_float_void) of 1 by default, which is equal to 100000 lux.
## float Intensity

The multiplier of the light color used to control color intensity. the higher the value, the brighter the light is.
- The minimum value of 1 corresponds to the least saturated light color.
- The maximum value of 100 equals the most bright and intense color.


## vec4 Color

The color of the light source. The default is opaque white, **(1, 1, 1, 1)**. The method takes effect only when the *Classic* color mode is set.
## Light.COLOR_MODE ColorMode

The color calculation mode of the light source. Light source color can be defined by the [color](#setColor_vec4_void) value (classic mode) or by the [color temperature](#setColorTemperature_float_void) and [color filter](#setColorFilter_vec4_void) values (physically based mode).
## int ViewportMask

The bit mask for rendering into the viewport. The light is rendered, if its mask matches the player's one.
## int ShadowMask

The light mask for the light source.
For the shadow from an object's surface to be rendered for the light source, this mask must match the following ones (one bit, at least):

- [Shadow mask of the surface](../../../api/library/objects/class.object_cs.md#setShadowMask_int_int_void) of the object
- [Shadow mask of the material](../../../api/library/rendering/class.material_cs.md#setShadowMask_int_void) assigned to this surface


## bool RenderOnTransparent

The value indicating if the light from the source is rendered on transparent objects.
## bool RenderOnWater

The value indicating if the light from the source is rendered on water objects.
## float FadeDistance

The distance, at which the light source gradually disappears. This parameter enables to render the light with decreasing radiance after the [Visible distance](#setVisibleDistance_float_void) is past.
## float ShadowDistance

The distance, at which shadow from the light source starts fading out to nonexistence.
## float VisibleDistance

The distance, at which the light source starts fading. If the distance is set to infinity, the source is always rendered.
## 🔒︎ int NumLensFlares

The total number of lens flares used for the per-light lens flare effect.
> **Notice:** The lens flare effect must be [enabled](#setLensFlaresEnabled_int_void) for the light source. This feature is available only for: [Omni Lights](../../../api/library/lights/class.lightomni_cs.md), [Projected Lights](../../../api/library/lights/class.lightproj_cs.md) and [World Lights](../../../api/library/lights/class.lightworld_cs.md).


## bool LensFlaresUseLightColor

The value indicating if light color modulation is enabled for per-light lens flares. when enabled, the lens flares will have the same color as the light source.
> **Notice:** The lens flare effect must be [enabled](#setLensFlaresEnabled_int_void) for the light source. This feature is available only for: [Omni Lights](../../../api/library/lights/class.lightomni_cs.md), [Projected Lights](../../../api/library/lights/class.lightproj_cs.md) and [World Lights](../../../api/library/lights/class.lightworld_cs.md).


## vec3 LensFlaresWorldPositionOffset

The offset from the world position of the light source for the per-light lens flares. offset is not available for [World Lights](../../../api/library/lights/class.lightworld_cs.md).
> **Notice:** The lens flare effect must be [enabled](#setLensFlaresEnabled_int_void) for the light source. This feature is available only for: [Omni Lights](../../../api/library/lights/class.lightomni_cs.md), [Projected Lights](../../../api/library/lights/class.lightproj_cs.md) and [World Lights](../../../api/library/lights/class.lightworld_cs.md).


## float LensFlaresOcclusionFadeBorder

The lens flare occlusion fade border value for the cases when the light source becomes occluded by the edges of the screen.
> **Notice:** The lens flare effect must be [enabled](#setLensFlaresEnabled_int_void) for the light source. This feature is available only for: [Omni Lights](../../../api/library/lights/class.lightomni_cs.md), [Projected Lights](../../../api/library/lights/class.lightproj_cs.md) and [World Lights](../../../api/library/lights/class.lightworld_cs.md).


## float LensFlaresOcclusionFade

The lens flare occlusion fade value for the cases when the light source becomes occluded by an object.
> **Notice:** The lens flare effect must be [enabled](#setLensFlaresEnabled_int_void) for the light source. This feature is available only for: [Omni Lights](../../../api/library/lights/class.lightomni_cs.md), [Projected Lights](../../../api/library/lights/class.lightproj_cs.md) and [World Lights](../../../api/library/lights/class.lightworld_cs.md).


## float LensFlaresIntensity

The intensity of per-light lens flares.
> **Notice:** The lens flare effect must be [enabled](#setLensFlaresEnabled_int_void) for the light source. This feature is available only for: [Omni Lights](../../../api/library/lights/class.lightomni_cs.md), [Projected Lights](../../../api/library/lights/class.lightproj_cs.md) and [World Lights](../../../api/library/lights/class.lightworld_cs.md).


## string LensFlaresTextureName

The name of the texture used for the per-light lens flare effect. This texture stores images for all lens flares used to render lens flares.
> **Notice:** The lens flare effect must be [enabled](#setLensFlaresEnabled_int_void) for the light source. This feature is available only for: [Omni Lights](../../../api/library/lights/class.lightomni_cs.md), [Projected Lights](../../../api/library/lights/class.lightproj_cs.md) and [World Lights](../../../api/library/lights/class.lightworld_cs.md).


## bool LensFlaresEnabled

The value indicating if the per-light lens flare effect is enabled for the light source.
> **Notice:** - This feature is available only for: [Omni Lights](../../../api/library/lights/class.lightomni_cs.md), [Projected Lights](../../../api/library/lights/class.lightproj_cs.md) and [World Lights](../../../api/library/lights/class.lightworld_cs.md).
> - The maximum number of per-light lens flares that can be rendered is 32.


## float ShadowScreenSpaceThresholdFar

The threshold value used to calculate screen-space shadows for the light source ([long distance range](#setShadowScreenSpaceThresholdFarDistance_float_void)). You can set different Step Size and Threshold values for objects located near the camera and far away from it. Thus, full-scale shadows will be rendered for large objects located far away, while within the close distance range only shadows cast by small objects will be rendered. This feature is especially useful for locations where details are required for both short and long-distance ranges.
## float ShadowScreenSpaceThresholdFarDistance

The distance from the camera after which the [Far Threshold](#setShadowScreenSpaceThresholdFar_float_void) is used for screen-space shadows calculation. You can set different Step Size and Threshold values for objects located near the camera and far away from it. Thus, full-scale shadows will be rendered for large objects located far away, while within the close distance range only shadows cast by small objects will be rendered. This feature is especially useful for locations where details are required for both short and long-distance ranges.
## float ShadowScreenSpaceThresholdNearDistance

The distance from the camera up to which the [Near Threshold](#setShadowScreenSpaceThresholdNear_float_void) is used for screen-space shadows calculation. You can set different Step Size and Threshold values for objects located near the camera and far away from it. Thus, full-scale shadows will be rendered for large objects located far away, while within the close distance range only shadows cast by small objects will be rendered. This feature is especially useful for locations where details are required for both short and long-distance ranges.
## float ShadowScreenSpaceStepSizeFar

The size of the step used to calculate screen-space shadows for the light source ([long distance range](#setShadowScreenSpaceStepSizeFarDistance_float_void)). This parameter can be used to adjust calculation of shadows for specific sizes of objects. You can set different Step Size and Threshold values for objects located near the camera and far away from it. Thus, full-scale shadows will be rendered for large objects located far away, while within the close distance range only shadows cast by small objects will be rendered. This feature is especially useful for locations where details are required for both short and long-distance ranges.
## float ShadowScreenSpaceStepSizeNearDistance

The distance from the camera up to which the [Near Step Size](#setShadowScreenSpaceStepSizeNear_float_void) is used for screen-space shadows calculation. You can set different Step Size and Threshold values for objects located near the camera and far away from it. Thus, full-scale shadows will be rendered for large objects located far away, while within the close distance range only shadows cast by small objects will be rendered. This feature is especially useful for locations where details are required for both short and long-distance ranges.
## float ShadowScreenSpaceStepSizeFarDistance

The distance from the camera after which the [Far Step Size](#setShadowScreenSpaceStepSizeFar_float_void) is used for screen-space shadows calculation. You can set different Step Size and Threshold values for objects located near the camera and far away from it. Thus, full-scale shadows will be rendered for large objects located far away, while within the close distance range only shadows cast by small objects will be rendered. This feature is especially useful for locations where details are required for both short and long-distance ranges.
## Light.SHADOW_COLOR_MODE ShadowColorTextureMode

The type of texture used to define light distribution.
> **Notice:** This feature is available only for Omni Lights and Projected Lights. See description of the modes in the corresponding articles for [Omni Lights](../../../objects/lights/omni/index.md#light_settings_mode) and [Projected Lights](../../../objects/lights/proj/index.md#light_settings_mode).


## float ShadowScreenSpaceTranslucentViewBias

The Sets a new *[View Bias](../../../objects/lights/parameters/index.md#sss_translucent_view_bias)* value for Screen-Space Shadows, that controls an effect of fuzziness for vegetation (e.g. simulating leaves of saintpaulia or providing a sponge-like look for tree crowns).
## float ShadowScreenSpaceTranslucentDepthPerspectiveCompensation

The *[Perspective Compensation](../../../objects/lights/parameters/index.md#sss_perspective_compensation)* value for Screen-Space Shadows, that defines whether the *[Translucent Depth](#setShadowScreenSpaceTranslucentDepth_float_void)* parameter depends on the distance from the camera to the surface or not. This effect is used to make tree crowns located far from the camera more translucent than the grass nearby.
## float ShadowScreenSpaceTranslucentDepth

The *[Translucent Depth](../../../objects/lights/parameters/index.md#sss_translucent_depth)* value for Screen-Space Shadows indicating how much the light passes through screen-space shadows on translucent materials (with **Translucence** option enabled).
## float ShadowFadeDistance

The distance from the camera after which the shadows gradually disappear.
## int Order

The light's [priority](../../../objects/lights/parameters/index.md#rendering_transparent_order) for rendering on transparent objects (glass, raindrops, etc.). Lower-priority lights may be randomly skipped for optimization purposes if the special globally-set [limit](../../../editor2/settings/render_settings/lights/index.md#forward_limits) is exceeded. A higher value means a higher priority.
## float SpecularRoughnessOffset

The offset applied to the surface roughness when computing this light's specular contribution, in the [0; 1] range: the value acts as the minimum effective roughness for this light, making very glossy surfaces respond as if they were rougher. Raising it softens and spreads the light's specular highlights, which suppresses specular aliasing (bright specular flickering) caused by the light on glossy materials. The default value is 0.
### Members

---

## void AllocateLensFlares ( int num )

Allocate a buffer for a given number of lens flares to be created. With this function, memory can be allocated once rather than in chunks, making the creation faster.
> **Notice:** The lens flare effect must be [enabled](#setLensFlaresEnabled_int_void) for the light source. This feature is available only for: [Omni Lights](../../../api/library/lights/class.lightomni_cs.md), [Projected Lights](../../../api/library/lights/class.lightproj_cs.md) and [World Lights](../../../api/library/lights/class.lightworld_cs.md).


### Arguments

- *int* **num** - Number of lens flares to be created in the allocated buffer.

## void AddLensFlare ( )

Add a new lens flare for the per-light lens flare effect.
> **Notice:** The lens flare effect must be [enabled](#setLensFlaresEnabled_int_void) for the light source. This feature is available only for: [Omni Lights](../../../api/library/lights/class.lightomni_cs.md), [Projected Lights](../../../api/library/lights/class.lightproj_cs.md) and [World Lights](../../../api/library/lights/class.lightworld_cs.md).


## LightLensFlare GetLensFlare ( int num )

Returns the given lens flare from the list of the ones used for the per-light lens flare effect.
> **Notice:** The lens flare effect must be [enabled](#setLensFlaresEnabled_int_void) for the light source. This feature is available only for: [Omni Lights](../../../api/library/lights/class.lightomni_cs.md), [Projected Lights](../../../api/library/lights/class.lightproj_cs.md) and [World Lights](../../../api/library/lights/class.lightworld_cs.md).


### Arguments

- *int* **num** - Lens flare number.

### Return value

[Light lens flare](../../../api/library/lights/class.lightlensflare_cs.md) instance.
## void CloneLensFlare ( int num )

Creates a clone of the lens flare with a given number in the list of lens flares used for the per-light lens flare effect.
> **Notice:** The lens flare effect must be [enabled](#setLensFlaresEnabled_int_void) for the light source. This feature is available only for: [Omni Lights](../../../api/library/lights/class.lightomni_cs.md), [Projected Lights](../../../api/library/lights/class.lightproj_cs.md) and [World Lights](../../../api/library/lights/class.lightworld_cs.md).


### Arguments

- *int* **num** - Number of lens flare to be cloned.

## void RemoveLensFlare ( int num )

Removes the lens flare with a given number from the list of lens flares used for the per-light lens flare effect.
> **Notice:** The lens flare effect must be [enabled](#setLensFlaresEnabled_int_void) for the light source. This feature is available only for: [Omni Lights](../../../api/library/lights/class.lightomni_cs.md), [Projected Lights](../../../api/library/lights/class.lightproj_cs.md) and [World Lights](../../../api/library/lights/class.lightworld_cs.md).


### Arguments

- *int* **num** - Number of lens flare to be removed.

## void ClearLensFlares ( )

Clears the list of lens flares used for the per-light lens flare effect.
> **Notice:** The lens flare effect must be [enabled](#setLensFlaresEnabled_int_void) for the light source. This feature is available only for: [Omni Lights](../../../api/library/lights/class.lightomni_cs.md), [Projected Lights](../../../api/library/lights/class.lightproj_cs.md) and [World Lights](../../../api/library/lights/class.lightworld_cs.md).


## vec4 CalculateFinalColor ( )

Calculates the final color of the light source depending on the [calculation mode](#setColorMode_int_void) used.
### Return value

Resulting color of the light source.
## bool SaveStateLight ( Stream stream )

Saves the state of the light source to the specified stream.
**Example** using SaveStateLight() and [RestoreStateLight()](#restoreStateLight_Stream_int) methods:


```csharp
// set the light state
light.ColorTemperature = 15000.0f;

// save state
Blob blob_state = new Blob();
light.SaveStateLight(blob_state);

// change the node state
light.ColorTemperature = 27000.0f;

// restore state
blob_state.SeekSet(0);	// returning the carriage to the start of the blob
light.RestoreStateLight(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream instance.

### Return value

true if the state of the light source is saved successfully; otherwise, false.
## bool RestoreStateLight ( Stream stream )

Restores the state of the light source from the specified stream.
**Example** using [SaveStateLight()](#saveStateLight_Stream_int) and RestoreStateLight() methods:


```csharp
// set the light state
light.ColorTemperature = 15000.0f;

// save state
Blob blob_state = new Blob();
light.SaveStateLight(blob_state);

// change the node state
light.ColorTemperature = 27000.0f;

// restore state
blob_state.SeekSet(0);	// returning the carriage to the start of the blob
light.RestoreStateLight(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream instance.

### Return value

true if the state of the light source is restored successfully; otherwise, false.
## bool SaveStateLensFlares ( Stream stream )

Saves the state of the per-light lens flare effect to the specified stream.
**Example** using SaveStateLensFlares() and [RestoreStateLensFlares()](#restoreStateLensFlares_Stream_int) methods:


```csharp
// set the lens flare state
lens_flare.LensFlaresIntensity = 0.75f;

// save state
Blob blob_state = new Blob();
lens_flare.SaveStateLensFlares(blob_state);

// change the node state
lens_flare.LensFlaresIntensity = 0.25f;

// restore state
blob_state.SeekSet(0);	// returning the carriage to the start of the blob
lens_flare.RestoreStateLensFlares(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream instance.

### Return value

true if the state of the per-light lens flare effect is saved successfully; otherwise, false.
## bool RestoreStateLensFlares ( Stream stream )

Restores the state of the per-light lens flare effect from the specified stream.
**Example** using [SaveStateLensFlares()](#saveStateLensFlares_Stream_int) and RestoreStateLensFlares() methods:


```csharp
// set the lens flare state
lens_flare.LensFlaresIntensity = 0.75f;

// save state
Blob blob_state = new Blob();
lens_flare.SaveStateLensFlares(blob_state);

// change the node state
lens_flare.LensFlaresIntensity = 0.25f;

// restore state
blob_state.SeekSet(0);	// returning the carriage to the start of the blob
lens_flare.RestoreStateLensFlares(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream instance.

### Return value

true if the state of the per-light lens flare effect is restored successfully; otherwise, false.
