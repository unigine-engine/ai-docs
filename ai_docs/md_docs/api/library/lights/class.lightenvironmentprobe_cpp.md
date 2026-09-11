# Unigine::LightEnvironmentProbe Class (CPP)

**Header:** #include <UnigineLights.h>

**Inherits from:** Light


This class allows creating and managing [Environment Probes](../../../objects/lights/envprobe/index.md).


## LightEnvironmentProbe Class

### Enums

## GRAB_DYNAMIC_FACES_PER_FRAME

| Name | Description |
|---|---|
| **GRAB_DYNAMIC_FACES_PER_FRAME_MODE_1** = 0 | Refresh only one face every frame. |
| **GRAB_DYNAMIC_FACES_PER_FRAME_MODE_2** = 1 | Refresh two faces every frame. |
| **GRAB_DYNAMIC_FACES_PER_FRAME_MODE_3** = 2 | Refresh three faces every frame. |
| **GRAB_DYNAMIC_FACES_PER_FRAME_MODE_4** = 3 | Refresh four faces every frame. |
| **GRAB_DYNAMIC_FACES_PER_FRAME_MODE_5** = 4 | Refresh five faces every frame. |
| **GRAB_DYNAMIC_FACES_PER_FRAME_MODE_6** = 5 | Refresh all six faces every frame. |

## GRAB_SUPERSAMPLING

| Name | Description |
|---|---|
| **GRAB_SUPERSAMPLING_MODE_1** = 0 | One sample per pixel. |
| **GRAB_SUPERSAMPLING_MODE_2** = 1 | Two samples per pixel. |
| **GRAB_SUPERSAMPLING_MODE_4** = 2 | Four samples per pixel. |
| **GRAB_SUPERSAMPLING_MODE_8** = 3 | Eight samples per pixel. |

## GRAB_RESOLUTION

| Name | Description |
|---|---|
| **GRAB_RESOLUTION_MODE_32** = 0 | 32-pixel texture resolution. |
| **GRAB_RESOLUTION_MODE_64** = 1 | 64-pixel texture resolution. |
| **GRAB_RESOLUTION_MODE_128** = 2 | 128-pixel texture resolution. |
| **GRAB_RESOLUTION_MODE_256** = 3 | 256-pixel texture resolution. |
| **GRAB_RESOLUTION_MODE_512** = 4 | 512-pixel texture resolution. |
| **GRAB_RESOLUTION_MODE_1024** = 5 | 1024-pixel texture resolution. |
| **GRAB_RESOLUTION_MODE_2048** = 6 | 2048-pixel texture resolution. |
| **GRAB_RESOLUTION_MODE_4096** = 7 | 4096-pixel texture resolution. |

## GRAB_MODE

| Name | Description |
|---|---|
| **GRAB_MODE_BAKED** = 0 | Reflections are static (the cubemap is pre-baked). |
| **GRAB_MODE_DYNAMIC** = 1 | Reflections are updated in realtime (the cubemap is generated dynamically). |

## SPECULAR_BRDF_MODE

| Name | Description |
|---|---|
| **SPECULAR_BRDF_MODE_BLINN** = 0 | Blinn-Phong reflection model. |
| **SPECULAR_BRDF_MODE_GGX** = 1 | GGX light distribution model. |

## PROJECTION_MODE

| Name | Description |
|---|---|
| **PROJECTION_MODE_SPHERE** = 0 | The spherical shape of projection. |
| **PROJECTION_MODE_BOX** = 1 | The box shape of projection. |
| **PROJECTION_MODE_RAYMARCHING** = 2 | The raymarching mode used to calculate reflections from the surrounding surfaces. |

## LAST_STEP_MODE

| Name | Description |
|---|---|
| **LAST_STEP_MODE_ENVIRONMENT_PROBE** = 0 | The cubemap used for the last step is the same as for all previous steps. |
| **LAST_STEP_MODE_ONLY_SKY** = 1 | The cubemap contains the sky and clouds only. |
| **LAST_STEP_MODE_UNDERLYING_PROBES** = 2 | Nothing is taken from the cubemap: at the last step the probe becomes partially transparent instead, letting the underlying lighting show through - voxel probes, planar probes, other environment probes, and the sky. |

## SECONDARY_BOUNCE_PROJECTION_MODE

| Name | Description |
|---|---|
| **SECONDARY_BOUNCE_PROJECTION_MODE_SPHERE** = 0 | Sphere projection. |
| **SECONDARY_BOUNCE_PROJECTION_MODE_RAYMARCHING** = 1 | Raymarching. |

## GRAB_DYNAMIC_REPROJECTION

Reprojection quality mode for a dynamic environment probe that refreshes fewer than 6 cube map faces per frame: the probe movement is compensated in the faces that were not redrawn this frame, so the reflection does not lag behind a moving probe.
| Name | Description |
|---|---|
| **GRAB_DYNAMIC_REPROJECTION_DISABLED** = 0 | No reprojection: the faces that were not redrawn this frame lag behind a moving probe (default). |
| **GRAB_DYNAMIC_REPROJECTION_LOW** = 1 | Low quality reprojection: the stale faces are reprojected to the new probe position using the stored depth. Cheaper than the high quality mode. |
| **GRAB_DYNAMIC_REPROJECTION_HIGH** = 2 | High quality reprojection: in addition to the low quality compensation, the depth of the previous frame is scattered into the new probe position, correcting parallax for geometry close to the probe. |

## GRAB_DYNAMIC_INTERLEAVED

Interleaved rendering mode for a dynamic environment probe: each updated cube map face is rendered at a reduced resolution and scattered into its own subset (phase) of the face texels, so the full-resolution face is reassembled over several updates.
| Name | Description |
|---|---|
| **GRAB_DYNAMIC_INTERLEAVED_DISABLED** = 0 | Interleaved rendering is disabled: each updated face is rendered at full resolution in one go (default). |
| **GRAB_DYNAMIC_INTERLEAVED_MODE_1X2** = 1 | The face is updated in 2 phases (a 1x2 interleave pattern): each update renders half of the face texels. |
| **GRAB_DYNAMIC_INTERLEAVED_MODE_2X2** = 2 | The face is updated in 4 phases (a 2x2 interleave pattern): each update renders a quarter of the face texels. |
| **GRAB_DYNAMIC_INTERLEAVED_MODE_4X4** = 3 | The face is updated in 16 phases (a 4x4 interleave pattern): each update renders one sixteenth of the face texels. |

## GRAB_DYNAMIC_INTERLEAVED_COLOR_CLAMPING

Color clamping mode suppressing ghosting between the interleaved phases of a dynamic environment probe: the texels of the phases that were not rendered this update are clamped to the color range of the freshly rendered one.
| Name | Description |
|---|---|
| **GRAB_DYNAMIC_INTERLEAVED_COLOR_CLAMPING_DISABLED** = 0 | No clamping: the phases keep their rendered colors until their own update. The cheapest mode; stale phases may lag behind changing content. |
| **GRAB_DYNAMIC_INTERLEAVED_COLOR_CLAMPING_ON_MOVEMENT** = 1 | The clamping is applied only while the probe is moving; the phases of a static probe accumulate unclamped (default). |
| **GRAB_DYNAMIC_INTERLEAVED_COLOR_CLAMPING_ALWAYS** = 2 | The clamping is applied on every update. |

### Members

## void setGrabMode ( LightEnvironmentProbe::GRAB_MODE mode )

Sets a new mode used to grab light and reflections for *Environment Probe*.
### Arguments

- *[LightEnvironmentProbe::GRAB_MODE](../../../api/library/lights/class.lightenvironmentprobe_cpp.md#GRAB_MODE)* **mode** - The grabbing mode to be set for the *Environment Probe*. One of the *GRAB_MODE* values.

## LightEnvironmentProbe::GRAB_MODE getGrabMode () const

Returns the current mode used to grab light and reflections for *Environment Probe*.
### Return value

Current grabbing mode to be set for the *Environment Probe*. One of the *GRAB_MODE* values.
## void setTextureFilePath ( const char * path )

Sets a new path to the reflection cube texture file used for the *Environment Probe*.
### Arguments

- *const char ** **path** - The path to a cube texture file.

## String getTextureFilePath () const

Returns the current path to the reflection cube texture file used for the *Environment Probe*.
### Return value

Current path to a cube texture file.
## void setAmbientContrast ( float contrast = 1.0f )

Sets a new ambient (Indirect Diffuse) contrast value for the *Environment Probe*.
### Arguments

- *float* **contrast** - The ambient contrast value within the [0.0f, 1.0f] range.

## float getAmbientContrast () const

Returns the current ambient (Indirect Diffuse) contrast value for the *Environment Probe*.
### Return value

Current ambient contrast value within the [0.0f, 1.0f] range.
## void setAmbientEnabled ( bool enabled )

Sets a new value indicating if ambient (Indirect Diffuse) lighting is enabled for the *Environment Probe*.
### Arguments

- *bool* **enabled** - Set **true** to enable ambient (Indirect Diffuse) lighting for the *Environment Probe*; **false** - to disable it.

## bool isAmbientEnabled () const

Returns the current value indicating if ambient (Indirect Diffuse) lighting is enabled for the *Environment Probe*.
### Return value

**true** if ambient (Indirect Diffuse) lighting for the *Environment Probe* is enabled ; otherwise **false**.
## void setSpecularEnabled ( bool enabled )

Sets a new value indicating if specular reflections are enabled for the *Environment Probe*.
### Arguments

- *bool* **enabled** - Set **true** to enable specular reflections for the *Environment Probe*; **false** - to disable it.

## bool isSpecularEnabled () const

Returns the current value indicating if specular reflections are enabled for the *Environment Probe*.
### Return value

**true** if specular reflections for the *Environment Probe* is enabled ; otherwise **false**.
## void setSphereReflectionParallax ( float parallax )

Sets a new parallax correction value for reflection cubemaps projected by the *Environment Probe*. by the minimum value of 0 reflection cubemaps are simply projected onto objects, and do not follow the viewer's perspective. This causes an unrealistic-looking reflection for most surfaces. Parallax correction enables to take camera's position into account.
> **Notice:** Parallax correction is not available for reflections on transparent objects.


### Arguments

- *float* **parallax** - The Parallax correction value to be set for reflection cubemaps projected by the *Environment Probe* in the range **[0;1]**:

  - By the minimum value of 0 parallax correction is disabled (reflections will look like objects are infinitely distant).
  - By the maximum value of 1 parallax correction is enabled (reflections will look like objects are at the distance close to the radius of the *Environment Probe*).
  - Values in-between represent a linear interpolation factor for parallax correction and are to be set when the *Environment Probe* is used to fit a medium or small object into the environment for additional correction.

## float getSphereReflectionParallax () const

Returns the current parallax correction value for reflection cubemaps projected by the *Environment Probe*. by the minimum value of 0 reflection cubemaps are simply projected onto objects, and do not follow the viewer's perspective. This causes an unrealistic-looking reflection for most surfaces. Parallax correction enables to take camera's position into account.
> **Notice:** Parallax correction is not available for reflections on transparent objects.


### Return value

Current Parallax correction value to be set for reflection cubemaps projected by the *Environment Probe* in the range **[0;1]**:
- By the minimum value of 0 parallax correction is disabled (reflections will look like objects are infinitely distant).
- By the maximum value of 1 parallax correction is enabled (reflections will look like objects are at the distance close to the radius of the *Environment Probe*).
- Values in-between represent a linear interpolation factor for parallax correction and are to be set when the *Environment Probe* is used to fit a medium or small object into the environment for additional correction.


## void setGrabZFar ( float zfar )

Sets a new distance to the far clipping plane used for image grabbing.
### Arguments

- *float* **zfar** - The distance to the far clipping plane.

## float getGrabZFar () const

Returns the current distance to the far clipping plane used for image grabbing.
### Return value

Current distance to the far clipping plane.
## void setGrabZNear ( float znear )

Sets a new distance to the near clipping plane used for image grabbing .
### Arguments

- *float* **znear** - The distance to the near clipping plane.

## float getGrabZNear () const

Returns the current distance to the near clipping plane used for image grabbing .
### Return value

Current distance to the near clipping plane.
## void setGrabViewportMask ( int mask )

Sets a new mask that specifies materials for which reflections are to be rendered in the viewport.
> **Notice:** The reflection viewport mask can be specified only for dynamic reflections (when the [Grab Mode](#setGrabMode_int_void) is set to DYNAMIC).


### Arguments

- *int* **mask** - The reflection viewport mask (integer, each bit of which is used to represent a mask).

## int getGrabViewportMask () const

Returns the current mask that specifies materials for which reflections are to be rendered in the viewport.
> **Notice:** The reflection viewport mask can be specified only for dynamic reflections (when the [Grab Mode](#setGrabMode_int_void) is set to DYNAMIC).


### Return value

Current reflection viewport mask (integer, each bit of which is used to represent a mask).
## void setGrabGGXMipmapsQuality ( Render::GGX_MIPMAPS_QUALITY quality )

Sets a new quality of GGX mipmaps.
### Arguments

- *[Render::GGX_MIPMAPS_QUALITY](../../../api/library/rendering/class.render_cpp.md#GGX_MIPMAPS_QUALITY)* **quality** - The quality of GGX mipmaps, one of the *[GGX_MIPMAPS_QUALITY](../../../api/library/rendering/class.render_cpp.md#GGX_MIPMAPS_QUALITY)*values.

## Render::GGX_MIPMAPS_QUALITY getGrabGGXMipmapsQuality () const

Returns the current quality of GGX mipmaps.
### Return value

Current quality of GGX mipmaps, one of the *[GGX_MIPMAPS_QUALITY](../../../api/library/rendering/class.render_cpp.md#GGX_MIPMAPS_QUALITY)*values.
## void setGrabSupersampling ( LightEnvironmentProbe::GRAB_SUPERSAMPLING supersampling = MODE_1 )

Sets a new supersampling mode for image grabbing.
### Arguments

- *[LightEnvironmentProbe::GRAB_SUPERSAMPLING](../../../api/library/lights/class.lightenvironmentprobe_cpp.md#GRAB_SUPERSAMPLING)* **supersampling** - The supersampling mode to be set, one of the GRAB_SUPERSAMPLING values.

## LightEnvironmentProbe::GRAB_SUPERSAMPLING getGrabSupersampling () const

Returns the current supersampling mode for image grabbing.
### Return value

Current supersampling mode to be set, one of the GRAB_SUPERSAMPLING values.
## void setGrabResolution ( LightEnvironmentProbe::GRAB_RESOLUTION resolution )

Sets a new resolution of the reflection mask in pixels.
### Arguments

- *[LightEnvironmentProbe::GRAB_RESOLUTION](../../../api/library/lights/class.lightenvironmentprobe_cpp.md#GRAB_RESOLUTION)* **resolution** - The resolution of the reflection mask in pixels, one of the GRAB_RESOLUTION values.

## LightEnvironmentProbe::GRAB_RESOLUTION getGrabResolution () const

Returns the current resolution of the reflection mask in pixels.
### Return value

Current resolution of the reflection mask in pixels, one of the GRAB_RESOLUTION values.
## void setGrabDynamicFacesPerFrame ( LightEnvironmentProbe::GRAB_DYNAMIC_FACES_PER_FRAME frame )

Sets a new update interval set for the cube texture used for dynamic reflections.
### Arguments

- *[LightEnvironmentProbe::GRAB_DYNAMIC_FACES_PER_FRAME](../../../api/library/lights/class.lightenvironmentprobe_cpp.md#GRAB_DYNAMIC_FACES_PER_FRAME)* **frame** - The value indicating the current update interval for the dynamic cube texture (faces per frame).

## LightEnvironmentProbe::GRAB_DYNAMIC_FACES_PER_FRAME getGrabDynamicFacesPerFrame () const

Returns the current update interval set for the cube texture used for dynamic reflections.
### Return value

Current value indicating the current update interval for the dynamic cube texture (faces per frame).
## void setBoxSize ( const Math:: vec3 && size )

Sets a new size for the *Environment Probe* when the *[Projection Mode](#setProjectionMode_int_void)* is set to Box.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &&* **size** - The *Environment Probe* box size along X, Y, and Z axes.

## Math:: vec3 & getBoxSize () const

Returns the current size for the *Environment Probe* when the *[Projection Mode](#setProjectionMode_int_void)* is set to Box.
### Return value

Current *Environment Probe* box size along X, Y, and Z axes.
## void setBoxGlossCorners ( float corners )

Sets a new value of the coefficient that controls glossiness of reflections in the corners of box projection.
> **Notice:** Available only when the *[Projection Mode](#setProjectionMode_int_void)* is set to Box.


### Arguments

- *float* **corners** - The value of the coefficient that controls glossiness of reflections in the corners of box projection.

## float getBoxGlossCorners () const

Returns the current value of the coefficient that controls glossiness of reflections in the corners of box projection.
> **Notice:** Available only when the *[Projection Mode](#setProjectionMode_int_void)* is set to Box.


### Return value

Current value of the coefficient that controls glossiness of reflections in the corners of box projection.
## void setBoxAmbientParallax ( float parallax )

Sets a new ambient parallax factor for box projection.
> **Notice:** Available only when the *[Projection Mode](#setProjectionMode_int_void)* is set to Box.


### Arguments

- *float* **parallax** - The ambient parallax factor.

## float getBoxAmbientParallax () const

Returns the current ambient parallax factor for box projection.
> **Notice:** Available only when the *[Projection Mode](#setProjectionMode_int_void)* is set to Box.


### Return value

Current ambient parallax factor.
## void setLocalSpace ( bool space )

Sets a new value indicating if local space (local coordinates) for the *Environment Probe* is enabled. Can be used for scenes with moving objects.
### Arguments

- *bool* **space** - Set **true** to enable local space (local coordinates) for the *Environment Probe*; **false** - to disable it.

## bool isLocalSpace () const

Returns the current value indicating if local space (local coordinates) for the *Environment Probe* is enabled. Can be used for scenes with moving objects.
### Return value

**true** if local space (local coordinates) for the *Environment Probe* is enabled ; otherwise **false**.
## void setCutoutByShadow ( bool shadow = false )

Sets a new value indicating if clipping of reflections occluded by obstacles is enabled. this feature uses the [depth texture](../../../api/library/lights/class.light_cpp.md#getBakedDepthTextureFilePath_cstr) grabbed for the *Environment Probe* to determine reflections that should be visible.
### Arguments

- *bool* **shadow** - Set **true** to enable clipping of reflections occluded by obstacles; **false** - to disable it.

## bool isCutoutByShadow () const

Returns the current value indicating if clipping of reflections occluded by obstacles is enabled. this feature uses the [depth texture](../../../api/library/lights/class.light_cpp.md#getBakedDepthTextureFilePath_cstr) grabbed for the *Environment Probe* to determine reflections that should be visible.
### Return value

**true** if clipping of reflections occluded by obstacles is enabled ; otherwise **false**.
## void setSkyCutout ( bool cutout = false )

Sets a new value indicating if sky cutout for image grabbing is enabled.
### Arguments

- *bool* **cutout** - Set **true** to enable sky cutout for image grabbing; **false** - to disable it.

## bool isSkyCutout () const

Returns the current value indicating if sky cutout for image grabbing is enabled.
### Return value

**true** if sky cutout for image grabbing is enabled ; otherwise **false**.
## void setAdditiveBlending ( bool blending = false )

Sets a new value indicating if additive blending is enabled for the *Environment Probe*. this option offers more flexibility in reflections control. you can use it to blend reflections of several Environment Probes together and control them separately.
### Arguments

- *bool* **blending** - Set **true** to enable additive blending mode for the *Environment Probe*; **false** - to disable it.

## bool isAdditiveBlending () const

Returns the current value indicating if additive blending is enabled for the *Environment Probe*. this option offers more flexibility in reflections control. you can use it to blend reflections of several Environment Probes together and control them separately.
### Return value

**true** if additive blending mode for the *Environment Probe* is enabled ; otherwise **false**.
## void setMultiplyBySkyColor ( bool color )

Sets a new Enables or disables sun color modulation for the *Environment Probe* (changing of the light in the *Environment Probe* as the sun color changes). This parameter can be used for outdoor-baked Environment Probes
### Arguments

- *bool* **color** - Set **true** to enable sun color modulation for the *Environment Probe*; **false** - to disable it.

## bool isMultiplyBySkyColor () const

Returns the current Enables or disables sun color modulation for the *Environment Probe* (changing of the light in the *Environment Probe* as the sun color changes). This parameter can be used for outdoor-baked Environment Probes
### Return value

**true** if sun color modulation for the *Environment Probe* is enabled ; otherwise **false**.
## void setProjectionMode ( LightEnvironmentProbe::PROJECTION_MODE mode )

Sets a new projection mode to be used for the *Environment Probe*.
### Arguments

- *[LightEnvironmentProbe::PROJECTION_MODE](../../../api/library/lights/class.lightenvironmentprobe_cpp.md#PROJECTION_MODE)* **mode** - The projection mode to be used for the *Environment Probe*, one of the *PROJECTION_MODE* values.

## LightEnvironmentProbe::PROJECTION_MODE getProjectionMode () const

Returns the current projection mode to be used for the *Environment Probe*.
### Return value

Current projection mode to be used for the *Environment Probe*, one of the *PROJECTION_MODE* values.
## void setGrabByBakeLighting ( bool lighting )

Sets a new value indicating whether the [cubemap texture](#setTextureFilePath_String_void) is to be modified by the [Bake Lighting Tool](../../../editor2/lighting/gi/bake_lighting/index.md).
### Arguments

- *bool* **lighting** - Set **true** to enable grabbing the cubemap texture with the Bake Lighting Tool; **false** - to disable it.

## bool isGrabByBakeLighting () const

Returns the current value indicating whether the [cubemap texture](#setTextureFilePath_String_void) is to be modified by the [Bake Lighting Tool](../../../editor2/lighting/gi/bake_lighting/index.md).
### Return value

**true** if grabbing the cubemap texture with the Bake Lighting Tool is enabled ; otherwise **false**.
## void setGrabDistanceScale ( float scale = 0.5f )

Sets a new distance scale for the reflection.
### Arguments

- *float* **scale** - The distance scale multiplier for the reflection.

## float getGrabDistanceScale () const

Returns the current distance scale for the reflection.
### Return value

Current distance scale multiplier for the reflection.
## void setAttenuationDistance ( const Math:: vec3 & distance )

Sets a new distance from the light source shape, at which the light source doesn't illuminate anything.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **distance** - The distance from the light source shape, at which the light source doesn't illuminate anything.

## Math:: vec3 getAttenuationDistance () const

Returns the current distance from the light source shape, at which the light source doesn't illuminate anything.
### Return value

Current distance from the light source shape, at which the light source doesn't illuminate anything.
## void setGrabBakeVisibilityLightmap ( bool lightmap )

Sets a new value indicating if baking of lightmapped surfaces to the *Environment Probe*. You can use this option together with [additive blending](#setAdditiveBlending_int_void) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make Environment Probes independent of each other and combine them to produce some sort of dynamic GI effect.
### Arguments

- *bool* **lightmap** - Set **true** to enable baking of lightmapped surfaces to the *Environment Probe*; **false** - to disable it.

## bool isGrabBakeVisibilityLightmap () const

Returns the current value indicating if baking of lightmapped surfaces to the *Environment Probe*. You can use this option together with [additive blending](#setAdditiveBlending_int_void) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make Environment Probes independent of each other and combine them to produce some sort of dynamic GI effect.
### Return value

**true** if baking of lightmapped surfaces to the *Environment Probe* is enabled ; otherwise **false**.
## void setGrabBakeVisibilityVoxelProbe ( bool probe )

Sets a new value indicating if *Voxel Probe* light sources are to be baked to the *Environment Probe*. you can use this option together with [additive blending](#setAdditiveBlending_int_void) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make Voxel Probes independent of each other and combine them to produce some sort of dynamic GI effect.
### Arguments

- *bool* **probe** - Set **true** to enable baking of Voxel Probes to the *Environment Probe*; **false** - to disable it.

## bool isGrabBakeVisibilityVoxelProbe () const

Returns the current value indicating if *Voxel Probe* light sources are to be baked to the *Environment Probe*. you can use this option together with [additive blending](#setAdditiveBlending_int_void) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make Voxel Probes independent of each other and combine them to produce some sort of dynamic GI effect.
### Return value

**true** if baking of Voxel Probes to the *Environment Probe* is enabled ; otherwise **false**.
## void setGrabBakeVisibilityEnvironmentProbe ( bool probe )

Sets a new value indicating if other *Environment Probe* light sources are to be baked to the *Environment Probe*. you can use this option together with [additive blending](#setAdditiveBlending_int_void) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make Voxel Probes independent of each other and combine them to produce some sort of dynamic GI effect.
### Arguments

- *bool* **probe** - Set **true** to enable baking of other Environment Probes to the *Environment Probe*; **false** - to disable it.

## bool isGrabBakeVisibilityEnvironmentProbe () const

Returns the current value indicating if other *Environment Probe* light sources are to be baked to the *Environment Probe*. you can use this option together with [additive blending](#setAdditiveBlending_int_void) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make Voxel Probes independent of each other and combine them to produce some sort of dynamic GI effect.
### Return value

**true** if baking of other Environment Probes to the *Environment Probe* is enabled ; otherwise **false**.
## void setGrabBakeVisibilityLightProj ( bool proj )

Sets a new value indicating if projected light sources are to be baked to the *Environment Probe*. You can use this option together with [additive blending](#setAdditiveBlending_int_void) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make Environment Probes independent of each other and combine them to produce some sort of dynamic GI effect.
### Arguments

- *bool* **proj** - Set **true** to enable baking of projected light sources to the *Environment Probe*; **false** - to disable it.

## bool isGrabBakeVisibilityLightProj () const

Returns the current value indicating if projected light sources are to be baked to the *Environment Probe*. You can use this option together with [additive blending](#setAdditiveBlending_int_void) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make Environment Probes independent of each other and combine them to produce some sort of dynamic GI effect.
### Return value

**true** if baking of projected light sources to the *Environment Probe* is enabled ; otherwise **false**.
## void setGrabBakeVisibilityLightOmni ( bool omni )

Sets a new value indicating if omni light sources are to be baked to the *Environment Probe*. You can use this option together with [additive blending](#setAdditiveBlending_int_void) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make Environment Probes independent of each other and combine them to produce some sort of dynamic GI effect.
### Arguments

- *bool* **omni** - Set **true** to enable baking of omni light sources to the *Environment Probe*; **false** - to disable it.

## bool isGrabBakeVisibilityLightOmni () const

Returns the current value indicating if omni light sources are to be baked to the *Environment Probe*. You can use this option together with [additive blending](#setAdditiveBlending_int_void) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make Environment Probes independent of each other and combine them to produce some sort of dynamic GI effect.
### Return value

**true** if baking of omni light sources to the *Environment Probe* is enabled ; otherwise **false**.
## void setGrabBakeVisibilityLightWorld ( bool world )

Sets a new value indicating if world light sources are to be baked to the *Environment Probe*. You can use this option together with [additive blending](#setAdditiveBlending_int_void) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make Environment Probes independent of each other and combine them to produce some sort of dynamic GI effect.
### Arguments

- *bool* **world** - Set **true** to enable baking of world light sources to the *Environment Probe*; **false** - to disable it.

## bool isGrabBakeVisibilityLightWorld () const

Returns the current value indicating if world light sources are to be baked to the *Environment Probe*. You can use this option together with [additive blending](#setAdditiveBlending_int_void) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make Environment Probes independent of each other and combine them to produce some sort of dynamic GI effect.
### Return value

**true** if baking of world light sources to the *Environment Probe* is enabled ; otherwise **false**.
## void setGrabBakeVisibilitySky ( bool sky )

Sets a new value indicating if lighting from the sky is to be baked to the *Environment Probe*. You can use this option together with [additive blending](#setAdditiveBlending_int_void) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make Environment Probes independent of each other and combine them to produce some sort of dynamic GI effect.
### Arguments

- *bool* **sky** - Set **true** to enable baking of lighting from the sky to the *Environment Probe*; **false** - to disable it.

## bool isGrabBakeVisibilitySky () const

Returns the current value indicating if lighting from the sky is to be baked to the *Environment Probe*. You can use this option together with [additive blending](#setAdditiveBlending_int_void) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make Environment Probes independent of each other and combine them to produce some sort of dynamic GI effect.
### Return value

**true** if baking of lighting from the sky to the *Environment Probe* is enabled ; otherwise **false**.
## void setGrabBakeVisibilityEmission ( bool emission )

Sets a new value indicating if emission light sources are to be baked to the *Environment Probe*. You can use this option together with [additive blending](#setAdditiveBlending_int_void) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make Environment Probes independent of each other and combine them to produce some sort of dynamic GI effect.
### Arguments

- *bool* **emission** - Set **true** to enable baking of emission light sources to the *Environment Probe*; **false** - to disable it.

## bool isGrabBakeVisibilityEmission () const

Returns the current value indicating if emission light sources are to be baked to the *Environment Probe*. You can use this option together with [additive blending](#setAdditiveBlending_int_void) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make Environment Probes independent of each other and combine them to produce some sort of dynamic GI effect.
### Return value

**true** if baking of emission light sources to the *Environment Probe* is enabled ; otherwise **false**.
## void setGrabBakeVisibilityHaze ( bool haze )

Sets a new value indicating if haze is to be baked to the *Environment Probe*. You can use this option together with [additive blending](#setAdditiveBlending_int_void) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make Environment Probes independent of each other and combine them to produce some sort of dynamic GI effect.
### Arguments

- *bool* **haze** - Set **true** to enable baking of haze to the *Environment Probe*; **false** - to disable it.

## bool isGrabBakeVisibilityHaze () const

Returns the current value indicating if haze is to be baked to the *Environment Probe*. You can use this option together with [additive blending](#setAdditiveBlending_int_void) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make Environment Probes independent of each other and combine them to produce some sort of dynamic GI effect.
### Return value

**true** if baking of haze to the *Environment Probe* is enabled ; otherwise **false**.
## void setGrabBakeVisibilityClouds ( bool clouds )

Sets a new value indicating if clouds to be baked to the *Environment Probe*. You can use this option together with [additive blending](#setAdditiveBlending_int_void) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make Environment Probes independent of each other and combine them to produce some sort of dynamic GI effect.
### Arguments

- *bool* **clouds** - Set **true** to enable baking of clouds to the *Environment Probe*; **false** - to disable it.

## bool isGrabBakeVisibilityClouds () const

Returns the current value indicating if clouds to be baked to the *Environment Probe*. You can use this option together with [additive blending](#setAdditiveBlending_int_void) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make Environment Probes independent of each other and combine them to produce some sort of dynamic GI effect.
### Return value

**true** if baking of clouds to the *Environment Probe* is enabled ; otherwise **false**.
## void setGrabEnvironmentReflectionIntensity ( float intensity )

Sets a new intensity of the environment reflection.
### Arguments

- *float* **intensity** - The intensity of the environment reflection.

## float getGrabEnvironmentReflectionIntensity () const

Returns the current intensity of the environment reflection.
### Return value

Current intensity of the environment reflection.
## void setGrabEnvironmentAmbientIntensity ( float intensity )

Sets a new intensity of the environment ambient lighting.
### Arguments

- *float* **intensity** - The intensity of the environment ambient lighting.

## float getGrabEnvironmentAmbientIntensity () const

Returns the current intensity of the environment ambient lighting.
### Return value

Current intensity of the environment ambient lighting.
## void setRaymarchingSpecularBRDF ( LightEnvironmentProbe::SPECULAR_BRDF_MODE brdf )

Sets a new light distribution model for matte surfaces. [GGX](#SPECULAR_BRDF_MODE) is more realistic, though increases noise and slightly reduces performance.
### Arguments

- *[LightEnvironmentProbe::SPECULAR_BRDF_MODE](../../../api/library/lights/class.lightenvironmentprobe_cpp.md#SPECULAR_BRDF_MODE)* **brdf** - The light distribution model for matte surfaces, one of the *[SPECULAR_BRDF_MODE](#SPECULAR_BRDF_MODE)* values. GGX is more realistic, though increases noise and slightly reduces performance.

## LightEnvironmentProbe::SPECULAR_BRDF_MODE getRaymarchingSpecularBRDF () const

Returns the current light distribution model for matte surfaces. [GGX](#SPECULAR_BRDF_MODE) is more realistic, though increases noise and slightly reduces performance.
### Return value

Current light distribution model for matte surfaces, one of the *[SPECULAR_BRDF_MODE](#SPECULAR_BRDF_MODE)* values. GGX is more realistic, though increases noise and slightly reduces performance.
## void setRaymarchingSpecularReplaceWithDiffuseRoughnessThreshold ( float threshold )

Sets a new rougness value starting from which *Indirect Specular* stops being calculated and is replaced with *Indirect Diffuse*. This setting is used to optimize matte reflections.
### Arguments

- *float* **threshold** - The rougness value starting from which *Indirect Specular* stops being calculated and is replaced with *Indirect Diffuse*.

## float getRaymarchingSpecularReplaceWithDiffuseRoughnessThreshold () const

Returns the current rougness value starting from which *Indirect Specular* stops being calculated and is replaced with *Indirect Diffuse*. This setting is used to optimize matte reflections.
### Return value

Current rougness value starting from which *Indirect Specular* stops being calculated and is replaced with *Indirect Diffuse*.
## void setRaymarchingSpecularInformationLostRaysMultiplier ( float multiplier )

Sets a new multiplier for the [number of rays](#RaymarchingSpecularNumRays) in the areas where the ghosting effect usually occurs. Increasing this value reduces the ghosting, but the more ghosting cases are, the more it affects performance.
### Arguments

- *float* **multiplier** - The multiplier for the [number of rays](#getRaymarchingSpecularNumRays_int) for the indirect specular in the areas where the ghosting effect usually occurs.

## float getRaymarchingSpecularInformationLostRaysMultiplier () const

Returns the current multiplier for the [number of rays](#RaymarchingSpecularNumRays) in the areas where the ghosting effect usually occurs. Increasing this value reduces the ghosting, but the more ghosting cases are, the more it affects performance.
### Return value

Current The multiplier for the [number of rays](#getRaymarchingSpecularNumRays_int) for the indirect specular in the areas where the ghosting effect usually occurs.
## void setRaymarchingSpecularMipOffset ( float offset )

Sets a new mipmap offset for the cubemap that is used for the specular reflections calculation. Increasing the value affects performance, lighting turns to be less detailed and realistic, small objects on the cubemap may be lost. The 0 value provides the most visually credible result, but more rays are required to eliminate the noise.
### Arguments

- *float* **offset** - The mipmap offset for the cubemap that is used for the specular reflections calculation. Increasing the value affects performance, lighting turns to be less detailed and realistic, small objects on the cubemap may be lost. The 0 value provides the most visually credible result, but more rays are required to eliminate the noise.

## float getRaymarchingSpecularMipOffset () const

Returns the current mipmap offset for the cubemap that is used for the specular reflections calculation. Increasing the value affects performance, lighting turns to be less detailed and realistic, small objects on the cubemap may be lost. The 0 value provides the most visually credible result, but more rays are required to eliminate the noise.
### Return value

Current mipmap offset for the cubemap that is used for the specular reflections calculation. Increasing the value affects performance, lighting turns to be less detailed and realistic, small objects on the cubemap may be lost. The 0 value provides the most visually credible result, but more rays are required to eliminate the noise.
## void setRaymarchingSpecularThresholdOcclusion ( float occlusion )

Sets a new value that limits imitation of environment cubemap occlusion in areas where information can't be obtained. Higher values make the effect less pronounced. This parameter is mainly used for indoor environment to correct false reflections on occluded areas (false reflections are replaced with black color). For outdoor environment, higher values of this parameter are recommended.
### Arguments

- *float* **occlusion** - The value that limits imitation of environment cubemap occlusion for the specular reflections in areas where information can't be obtained.

## float getRaymarchingSpecularThresholdOcclusion () const

Returns the current value that limits imitation of environment cubemap occlusion in areas where information can't be obtained. Higher values make the effect less pronounced. This parameter is mainly used for indoor environment to correct false reflections on occluded areas (false reflections are replaced with black color). For outdoor environment, higher values of this parameter are recommended.
### Return value

Current The value that limits imitation of environment cubemap occlusion for the specular reflections in areas where information can't be obtained.
## void setRaymarchingSpecularThreshold ( float threshold )

Sets a new threshold used for the specular reflections calculation to limit imitation of reflections in areas where information can't be obtained. Higher values make the effect less pronounced.
### Arguments

- *float* **threshold** - The threshold used for the specular reflections calculation to limit imitation of specular in areas where information can't be obtained.

## float getRaymarchingSpecularThreshold () const

Returns the current threshold used for the specular reflections calculation to limit imitation of reflections in areas where information can't be obtained. Higher values make the effect less pronounced.
### Return value

Current threshold used for the specular reflections calculation to limit imitation of specular in areas where information can't be obtained.
## void setRaymarchingSpecularNumStepsRoughnessThreshold ( float threshold )

Sets a new roughness value at which the [number of steps](#RaymarchingSpecularNumSteps) equals to 1. This is required for optimization, as calculating matte reflections as correctly as possible may be unnecessary.
### Arguments

- *float* **threshold** - The roughness value at which the [number of steps](#getRaymarchingSpecularNumSteps_int) equals to 1.

## float getRaymarchingSpecularNumStepsRoughnessThreshold () const

Returns the current roughness value at which the [number of steps](#RaymarchingSpecularNumSteps) equals to 1. This is required for optimization, as calculating matte reflections as correctly as possible may be unnecessary.
### Return value

Current roughness value at which the [number of steps](#getRaymarchingSpecularNumSteps_int) equals to 1.
## void setRaymarchingSpecularNumSteps ( int steps )

Sets a new number of steps per ray that are used for trace calculation. The number of steps defines accuracy of reflections and causes a reasonable performance impact. The higher the value, the more accurate obstacles between objects are taken into account.
### Arguments

- *int* **steps** - The number of steps per ray that are used for trace calculation.

## int getRaymarchingSpecularNumSteps () const

Returns the current number of steps per ray that are used for trace calculation. The number of steps defines accuracy of reflections and causes a reasonable performance impact. The higher the value, the more accurate obstacles between objects are taken into account.
### Return value

Current number of steps per ray that are used for trace calculation.
## void setRaymarchingSpecularNumRays ( int rays )

Sets a new number of rays per pixel that are used to calculate specular reflections from rough surfaces. Using more rays provides more precise reflection roughness calculation, however, it is more expensive.
### Arguments

- *int* **rays** - The number of rays per pixel that are used to calculate specular reflections from rough surfaces.

## int getRaymarchingSpecularNumRays () const

Returns the current number of rays per pixel that are used to calculate specular reflections from rough surfaces. Using more rays provides more precise reflection roughness calculation, however, it is more expensive.
### Return value

Current number of rays per pixel that are used to calculate specular reflections from rough surfaces.
## void setRaymarchingSpecularStepSize ( float size )

Sets a new size of the trace step used for the specular reflection calculation. Higher values result in longer traces (however, tiny objects may become missing), lower values produce more detailed reflections of tiny objects.
### Arguments

- *float* **size** - The size of the trace step used for the indirect specular reflection calculation.

## float getRaymarchingSpecularStepSize () const

Returns the current size of the trace step used for the specular reflection calculation. Higher values result in longer traces (however, tiny objects may become missing), lower values produce more detailed reflections of tiny objects.
### Return value

Current size of the trace step used for the indirect specular reflection calculation.
## void setRaymarchingDiffuseTranslucenceAnisotropy ( float anisotropy )

Sets a new value defining the extent of the light penetration through transparent surfaces.
### Arguments

- *float* **anisotropy** - The value defining the extent of the light penetration through transparent surfaces. The example values have the following effect:

  - 0 � light does not penetrate through surfaces.
  - 0.5 � light is distributed equally on both sides of the surface (along the ray direction and towards the light source)
  - 1.0 � all light passes through the surface along the ray direction.

## float getRaymarchingDiffuseTranslucenceAnisotropy () const

Returns the current value defining the extent of the light penetration through transparent surfaces.
### Return value

Current value defining the extent of the light penetration through transparent surfaces. The example values have the following effect:
- 0 � light does not penetrate through surfaces.
- 0.5 � light is distributed equally on both sides of the surface (along the ray direction and towards the light source)
- 1.0 � all light passes through the surface along the ray direction.


## void setRaymarchingDiffuseInformationLostRaysMultiplier ( float multiplier )

Sets a new multiplier for the [number of rays](#getRaymarchingDiffuseNumRays_int) for the indirect diffuse in the areas where the ghosting effect usually occurs. Increasing this value reduces the ghosting, but the more ghosting cases are, the more it affects performance.
### Arguments

- *float* **multiplier** - The multiplier for the [number of rays](#getRaymarchingDiffuseNumRays_int) for the indirect diffuse in the areas where the ghosting effect usually occurs.

## float getRaymarchingDiffuseInformationLostRaysMultiplier () const

Returns the current multiplier for the [number of rays](#getRaymarchingDiffuseNumRays_int) for the indirect diffuse in the areas where the ghosting effect usually occurs. Increasing this value reduces the ghosting, but the more ghosting cases are, the more it affects performance.
### Return value

Current multiplier for the [number of rays](#getRaymarchingDiffuseNumRays_int) for the indirect diffuse in the areas where the ghosting effect usually occurs.
## void setRaymarchingDiffuseMipOffset ( float offset )

Sets a new mipmap offset for the cubemap that is used for the diffuse light calculation. Increasing the value affects performance, lighting turns to be less detailed and realistic, small objects on the cubemap may be lost. The 0 value provides the most visually credible result, but more rays are required to eliminate the noise.
### Arguments

- *float* **offset** - The mipmap offset for the cubemap that is used for the diffuse light calculation.

## float getRaymarchingDiffuseMipOffset () const

Returns the current mipmap offset for the cubemap that is used for the diffuse light calculation. Increasing the value affects performance, lighting turns to be less detailed and realistic, small objects on the cubemap may be lost. The 0 value provides the most visually credible result, but more rays are required to eliminate the noise.
### Return value

Current mipmap offset for the cubemap that is used for the diffuse light calculation.
## void setRaymarchingDiffuseThresholdOcclusion ( float occlusion )

Sets a new value that limits imitation of environment cubemap occlusion in areas where information can't be obtained. Higher values make the effect less pronounced. This parameter is mainly used for indoor environment to correct false reflections on occluded areas (false reflections are replaced with black color). For outdoor environment, higher values of this parameter are recommended.
### Arguments

- *float* **occlusion** - The value that limits imitation of environment cubemap occlusion for the diffuse light in areas where information can't be obtained.

## float getRaymarchingDiffuseThresholdOcclusion () const

Returns the current value that limits imitation of environment cubemap occlusion in areas where information can't be obtained. Higher values make the effect less pronounced. This parameter is mainly used for indoor environment to correct false reflections on occluded areas (false reflections are replaced with black color). For outdoor environment, higher values of this parameter are recommended.
### Return value

Current value that limits imitation of environment cubemap occlusion for the diffuse light in areas where information can't be obtained.
## void setRaymarchingDiffuseThreshold ( float threshold )

Sets a new threshold used for the diffuse light calculation to limit imitation of reflections in areas where information can't be obtained. Higher values make the effect less pronounced.
### Arguments

- *float* **threshold** - The threshold used for the diffuse light calculation to limit imitation of diffuse light in areas where information can't be obtained.

## float getRaymarchingDiffuseThreshold () const

Returns the current threshold used for the diffuse light calculation to limit imitation of reflections in areas where information can't be obtained. Higher values make the effect less pronounced.
### Return value

Current threshold used for the diffuse light calculation to limit imitation of diffuse light in areas where information can't be obtained.
## void setRaymarchingDiffuseNumSteps ( int steps )

Sets a new number of steps per ray that are used for trace calculation. The number of steps defines accuracy of indirect light and causes a reasonable performance impact. The higher the value, the more accurate obstacles between objects are taken into account.
### Arguments

- *int* **steps** - The number of steps per ray that are used for trace calculation.

## int getRaymarchingDiffuseNumSteps () const

Returns the current number of steps per ray that are used for trace calculation. The number of steps defines accuracy of indirect light and causes a reasonable performance impact. The higher the value, the more accurate obstacles between objects are taken into account.
### Return value

Current number of steps per ray that are used for trace calculation.
## void setRaymarchingDiffuseNumRays ( int rays )

Sets a new number of rays per pixel that are used to calculate diffuse reflections from rough surfaces. Using more rays provides more precise reflection roughness calculation, however, it is more expensive.
### Arguments

- *int* **rays** - The number of rays per pixel that are used to calculate diffuse reflections from rough surfaces.

## int getRaymarchingDiffuseNumRays () const

Returns the current number of rays per pixel that are used to calculate diffuse reflections from rough surfaces. Using more rays provides more precise reflection roughness calculation, however, it is more expensive.
### Return value

Current number of rays per pixel that are used to calculate diffuse reflections from rough surfaces.
## void setRaymarchingDiffuseStepSize ( float size )

Sets a new size of the trace step used for the diffuse reflection calculation. Higher values result in longer traces (however, tiny objects may become missing), lower values produce more detailed reflections of tiny objects.
### Arguments

- *float* **size** - The size of the trace step used for the diffuse reflection calculation.

## float getRaymarchingDiffuseStepSize () const

Returns the current size of the trace step used for the diffuse reflection calculation. Higher values result in longer traces (however, tiny objects may become missing), lower values produce more detailed reflections of tiny objects.
### Return value

Current size of the trace step used for the diffuse reflection calculation.
## void setRaymarchingNoiseFramesNumber ( int number )

Sets a new number of variations of the noise pattern, which is changed every frame. Higher values result in a more dynamic noise effect, but a significant temporal accumulation of frames will make the image look like more rays are used. Smaller values result in a more static noise pattern.
### Arguments

- *int* **number** - The number of noise pattern variations

## int getRaymarchingNoiseFramesNumber () const

Returns the current number of variations of the noise pattern, which is changed every frame. Higher values result in a more dynamic noise effect, but a significant temporal accumulation of frames will make the image look like more rays are used. Smaller values result in a more static noise pattern.
### Return value

Current number of noise pattern variations
## void setRaymarchingSpecularNonLinearStepSize ( float size )

Sets a new raymarching step size adjustment value. The value of 0 means that the step size is the same for each step, and at the value of 1 each subsequent raymarching step is twice wider than the previous one.
### Arguments

- *float* **size** - The raymarching step size adjustment value.

## float getRaymarchingSpecularNonLinearStepSize () const

Returns the current raymarching step size adjustment value. The value of 0 means that the step size is the same for each step, and at the value of 1 each subsequent raymarching step is twice wider than the previous one.
### Return value

Current raymarching step size adjustment value.
## void setRaymarchingSpecularPerspectiveCompensation ( float compensation )

Sets a new perspective compensation for the raymarching step size. 0 means that the raymarching step size is bound to the World Space, and 1 means that it is bound to the Screen Space. As a result, at the value of 1, the ray length at the distance from the camera will be more than at a closer distance, which makes sense for large objects, but the details on small objects in the distance may will be lost.
### Arguments

- *float* **compensation** - The perspective compensation for the raymarching step size.

## float getRaymarchingSpecularPerspectiveCompensation () const

Returns the current perspective compensation for the raymarching step size. 0 means that the raymarching step size is bound to the World Space, and 1 means that it is bound to the Screen Space. As a result, at the value of 1, the ray length at the distance from the camera will be more than at a closer distance, which makes sense for large objects, but the details on small objects in the distance may will be lost.
### Return value

Current perspective compensation for the raymarching step size.
## void setRaymarchingSpecularReconstructionSamples ( int samples )

Sets a new number of iterations required for a more accurate detection of the screen-space ray-surface intersection for the indirect specular. Higher values define the intersection more precisely, however significantly affect performance.
### Arguments

- *int* **samples** - The number of iterations for the intersection detection.

## int getRaymarchingSpecularReconstructionSamples () const

Returns the current number of iterations required for a more accurate detection of the screen-space ray-surface intersection for the indirect specular. Higher values define the intersection more precisely, however significantly affect performance.
### Return value

Current number of iterations for the intersection detection.
## void setRaymarchingSpecularThresholdBinarySearch ( float search )

Sets a new threshold value used for the intersection detection that defines the depth of the ray penetration under the surface. Higher values may cause more false intersections, but make the process of intersection detection easier.
### Arguments

- *float* **search** - The threshold value used for the intersection detection that defines the depth of the ray penetration under the surface.

## float getRaymarchingSpecularThresholdBinarySearch () const

Returns the current threshold value used for the intersection detection that defines the depth of the ray penetration under the surface. Higher values may cause more false intersections, but make the process of intersection detection easier.
### Return value

Current threshold value used for the intersection detection that defines the depth of the ray penetration under the surface.
## void setRaymarchingDiffuseNonLinearStepSize ( float size )

Sets a new raymarching step size adjustment value. The value of 0 means that the step size is the same for each step, and at the value of 1 each subsequent raymarching step is twice wider than the previous one.
### Arguments

- *float* **size** - The raymarching step size adjustment value. The value of 0 means that the step size is the same for each step, and at the value of 1 each subsequent raymarching step is twice wider than the previous one.

## float getRaymarchingDiffuseNonLinearStepSize () const

Returns the current raymarching step size adjustment value. The value of 0 means that the step size is the same for each step, and at the value of 1 each subsequent raymarching step is twice wider than the previous one.
### Return value

Current raymarching step size adjustment value. The value of 0 means that the step size is the same for each step, and at the value of 1 each subsequent raymarching step is twice wider than the previous one.
## void setRaymarchingDiffusePerspectiveCompensation ( float compensation )

Sets a new perspective compensation for the raymarching step size. 0 means that the raymarching step size is bound to the World Space, and 1 means that it is bound to the Screen Space. As a result, at the value of 1, the ray length at the distance from the camera will be more than at a closer distance, which makes sense for large objects, but the details on small objects in the distance may will be lost.
### Arguments

- *float* **compensation** - The perspective compensation for the raymarching step size.

## float getRaymarchingDiffusePerspectiveCompensation () const

Returns the current perspective compensation for the raymarching step size. 0 means that the raymarching step size is bound to the World Space, and 1 means that it is bound to the Screen Space. As a result, at the value of 1, the ray length at the distance from the camera will be more than at a closer distance, which makes sense for large objects, but the details on small objects in the distance may will be lost.
### Return value

Current perspective compensation for the raymarching step size.
## void setRaymarchingDiffuseReconstructionSamples ( int samples )

Sets a new number of iterations required for a more accurate detection of the screen-space ray-surface intersection for the indirect diffuse. Higher values define the intersection more precisely, however significantly affect performance.
### Arguments

- *int* **samples** - The number of iterations for the intersection detection.

## int getRaymarchingDiffuseReconstructionSamples () const

Returns the current number of iterations required for a more accurate detection of the screen-space ray-surface intersection for the indirect diffuse. Higher values define the intersection more precisely, however significantly affect performance.
### Return value

Current number of iterations for the intersection detection.
## void setRaymarchingDiffuseThresholdBinarySearch ( float search )

Sets a new threshold value used for the intersection detection that defines the depth of the ray penetration under the surface. Higher values may cause more false intersections, but make the process of intersection detection easier.
### Arguments

- *float* **search** - The threshold value used for the intersection detection that defines the depth of the ray penetration under the surface.

## float getRaymarchingDiffuseThresholdBinarySearch () const

Returns the current threshold value used for the intersection detection that defines the depth of the ray penetration under the surface. Higher values may cause more false intersections, but make the process of intersection detection easier.
### Return value

Current threshold value used for the intersection detection that defines the depth of the ray penetration under the surface.
## void setRaymarchingAmbientOcclusionRadius ( float radius )

Sets a new radius of sample pixels used in the Ambient Occlusion effect, controlling the extent of the darkened area.
### Arguments

- *float* **radius** - The radius of sample pixels used in the Ambient Occlusion effect.

## float getRaymarchingAmbientOcclusionRadius () const

Returns the current radius of sample pixels used in the Ambient Occlusion effect, controlling the extent of the darkened area.
### Return value

Current radius of sample pixels used in the Ambient Occlusion effect.
## void setRaymarchingAmbientOcclusionIntensity ( float intensity )

Sets a new ambient occlusion intensity. Keep in mind that ambient occlusion doesn't exist in the real world, this is a method to imitate shadows between objects. For photorealistic visualization, we recommend keeping this value equal to 0.
### Arguments

- *float* **intensity** - The ambient occlusion intensity value.

## float getRaymarchingAmbientOcclusionIntensity () const

Returns the current ambient occlusion intensity. Keep in mind that ambient occlusion doesn't exist in the real world, this is a method to imitate shadows between objects. For photorealistic visualization, we recommend keeping this value equal to 0.
### Return value

Current ambient occlusion intensity value.
## void setRaymarchingLastStepMode ( LightEnvironmentProbe::LAST_STEP_MODE mode )

Sets a new cubemap to be used for the last raymarching step. The following modes are available:
- **Environment Probe** � the cubemap used for the last step is the same as for all previous steps.
- **Only Sky** � the cubemap contains the sky and clouds only. This option is designed to fix the incorrect parallax that may occur in reflections due to the infinite length of the last step.


### Arguments

- *[LightEnvironmentProbe::LAST_STEP_MODE](../../../api/library/lights/class.lightenvironmentprobe_cpp.md#LAST_STEP_MODE)* **mode** - The cubemap for the last step. One of the *[LAST_STEP_MODE](#LAST_STEP_MODE)* values.

## LightEnvironmentProbe::LAST_STEP_MODE getRaymarchingLastStepMode () const

Returns the current cubemap to be used for the last raymarching step. The following modes are available:
- **Environment Probe** � the cubemap used for the last step is the same as for all previous steps.
- **Only Sky** � the cubemap contains the sky and clouds only. This option is designed to fix the incorrect parallax that may occur in reflections due to the infinite length of the last step.


### Return value

Current cubemap for the last step. One of the *[LAST_STEP_MODE](#LAST_STEP_MODE)* values.
## void setRaymarchingSecondaryBounceProjectionMode ( LightEnvironmentProbe::SECONDARY_BOUNCE_PROJECTION_MODE mode )

Sets a new secondary bounce projection mode.
### Arguments

- *[LightEnvironmentProbe::SECONDARY_BOUNCE_PROJECTION_MODE](../../../api/library/lights/class.lightenvironmentprobe_cpp.md#SECONDARY_BOUNCE_PROJECTION_MODE)* **mode** - The secondary bounce projection mode. One of the *[SECONDARY_BOUNCE_PROJECTION_MODE](#SECONDARY_BOUNCE_PROJECTION_MODE)* values.

## LightEnvironmentProbe::SECONDARY_BOUNCE_PROJECTION_MODE getRaymarchingSecondaryBounceProjectionMode () const

Returns the current secondary bounce projection mode.
### Return value

Current secondary bounce projection mode. One of the *[SECONDARY_BOUNCE_PROJECTION_MODE](#SECONDARY_BOUNCE_PROJECTION_MODE)* values.
## void setReflectionCubicFiltering ( bool filtering )

Sets a new value indicating if bicubic interpolation for the Enviropment Probe cubemap is enabled instead of the standard bilinear interpolation. This effect is only applicable to reflected lighting and calculated if a pixel has a low *[Roughness](../../../content/materials/library/mesh_base/index.md#parameter_roughness)* value. Modifications are applied only to the first mip of the cubemap. The effect visually represents slight blurring of neighboring pixels. However, this is not antialiasing and might affect the visual quality of high-resolution probes.
This option may be combined with *[setSrgbModified()](../../...md#setSrgbModified_int_void)* to achieve a better gradient between pixels.


> **Notice:** - Enabling this option affects performance, thus it is recommended to enable it only for Environment Probes affecting a big number of reflective/mirror pixels, especially if it is a realtime low-resolution Probe.
> - For this option to have an effect on a **transparent** sufrace, the *[Reflection Cubic Filtering](../../../content/materials/library/mesh_base/index.md#option_reflection_cubic_filtering)* state should be enabled for the material (for non-transparent materials the option is applied automatically).
> - The option does not affect [Impostors](../../../editor2/tools/impostors_creator/index.md).


### Arguments

- *bool* **filtering** - Set **true** to enable bicubic interpolation for Enviropment Probe; **false** - to disable it.

## bool isReflectionCubicFiltering () const

Returns the current value indicating if bicubic interpolation for the Enviropment Probe cubemap is enabled instead of the standard bilinear interpolation. This effect is only applicable to reflected lighting and calculated if a pixel has a low *[Roughness](../../../content/materials/library/mesh_base/index.md#parameter_roughness)* value. Modifications are applied only to the first mip of the cubemap. The effect visually represents slight blurring of neighboring pixels. However, this is not antialiasing and might affect the visual quality of high-resolution probes.
This option may be combined with *[setSrgbModified()](../../...md#setSrgbModified_int_void)* to achieve a better gradient between pixels.


> **Notice:** - Enabling this option affects performance, thus it is recommended to enable it only for Environment Probes affecting a big number of reflective/mirror pixels, especially if it is a realtime low-resolution Probe.
> - For this option to have an effect on a **transparent** sufrace, the *[Reflection Cubic Filtering](../../../content/materials/library/mesh_base/index.md#option_reflection_cubic_filtering)* state should be enabled for the material (for non-transparent materials the option is applied automatically).
> - The option does not affect [Impostors](../../../editor2/tools/impostors_creator/index.md).


### Return value

**true** if bicubic interpolation for Enviropment Probe is enabled ; otherwise **false**.
## void setSrgbModified ( bool modified )

Sets a new value indicating if the *Environment Probe* cubemap or realtime calculation is converted to sRGB color model and modified to a lower dynamic range. Applying this option makes transition between the neighboring probe pixels smoother, which visually improves low-resolution probes or probes containing bright or constant pixels. Enabing or disabling this option requires rebaking of the static cubemap, otherwise lighting will be visually incorrect. If a static *Environment Probe* reuses a cubemap that has been baked with this option enabled, it should be enabled for this probe as well.
This option may be combined with *[setReflectionCubicFiltering()](../../...md#setReflectionCubicFiltering_int_void)* to achieve a better gradient between pixels.


### Arguments

- *bool* **modified** - Set **true** to enable conversion to sRGB and a lower dynamic range for cubemap or realtime calculation; **false** - to disable it.

## bool isSrgbModified () const

Returns the current value indicating if the *Environment Probe* cubemap or realtime calculation is converted to sRGB color model and modified to a lower dynamic range. Applying this option makes transition between the neighboring probe pixels smoother, which visually improves low-resolution probes or probes containing bright or constant pixels. Enabing or disabling this option requires rebaking of the static cubemap, otherwise lighting will be visually incorrect. If a static *Environment Probe* reuses a cubemap that has been baked with this option enabled, it should be enabled for this probe as well.
This option may be combined with *[setReflectionCubicFiltering()](../../...md#setReflectionCubicFiltering_int_void)* to achieve a better gradient between pixels.


### Return value

**true** if conversion to sRGB and a lower dynamic range for cubemap or realtime calculation is enabled ; otherwise **false**.
## void setGrabDynamicReprojection ( LightEnvironmentProbe::GRAB_DYNAMIC_REPROJECTION reprojection )

Sets a new reprojection mode compensating the probe movement in the cube map faces that were not redrawn this frame, one of the *GRAB_DYNAMIC_REPROJECTION_** values. Effective only for probes with the dynamic grab mode refreshing fewer than 6 faces per frame. Disabled by default.
### Arguments

- *[LightEnvironmentProbe::GRAB_DYNAMIC_REPROJECTION](../../../api/library/lights/class.lightenvironmentprobe_cpp.md#GRAB_DYNAMIC_REPROJECTION)* **reprojection** - The reprojection mode of the dynamic grab

## LightEnvironmentProbe::GRAB_DYNAMIC_REPROJECTION getGrabDynamicReprojection () const

Returns the current reprojection mode compensating the probe movement in the cube map faces that were not redrawn this frame, one of the *GRAB_DYNAMIC_REPROJECTION_** values. Effective only for probes with the dynamic grab mode refreshing fewer than 6 faces per frame. Disabled by default.
### Return value

Current reprojection mode of the dynamic grab
## void setGrabDynamicInterleaved ( LightEnvironmentProbe::GRAB_DYNAMIC_INTERLEAVED interleaved )

Sets a new interleaved rendering mode for the cube map faces updated by the dynamic grab, one of the *GRAB_DYNAMIC_INTERLEAVED_** values: each updated face is rendered at a reduced resolution and scattered into its own subset (phase) of the face texels, spreading the full-resolution refresh over several updates and reducing the per-update cost accordingly. Disabled by default.
### Arguments

- *[LightEnvironmentProbe::GRAB_DYNAMIC_INTERLEAVED](../../../api/library/lights/class.lightenvironmentprobe_cpp.md#GRAB_DYNAMIC_INTERLEAVED)* **interleaved** - The interleaved rendering mode of the dynamic grab

## LightEnvironmentProbe::GRAB_DYNAMIC_INTERLEAVED getGrabDynamicInterleaved () const

Returns the current interleaved rendering mode for the cube map faces updated by the dynamic grab, one of the *GRAB_DYNAMIC_INTERLEAVED_** values: each updated face is rendered at a reduced resolution and scattered into its own subset (phase) of the face texels, spreading the full-resolution refresh over several updates and reducing the per-update cost accordingly. Disabled by default.
### Return value

Current interleaved rendering mode of the dynamic grab
## void setGrabDynamicInterleavedColorClamping ( LightEnvironmentProbe::GRAB_DYNAMIC_INTERLEAVED_COLOR_CLAMPING clamping )

Sets a new color clamping mode suppressing ghosting between the interleaved phases of the dynamic grab, one of the *GRAB_DYNAMIC_INTERLEAVED_COLOR_CLAMPING_** values. Effective only when interleaved rendering is enabled via the **[getGrabDynamicInterleaved()](../../...md#getGrabDynamicInterleaved_int)** property. By default the clamping is applied on movement only.
### Arguments

- *[LightEnvironmentProbe::GRAB_DYNAMIC_INTERLEAVED_COLOR_CLAMPING](../../../api/library/lights/class.lightenvironmentprobe_cpp.md#GRAB_DYNAMIC_INTERLEAVED_COLOR_CLAMPING)* **clamping** - The color clamping mode of the interleaved dynamic grab

## LightEnvironmentProbe::GRAB_DYNAMIC_INTERLEAVED_COLOR_CLAMPING getGrabDynamicInterleavedColorClamping () const

Returns the current color clamping mode suppressing ghosting between the interleaved phases of the dynamic grab, one of the *GRAB_DYNAMIC_INTERLEAVED_COLOR_CLAMPING_** values. Effective only when interleaved rendering is enabled via the **[getGrabDynamicInterleaved()](../../...md#getGrabDynamicInterleaved_int)** property. By default the clamping is applied on movement only.
### Return value

Current color clamping mode of the interleaved dynamic grab
---

## static LightEnvironmentProbePtr create ( const Math:: vec4 & color , const Math:: vec3 & attenuation_distance , const char * name = 0 )

Constructor. Creates a new *Environment Probe* with cubemap modulation based on given parameters.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color of the *Environment Probe*.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **attenuation_distance** - Radii of the *Environment Probe*.
- *const char ** **name** - Path to a cube texture of the *Environment Probe*.

## static int type ( )

Returns the type of the node.
### Return value

[LightEnvironmentProbe](../../../api/library/nodes/class.node_cpp.md#LIGHT_ENVIRONMENT_PROBE) type identifier.
