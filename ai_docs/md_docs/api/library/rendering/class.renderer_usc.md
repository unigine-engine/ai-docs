# Unigine.Renderer Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


## Renderer Class

### Structs

## struct CBufferCamera

A structure that represents a buffer for storing camera parameters.
### Fields

- *int* **is_oblique_frustum** - Flag indicating if the viewing frustum is oblique.
- *float* **camera_fov** - Camera vertical field of view.
- *int* **shadow_cascade_target** - Current shadow cascade used for rendering shadows.

## struct CBufferScattering

A structure that represents a buffer for storing [scattering parameters](../../../editor2/settings/render_settings/environment/index.md).
### Fields

- *float* **environment_ambient_intensity** - [Intensity](../../../api/library/rendering/class.renderenvironmentpreset_usc.md#getAmbientIntensity_float) of the environment ambient lighting. The higher the value, the more ambient lighting affects the environment. 0s means no environment reflection.
- *float* **environment_reflection_intensity** - [Intensity](../../../api/library/rendering/class.renderenvironmentpreset_usc.md#getReflectionIntensity_float) of the environment reflection.
- *float* **environment_sky_intensity** - [Intensity](../../../api/library/rendering/class.renderenvironmentpreset_usc.md#getSkyIntensity_float) of the environment sky. 0 means no environment sky.
- *float* **haze_max_distance** - [Distance](../../../api/library/rendering/class.renderenvironmentpreset_usc.md#getHazeMaxDistance_float) starting from which the haze becomes completely solid, so nothing will be seen behind.
- *float* **haze_density** - [Haze density](../../../api/library/rendering/class.renderenvironmentpreset_usc.md#getHazeDensity_float).
- *float* **haze_physical_start_height** - [Reference height](../../../api/library/rendering/class.renderenvironmentpreset_usc.md#getHazePhysicalStartHeight_float) value for the half visibility distance and half faloff height.
- *float* **haze_physical_density** - [Distance](../../../api/library/rendering/class.renderenvironmentpreset_usc.md#getHazePhysicalHalfVisibilityDistance_float) to the boundary at which the visibility comprises 50%. There is no zero-visibility in the real world, so the half-visibility boundary is used to adjust haze distance.
- *float* **haze_physical_falloff** - [Height](../../../api/library/rendering/class.renderenvironmentpreset_usc.md#getHazePhysicalHalfFalloffHeight_float) of the haze density gradient. The higher the value, the longer the haze desity reduces as the height grows, making the transition between the clear sky and haze smoother.
- *float* **haze_physical_zero_visibility_height** - Height at which the haze completely overlaps the scene.
- *float* **haze_physical_screen_space_global_illumination** - [Value](../../../api/library/rendering/class.render_usc.md#setEnvironmentHazeScreenSpaceGlobalIllumination_int_void) indicating if the Screen-Space Haze Global Illumination effect is enabled.
- *float* **haze_physical_ambient_light_intensity** - [Intensity](../../../api/library/rendering/class.renderenvironmentpreset_usc.md#getHazePhysicalAmbientLightIntensity_float) of the impact of the ambient lighting on haze (how much the ambient lighting affects the haze).
- *float* **haze_physical_ambient_color_saturation** - [Intensity](../../../api/library/rendering/class.renderenvironmentpreset_usc.md#getHazePhysicalAmbientColorSaturation_float) of the ambient color's contribution to the haze (how much the sunlight affects the haze).
- *float* **haze_physical_sun_light_intensity** - [Intensity](../../../api/library/rendering/class.renderenvironmentpreset_usc.md#getHazePhysicalSunLightIntensity_float) of the impact of the sunlight on haze (how much the sunlight affects the haze).
- *float* **haze_physical_sun_color_saturation** - [Intensity](../../../api/library/rendering/class.renderenvironmentpreset_usc.md#getHazePhysicalSunColorSaturation_float) of the impact of the sunlight on haze (how much the sunlight affects the haze).
- *float* **haze_scattering_mie_intensity** - Minimum [Mie intensity](../../../api/library/rendering/class.renderenvironmentpreset_usc.md#getHazeScatteringMieIntensity_float) value for geometry-occluded areas. This value specifies the fraction of Mie intensity visible when the surface is viewed from straight on.
- *float* **haze_scattering_mie_front_side_intensity** - [Falloff](../../../api/library/rendering/class.renderenvironmentpreset_usc.md#getHazeScatteringMieFrontSideIntensity_float) of the Fresnel effect for Mie intensity. This value is used to control occlusion of light from a World light source by the geometry.
- *float* **haze_scattering_mie_fresnel_power** - [Power](../../../api/library/rendering/class.renderenvironmentpreset_usc.md#getHazeScatteringMieFresnelPower_float) of the Fresnel effect for Mie visibility. Higher values will tighten up the areas affected, while lower ones will allow more areas to be affected by the Fresnel effect.
- *float* **sky_altitude** - Sky altitude.

## struct CBufferTonemapper

A structure that represents a buffer for storing [tone mapping parameters](../../../editor2/settings/render_settings/color/index.md#tonemapper).
### Fields

- *float* **filmic_saturation_recovery** - [Color saturation recovery](../../../api/library/rendering/class.render_usc.md#getFilmicSaturationRecovery_float) value for the filmic tonemapper.
- *float* **aces_white_clip** - [White clip](../../../api/library/rendering/class.render_usc.md#getACESWithReinhardWhiteClip_float) parameter for the ACES operator. Controls the cut-off point for white.
- *float* **aces_toe** - [Toe parameter](../../../api/library/rendering/class.render_usc.md#getACESToe_float) for the ACES operator. Controls the dark color. Higher values result in darker colors.
- *float* **aces_shoulder_angle** - [Shoulder angle parameter](../../../api/library/rendering/class.render_usc.md#getACESShoulderAngle_float) for the ACES operator. Controls how much overshoot should be added to the curve's shoulder.
- *float* **aces_shoulder_strength** - [Shoulder strength parameter](../../../api/library/rendering/class.render_usc.md#getACESShoulderStrength_float) for the ACES operator. Controls the strength of the transition between the curve's midsection and the curve's shoulder.
- *float* **aces_shoulder_length** - [Shoulder length parameter](../../../api/library/rendering/class.render_usc.md#getACESShoulderLength_float) for the ACES operator. Controls the amount of f-stops to add to the dynamic range of the curve. Defines how much of the highlights the curve takes into account.
- *float* **aces_with_reinhard_mix** - [ACES with Reinhard tone mapping](../../../api/library/rendering/class.render_usc.md#getACESWithReinhardMix_float) operator contribution.
- *float* **aces_with_reinhard_white_clip** - [White clip](../../../api/library/rendering/class.render_usc.md#getACESWithReinhardWhiteClip_float) parameter for the ACES with Reinhard operator. Controls the cut-off point for white.ACES with Reinhard operator's white clip.
- *float* **aces_with_reinhard_toe** - [Toe parameter](../../../api/library/rendering/class.render_usc.md#getACESWithReinhardToe_float) for the ACES with Reinhard operator. Controls the dark color. Higher values result in darker colors.
- *float* **aces_with_reinhard_shoulder_angle** - [Shoulder angle](../../../api/library/rendering/class.render_usc.md#getACESWithReinhardShoulderAngle_float) parameter for the ACES with Reinhard operator. Controls how much overshoot should be added to the curve's shoulder.
- *float* **aces_with_reinhard_shoulder_strength** - [Shoulder strength](../../../api/library/rendering/class.render_usc.md#getACESWithReinhardShoulderStrength_float) parameter for the ACES with Reinhard operator. Controls the strength of the transition between the curve's midsection and the curve's shoulder.
- *float* **aces_with_reinhard_shoulder_length** - [Shoulder length](../../../api/library/rendering/class.render_usc.md#getACESWithReinhardShoulderLength_float) parameter for the ACES with Reinhard operator. Controls the amount of f-stops to add to the dynamic range of the curve. Defines how much of the highlights the curve takes into account.
- *float* **reinhard_contribution** - [Reinhard tone mapping](../../../api/library/rendering/class.render_usc.md#getReinhardContribution_float) operator contribution.
- *float* **reinhard_luma_based_contribution** - [Reinhard Luma-Based tone mapping](../../../api/library/rendering/class.render_usc.md#getReinhardLumaBasedContribution_float) operator contribution. Controls the overall contribution that the Reinhard operator makes to the final color grading of the image.

### Members

## getTextureGBufferVelocity () const

Returns the current [Gbuffer velocity texture](../../../principles/render/sequence/index.md#velocity).
### Return value

Current Gbuffer velocity texture.
## getTextureGBufferFeatures () const

Returns the current texture that stores intensity of the [screen-space bevel effect](../../../api/library/rendering/class.render_usc.md#setSSBevel_int_void).
### Return value

Current texture storing intensity of the bevels. The texture is **RGBA8**, the intensity value is written to the **R** channel.
## getTextureGBufferNormal () const

Returns the current [Gbuffer normal texture](../../../principles/render/sequence/index.md#normal).
### Return value

Current Gbuffer normal texture.
## getTextureGBufferShading () const

Returns the current [Gbuffer shading texture](../../../principles/render/sequence/index.md#shading).
### Return value

Current Gbuffer shading texture.
## getTextureGBufferAlbedo () const

Returns the current [Gbuffer albedo texture](../../../principles/render/sequence/index.md#albedo).
### Return value

Current Gbuffer albedo texture.
## getTextureClouds () const

Returns the current clouds texture. This texture is rendered during the separate clouds pass.
### Return value

Current clouds texture.
## getTextureAutoWhiteBalance () const

Returns the current [auto white balance texture](../../../editor2/settings/render_settings/camera_effects/index.md#white_balance).
### Return value

Current auto-white-balance texture.
## getTextureAutoExposure () const

Returns the current autoexposure texture.
### Return value

Current autoexposure texture.
## getTextureDOFMask () const

Returns the current DoF mask texture. This texture is used at the [camera effects stage](../../../principles/render/sequence/index.md#dof).
### Return value

Current DoF mask texture.
## getTextureSSCurvature () const

Returns the current texture used by the [Screen-Space Dirt (SSDirt) effect](../../../editor2/settings/render_settings/ssdirt/index.md).
### Return value

Current curvature texture used by the [Screen-Space Dirt (SSDirt) effect](../../../editor2/settings/render_settings/ssdirt/index.md).
## getTextureSSR () const

Returns the current [SSR texture](../../../principles/render/sequence/index.md#ssr).
### Return value

Current SSR texture.
## getTextureSSGI () const

Returns the current [SSGI texture](../../../principles/render/sequence/index.md#ssgi).
### Return value

Current SSGI texture.
## getTextureSSShadowShafts () const

Returns the current Screen-Space Shadow Shafts texture.
### Return value

Current Screen-Space Shadow Shafts texture.
## getTextureSSAO () const

Returns the current [SSAO texture](../../../principles/render/sequence/index.md#ssao).
### Return value

Current SSAO texture.
## getTextureBentNormal () const

Returns the current bent normal texture. This texture is used during the [Screen-Space Global Illumination stage](../../../principles/render/sequence/index.md#ssgi).
### Return value

Current bent normal texture.
## getTextureIndirectLights () const

Returns the current array texture storing contents of the [deferred reflections buffer](../../../principles/render/sequence/index.md#deferred_reflection). The texture contains two **RG11B10F** textures: the first layer stores the environment reflection color, and the second layer stores the environment ambient light.
### Return value

Current texture storing contents of the deferred reflections buffer.
## getTextureDirectLights () const

Returns the current array texture storing contents of the [deferred light buffer](../../../principles/render/sequence/index.md#lights). The texture contains two **RG11B10F** textures: the first layer stores the diffuse light, and the second layer stores the specular light.
### Return value

Current texture storing contents of the deferred light buffer.
## getTextureTransparentBlur () const

Returns the current transparent blur texture. This texture is rendered during the transparent blur pass.
### Return value

Current transparent blur texture.
## getTextureRefractionMask () const

Returns the current [refraction](../../../principles/render/sequence/index.md#refraction_apply) mask texture.
### Return value

Current refraction mask texture.
## getTextureRefraction () const

Returns the current [refraction texture](../../../principles/render/sequence/index.md#refraction).
### Return value

Current refraction texture.
## getTextureAuxiliary () const

Returns the current [auxiliary texture](../../../principles/render/sequence/index.md#auxiliary).
### Return value

Current auxiliary texture.
## getTextureLinearDepth () const

Returns the current texture that stores linear depth data.
### Return value

Current texture that stores linear depth data.
## getTextureOpacityDepth () const

Returns the current [opacity depth texture](../../../principles/render/sequence/index.md#depth_pre_pass).
### Return value

Current opacity depth texture.
## getTextureCurrentDepth () const

Returns the current [depth texture](../../../principles/render/sequence/index.md#depth).
### Return value

Current depth texture.
## getTextureNormalUnpack () const

Returns the current texture that stores unpacked normals. Available for the following post-effects: SSR, SSGI, SSRTGI, Screen-Space Shadows.
### Return value

Current texture that stores unpacked normals.
## getTextureColorOldReprojection () const

Returns the current [color old reprojection texture](../../../principles/render/sequence/index.md#linear_depth_for_ss).
### Return value

Current color old reprojection texture.
## getTextureColorOld () const

Returns the current [color old texture](../../../principles/render/sequence/index.md#linear_depth_for_ss).
### Return value

Current color old texture.
## getTextureColorOpacity () const

Returns the current color opacity texture.
### Return value

Current color opacity texture.
## getTextureColor () const

Returns the current [color texture](../../../principles/render/sequence/index.md#opaque_deferred).
### Return value

Current color texture.
## getPostRenderTarget () const

Returns the current post [texture render](../../../api/library/rendering/class.rendertarget_usc.md).
### Return value

Current post render target.
## getRenderTarget () const

Returns the current [render target](../../../api/library/rendering/class.rendertarget_usc.md).
### Return value

Current render target.
## int getHeight () const

Returns the current screen height.
### Return value

Current screen height.
## int getWidth () const

Returns the current screen width.
### Return value

Current screen width.
## getCurrentLight () const

Returns the current rendered light source. This method can be used to obtain shadow maps for a certain light source in an [event handler](../../../api/library/rendering/class.render_usc.md#getEventBegin_Event) (see *[BeginShadows](../../../api/library/rendering/class.render_usc.md#getEventBeginShadows_Event)* event).
### Return value

Current rendered light source.
## void setObliqueFrustum ( bool frustum )

Sets a new value indicating if the viewing frustum is oblique.
> **Notice:** It is recommended to set oblique viewing frustum using this method, as it doesn't affect the projection matrix. To specify the near clipping plane use the *[setObliqueFrustumPlane()](#setObliqueFrustumPlane_Vec4_void)* method.

### Arguments

- *bool* **frustum** - Set **true** to enable viewing frustum is oblique; **false** - to disable it.

## bool isObliqueFrustum () const

Returns the current value indicating if the viewing frustum is oblique.
> **Notice:** It is recommended to set oblique viewing frustum using this method, as it doesn't affect the projection matrix. To specify the near clipping plane use the *[setObliqueFrustumPlane()](#setObliqueFrustumPlane_Vec4_void)* method.

### Return value

**true** if viewing frustum is oblique; otherwise **false**.
## float getZFar () const

Returns the current far clipping plane.
### Return value

Current far clipping plane.
## float getZNear () const

Returns the current near clipping plane.
### Return value

Current near clipping plane.
## getIModelview () const

Returns the current inverse view matrix.
### Return value

Current inverse view matrix.
## getProjectionWithoutTAA () const

Returns the current projection matrix without TAA.
### Return value

Current projection matrix without TAA.
## getViewport () const

Returns the current rendering viewport smart pointer.
### Return value

Current rendering viewport smart pointer.
## void setProjectionFullViewport ( )

Sets a new full viewport projection matrix. In *[PSSM](../../../principles/render/lights_shadows/shadows/pssm.md)*, the full viewport is the 0th cascade; in VR foveated rendering, it's the context viewport. This matrix can be used to derive Screen Space Scaling of the object (e.g. *[ObjectParticles](../../../api/library/objects/class.objectparticles_usc.md)*), ensuring they maintain consistent size across cascades and context/focus viewports.
### Arguments

- **viewport** - The projection matrix to be used for full viewport rendering.

## getProjectionFullViewport () const

Returns the current full viewport projection matrix. In *[PSSM](../../../principles/render/lights_shadows/shadows/pssm.md)*, the full viewport is the 0th cascade; in VR foveated rendering, it's the context viewport. This matrix can be used to derive Screen Space Scaling of the object (e.g. *[ObjectParticles](../../../api/library/objects/class.objectparticles_usc.md)*), ensuring they maintain consistent size across cascades and context/focus viewports.
### Return value

Current projection matrix to be used for full viewport rendering.
## int getStereoMode () const

Returns the current stereo mode.
### Return value

Current
## getStereoCurrentEye () const

Returns the current stereo eye.
### Return value

Current
## int getSkipFlags () const

Returns the current [skip flag](../../../api/library/rendering/class.viewport_usc.md#SKIP_DYNAMIC_REFLECTIONS) for the rendering viewport.
### Return value

Current [skip flag](../../../api/library/rendering/class.viewport_usc.md#SKIP_DYNAMIC_REFLECTIONS).
## int getReflectionViewportMask () const

Returns the current reflection viewport mask.
### Return value

Current reflection viewport mask.
## int getViewportMask () const

Returns the current viewport mask.
### Return value

Current viewport mask.
## bool isStereo () const

Returns the current value indicating if stereo rendering is enabled.
### Return value

**true** if stereo rendering is enabled ; otherwise **false**.
## bool isShadow () const

Returns the current value indicating if shadows are rendered.
### Return value

**true** if shadows rendering is enabled ; otherwise **false**.
## bool isReflection () const

Returns the current value indicating if reflection rendering is in progress.
### Return value

**true** if reflection rendering is in progress; otherwise **false**.
## bool isNode () const

Returns the current value indicating if node rendering is in progress.
### Return value

**true** if node rendering is in progress; otherwise **false**.
## getShaderCBufferScattering () const

Returns the current buffer containing scattering parameters to be passed to a custom shader. This method can be used in a [event handler](../../../api/library/rendering/class.render_usc.md#getEventBegin_Event) to obtain scattering parameters at a certain stage of the rendering sequence and pass them to a custom shader.
### Return value

Current buffer containing scattering parameters to be passed to a custom shader.
## getShaderCBufferCamera () const

Returns the current buffer containing camera parameters to be passed to a custom shader. This method can be used in a [event handler](../../../api/library/rendering/class.render_usc.md#getEventBegin_Event) to obtain camera parameters at a certain stage of the rendering sequence and pass them to a custom shader.
### Return value

Current buffer containing camera parameters to be passed to a custom shader.
## bool isStereoPeripheral () const

Returns the current value indicating if peripheral stereo rendering is enabled.
### Return value

**true** if peripheral stereo rendering is enabled ; otherwise **false**.
## CBufferTonemapper getShaderCBufferTonemapper () const

Returns the current buffer containing tone mapping parameters to be passed to a custom shader. This method can be used in a [event handler](../../../api/library/rendering/class.render_usc.md#getEventBegin_Event) to obtain tone mapping parameters at a certain stage of the rendering sequence and pass them to a custom shader.
### Return value

Current buffer containing tone mapping parameters to be passed to a custom shader.
## void setVR ( int vr )

Sets a new value indicating if the VR rendering mode is enabled.
### Arguments

- *int* **vr** - The the VR rendering mode

## int isVR () const

Returns the current value indicating if the VR rendering mode is enabled.
### Return value

Current the VR rendering mode
## ivec2 getOutputResolution () const

Returns the current resolution, in pixels, of the final output (target) image of the current frame: the resolution the image is presented or upscaled to.
### Return value

Current resolution of the final output image
## ivec2 getRenderResolution () const

Returns the current actual internal resolution, in pixels, at which the current frame is rendered. It differs from the output resolution when dynamic resolution or an upscaler is active: in that case it is the per-frame varying input resolution of the upscaler.
### Return value

Current actual internal render resolution of the current frame
## ivec2 getRenderResolutionMax () const

Returns the current upper bound of the internal render resolution for the current configuration. With dynamic resolution enabled, the per-frame render resolution moves between the minimum and this bound; otherwise it matches the render resolution.
### Return value

Current upper bound of the internal render resolution
## ivec2 getRenderResolutionMin () const

Returns the current lower bound of the internal render resolution for the current configuration. With dynamic resolution enabled, the per-frame render resolution moves between this bound and the maximum; otherwise it matches the render resolution.
### Return value

Current lower bound of the internal render resolution
## Texture getTextureGBufferReactiveMask () const

Returns the current reactive mask texture of the G-buffer of the current frame: a single-channel screen texture into which transparent materials with reactivity enabled write their reactivity factor. It is consumed by the temporal upscalers to reduce ghosting on surfaces whose color changes cannot be explained by motion vectors (transparency, particles). The texture exists only while an upscaler is enabled.
### Return value

Current reactive mask texture of the G-buffer
## Texture getTextureGBufferSurfaceID () const

Returns the current surface ID texture of the opaque G-buffer (*R32U*, one surface ID per pixel). The buffer is cleared to the sky ID each frame, so pixels not covered by any opaque surface are marked as sky.
### Return value

Current surface ID texture of the opaque G-buffer
## Texture getTextureSurfaceIDDecal () const

Returns the current surface ID texture of the decal stage (*R32U*). A separate per-stage buffer exists only when *[SurfaceIDMultilayered](../../../api/library/rendering/class.render_usc.md#isSurfaceIDMultilayered_int)* is enabled; otherwise, the composite scene surface ID texture is returned.
### Return value

Current surface ID texture of the decal stage
## Texture getTextureSurfaceIDScene () const

Returns the current composite scene surface ID texture: the opaque surface IDs with the decal, transparency, and water surface IDs composited on top (*R32U*). When *[SurfaceIDMultilayered](../../../api/library/rendering/class.render_usc.md#isSurfaceIDMultilayered_int)* is disabled, this is the same texture as the G-buffer surface ID texture.
### Return value

Current composite scene surface ID texture
## Texture getTextureSurfaceIDTransparent () const

Returns the current surface ID texture of the transparent stage (*R32U*). A separate per-stage buffer exists only when *[SurfaceIDMultilayered](../../../api/library/rendering/class.render_usc.md#isSurfaceIDMultilayered_int)* is enabled; otherwise, the composite scene surface ID texture is returned.
### Return value

Current surface ID texture of the transparent stage
## Texture getTextureSurfaceIDWater () const

Returns the current surface ID texture of the water stage (*R32U*). A separate per-stage buffer exists only when *[SurfaceIDMultilayered](../../../api/library/rendering/class.render_usc.md#isSurfaceIDMultilayered_int)* is enabled; otherwise, the composite scene surface ID texture is returned.
### Return value

Current surface ID texture of the water stage
---

## int hasGeodeticPivot ( )

Returns a value indicating if the rendering scene has a *GeodeticPivot*.
### Return value

**1** if the rendering scene has a *GeodeticPivot*; otherwise, **0**.
## int isNode ( )

Returns a value indicating if node rendering is in progress.
### Return value

**1** if the node rendering is in progress, otherwise **0**.
## int isReflection ( )

Returns a value indicating if reflection rendering is in progress.
### Return value

**1** if reflection rendering is in progress, otherwise **0**.
## int isShadow ( )

Returns a value indicating if shadows are rendered.
### Return value

**1** if shadows are rendered; otherwise, **0**.
## int isStereo ( )

Returns a value indicating if stereo rendering is enabled.
### Return value

**1** if the stereo rendering is enabled; otherwise, **0**.
## int getStereoCurrentEye ( )

Returns the current stereo eye.
### Return value

## Texture getTextureDirectLights ( )

Returns the array texture storing contents of the [deferred light buffer](../../../principles/render/sequence/index.md#lights). The texture contains two **RG11B10F** textures: the first layer stores the diffuse light, and the second layer stores the specular light.
### Return value

A texture storing contents of the deferred light buffer.
## Texture getTextureIndirectLights ( )

Returns the array texture storing contents of the [deferred reflections buffer](../../../principles/render/sequence/index.md#deferred_reflection). The texture contains two **RG11B10F** textures: the first layer stores the environment reflection color, and the second layer stores the environment ambient light.
### Return value

A texture storing contents of the deferred reflections buffer.
## Texture getTextureSSShadowShafts ( )

Returns the Screen-Space Shadow Shafts texture.
### Return value

Screen-Space Shadow Shafts texture.
## RenderTarget getRenderTarget ( )

Returns the [render target](../../../api/library/rendering/class.rendertarget_usc.md).
### Return value

Render target.
## RenderTarget getPostRenderTarget ( )

Returns the post [texture render](../../../api/library/rendering/class.rendertarget_usc.md).
### Return value

Post render target.
## int useDynamicReflections ( )

Returns a value indicating if rendering of dynamic reflections is enabled.
### Return value

**1** if rendering of dynamic reflections is enabled; otherwise, **0**.
## int useOcclusionQueries ( )

Returns a value indicating if the occlusion query test is enabled.
### Return value

**1** if the occlusion query test is enabled; otherwise, **0**.
## int usePostEffects ( )

Returns a value indicating if rendering of post effects is enabled.
### Return value

**1** if rendering of post effects is enabled; otherwise, **0**.
## int useShadows ( )

Returns a value indicating if rendering of shadows is enabled.
### Return value

**1** if rendering of shadows is enabled; otherwise, **0**.
## int useTAA ( )

Returns a value indicating if the Temporal Anti-Aliasing (TAA) is enabled.
### Return value

**1** if the Temporal Anti-Aliasing (TAA) is enabled; otherwise, **0**.
## void setUseTAAOffset ( int offset )

Sets a value indicating if skipping render mode check is enabled for using TAA. Can be used to ensure proper TAA calculation when rendering mode for the *Viewport* is set to [RENDER_DEPTH](../../../api/library/rendering/class.viewport_usc.md#RENDER_DEPTH).
### Arguments

- *int* **offset** - **1** to enable skipping render mode check and use TAA; otherwise **0**.

## int isUseTAAOffset ( )

Returns a value indicating if skipping render mode check is enabled for using TAA. Can be used to ensure proper TAA calculation when rendering mode for the *Viewport* is set to [RENDER_DEPTH](../../../api/library/rendering/class.viewport_usc.md#RENDER_DEPTH).
### Return value

**1** if skipping render mode check is enabled for using TAA; otherwise **0**.
## int useVelocityBuffer ( )

Returns a value indicating if rendering to the velocity buffer is enabled.
### Return value

**1** if rendering to the velocity buffer is enabled; otherwise, **0**.
## int useVisualizer ( )

Returns a value indicating if rendering of the visualizer is enabled.
### Return value

**1** if rendering of the visualizer is enabled; otherwise, **0**.
## Texture createCustomTexture3D ( string name , int width , int height , int depth , int format , int flags = 0 )


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
- *int* **format** - Texture format, one of the [TEXTURE_FORMAT_](../../../api/library/rendering/class.texture_usc.md#FORMAT_ATI1) values.
- *int* **flags** - Texture flags. A combination of flags (such as [TEXTURE_FORMAT_USAGE_](../../../api/library/rendering/class.texture_usc.md#FORMAT_USAGE_DYNAMIC), [TEXTURE_SAMPLER_WRAP_](../../../api/library/rendering/class.texture_usc.md#SAMPLER_WRAP_BORDER), etc.)

### Return value

New created custom 3D texture.
## Texture createCustomTexture2D ( string name , int width , int height , int format , int flags = 0 )


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
- *int* **format** - Texture format, one of the [TEXTURE_FORMAT_](../../../api/library/rendering/class.texture_usc.md#FORMAT_ATI1) values.
- *int* **flags** - Texture flags. A combination of flags (such as [TEXTURE_FORMAT_USAGE_](../../../api/library/rendering/class.texture_usc.md#FORMAT_USAGE_DYNAMIC), [TEXTURE_SAMPLER_WRAP_](../../../api/library/rendering/class.texture_usc.md#SAMPLER_WRAP_BORDER), etc.)

### Return value

New created custom 2D texture.
## Texture createCustomTexture2DArray ( string name , int width , int height , int depth , int format , int flags = 0 )


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
- *int* **format** - Texture format, one of the [TEXTURE_FORMAT_](../../../api/library/rendering/class.texture_usc.md#FORMAT_ATI1) values.
- *int* **flags** - Texture flags. A combination of flags (such as [TEXTURE_FORMAT_USAGE_](../../../api/library/rendering/class.texture_usc.md#FORMAT_USAGE_DYNAMIC), [TEXTURE_SAMPLER_WRAP_](../../../api/library/rendering/class.texture_usc.md#SAMPLER_WRAP_BORDER), etc.)

### Return value

New created custom 2D texture array.
## Texture getCustomTexture ( string name )

Returns a custom texture by its name. Custom textures can be created using [*createCustomTexture3D()*](#createCustomTexture3D_cstr_int_int_int_int_int_Texture), [*createCustomTexture3D()*](#createCustomTexture3D_cstr_int_int_int_int_int_Texture), and [*createCustomTexture3D()*](#createCustomTexture3D_cstr_int_int_int_int_int_Texture) methods.
### Arguments

- *string* **name** - Custom texture name.

### Return value

Custom texture corresponding to the specified name, if it exists, otherwise NULL.
## CBufferCamera getShaderCBufferCamera ( )

Returns a buffer containing camera parameters to be passed to a custom shader. This method can be used in a [event handler](../../../api/library/rendering/class.render_usc.md#getEventBegin_Event) to obtain camera parameters at a certain stage of the rendering sequence and pass them to a custom shader.
### Return value

Buffer containing camera parameters to be passed to a custom shader.
## CBufferScattering getShaderCBufferScattering ( )

Returns a buffer containing scattering parameters to be passed to a custom shader. This method can be used in a [event handler](../../../api/library/rendering/class.render_usc.md#getEventBegin_Event) to obtain scattering parameters at a certain stage of the rendering sequence and pass them to a custom shader.
### Return value

Buffer containing scattering parameters to be passed to a custom shader.
## Light getCurrentLight ( )

Returns the currently rendered light source. This method can be used to obtain shadow maps for a certain light source in a [event handler](../../../api/library/rendering/class.render_usc.md#getEventBegin_Event) (see *[BeginShadows](../../../api/library/rendering/class.render_usc.md#getEventBeginShadows_Event)* event).
### Return value

Currently rendered light source.
## void setOverlapEnvironmentTexture ( Texture texture )

Sets a new environment cubemap texture.
### Arguments

- *[Texture](../../../api/library/rendering/class.texture_usc.md)* **texture** - Environment cubemap texture to be used.

## Texture getOverlapEnvironmentTexture ( )

Returns the currently used environment cubemap texture.
### Return value

Currently used environment cubemap texture.
## void resetOverlapEnvironmentTexture ( )

Resets the environment cubemap texture to default (no environment texture is used).
## Texture getTextureNormalUnpack ( )

Returns the texture that stores unpacked normals. Available for the following post-effects: SSR, SSGI, SSRTGI, Screen-Space Shadows.
### Return value

The texture that stores unpacked normals.
## Texture getTextureLinearDepth ( )

Returns the texture that stores linear depth data.
### Return value

The texture that stores linear depth data.
## void renderMesh ( MeshRender mesh , Material material , string pass_name , Mat4 transform , Camera camera )

Renders the specified [render mesh](../../../api/library/rendering/class.meshrender_usc.md) with the specified material applied to it during the specified render pass as viewed from by specified camera.
### Arguments

- *[MeshRender](../../../api/library/rendering/class.meshrender_usc.md)* **mesh** - Render mesh to be rendered.
- *[Material](../../../api/library/rendering/class.material_usc.md)* **material** - Material to be used to render the mesh.
- *string* **pass_name** - Name of the rendering pass during which the mesh is to be rendered.
- *Mat4* **transform** - Transformation to be passed to shader for rendering.
- *[Camera](../../../api/library/rendering/class.camera_usc.md)* **camera** - Camera to be used for mesh rendering.

## int isStereoPeripheral ( )

Returns a value indicating if the Stereo Peripheral rendering mode is enabled. This rendering mode is used for HMDs having context (low-res) and focus (high-res) displays.
### Return value

true if stereo peripheral rendering is enabled; otherwise false.
## int useUpscale ( )

Returns a value indicating if the upscaling is enabled. It is a technology to be used to render high-resolution images based on the lower resolution source.
### Return value

true if upscaling (*DLSS or FSR*) is used and the final image is rendered with post-processing; otherwise false.
## int useDepthPrePass ( )

Returns a value indicating if *[depth pre-pass](../../../principles/render/sequence/index.md#depth_pre_pass)* is enabled. In this pre-pass, the GPU performs a depth-test for surface culling.
### Return value

true if depth pre-pass is used; otherwise false.
## int useReactiveMask ( )

Returns a value indicating if the reactive mask of the G-buffer is used in the current rendering, which is the case when a temporal upscaler is enabled.
### Return value

true if the reactive mask is used in the current rendering; otherwise, false.
