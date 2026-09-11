# Unigine::LightEnvironmentProbe Class (CS)

**Inherits from:** Light


This class allows creating and managing [Environment Probes](../../../objects/lights/envprobe/index.md).


## LightEnvironmentProbe Class

### Enums

## GRAB_DYNAMIC_FACES_PER_FRAME

| Name | Description |
|---|---|
| **MODE_1** = 0 | Refresh only one face every frame. |
| **MODE_2** = 1 | Refresh two faces every frame. |
| **MODE_3** = 2 | Refresh three faces every frame. |
| **MODE_4** = 3 | Refresh four faces every frame. |
| **MODE_5** = 4 | Refresh five faces every frame. |
| **MODE_6** = 5 | Refresh all six faces every frame. |

## GRAB_SUPERSAMPLING

| Name | Description |
|---|---|
| **MODE_1** = 0 | One sample per pixel. |
| **MODE_2** = 1 | Two samples per pixel. |
| **MODE_4** = 2 | Four samples per pixel. |
| **MODE_8** = 3 | Eight samples per pixel. |

## GRAB_RESOLUTION

| Name | Description |
|---|---|
| **MODE_32** = 0 | 32-pixel texture resolution. |
| **MODE_64** = 1 | 64-pixel texture resolution. |
| **MODE_128** = 2 | 128-pixel texture resolution. |
| **MODE_256** = 3 | 256-pixel texture resolution. |
| **MODE_512** = 4 | 512-pixel texture resolution. |
| **MODE_1024** = 5 | 1024-pixel texture resolution. |
| **MODE_2048** = 6 | 2048-pixel texture resolution. |
| **MODE_4096** = 7 | 4096-pixel texture resolution. |

## GRAB_MODE

| Name | Description |
|---|---|
| **BAKED** = 0 | Reflections are static (the cubemap is pre-baked). |
| **DYNAMIC** = 1 | Reflections are updated in realtime (the cubemap is generated dynamically). |

## SPECULAR_BRDF_MODE

| Name | Description |
|---|---|
| **BLINN** = 0 | Blinn-Phong reflection model. |
| **GGX** = 1 | GGX light distribution model. |

## PROJECTION_MODE

| Name | Description |
|---|---|
| **SPHERE** = 0 | The spherical shape of projection. |
| **BOX** = 1 | The box shape of projection. |
| **RAYMARCHING** = 2 | The raymarching mode used to calculate reflections from the surrounding surfaces. |

## LAST_STEP_MODE

| Name | Description |
|---|---|
| **ENVIRONMENT_PROBE** = 0 | The cubemap used for the last step is the same as for all previous steps. |
| **ONLY_SKY** = 1 | The cubemap contains the sky and clouds only. |
| **UNDERLYING_PROBES** = 2 | Nothing is taken from the cubemap: at the last step the probe becomes partially transparent instead, letting the underlying lighting show through - voxel probes, planar probes, other environment probes, and the sky. |

## SECONDARY_BOUNCE_PROJECTION_MODE

| Name | Description |
|---|---|
| **SPHERE** = 0 | Sphere projection. |
| **RAYMARCHING** = 1 | Raymarching. |

## GRAB_DYNAMIC_REPROJECTION

Reprojection quality mode for a dynamic environment probe that refreshes fewer than 6 cube map faces per frame: the probe movement is compensated in the faces that were not redrawn this frame, so the reflection does not lag behind a moving probe.
| Name | Description |
|---|---|
| **DISABLED** = 0 | No reprojection: the faces that were not redrawn this frame lag behind a moving probe (default). |
| **LOW** = 1 | Low quality reprojection: the stale faces are reprojected to the new probe position using the stored depth. Cheaper than the high quality mode. |
| **HIGH** = 2 | High quality reprojection: in addition to the low quality compensation, the depth of the previous frame is scattered into the new probe position, correcting parallax for geometry close to the probe. |

## GRAB_DYNAMIC_INTERLEAVED

Interleaved rendering mode for a dynamic environment probe: each updated cube map face is rendered at a reduced resolution and scattered into its own subset (phase) of the face texels, so the full-resolution face is reassembled over several updates.
| Name | Description |
|---|---|
| **DISABLED** = 0 | Interleaved rendering is disabled: each updated face is rendered at full resolution in one go (default). |
| **MODE_1X2** = 1 | The face is updated in 2 phases (a 1x2 interleave pattern): each update renders half of the face texels. |
| **MODE_2X2** = 2 | The face is updated in 4 phases (a 2x2 interleave pattern): each update renders a quarter of the face texels. |
| **MODE_4X4** = 3 | The face is updated in 16 phases (a 4x4 interleave pattern): each update renders one sixteenth of the face texels. |

## GRAB_DYNAMIC_INTERLEAVED_COLOR_CLAMPING

Color clamping mode suppressing ghosting between the interleaved phases of a dynamic environment probe: the texels of the phases that were not rendered this update are clamped to the color range of the freshly rendered one.
| Name | Description |
|---|---|
| **DISABLED** = 0 | No clamping: the phases keep their rendered colors until their own update. The cheapest mode; stale phases may lag behind changing content. |
| **ON_MOVEMENT** = 1 | The clamping is applied only while the probe is moving; the phases of a static probe accumulate unclamped (default). |
| **ALWAYS** = 2 | The clamping is applied on every update. |

### Properties

## LightEnvironmentProbe.GRAB_MODE GrabMode

The mode used to grab light and reflections for *Environment Probe*.
## string TextureFilePath

The path to the reflection cube texture file used for the *Environment Probe*.
## float AmbientContrast

The ambient (Indirect Diffuse) contrast value for the *Environment Probe*.
## bool AmbientEnabled

The value indicating if ambient (Indirect Diffuse) lighting is enabled for the *Environment Probe*.
## bool SpecularEnabled

The value indicating if specular reflections are enabled for the *Environment Probe*.
## float SphereReflectionParallax

The parallax correction value for reflection cubemaps projected by the *Environment Probe*. by the minimum value of 0 reflection cubemaps are simply projected onto objects, and do not follow the viewer's perspective. This causes an unrealistic-looking reflection for most surfaces. Parallax correction enables to take camera's position into account.
> **Notice:** Parallax correction is not available for reflections on transparent objects.


## float GrabZFar

The distance to the far clipping plane used for image grabbing.
## float GrabZNear

The distance to the near clipping plane used for image grabbing .
## int GrabViewportMask

The mask that specifies materials for which reflections are to be rendered in the viewport.
> **Notice:** The reflection viewport mask can be specified only for dynamic reflections (when the [Grab Mode](#setGrabMode_int_void) is set to DYNAMIC).


## Render.GGX_MIPMAPS_QUALITY GrabGGXMipmapsQuality

The quality of GGX mipmaps.
## LightEnvironmentProbe.GRAB_SUPERSAMPLING GrabSupersampling

The supersampling mode for image grabbing.
## LightEnvironmentProbe.GRAB_RESOLUTION GrabResolution

The resolution of the reflection mask in pixels.
## LightEnvironmentProbe.GRAB_DYNAMIC_FACES_PER_FRAME GrabDynamicFacesPerFrame

The update interval set for the cube texture used for dynamic reflections.
## vec3 BoxSize

The size for the *Environment Probe* when the *[Projection Mode](#setProjectionMode_int_void)* is set to Box.
## float BoxGlossCorners

The value of the coefficient that controls glossiness of reflections in the corners of box projection.
> **Notice:** Available only when the *[Projection Mode](#setProjectionMode_int_void)* is set to Box.


## float BoxAmbientParallax

The ambient parallax factor for box projection.
> **Notice:** Available only when the *[Projection Mode](#setProjectionMode_int_void)* is set to Box.


## bool LocalSpace

The value indicating if local space (local coordinates) for the *Environment Probe* is enabled. Can be used for scenes with moving objects.
## bool CutoutByShadow

The value indicating if clipping of reflections occluded by obstacles is enabled. this feature uses the [depth texture](../../../api/library/lights/class.light_cs.md#getBakedDepthTextureFilePath_cstr) grabbed for the *Environment Probe* to determine reflections that should be visible.
## bool SkyCutout

The value indicating if sky cutout for image grabbing is enabled.
## bool AdditiveBlending

The value indicating if additive blending is enabled for the *Environment Probe*. this option offers more flexibility in reflections control. you can use it to blend reflections of several Environment Probes together and control them separately.
## bool MultiplyBySkyColor

The Enables or disables sun color modulation for the *Environment Probe* (changing of the light in the *Environment Probe* as the sun color changes). This parameter can be used for outdoor-baked Environment Probes
## LightEnvironmentProbe.PROJECTION_MODE ProjectionMode

The projection mode to be used for the *Environment Probe*.
## bool GrabByBakeLighting

The value indicating whether the [cubemap texture](#setTextureFilePath_String_void) is to be modified by the [Bake Lighting Tool](../../../editor2/lighting/gi/bake_lighting/index.md).
## float GrabDistanceScale

The distance scale for the reflection.
## vec3 AttenuationDistance

The distance from the light source shape, at which the light source doesn't illuminate anything.
## bool GrabBakeVisibilityLightmap

The value indicating if baking of lightmapped surfaces to the *Environment Probe*. You can use this option together with [additive blending](#setAdditiveBlending_int_void) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make Environment Probes independent of each other and combine them to produce some sort of dynamic GI effect.
## bool GrabBakeVisibilityVoxelProbe

The value indicating if *Voxel Probe* light sources are to be baked to the *Environment Probe*. you can use this option together with [additive blending](#setAdditiveBlending_int_void) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make Voxel Probes independent of each other and combine them to produce some sort of dynamic GI effect.
## bool GrabBakeVisibilityEnvironmentProbe

The value indicating if other *Environment Probe* light sources are to be baked to the *Environment Probe*. you can use this option together with [additive blending](#setAdditiveBlending_int_void) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make Voxel Probes independent of each other and combine them to produce some sort of dynamic GI effect.
## bool GrabBakeVisibilityLightProj

The value indicating if projected light sources are to be baked to the *Environment Probe*. You can use this option together with [additive blending](#setAdditiveBlending_int_void) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make Environment Probes independent of each other and combine them to produce some sort of dynamic GI effect.
## bool GrabBakeVisibilityLightOmni

The value indicating if omni light sources are to be baked to the *Environment Probe*. You can use this option together with [additive blending](#setAdditiveBlending_int_void) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make Environment Probes independent of each other and combine them to produce some sort of dynamic GI effect.
## bool GrabBakeVisibilityLightWorld

The value indicating if world light sources are to be baked to the *Environment Probe*. You can use this option together with [additive blending](#setAdditiveBlending_int_void) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make Environment Probes independent of each other and combine them to produce some sort of dynamic GI effect.
## bool GrabBakeVisibilitySky

The value indicating if lighting from the sky is to be baked to the *Environment Probe*. You can use this option together with [additive blending](#setAdditiveBlending_int_void) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make Environment Probes independent of each other and combine them to produce some sort of dynamic GI effect.
## bool GrabBakeVisibilityEmission

The value indicating if emission light sources are to be baked to the *Environment Probe*. You can use this option together with [additive blending](#setAdditiveBlending_int_void) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make Environment Probes independent of each other and combine them to produce some sort of dynamic GI effect.
## bool GrabBakeVisibilityHaze

The value indicating if haze is to be baked to the *Environment Probe*. You can use this option together with [additive blending](#setAdditiveBlending_int_void) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make Environment Probes independent of each other and combine them to produce some sort of dynamic GI effect.
## bool GrabBakeVisibilityClouds

The value indicating if clouds to be baked to the *Environment Probe*. You can use this option together with [additive blending](#setAdditiveBlending_int_void) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make Environment Probes independent of each other and combine them to produce some sort of dynamic GI effect.
## float GrabEnvironmentReflectionIntensity

The intensity of the environment reflection.
## float GrabEnvironmentAmbientIntensity

The intensity of the environment ambient lighting.
## LightEnvironmentProbe.SPECULAR_BRDF_MODE RaymarchingSpecularBRDF

The light distribution model for matte surfaces. [GGX](#SPECULAR_BRDF_MODE) is more realistic, though increases noise and slightly reduces performance.
## float RaymarchingSpecularReplaceWithDiffuseRoughnessThreshold

The rougness value starting from which *Indirect Specular* stops being calculated and is replaced with *Indirect Diffuse*. This setting is used to optimize matte reflections.
## float RaymarchingSpecularInformationLostRaysMultiplier

The multiplier for the [number of rays](#RaymarchingSpecularNumRays) in the areas where the ghosting effect usually occurs. Increasing this value reduces the ghosting, but the more ghosting cases are, the more it affects performance.
## float RaymarchingSpecularMipOffset

The mipmap offset for the cubemap that is used for the specular reflections calculation. Increasing the value affects performance, lighting turns to be less detailed and realistic, small objects on the cubemap may be lost. The 0 value provides the most visually credible result, but more rays are required to eliminate the noise.
## float RaymarchingSpecularThresholdOcclusion

The value that limits imitation of environment cubemap occlusion in areas where information can't be obtained. Higher values make the effect less pronounced. This parameter is mainly used for indoor environment to correct false reflections on occluded areas (false reflections are replaced with black color). For outdoor environment, higher values of this parameter are recommended.
## float RaymarchingSpecularThreshold

The threshold used for the specular reflections calculation to limit imitation of reflections in areas where information can't be obtained. Higher values make the effect less pronounced.
## float RaymarchingSpecularNumStepsRoughnessThreshold

The roughness value at which the [number of steps](#RaymarchingSpecularNumSteps) equals to 1. This is required for optimization, as calculating matte reflections as correctly as possible may be unnecessary.
## int RaymarchingSpecularNumSteps

The number of steps per ray that are used for trace calculation. The number of steps defines accuracy of reflections and causes a reasonable performance impact. The higher the value, the more accurate obstacles between objects are taken into account.
## int RaymarchingSpecularNumRays

The number of rays per pixel that are used to calculate specular reflections from rough surfaces. Using more rays provides more precise reflection roughness calculation, however, it is more expensive.
## float RaymarchingSpecularStepSize

The size of the trace step used for the specular reflection calculation. Higher values result in longer traces (however, tiny objects may become missing), lower values produce more detailed reflections of tiny objects.
## float RaymarchingDiffuseTranslucenceAnisotropy

The value defining the extent of the light penetration through transparent surfaces.
## float RaymarchingDiffuseInformationLostRaysMultiplier

The multiplier for the [number of rays](#getRaymarchingDiffuseNumRays_int) for the indirect diffuse in the areas where the ghosting effect usually occurs. Increasing this value reduces the ghosting, but the more ghosting cases are, the more it affects performance.
## float RaymarchingDiffuseMipOffset

The mipmap offset for the cubemap that is used for the diffuse light calculation. Increasing the value affects performance, lighting turns to be less detailed and realistic, small objects on the cubemap may be lost. The 0 value provides the most visually credible result, but more rays are required to eliminate the noise.
## float RaymarchingDiffuseThresholdOcclusion

The value that limits imitation of environment cubemap occlusion in areas where information can't be obtained. Higher values make the effect less pronounced. This parameter is mainly used for indoor environment to correct false reflections on occluded areas (false reflections are replaced with black color). For outdoor environment, higher values of this parameter are recommended.
## float RaymarchingDiffuseThreshold

The threshold used for the diffuse light calculation to limit imitation of reflections in areas where information can't be obtained. Higher values make the effect less pronounced.
## int RaymarchingDiffuseNumSteps

The number of steps per ray that are used for trace calculation. The number of steps defines accuracy of indirect light and causes a reasonable performance impact. The higher the value, the more accurate obstacles between objects are taken into account.
## int RaymarchingDiffuseNumRays

The number of rays per pixel that are used to calculate diffuse reflections from rough surfaces. Using more rays provides more precise reflection roughness calculation, however, it is more expensive.
## float RaymarchingDiffuseStepSize

The size of the trace step used for the diffuse reflection calculation. Higher values result in longer traces (however, tiny objects may become missing), lower values produce more detailed reflections of tiny objects.
## int RaymarchingNoiseFramesNumber

The number of variations of the noise pattern, which is changed every frame. Higher values result in a more dynamic noise effect, but a significant temporal accumulation of frames will make the image look like more rays are used. Smaller values result in a more static noise pattern.
## float RaymarchingSpecularNonLinearStepSize

The raymarching step size adjustment value. The value of 0 means that the step size is the same for each step, and at the value of 1 each subsequent raymarching step is twice wider than the previous one.
## float RaymarchingSpecularPerspectiveCompensation

The perspective compensation for the raymarching step size. 0 means that the raymarching step size is bound to the World Space, and 1 means that it is bound to the Screen Space. As a result, at the value of 1, the ray length at the distance from the camera will be more than at a closer distance, which makes sense for large objects, but the details on small objects in the distance may will be lost.
## int RaymarchingSpecularReconstructionSamples

The number of iterations required for a more accurate detection of the screen-space ray-surface intersection for the indirect specular. Higher values define the intersection more precisely, however significantly affect performance.
## float RaymarchingSpecularThresholdBinarySearch

The threshold value used for the intersection detection that defines the depth of the ray penetration under the surface. Higher values may cause more false intersections, but make the process of intersection detection easier.
## float RaymarchingDiffuseNonLinearStepSize

The raymarching step size adjustment value. The value of 0 means that the step size is the same for each step, and at the value of 1 each subsequent raymarching step is twice wider than the previous one.
## float RaymarchingDiffusePerspectiveCompensation

The perspective compensation for the raymarching step size. 0 means that the raymarching step size is bound to the World Space, and 1 means that it is bound to the Screen Space. As a result, at the value of 1, the ray length at the distance from the camera will be more than at a closer distance, which makes sense for large objects, but the details on small objects in the distance may will be lost.
## int RaymarchingDiffuseReconstructionSamples

The number of iterations required for a more accurate detection of the screen-space ray-surface intersection for the indirect diffuse. Higher values define the intersection more precisely, however significantly affect performance.
## float RaymarchingDiffuseThresholdBinarySearch

The threshold value used for the intersection detection that defines the depth of the ray penetration under the surface. Higher values may cause more false intersections, but make the process of intersection detection easier.
## float RaymarchingAmbientOcclusionRadius

The radius of sample pixels used in the Ambient Occlusion effect, controlling the extent of the darkened area.
## float RaymarchingAmbientOcclusionIntensity

The ambient occlusion intensity. Keep in mind that ambient occlusion doesn't exist in the real world, this is a method to imitate shadows between objects. For photorealistic visualization, we recommend keeping this value equal to 0.
## LightEnvironmentProbe.LAST_STEP_MODE RaymarchingLastStepMode

The cubemap to be used for the last raymarching step. The following modes are available:
- **Environment Probe** � the cubemap used for the last step is the same as for all previous steps.
- **Only Sky** � the cubemap contains the sky and clouds only. This option is designed to fix the incorrect parallax that may occur in reflections due to the infinite length of the last step.


## LightEnvironmentProbe.SECONDARY_BOUNCE_PROJECTION_MODE RaymarchingSecondaryBounceProjectionMode

The secondary bounce projection mode.
## bool ReflectionCubicFiltering

The value indicating if bicubic interpolation for the Enviropment Probe cubemap is enabled instead of the standard bilinear interpolation. This effect is only applicable to reflected lighting and calculated if a pixel has a low *[Roughness](../../../content/materials/library/mesh_base/index.md#parameter_roughness)* value. Modifications are applied only to the first mip of the cubemap. The effect visually represents slight blurring of neighboring pixels. However, this is not antialiasing and might affect the visual quality of high-resolution probes.
This option may be combined with *[SrgbModified](../../...md#setSrgbModified_int_void)* to achieve a better gradient between pixels.


> **Notice:** - Enabling this option affects performance, thus it is recommended to enable it only for Environment Probes affecting a big number of reflective/mirror pixels, especially if it is a realtime low-resolution Probe.
> - For this option to have an effect on a **transparent** sufrace, the *[Reflection Cubic Filtering](../../../content/materials/library/mesh_base/index.md#option_reflection_cubic_filtering)* state should be enabled for the material (for non-transparent materials the option is applied automatically).
> - The option does not affect [Impostors](../../../editor2/tools/impostors_creator/index.md).


## bool SrgbModified

The value indicating if the *Environment Probe* cubemap or realtime calculation is converted to sRGB color model and modified to a lower dynamic range. Applying this option makes transition between the neighboring probe pixels smoother, which visually improves low-resolution probes or probes containing bright or constant pixels. Enabing or disabling this option requires rebaking of the static cubemap, otherwise lighting will be visually incorrect. If a static *Environment Probe* reuses a cubemap that has been baked with this option enabled, it should be enabled for this probe as well.
This option may be combined with *[ReflectionCubicFiltering](../../...md#setReflectionCubicFiltering_int_void)* to achieve a better gradient between pixels.


## LightEnvironmentProbe.GRAB_DYNAMIC_REPROJECTION GrabDynamicReprojection

The reprojection mode compensating the probe movement in the cube map faces that were not redrawn this frame, one of the *GRAB_DYNAMIC_REPROJECTION_** values. Effective only for probes with the dynamic grab mode refreshing fewer than 6 faces per frame. Disabled by default.
## LightEnvironmentProbe.GRAB_DYNAMIC_INTERLEAVED GrabDynamicInterleaved

The interleaved rendering mode for the cube map faces updated by the dynamic grab, one of the *GRAB_DYNAMIC_INTERLEAVED_** values: each updated face is rendered at a reduced resolution and scattered into its own subset (phase) of the face texels, spreading the full-resolution refresh over several updates and reducing the per-update cost accordingly. Disabled by default.
## LightEnvironmentProbe.GRAB_DYNAMIC_INTERLEAVED_COLOR_CLAMPING GrabDynamicInterleavedColorClamping

The color clamping mode suppressing ghosting between the interleaved phases of the dynamic grab, one of the *GRAB_DYNAMIC_INTERLEAVED_COLOR_CLAMPING_** values. Effective only when interleaved rendering is enabled via the **[GrabDynamicInterleaved](../../...md#getGrabDynamicInterleaved_int)** property. By default the clamping is applied on movement only.
### Members

---

## LightEnvironmentProbe ( vec4 color , vec3 attenuation_distance , string name = 0 )

Constructor. Creates a new *Environment Probe* with cubemap modulation based on given parameters.
### Arguments

- *vec4* **color** - Color of the *Environment Probe*.
- *vec3* **attenuation_distance** - Radii of the *Environment Probe*.
- *string* **name** - Path to a cube texture of the *Environment Probe*.

## static int type ( )

Returns the type of the node.
### Return value

[LightEnvironmentProbe](../../../api/library/nodes/class.node_cs.md#LIGHT_ENVIRONMENT_PROBE) type identifier.
