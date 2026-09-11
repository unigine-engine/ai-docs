# Unigine.Renderer Class (CS)

> **Notice:** This class is a singleton.


A basic interface for setting a renderer state (changing rendering passes parameters): pass shader uniforms, set *modelview* and *projection* matrices, etc. This class is used for rendering custom nodes (for example, a node inherited from *[ObjectExtern](../../../api/library/objects/class.objectextern_cs.md)*).


The *Renderer* class provides the following structures representing constant buffers:


## Renderer Class

### Enums

## RENDER_STEREO_EYE

Stereo eye enumeration.
| Name | Description |
|---|---|
| **NONE** = 0 | None of the stereo eyes. |
| **LEFT** = 1 | Left stereo eye. |
| **RIGHT** = 2 | Right stereo eye. |
| **LEFT_FOCUS** = 3 | Left eye focus view. |
| **RIGHT_FOCUS** = 4 | Right eye focus view. |

### Structs

## struct CBufferCamera

A structure that represents a buffer for storing camera parameters.
### Fields

- *mat4* **camera_projection** - Camera projection matrix.
- *mat4* **camera_iprojection** - Camera inverse projection matrix.
- *mat4* **oblique_frustum_plane** - World coordinates of the oblique frustum culling plane in the format *(Nx, Ny, Nz, D)*, where *Nx, Ny, Nz* are the coordinates of the plane normal, and *D* is the distance from the origin to the plane.
- *int* **is_oblique_frustum** - Flag indicating if the viewing frustum is oblique.
- *mat4* **projection** - Projection matrix.
- *mat4* **iprojection** - Inverse projection matrix.
- *mat4* **projection_screen** - Projection matrix for the screen space effect.
- *mat4* **iprojection_screen** - Inverse projection matrix for the screen space effect.
- *mat4* **imodelview** - Inverse view matrix.
- *mat4* **old_imodelview** - Inverse old view matrix used for rendering of the previous frame.
- *mat4* **old_imodelview_delta** - Delta of the old inverse view and inverse view matrices.
- *mat4* **modelview** - View matrix.
- *mat4* **old_modelview** - Old view matrix.
- *vec3* **camera_offset** - Camera additional transformation (offset). This transformation is applied after the view transformation. The offset does not affect the view matrix or the camera position.
- *vec3* **camera_position** - Camera position.
- *vec3* **camera_direction** - Inverted normalized camera direction vector.
- *vec3* **projection_row_0** - The first row of the camera projection matrix.
- *vec3* **projection_row_1** - The second row of the camera projection matrix.
- *vec3* **projection_row_2** - The third row of the camera projection matrix.
- *vec4* **modelview_projection_x** - The first row of the view projection matrix.
- *vec4* **modelview_projection_y** - The second row of the view projection matrix.
- *vec4* **modelview_projection_w** - The third row of the view projection matrix.
- *vec4* **modelview_projection_old_x** - The first row of the old view projection matrix used for rendering of the previous frame.
- *vec4* **modelview_projection_old_y** - The second row of the old view projection matrix used for rendering of the previous frame.
- *vec4* **modelview_projection_old_w** - The third row of the old view projection matrix used for rendering of the previous frame.
- *float* **camera_fov** - Camera vertical field of view.
- *int* **shadow_cascade_target** - Current shadow cascade used for rendering shadows.

## struct CBufferScattering

A structure that represents a buffer for storing [scattering parameters](../../../editor2/settings/render_settings/environment/index.md).
### Fields

- *vec3* **scattering_sun_dir** - Direction vector of the World light source having the Sun [scattering mode](../../../api/library/lights/class.lightworld_cs.md#SCATTERING).
- *vec3* **scattering_moon_dir** - Direction vector of the World light source having the Moon [scattering mode](../../../api/library/lights/class.lightworld_cs.md#SCATTERING).
- *float* **environment_ambient_intensity** - [Intensity](../../../api/library/rendering/class.renderenvironmentpreset_cs.md#getAmbientIntensity_float) of the environment ambient lighting. The higher the value, the more ambient lighting affects the environment. 0s means no environment reflection.
- *float* **environment_reflection_intensity** - [Intensity](../../../api/library/rendering/class.renderenvironmentpreset_cs.md#getReflectionIntensity_float) of the environment reflection.
- *float* **environment_sky_intensity** - [Intensity](../../../api/library/rendering/class.renderenvironmentpreset_cs.md#getSkyIntensity_float) of the environment sky. 0 means no environment sky.
- *vec4* **haze_color** - [Haze color](../../../api/library/rendering/class.renderenvironmentpreset_cs.md#getHazeColor_vec4).
- *float* **haze_max_distance** - [Distance](../../../api/library/rendering/class.renderenvironmentpreset_cs.md#getHazeMaxDistance_float) starting from which the haze becomes completely solid, so nothing will be seen behind.
- *float* **haze_density** - [Haze density](../../../api/library/rendering/class.renderenvironmentpreset_cs.md#getHazeDensity_float).
- *float* **haze_physical_start_height** - [Reference height](../../../api/library/rendering/class.renderenvironmentpreset_cs.md#getHazePhysicalStartHeight_float) value for the half visibility distance and half faloff height.
- *float* **haze_physical_density** - [Distance](../../../api/library/rendering/class.renderenvironmentpreset_cs.md#getHazePhysicalHalfVisibilityDistance_float) to the boundary at which the visibility comprises 50%. There is no zero-visibility in the real world, so the half-visibility boundary is used to adjust haze distance.
- *float* **haze_physical_falloff** - [Height](../../../api/library/rendering/class.renderenvironmentpreset_cs.md#getHazePhysicalHalfFalloffHeight_float) of the haze density gradient. The higher the value, the longer the haze desity reduces as the height grows, making the transition between the clear sky and haze smoother.
- *float* **haze_physical_zero_visibility_height** - Height at which the haze completely overlaps the scene.
- *float* **haze_physical_screen_space_global_illumination** - [Value](../../../api/library/rendering/class.render_cs.md#setEnvironmentHazeScreenSpaceGlobalIllumination_int_void) indicating if the Screen-Space Haze Global Illumination effect is enabled.
- *float* **haze_physical_ambient_light_intensity** - [Intensity](../../../api/library/rendering/class.renderenvironmentpreset_cs.md#getHazePhysicalAmbientLightIntensity_float) of the impact of the ambient lighting on haze (how much the ambient lighting affects the haze).
- *float* **haze_physical_ambient_color_saturation** - [Intensity](../../../api/library/rendering/class.renderenvironmentpreset_cs.md#getHazePhysicalAmbientColorSaturation_float) of the ambient color's contribution to the haze (how much the sunlight affects the haze).
- *float* **haze_physical_sun_light_intensity** - [Intensity](../../../api/library/rendering/class.renderenvironmentpreset_cs.md#getHazePhysicalSunLightIntensity_float) of the impact of the sunlight on haze (how much the sunlight affects the haze).
- *float* **haze_physical_sun_color_saturation** - [Intensity](../../../api/library/rendering/class.renderenvironmentpreset_cs.md#getHazePhysicalSunColorSaturation_float) of the impact of the sunlight on haze (how much the sunlight affects the haze).
- *float* **haze_scattering_mie_intensity** - Minimum [Mie intensity](../../../api/library/rendering/class.renderenvironmentpreset_cs.md#getHazeScatteringMieIntensity_float) value for geometry-occluded areas. This value specifies the fraction of Mie intensity visible when the surface is viewed from straight on.
- *float* **haze_scattering_mie_front_side_intensity** - [Falloff](../../../api/library/rendering/class.renderenvironmentpreset_cs.md#getHazeScatteringMieFrontSideIntensity_float) of the Fresnel effect for Mie intensity. This value is used to control occlusion of light from a World light source by the geometry.
- *float* **haze_scattering_mie_fresnel_power** - [Power](../../../api/library/rendering/class.renderenvironmentpreset_cs.md#getHazeScatteringMieFresnelPower_float) of the Fresnel effect for Mie visibility. Higher values will tighten up the areas affected, while lower ones will allow more areas to be affected by the Fresnel effect.
- *vec3* **sky_up** - Sky up vector.
- *float* **sky_altitude** - Sky altitude.
- *mat4* **sky_transform** - Sky transformation matrix.
- *vec3* **sun_color** - Sun color.
- *mat4* **sun_rotation** - Sun rotation matrix.
- *mat4* **moon_rotation** - Moon rotation matrix.

## struct CBufferTonemapper

A structure that represents a buffer for storing [tone mapping parameters](../../../editor2/settings/render_settings/color/index.md#tonemapper).
### Fields

- *vec4* **filmic_curve** - Vector of parameters for a [tone mapping curve](../../../editor2/settings/render_settings/color/index.md#filmic).
- *vec4* **filmic_white** - Parameter determining the brightness at which a pixel becomes pure white in the resulting image.
- *float* **filmic_saturation_recovery** - [Color saturation recovery](../../../api/library/rendering/class.render_cs.md#getFilmicSaturationRecovery_float) value for the filmic tonemapper.
- *float* **aces_white_clip** - [White clip](../../../api/library/rendering/class.render_cs.md#getACESWithReinhardWhiteClip_float) parameter for the ACES operator. Controls the cut-off point for white.
- *float* **aces_toe** - [Toe parameter](../../../api/library/rendering/class.render_cs.md#getACESToe_float) for the ACES operator. Controls the dark color. Higher values result in darker colors.
- *float* **aces_shoulder_angle** - [Shoulder angle parameter](../../../api/library/rendering/class.render_cs.md#getACESShoulderAngle_float) for the ACES operator. Controls how much overshoot should be added to the curve's shoulder.
- *float* **aces_shoulder_strength** - [Shoulder strength parameter](../../../api/library/rendering/class.render_cs.md#getACESShoulderStrength_float) for the ACES operator. Controls the strength of the transition between the curve's midsection and the curve's shoulder.
- *float* **aces_shoulder_length** - [Shoulder length parameter](../../../api/library/rendering/class.render_cs.md#getACESShoulderLength_float) for the ACES operator. Controls the amount of f-stops to add to the dynamic range of the curve. Defines how much of the highlights the curve takes into account.
- *float* **aces_with_reinhard_mix** - [ACES with Reinhard tone mapping](../../../api/library/rendering/class.render_cs.md#getACESWithReinhardMix_float) operator contribution.
- *float* **aces_with_reinhard_white_clip** - [White clip](../../../api/library/rendering/class.render_cs.md#getACESWithReinhardWhiteClip_float) parameter for the ACES with Reinhard operator. Controls the cut-off point for white.ACES with Reinhard operator's white clip.
- *float* **aces_with_reinhard_toe** - [Toe parameter](../../../api/library/rendering/class.render_cs.md#getACESWithReinhardToe_float) for the ACES with Reinhard operator. Controls the dark color. Higher values result in darker colors.
- *float* **aces_with_reinhard_shoulder_angle** - [Shoulder angle](../../../api/library/rendering/class.render_cs.md#getACESWithReinhardShoulderAngle_float) parameter for the ACES with Reinhard operator. Controls how much overshoot should be added to the curve's shoulder.
- *float* **aces_with_reinhard_shoulder_strength** - [Shoulder strength](../../../api/library/rendering/class.render_cs.md#getACESWithReinhardShoulderStrength_float) parameter for the ACES with Reinhard operator. Controls the strength of the transition between the curve's midsection and the curve's shoulder.
- *float* **aces_with_reinhard_shoulder_length** - [Shoulder length](../../../api/library/rendering/class.render_cs.md#getACESWithReinhardShoulderLength_float) parameter for the ACES with Reinhard operator. Controls the amount of f-stops to add to the dynamic range of the curve. Defines how much of the highlights the curve takes into account.
- *float* **reinhard_contribution** - [Reinhard tone mapping](../../../api/library/rendering/class.render_cs.md#getReinhardContribution_float) operator contribution.
- *float* **reinhard_luma_based_contribution** - [Reinhard Luma-Based tone mapping](../../../api/library/rendering/class.render_cs.md#getReinhardLumaBasedContribution_float) operator contribution. Controls the overall contribution that the Reinhard operator makes to the final color grading of the image.

### Properties

## 🔒︎ Texture TextureGBufferVelocity

The [Gbuffer velocity texture](../../../principles/render/sequence/index.md#velocity).
## 🔒︎ Texture TextureGBufferFeatures

The texture that stores intensity of the [screen-space bevel effect](../../../api/library/rendering/class.render_cs.md#setSSBevel_int_void).
## 🔒︎ Texture TextureGBufferNormal

The [Gbuffer normal texture](../../../principles/render/sequence/index.md#normal).
## 🔒︎ Texture TextureGBufferShading

The [Gbuffer shading texture](../../../principles/render/sequence/index.md#shading).
## 🔒︎ Texture TextureGBufferAlbedo

The [Gbuffer albedo texture](../../../principles/render/sequence/index.md#albedo).
## 🔒︎ Texture TextureClouds

The clouds texture. This texture is rendered during the separate clouds pass.
## 🔒︎ Texture TextureAutoWhiteBalance

The [auto white balance texture](../../../editor2/settings/render_settings/camera_effects/index.md#white_balance).
## 🔒︎ Texture TextureAutoExposure

The autoexposure texture.
## 🔒︎ Texture TextureDOFMask

The DoF mask texture. This texture is used at the [camera effects stage](../../../principles/render/sequence/index.md#dof).
## 🔒︎ Texture TextureSSCurvature

The texture used by the [Screen-Space Dirt (SSDirt) effect](../../../editor2/settings/render_settings/ssdirt/index.md).
## 🔒︎ Texture TextureSSR

The [SSR texture](../../../principles/render/sequence/index.md#ssr).
## 🔒︎ Texture TextureSSGI

The [SSGI texture](../../../principles/render/sequence/index.md#ssgi).
## 🔒︎ Texture TextureSSShadowShafts

The Screen-Space Shadow Shafts texture.
## 🔒︎ Texture TextureSSAO

The [SSAO texture](../../../principles/render/sequence/index.md#ssao).
## 🔒︎ Texture TextureBentNormal

The bent normal texture. This texture is used during the [Screen-Space Global Illumination stage](../../../principles/render/sequence/index.md#ssgi).
## 🔒︎ Texture TextureIndirectLights

The array texture storing contents of the [deferred reflections buffer](../../../principles/render/sequence/index.md#deferred_reflection). The texture contains two **RG11B10F** textures: the first layer stores the environment reflection color, and the second layer stores the environment ambient light.
## 🔒︎ Texture TextureDirectLights

The array texture storing contents of the [deferred light buffer](../../../principles/render/sequence/index.md#lights). The texture contains two **RG11B10F** textures: the first layer stores the diffuse light, and the second layer stores the specular light.
## 🔒︎ Texture TextureTransparentBlur

The transparent blur texture. This texture is rendered during the transparent blur pass.
## 🔒︎ Texture TextureRefractionMask

The [refraction](../../../principles/render/sequence/index.md#refraction_apply) mask texture.
## 🔒︎ Texture TextureRefraction

The [refraction texture](../../../principles/render/sequence/index.md#refraction).
## 🔒︎ Texture TextureAuxiliary

The [auxiliary texture](../../../principles/render/sequence/index.md#auxiliary).
## 🔒︎ Texture TextureLinearDepth

The texture that stores linear depth data.
## 🔒︎ Texture TextureOpacityDepth

The [opacity depth texture](../../../principles/render/sequence/index.md#depth_pre_pass).
## 🔒︎ Texture TextureCurrentDepth

The [depth texture](../../../principles/render/sequence/index.md#depth).
## 🔒︎ Texture TextureNormalUnpack

The texture that stores unpacked normals. Available for the following post-effects: SSR, SSGI, SSRTGI, Screen-Space Shadows.
## 🔒︎ Texture TextureColorOldReprojection

The [color old reprojection texture](../../../principles/render/sequence/index.md#linear_depth_for_ss).
## 🔒︎ Texture TextureColorOld

The [color old texture](../../../principles/render/sequence/index.md#linear_depth_for_ss).
## 🔒︎ Texture TextureColorOpacity

The color opacity texture.
## 🔒︎ Texture TextureColor

The [color texture](../../../principles/render/sequence/index.md#opaque_deferred).
## 🔒︎ RenderTarget PostRenderTarget

The post [texture render](../../../api/library/rendering/class.rendertarget_cs.md).
## 🔒︎ RenderTarget RenderTarget

The [render target](../../../api/library/rendering/class.rendertarget_cs.md).
## 🔒︎ int Height

The screen height.
## 🔒︎ int Width

The screen width.
## Texture OverlapEnvironmentTexture

The environment cubemap texture.
## 🔒︎ Light CurrentLight

The rendered light source. This method can be used to obtain shadow maps for a certain light source in an [event handler](../../../api/library/rendering/class.render_cs.md#getEventBegin_Event) (see *[BeginShadows](../../../api/library/rendering/class.render_cs.md#getEventBeginShadows_Event)* event).
## bool ObliqueFrustum

The value indicating if the viewing frustum is oblique.
> **Notice:** It is recommended to set oblique viewing frustum using this method, as it doesn't affect the projection matrix. To specify the near clipping plane use the *[setObliqueFrustumPlane()](#setObliqueFrustumPlane_Vec4_void)* method.

## vec4 ObliqueFrustumPlane

The oblique near clipping plane of the viewing frustum.
## 🔒︎ float ZFar

The far clipping plane.
## 🔒︎ float ZNear

The near clipping plane.
## vec3 CameraPosition

The camera position.
## mat4 OldModelview

The old view matrix.
## 🔒︎ mat4 IModelview

The inverse view matrix.
## mat4 Modelview

The view matrix.
## 🔒︎ mat4 ProjectionWithoutTAA

The projection matrix without TAA.
## mat4 OldProjection

The old projection matrix.
## mat4 Projection

The projection matrix.
## 🔒︎ Viewport Viewport

The rendering viewport smart pointer.
## mat4 ProjectionFullViewport

The full viewport projection matrix. In *[PSSM](../../../principles/render/lights_shadows/shadows/pssm.md)*, the full viewport is the 0th cascade; in VR foveated rendering, it's the context viewport. This matrix can be used to derive Screen Space Scaling of the object (e.g. *[ObjectParticles](../../../api/library/objects/class.objectparticles_cs.md)*), ensuring they maintain consistent size across cascades and context/focus viewports.
## 🔒︎ int StereoMode

The stereo mode.
## 🔒︎ Renderer.RENDER_STEREO_EYE StereoCurrentEye

The stereo eye.
## 🔒︎ int SkipFlags

The [skip flag](../../../api/library/rendering/class.viewport_cs.md#SKIP_DYNAMIC_REFLECTIONS) for the rendering viewport.
## 🔒︎ int ReflectionViewportMask

The reflection viewport mask.
## 🔒︎ int ViewportMask

The viewport mask.
## 🔒︎ bool IsStereo

The value indicating if stereo rendering is enabled.
## 🔒︎ bool IsShadow

The value indicating if shadows are rendered.
## 🔒︎ bool IsReflection

The value indicating if reflection rendering is in progress.
## 🔒︎ bool IsNode

The value indicating if node rendering is in progress.
## 🔒︎ CBufferScattering ShaderCBufferScattering

The buffer containing scattering parameters to be passed to a custom shader. This method can be used in a [event handler](../../../api/library/rendering/class.render_cs.md#getEventBegin_Event) to obtain scattering parameters at a certain stage of the rendering sequence and pass them to a custom shader.
## 🔒︎ CBufferCamera ShaderCBufferCamera

The buffer containing camera parameters to be passed to a custom shader. This method can be used in a [event handler](../../../api/library/rendering/class.render_cs.md#getEventBegin_Event) to obtain camera parameters at a certain stage of the rendering sequence and pass them to a custom shader.
## bool UseTAAOffset

The value indicating if skipping render mode check is enabled for using TAA. Can be used to ensure proper TAA calculation when rendering mode for the *Viewport* is set to [RENDER_DEPTH](../../../api/library/rendering/class.viewport_cs.md#RENDER_DEPTH).
## 🔒︎ bool IsStereoPeripheral

The value indicating if peripheral stereo rendering is enabled.
## 🔒︎ CBufferTonemapper ShaderCBufferTonemapper

The buffer containing tone mapping parameters to be passed to a custom shader. This method can be used in a [event handler](../../../api/library/rendering/class.render_cs.md#getEventBegin_Event) to obtain tone mapping parameters at a certain stage of the rendering sequence and pass them to a custom shader.
## bool VR

The value indicating if the VR rendering mode is enabled.
## 🔒︎ ivec2 OutputResolution

The resolution, in pixels, of the final output (target) image of the current frame: the resolution the image is presented or upscaled to.
## 🔒︎ ivec2 RenderResolution

The actual internal resolution, in pixels, at which the current frame is rendered. It differs from the output resolution when dynamic resolution or an upscaler is active: in that case it is the per-frame varying input resolution of the upscaler.
## 🔒︎ ivec2 RenderResolutionMax

The upper bound of the internal render resolution for the current configuration. With dynamic resolution enabled, the per-frame render resolution moves between the minimum and this bound; otherwise it matches the render resolution.
## 🔒︎ ivec2 RenderResolutionMin

The lower bound of the internal render resolution for the current configuration. With dynamic resolution enabled, the per-frame render resolution moves between this bound and the maximum; otherwise it matches the render resolution.
## 🔒︎ Texture TextureGBufferReactiveMask

The reactive mask texture of the G-buffer of the current frame: a single-channel screen texture into which transparent materials with reactivity enabled write their reactivity factor. It is consumed by the temporal upscalers to reduce ghosting on surfaces whose color changes cannot be explained by motion vectors (transparency, particles). The texture exists only while an upscaler is enabled.
## 🔒︎ Texture TextureGBufferSurfaceID

The surface ID texture of the opaque G-buffer (*R32U*, one surface ID per pixel). The buffer is cleared to the sky ID each frame, so pixels not covered by any opaque surface are marked as sky.
## 🔒︎ Texture TextureSurfaceIDDecal

The surface ID texture of the decal stage (*R32U*). A separate per-stage buffer exists only when *[SurfaceIDMultilayered](../../../api/library/rendering/class.render_cs.md#isSurfaceIDMultilayered_int)* is enabled; otherwise, the composite scene surface ID texture is returned.
## 🔒︎ Texture TextureSurfaceIDScene

The composite scene surface ID texture: the opaque surface IDs with the decal, transparency, and water surface IDs composited on top (*R32U*). When *[SurfaceIDMultilayered](../../../api/library/rendering/class.render_cs.md#isSurfaceIDMultilayered_int)* is disabled, this is the same texture as the G-buffer surface ID texture.
## 🔒︎ Texture TextureSurfaceIDTransparent

The surface ID texture of the transparent stage (*R32U*). A separate per-stage buffer exists only when *[SurfaceIDMultilayered](../../../api/library/rendering/class.render_cs.md#isSurfaceIDMultilayered_int)* is enabled; otherwise, the composite scene surface ID texture is returned.
## 🔒︎ Texture TextureSurfaceIDWater

The surface ID texture of the water stage (*R32U*). A separate per-stage buffer exists only when *[SurfaceIDMultilayered](../../../api/library/rendering/class.render_cs.md#isSurfaceIDMultilayered_int)* is enabled; otherwise, the composite scene surface ID texture is returned.
### Members

---

## void ClearStates ( )


Clears rendering states and textures.


> **Notice:** The shader will also be cleared.


## void ClearShader ( )

Clears the shader.
## void SetBlendFunc ( Render.PASS pass , Material material )

Sets the light blending function for a given rendering pass and material.
### Arguments

- *[Render.PASS](../../../api/library/rendering/class.render_cs.md#PASS)* **pass** - Rendering pass. One of the following values:

  - [PASS_AMBIENT](../../../api/library/rendering/class.render_cs.md#PASS_AMBIENT)
  - [PASS_EMISSION](../../../api/library/rendering/class.render_cs.md#PASS_EMISSION)
- *[Material](../../../api/library/rendering/class.material_cs.md)* **material** - Material smart pointer.

## void SetBufferMask ( Render.PASS pass , Material material )


Sets the buffer mask for a given rendering pass and material.


> **Notice:** If the material does not use a depth mask and [ambient pass](../../../api/library/rendering/class.render_cs.md#PASS_AMBIENT) is specified, the [BUFFER_COLOR](../../../api/library/rendering/class.renderstate_cs.md#BUFFER_COLOR) mask will be set; otherwise, the [BUFFER_ALL](../../../api/library/rendering/class.renderstate_cs.md#BUFFER_ALL) mask will be set.


### Arguments

- *[Render.PASS](../../../api/library/rendering/class.render_cs.md#PASS)* **pass** - Rendering pass. One of the following values:

  - [PASS_DEFERRED](../../../api/library/rendering/class.render_cs.md#PASS_DEFERRED)
  - [PASS_AMBIENT](../../../api/library/rendering/class.render_cs.md#PASS_AMBIENT)
- *[Material](../../../api/library/rendering/class.material_cs.md)* **material** - Material smart pointer.

## void SetDepthFunc ( Render.PASS pass , Material material )


Sets depth function for a given rendering pass and material.


> **Notice:** If the *depth_test* option of the material is enabled, the *[DEPTH_GEQUAL](../../../api/library/rendering/class.renderstate_cs.md#DEPTH_GEQUAL)* function will be used; otherwise the depth comparison function will be disabled.


### Arguments

- *[Render.PASS](../../../api/library/rendering/class.render_cs.md#PASS)* **pass** - Rendering pass. One of the [PASS_*](../../../api/library/rendering/class.render_cs.md#PASS_WIREFRAME) variables, except the following: *PASS_DEFERRED, PASS_SHADOW, PASS_DEPTH_PRE_PASS, PASS_EMISSION*.
- *[Material](../../../api/library/rendering/class.material_cs.md)* **material** - Material smart pointer.

## bool HasGeodeticPivot ( )

Returns a value indicating if the rendering scene has a *GeodeticPivot*.
### Return value

true if the rendering scene has a *GeodeticPivot*; otherwise, false.
## void SetMaterial ( Render.PASS pass , Material material )

Sets material and initialize all material textures for the specified rendeting pass.
### Arguments

- *[Render.PASS](../../../api/library/rendering/class.render_cs.md#PASS)* **pass** - Rendering pass. One of the [PASS_*](../../../api/library/rendering/class.render_cs.md#PASS_WIREFRAME) variables.
- *[Material](../../../api/library/rendering/class.material_cs.md)* **material** - Material smart pointer.

## void SetPolygonCull ( Render.PASS pass , Material material )


Sets the polygon culling mode for a given rendering pass and material.


> **Notice:** If the material is one-sided, the back-facing polygons will be culled; otherwise, polygon culling for the material will be disabled.


### Arguments

- *[Render.PASS](../../../api/library/rendering/class.render_cs.md#PASS)* **pass** - Rendering pass. One of the [RENDER_PASS_*](../../../api/library/rendering/class.render_cs.md#PASS_WIREFRAME) variables.
- *[Material](../../../api/library/rendering/class.material_cs.md)* **material** - Material smart pointer.

## void SetShaderParameters ( Render.PASS pass , Shader shader , bool is_screen_space = 0 )

Sets the parameters of the specified shader for a given rendering pass.
### Arguments

- *[Render.PASS](../../../api/library/rendering/class.render_cs.md#PASS)* **pass** - Rendering pass. One of the [PASS_*](../../../api/library/rendering/class.render_cs.md#PASS_WIREFRAME) variables.
- *[Shader](../../../api/library/rendering/class.shader_cs.md)* **shader** - Shader smart pointer.
- *bool* **is_screen_space** - Screenspace flag: **1** to set the parameters for the screen space effect; otherwise 0.

## void SetShaderParameters ( Render.PASS pass , Shader shader , Material material , bool is_screen_space = 0 )

Sets the parameters of the specified shader for a given rendering pass and material.
### Arguments

- *[Render.PASS](../../../api/library/rendering/class.render_cs.md#PASS)* **pass** - Rendering pass. One of the [PASS_*](../../../api/library/rendering/class.render_cs.md#PASS_WIREFRAME) variables.
- *[Shader](../../../api/library/rendering/class.shader_cs.md)* **shader** - Shader smart pointer.
- *[Material](../../../api/library/rendering/class.material_cs.md)* **material** - Material smart pointer.
- *bool* **is_screen_space** - Screenspace flag: **1** to set the parameters for the screen space effect; otherwise 0.

## void SetShaderParameters ( Render.PASS pass , Shader shader , Material material , Object object , int surface , bool is_screen_space = 0 )

Sets the parameters of the specified shader for a given rendering pass, material, object and surface.
### Arguments

- *[Render.PASS](../../../api/library/rendering/class.render_cs.md#PASS)* **pass** - Rendering pass. One of the [PASS_*](../../../api/library/rendering/class.render_cs.md#PASS_WIREFRAME) variables.
- *[Shader](../../../api/library/rendering/class.shader_cs.md)* **shader** - Shader smart pointer.
- *[Material](../../../api/library/rendering/class.material_cs.md)* **material** - Material smart pointer.
- *[Object](../../../api/library/objects/class.object_cs.md)* **object** - Object smart pointer.
- *int* **surface** - Surface number.
- *bool* **is_screen_space** - Screenspace flag: **1** to set the parameters for the screen space effect; otherwise 0.

## void SetShaderParameters ( Render.PASS pass , Material material , bool is_screen_space = 0 )

Sets the parameters of the shader for a given rendering pass and material.
### Arguments

- *[Render.PASS](../../../api/library/rendering/class.render_cs.md#PASS)* **pass** - Rendering pass. One of the [PASS_*](../../../api/library/rendering/class.render_cs.md#PASS_WIREFRAME) variables.
- *[Material](../../../api/library/rendering/class.material_cs.md)* **material** - Material smart pointer.
- *bool* **is_screen_space** - Screenspace flag: **1** to set the parameters for the screen space effect; otherwise 0.

## void SetShaderParameters ( Render.PASS pass , Object object , int surface , bool is_screen_space = 0 )

Sets the parameters of the shader for a given rendering pass, object and surface.
### Arguments

- *[Render.PASS](../../../api/library/rendering/class.render_cs.md#PASS)* **pass** - Rendering pass. One of the [PASS_*](../../../api/library/rendering/class.render_cs.md#PASS_WIREFRAME) variables.
- *[Object](../../../api/library/objects/class.object_cs.md)* **object** - Object smart pointer.
- *int* **surface** - Surface number.
- *bool* **is_screen_space** - Screenspace flag: **1** to set the parameters for the screen space effect; otherwise 0.

## int CheckSkipFlags ( int flags )

Returns a value indicating if the specified [skip flag](../../../api/library/rendering/class.viewport_cs.md#SKIP_DYNAMIC_REFLECTIONS) is set.
### Arguments

- *int* **flags** - [Skip flag](../../../api/library/rendering/class.viewport_cs.md#SKIP_DYNAMIC_REFLECTIONS).

### Return value

true if the specified [skip flag](../../../api/library/rendering/class.viewport_cs.md#SKIP_DYNAMIC_REFLECTIONS) is set; otherwise, false.
## void SaveState ( )

Saves current renderer matrices.
## void RestoreState ( )

Restores current renderer matrices.
## bool UseDynamicReflections ( )

Returns a value indicating if rendering of dynamic reflections is enabled.
### Return value

true if rendering of dynamic reflections is enabled; otherwise, false.
## bool UseOcclusionQueries ( )

Returns a value indicating if the occlusion query test is enabled.
### Return value

true if the occlusion query test is enabled; otherwise, false.
## bool UsePostEffects ( )

Returns a value indicating if rendering of post effects is enabled.
### Return value

true if rendering of post effects is enabled; otherwise, false.
## bool UseShadows ( )

Returns a value indicating if rendering of shadows is enabled.
### Return value

true if rendering of shadows is enabled; otherwise, false.
## bool UseTAA ( )

Returns a value indicating if the Temporal Anti-Aliasing (TAA) is enabled.
### Return value

true if the Temporal Anti-Aliasing (TAA) is enabled; otherwise, false.
## bool UseVelocityBuffer ( )

Returns a value indicating if rendering to the velocity buffer is enabled.
### Return value

true if rendering to the velocity buffer is enabled; otherwise, false.
## bool UseVisualizer ( )

Returns a value indicating if rendering of the visualizer is enabled.
### Return value

true if rendering of the visualizer is enabled; otherwise, false.
## Texture CreateCustomTexture3D ( string name , int width , int height , int depth , int format , int flags = 0 )


Creates a custom 3D texture. Such textures can be used in your materials.


In your [base material](../../../content/materials/index.md#base_materials):


```xml
<!-- ... -->
<texture type="texture_name"/>
<!-- ... -->

```


Create a corresponding custom texture via code:


```cpp
// ...
 // creating a custom texture
 Renderer::createCustomTexture3D("texture_name", 512, 512, 512, Texture::FORMAT_RGBA8);

```


### Arguments

- *string* **name** - Texture name.
- *int* **width** - Texture width, in pixels.
- *int* **height** - Texture height, in pixels.
- *int* **depth** - Texture depth, in pixels.
- *int* **format** - Texture format, one of the [Texture.FORMAT_](../../../api/library/rendering/class.texture_cs.md#FORMAT_ATI1) values.
- *int* **flags** - Texture flags. A combination of flags (such as [Texture.FORMAT_USAGE_](../../../api/library/rendering/class.texture_cs.md#FORMAT_USAGE_DYNAMIC), [Texture.SAMPLER_WRAP_](../../../api/library/rendering/class.texture_cs.md#SAMPLER_WRAP_BORDER), etc.)

### Return value

New created custom 3D texture.
## Texture CreateCustomTexture2D ( string name , int width , int height , int format , int flags = 0 )


Creates a custom 2D texture array. Such texture can be used in your materials.


In your [base material](../../../content/materials/index.md#base_materials):


```xml
<!-- ... -->
<texture type="texture_name"/>
<!-- ... -->

```


Create a corresponding custom texture via code:


```cpp
// ...
 // creating a custom texture
 Renderer::createCustomTexture2D("texture_name", 512, 512, Texture::FORMAT_RGBA8);

```


### Arguments

- *string* **name** - Texture name.
- *int* **width** - Texture width, in pixels.
- *int* **height** - Texture height, in pixels.
- *int* **format** - Texture format, one of the [Texture.FORMAT_](../../../api/library/rendering/class.texture_cs.md#FORMAT_ATI1) values.
- *int* **flags** - Texture flags. A combination of flags (such as [Texture.FORMAT_USAGE_](../../../api/library/rendering/class.texture_cs.md#FORMAT_USAGE_DYNAMIC), [Texture.SAMPLER_WRAP_](../../../api/library/rendering/class.texture_cs.md#SAMPLER_WRAP_BORDER), etc.)

### Return value

New created custom 2D texture.
## Texture CreateCustomTexture2DArray ( string name , int width , int height , int depth , int format , int flags = 0 )


Creates a custom 2D texture array. Such texture can be used in your materials.


```xml
<!-- ... -->
<texture type="texture_name"/>
<!-- ... -->

```


Create a corresponding custom texture via code:


```cpp
// ...
 // creating a custom texture
 Renderer::createCustomTexture2DArray("texture_name", 512, 512, 16, Texture::FORMAT_RGBA8);

```


### Arguments

- *string* **name** - Texture name.
- *int* **width** - Texture width, in pixels.
- *int* **height** - Texture height, in pixels.
- *int* **depth** - Number of elements in the array.
- *int* **format** - Texture format, one of the [Texture.FORMAT_](../../../api/library/rendering/class.texture_cs.md#FORMAT_ATI1) values.
- *int* **flags** - Texture flags. A combination of flags (such as [Texture.FORMAT_USAGE_](../../../api/library/rendering/class.texture_cs.md#FORMAT_USAGE_DYNAMIC), [Texture.SAMPLER_WRAP_](../../../api/library/rendering/class.texture_cs.md#SAMPLER_WRAP_BORDER), etc.)

### Return value

New created custom 2D texture array.
## Texture GetCustomTexture ( string name )

Returns a custom texture by its name. Custom textures can be created using [*createCustomTexture3D()*](#createCustomTexture3D_cstr_int_int_int_int_int_Texture), [*createCustomTexture3D()*](#createCustomTexture3D_cstr_int_int_int_int_int_Texture), and [*createCustomTexture3D()*](#createCustomTexture3D_cstr_int_int_int_int_int_Texture) methods.
### Arguments

- *string* **name** - Custom texture name.

### Return value

Custom texture corresponding to the specified name, if it exists, otherwise NULL.
## void ResetOverlapEnvironmentTexture ( )

Resets the environment cubemap texture to default (no environment texture is used).
## void RenderMesh ( MeshRender mesh , Material material , string pass_name , mat4 transform , Camera camera )

Renders the specified [render mesh](../../../api/library/rendering/class.meshrender_cs.md) with the specified material applied to it during the specified render pass as viewed from by specified camera.
### Arguments

- *[MeshRender](../../../api/library/rendering/class.meshrender_cs.md)* **mesh** - Render mesh to be rendered.
- *[Material](../../../api/library/rendering/class.material_cs.md)* **material** - Material to be used to render the mesh.
- *string* **pass_name** - Name of the rendering pass during which the mesh is to be rendered.
- *mat4* **transform** - Transformation to be passed to shader for rendering.
- *[Camera](../../../api/library/rendering/class.camera_cs.md)* **camera** - Camera to be used for mesh rendering.

## bool UseUpscale ( )

Returns a value indicating if the upscaling is enabled. It is a technology to be used to render high-resolution images based on the lower resolution source.
### Return value

true if upscaling (*DLSS or FSR*) is used and the final image is rendered with post-processing; otherwise false.
## bool UseDepthPrePass ( )

Returns a value indicating if *[depth pre-pass](../../../principles/render/sequence/index.md#depth_pre_pass)* is enabled. In this pre-pass, the GPU performs a depth-test for surface culling.
### Return value

true if depth pre-pass is used; otherwise false.
## bool UseReactiveMask ( )

Returns a value indicating if the reactive mask of the G-buffer is used in the current rendering, which is the case when a temporal upscaler is enabled.
### Return value

true if the reactive mask is used in the current rendering; otherwise, false.
