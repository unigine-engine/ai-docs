# Unigine.Renderer Class (CPP)

**Header:** #include <UnigineRender.h>

> **Notice:** This class is a singleton.


A basic interface for setting a renderer state (changing rendering passes parameters): pass shader uniforms, set *modelview* and *projection* matrices, etc. This class is used for rendering custom nodes (for example, a node inherited from *[ObjectExtern](../../../api/library/objects/class.objectextern_cpp.md)*).


The *Renderer* class provides the following structures representing constant buffers:


## Renderer Class

### Enums

## RENDER_STEREO_EYE

Stereo eye enumeration.
| Name | Description |
|---|---|
| **RENDER_STEREO_EYE_NONE** = 0 | None of the stereo eyes. |
| **RENDER_STEREO_EYE_LEFT** = 1 | Left stereo eye. |
| **RENDER_STEREO_EYE_RIGHT** = 2 | Right stereo eye. |
| **RENDER_STEREO_EYE_LEFT_FOCUS** = 3 | Left eye focus view. |
| **RENDER_STEREO_EYE_RIGHT_FOCUS** = 4 | Right eye focus view. |

### Structs

## struct CBufferCamera

A structure that represents a buffer for storing camera parameters.
### Fields

- *Math::[mat4](../../../api/library/math/class.mat4_cpp.md)* **camera_projection** - Camera projection matrix.
- *Math::[mat4](../../../api/library/math/class.mat4_cpp.md)* **camera_iprojection** - Camera inverse projection matrix.
- *Math::[mat4](../../../api/library/math/class.mat4_cpp.md)* **oblique_frustum_plane** - World coordinates of the oblique frustum culling plane in the format *(Nx, Ny, Nz, D)*, where *Nx, Ny, Nz* are the coordinates of the plane normal, and *D* is the distance from the origin to the plane.
- *int* **is_oblique_frustum** - Flag indicating if the viewing frustum is oblique.
- *Math::[mat4](../../../api/library/math/class.mat4_cpp.md)* **projection** - Projection matrix.
- *Math::[mat4](../../../api/library/math/class.mat4_cpp.md)* **iprojection** - Inverse projection matrix.
- *Math::[mat4](../../../api/library/math/class.mat4_cpp.md)* **projection_screen** - Projection matrix for the screen space effect.
- *Math::[mat4](../../../api/library/math/class.mat4_cpp.md)* **iprojection_screen** - Inverse projection matrix for the screen space effect.
- *Math::[mat4](../../../api/library/math/class.mat4_cpp.md)* **imodelview** - Inverse view matrix.
- *Math::[mat4](../../../api/library/math/class.mat4_cpp.md)* **old_imodelview** - Inverse old view matrix used for rendering of the previous frame.
- *Math::[mat4](../../../api/library/math/class.mat4_cpp.md)* **old_imodelview_delta** - Delta of the old inverse view and inverse view matrices.
- *Math::[mat4](../../../api/library/math/class.mat4_cpp.md)* **modelview** - View matrix.
- *Math::[mat4](../../../api/library/math/class.mat4_cpp.md)* **old_modelview** - Old view matrix.
- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md)* **camera_offset** - Camera additional transformation (offset). This transformation is applied after the view transformation. The offset does not affect the view matrix or the camera position.
- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md)* **camera_position** - Camera position.
- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md)* **camera_direction** - Inverted normalized camera direction vector.
- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md)* **projection_row_0** - The first row of the camera projection matrix.
- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md)* **projection_row_1** - The second row of the camera projection matrix.
- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md)* **projection_row_2** - The third row of the camera projection matrix.
- *Math::[vec4](../../../api/library/math/class.vec4_cpp.md)* **modelview_projection_x** - The first row of the view projection matrix.
- *Math::[vec4](../../../api/library/math/class.vec4_cpp.md)* **modelview_projection_y** - The second row of the view projection matrix.
- *Math::[vec4](../../../api/library/math/class.vec4_cpp.md)* **modelview_projection_w** - The third row of the view projection matrix.
- *Math::[vec4](../../../api/library/math/class.vec4_cpp.md)* **modelview_projection_old_x** - The first row of the old view projection matrix used for rendering of the previous frame.
- *Math::[vec4](../../../api/library/math/class.vec4_cpp.md)* **modelview_projection_old_y** - The second row of the old view projection matrix used for rendering of the previous frame.
- *Math::[vec4](../../../api/library/math/class.vec4_cpp.md)* **modelview_projection_old_w** - The third row of the old view projection matrix used for rendering of the previous frame.
- *float* **camera_fov** - Camera vertical field of view.
- *int* **shadow_cascade_target** - Current shadow cascade used for rendering shadows.

## struct CBufferScattering

A structure that represents a buffer for storing [scattering parameters](../../../editor2/settings/render_settings/environment/index.md).
### Fields

- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md)* **scattering_sun_dir** - Direction vector of the World light source having the Sun [scattering mode](../../../api/library/lights/class.lightworld_cpp.md#SCATTERING).
- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md)* **scattering_moon_dir** - Direction vector of the World light source having the Moon [scattering mode](../../../api/library/lights/class.lightworld_cpp.md#SCATTERING).
- *float* **environment_ambient_intensity** - [Intensity](../../../api/library/rendering/class.renderenvironmentpreset_cpp.md#getAmbientIntensity_float) of the environment ambient lighting. The higher the value, the more ambient lighting affects the environment. 0s means no environment reflection.
- *float* **environment_reflection_intensity** - [Intensity](../../../api/library/rendering/class.renderenvironmentpreset_cpp.md#getReflectionIntensity_float) of the environment reflection.
- *float* **environment_sky_intensity** - [Intensity](../../../api/library/rendering/class.renderenvironmentpreset_cpp.md#getSkyIntensity_float) of the environment sky. 0 means no environment sky.
- *Math::[vec4](../../../api/library/math/class.vec4_cpp.md)* **haze_color** - [Haze color](../../../api/library/rendering/class.renderenvironmentpreset_cpp.md#getHazeColor_vec4).
- *float* **haze_max_distance** - [Distance](../../../api/library/rendering/class.renderenvironmentpreset_cpp.md#getHazeMaxDistance_float) starting from which the haze becomes completely solid, so nothing will be seen behind.
- *float* **haze_density** - [Haze density](../../../api/library/rendering/class.renderenvironmentpreset_cpp.md#getHazeDensity_float).
- *float* **haze_physical_start_height** - [Reference height](../../../api/library/rendering/class.renderenvironmentpreset_cpp.md#getHazePhysicalStartHeight_float) value for the half visibility distance and half faloff height.
- *float* **haze_physical_density** - [Distance](../../../api/library/rendering/class.renderenvironmentpreset_cpp.md#getHazePhysicalHalfVisibilityDistance_float) to the boundary at which the visibility comprises 50%. There is no zero-visibility in the real world, so the half-visibility boundary is used to adjust haze distance.
- *float* **haze_physical_falloff** - [Height](../../../api/library/rendering/class.renderenvironmentpreset_cpp.md#getHazePhysicalHalfFalloffHeight_float) of the haze density gradient. The higher the value, the longer the haze desity reduces as the height grows, making the transition between the clear sky and haze smoother.
- *float* **haze_physical_zero_visibility_height** - Height at which the haze completely overlaps the scene.
- *float* **haze_physical_screen_space_global_illumination** - [Value](../../../api/library/rendering/class.render_cpp.md#setEnvironmentHazeScreenSpaceGlobalIllumination_int_void) indicating if the Screen-Space Haze Global Illumination effect is enabled.
- *float* **haze_physical_ambient_light_intensity** - [Intensity](../../../api/library/rendering/class.renderenvironmentpreset_cpp.md#getHazePhysicalAmbientLightIntensity_float) of the impact of the ambient lighting on haze (how much the ambient lighting affects the haze).
- *float* **haze_physical_ambient_color_saturation** - [Intensity](../../../api/library/rendering/class.renderenvironmentpreset_cpp.md#getHazePhysicalAmbientColorSaturation_float) of the ambient color's contribution to the haze (how much the sunlight affects the haze).
- *float* **haze_physical_sun_light_intensity** - [Intensity](../../../api/library/rendering/class.renderenvironmentpreset_cpp.md#getHazePhysicalSunLightIntensity_float) of the impact of the sunlight on haze (how much the sunlight affects the haze).
- *float* **haze_physical_sun_color_saturation** - [Intensity](../../../api/library/rendering/class.renderenvironmentpreset_cpp.md#getHazePhysicalSunColorSaturation_float) of the impact of the sunlight on haze (how much the sunlight affects the haze).
- *float* **haze_scattering_mie_intensity** - Minimum [Mie intensity](../../../api/library/rendering/class.renderenvironmentpreset_cpp.md#getHazeScatteringMieIntensity_float) value for geometry-occluded areas. This value specifies the fraction of Mie intensity visible when the surface is viewed from straight on.
- *float* **haze_scattering_mie_front_side_intensity** - [Falloff](../../../api/library/rendering/class.renderenvironmentpreset_cpp.md#getHazeScatteringMieFrontSideIntensity_float) of the Fresnel effect for Mie intensity. This value is used to control occlusion of light from a World light source by the geometry.
- *float* **haze_scattering_mie_fresnel_power** - [Power](../../../api/library/rendering/class.renderenvironmentpreset_cpp.md#getHazeScatteringMieFresnelPower_float) of the Fresnel effect for Mie visibility. Higher values will tighten up the areas affected, while lower ones will allow more areas to be affected by the Fresnel effect.
- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md)* **sky_up** - Sky up vector.
- *float* **sky_altitude** - Sky altitude.
- *Math::[mat4](../../../api/library/math/class.mat4_cpp.md)* **sky_transform** - Sky transformation matrix.
- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md)* **sun_color** - Sun color.
- *Math::[mat4](../../../api/library/math/class.mat4_cpp.md)* **sun_rotation** - Sun rotation matrix.
- *Math::[mat4](../../../api/library/math/class.mat4_cpp.md)* **moon_rotation** - Moon rotation matrix.

## struct CBufferTonemapper

A structure that represents a buffer for storing [tone mapping parameters](../../../editor2/settings/render_settings/color/index.md#tonemapper).
### Fields

- *Math::[vec4](../../../api/library/math/class.vec4_cpp.md)* **filmic_curve** - Vector of parameters for a [tone mapping curve](../../../editor2/settings/render_settings/color/index.md#filmic).
- *Math::[vec4](../../../api/library/math/class.vec4_cpp.md)* **filmic_white** - Parameter determining the brightness at which a pixel becomes pure white in the resulting image.
- *float* **filmic_saturation_recovery** - [Color saturation recovery](../../../api/library/rendering/class.render_cpp.md#getFilmicSaturationRecovery_float) value for the filmic tonemapper.
- *float* **aces_white_clip** - [White clip](../../../api/library/rendering/class.render_cpp.md#getACESWithReinhardWhiteClip_float) parameter for the ACES operator. Controls the cut-off point for white.
- *float* **aces_toe** - [Toe parameter](../../../api/library/rendering/class.render_cpp.md#getACESToe_float) for the ACES operator. Controls the dark color. Higher values result in darker colors.
- *float* **aces_shoulder_angle** - [Shoulder angle parameter](../../../api/library/rendering/class.render_cpp.md#getACESShoulderAngle_float) for the ACES operator. Controls how much overshoot should be added to the curve's shoulder.
- *float* **aces_shoulder_strength** - [Shoulder strength parameter](../../../api/library/rendering/class.render_cpp.md#getACESShoulderStrength_float) for the ACES operator. Controls the strength of the transition between the curve's midsection and the curve's shoulder.
- *float* **aces_shoulder_length** - [Shoulder length parameter](../../../api/library/rendering/class.render_cpp.md#getACESShoulderLength_float) for the ACES operator. Controls the amount of f-stops to add to the dynamic range of the curve. Defines how much of the highlights the curve takes into account.
- *float* **aces_with_reinhard_mix** - [ACES with Reinhard tone mapping](../../../api/library/rendering/class.render_cpp.md#getACESWithReinhardMix_float) operator contribution.
- *float* **aces_with_reinhard_white_clip** - [White clip](../../../api/library/rendering/class.render_cpp.md#getACESWithReinhardWhiteClip_float) parameter for the ACES with Reinhard operator. Controls the cut-off point for white.ACES with Reinhard operator's white clip.
- *float* **aces_with_reinhard_toe** - [Toe parameter](../../../api/library/rendering/class.render_cpp.md#getACESWithReinhardToe_float) for the ACES with Reinhard operator. Controls the dark color. Higher values result in darker colors.
- *float* **aces_with_reinhard_shoulder_angle** - [Shoulder angle](../../../api/library/rendering/class.render_cpp.md#getACESWithReinhardShoulderAngle_float) parameter for the ACES with Reinhard operator. Controls how much overshoot should be added to the curve's shoulder.
- *float* **aces_with_reinhard_shoulder_strength** - [Shoulder strength](../../../api/library/rendering/class.render_cpp.md#getACESWithReinhardShoulderStrength_float) parameter for the ACES with Reinhard operator. Controls the strength of the transition between the curve's midsection and the curve's shoulder.
- *float* **aces_with_reinhard_shoulder_length** - [Shoulder length](../../../api/library/rendering/class.render_cpp.md#getACESWithReinhardShoulderLength_float) parameter for the ACES with Reinhard operator. Controls the amount of f-stops to add to the dynamic range of the curve. Defines how much of the highlights the curve takes into account.
- *float* **reinhard_contribution** - [Reinhard tone mapping](../../../api/library/rendering/class.render_cpp.md#getReinhardContribution_float) operator contribution.
- *float* **reinhard_luma_based_contribution** - [Reinhard Luma-Based tone mapping](../../../api/library/rendering/class.render_cpp.md#getReinhardLumaBasedContribution_float) operator contribution. Controls the overall contribution that the Reinhard operator makes to the final color grading of the image.

### Members

## Ptr < Texture > getTextureGBufferVelocity () const

Returns the current [Gbuffer velocity texture](../../../principles/render/sequence/index.md#velocity).
### Return value

Current Gbuffer velocity texture.
## Ptr < Texture > getTextureGBufferFeatures () const

Returns the current texture that stores intensity of the [screen-space bevel effect](../../../api/library/rendering/class.render_cpp.md#setSSBevel_int_void).
### Return value

Current texture storing intensity of the bevels. The texture is **RGBA8**, the intensity value is written to the **R** channel.
## Ptr < Texture > getTextureGBufferNormal () const

Returns the current [Gbuffer normal texture](../../../principles/render/sequence/index.md#normal).
### Return value

Current Gbuffer normal texture.
## Ptr < Texture > getTextureGBufferShading () const

Returns the current [Gbuffer shading texture](../../../principles/render/sequence/index.md#shading).
### Return value

Current Gbuffer shading texture.
## Ptr < Texture > getTextureGBufferAlbedo () const

Returns the current [Gbuffer albedo texture](../../../principles/render/sequence/index.md#albedo).
### Return value

Current Gbuffer albedo texture.
## Ptr < Texture > getTextureClouds () const

Returns the current clouds texture. This texture is rendered during the separate clouds pass.
### Return value

Current clouds texture.
## Ptr < Texture > getTextureAutoWhiteBalance () const

Returns the current [auto white balance texture](../../../editor2/settings/render_settings/camera_effects/index.md#white_balance).
### Return value

Current auto-white-balance texture.
## Ptr < Texture > getTextureAutoExposure () const

Returns the current autoexposure texture.
### Return value

Current autoexposure texture.
## Ptr < Texture > getTextureDOFMask () const

Returns the current DoF mask texture. This texture is used at the [camera effects stage](../../../principles/render/sequence/index.md#dof).
### Return value

Current DoF mask texture.
## Ptr < Texture > getTextureSSCurvature () const

Returns the current texture used by the [Screen-Space Dirt (SSDirt) effect](../../../editor2/settings/render_settings/ssdirt/index.md).
### Return value

Current curvature texture used by the [Screen-Space Dirt (SSDirt) effect](../../../editor2/settings/render_settings/ssdirt/index.md).
## Ptr < Texture > getTextureSSR () const

Returns the current [SSR texture](../../../principles/render/sequence/index.md#ssr).
### Return value

Current SSR texture.
## Ptr < Texture > getTextureSSGI () const

Returns the current [SSGI texture](../../../principles/render/sequence/index.md#ssgi).
### Return value

Current SSGI texture.
## Ptr < Texture > getTextureSSShadowShafts () const

Returns the current Screen-Space Shadow Shafts texture.
### Return value

Current Screen-Space Shadow Shafts texture.
## Ptr < Texture > getTextureSSAO () const

Returns the current [SSAO texture](../../../principles/render/sequence/index.md#ssao).
### Return value

Current SSAO texture.
## Ptr < Texture > getTextureBentNormal () const

Returns the current bent normal texture. This texture is used during the [Screen-Space Global Illumination stage](../../../principles/render/sequence/index.md#ssgi).
### Return value

Current bent normal texture.
## Ptr < Texture > getTextureIndirectLights () const

Returns the current array texture storing contents of the [deferred reflections buffer](../../../principles/render/sequence/index.md#deferred_reflection). The texture contains two **RG11B10F** textures: the first layer stores the environment reflection color, and the second layer stores the environment ambient light.
### Return value

Current texture storing contents of the deferred reflections buffer.
## Ptr < Texture > getTextureDirectLights () const

Returns the current array texture storing contents of the [deferred light buffer](../../../principles/render/sequence/index.md#lights). The texture contains two **RG11B10F** textures: the first layer stores the diffuse light, and the second layer stores the specular light.
### Return value

Current texture storing contents of the deferred light buffer.
## Ptr < Texture > getTextureTransparentBlur () const

Returns the current transparent blur texture. This texture is rendered during the transparent blur pass.
### Return value

Current transparent blur texture.
## Ptr < Texture > getTextureRefractionMask () const

Returns the current [refraction](../../../principles/render/sequence/index.md#refraction_apply) mask texture.
### Return value

Current refraction mask texture.
## Ptr < Texture > getTextureRefraction () const

Returns the current [refraction texture](../../../principles/render/sequence/index.md#refraction).
### Return value

Current refraction texture.
## Ptr < Texture > getTextureAuxiliary () const

Returns the current [auxiliary texture](../../../principles/render/sequence/index.md#auxiliary).
### Return value

Current auxiliary texture.
## Ptr < Texture > getTextureLinearDepth () const

Returns the current texture that stores linear depth data.
### Return value

Current texture that stores linear depth data.
## Ptr < Texture > getTextureOpacityDepth () const

Returns the current [opacity depth texture](../../../principles/render/sequence/index.md#depth_pre_pass).
### Return value

Current opacity depth texture.
## Ptr < Texture > getTextureCurrentDepth () const

Returns the current [depth texture](../../../principles/render/sequence/index.md#depth).
### Return value

Current depth texture.
## Ptr < Texture > getTextureNormalUnpack () const

Returns the current texture that stores unpacked normals. Available for the following post-effects: SSR, SSGI, SSRTGI, Screen-Space Shadows.
### Return value

Current texture that stores unpacked normals.
## Ptr < Texture > getTextureColorOldReprojection () const

Returns the current [color old reprojection texture](../../../principles/render/sequence/index.md#linear_depth_for_ss).
### Return value

Current color old reprojection texture.
## Ptr < Texture > getTextureColorOld () const

Returns the current [color old texture](../../../principles/render/sequence/index.md#linear_depth_for_ss).
### Return value

Current color old texture.
## Ptr < Texture > getTextureColorOpacity () const

Returns the current color opacity texture.
### Return value

Current color opacity texture.
## Ptr < Texture > getTextureColor () const

Returns the current [color texture](../../../principles/render/sequence/index.md#opaque_deferred).
### Return value

Current color texture.
## Ptr < RenderTarget > getPostRenderTarget () const

Returns the current post [texture render](../../../api/library/rendering/class.rendertarget_cpp.md).
### Return value

Current post render target.
## Ptr < RenderTarget > getRenderTarget () const

Returns the current [render target](../../../api/library/rendering/class.rendertarget_cpp.md).
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
## Ptr < Light > getCurrentLight () const

Returns the current rendered light source. This method can be used to obtain shadow maps for a certain light source in an [event handler](../../../api/library/rendering/class.render_cpp.md#getEventBegin_Event) (see *[BeginShadows](../../../api/library/rendering/class.render_cpp.md#getEventBeginShadows_Event)* event).
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
## Math:: Mat4 getIModelview () const

Returns the current inverse view matrix.
### Return value

Current inverse view matrix.
## Math:: mat4 getProjectionWithoutTAA () const

Returns the current projection matrix without TAA.
### Return value

Current projection matrix without TAA.
## Ptr < Viewport > getViewport () const

Returns the current rendering viewport smart pointer.
### Return value

Current rendering viewport smart pointer.
## void setProjectionFullViewport ( const Math:: mat4 & viewport )

Sets a new full viewport projection matrix. In *[PSSM](../../../principles/render/lights_shadows/shadows/pssm.md)*, the full viewport is the 0th cascade; in VR foveated rendering, it's the context viewport. This matrix can be used to derive Screen Space Scaling of the object (e.g. *[ObjectParticles](../../../api/library/objects/class.objectparticles_cpp.md)*), ensuring they maintain consistent size across cascades and context/focus viewports.
### Arguments

- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md)&* **viewport** - The projection matrix to be used for full viewport rendering.

## Math:: mat4 getProjectionFullViewport () const

Returns the current full viewport projection matrix. In *[PSSM](../../../principles/render/lights_shadows/shadows/pssm.md)*, the full viewport is the 0th cascade; in VR foveated rendering, it's the context viewport. This matrix can be used to derive Screen Space Scaling of the object (e.g. *[ObjectParticles](../../../api/library/objects/class.objectparticles_cpp.md)*), ensuring they maintain consistent size across cascades and context/focus viewports.
### Return value

Current projection matrix to be used for full viewport rendering.
## int getStereoMode () const

Returns the current stereo mode.
### Return value

Current stereo mode. One of the [RENDER_STEREO_*](#RENDER_STEREO_VERTICAL) variables.
## Renderer::RENDER_STEREO_EYE getStereoCurrentEye () const

Returns the current stereo eye.
### Return value

Current stereo eye. One of the [RENDER_STEREO_EYE_*](#RENDER_STEREO_EYE) variables.
## int getSkipFlags () const

Returns the current [skip flag](../../../api/library/rendering/class.viewport_cpp.md#SKIP_DYNAMIC_REFLECTIONS) for the rendering viewport.
### Return value

Current [skip flag](../../../api/library/rendering/class.viewport_cpp.md#SKIP_DYNAMIC_REFLECTIONS).
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
## Renderer::CBufferScattering getShaderCBufferScattering () const

Returns the current buffer containing scattering parameters to be passed to a custom shader. This method can be used in a [event handler](../../../api/library/rendering/class.render_cpp.md#getEventBegin_Event) to obtain scattering parameters at a certain stage of the rendering sequence and pass them to a custom shader.
### Return value

Current buffer containing scattering parameters to be passed to a custom shader.
## Renderer::CBufferCamera getShaderCBufferCamera () const

Returns the current buffer containing camera parameters to be passed to a custom shader. This method can be used in a [event handler](../../../api/library/rendering/class.render_cpp.md#getEventBegin_Event) to obtain camera parameters at a certain stage of the rendering sequence and pass them to a custom shader.
### Return value

Current buffer containing camera parameters to be passed to a custom shader.
## bool isStereoPeripheral () const

Returns the current value indicating if peripheral stereo rendering is enabled.
### Return value

**true** if peripheral stereo rendering is enabled ; otherwise **false**.
## Renderer::CBufferTonemapper getShaderCBufferTonemapper () const

Returns the current buffer containing tone mapping parameters to be passed to a custom shader. This method can be used in a [event handler](../../../api/library/rendering/class.render_cpp.md#getEventBegin_Event) to obtain tone mapping parameters at a certain stage of the rendering sequence and pass them to a custom shader.
### Return value

Current buffer containing tone mapping parameters to be passed to a custom shader.
## void setVR ( bool vr )

Sets a new value indicating if the VR rendering mode is enabled.
### Arguments

- *bool* **vr** - Set **true** to enable the VR rendering mode; **false** - to disable it.

## bool isVR () const

Returns the current value indicating if the VR rendering mode is enabled.
### Return value

**true** if the VR rendering mode is enabled ; otherwise **false**.
## Math:: ivec2 getOutputResolution () const

Returns the current resolution, in pixels, of the final output (target) image of the current frame: the resolution the image is presented or upscaled to.
### Return value

Current resolution of the final output image
## Math:: ivec2 getRenderResolution () const

Returns the current actual internal resolution, in pixels, at which the current frame is rendered. It differs from the output resolution when dynamic resolution or an upscaler is active: in that case it is the per-frame varying input resolution of the upscaler.
### Return value

Current actual internal render resolution of the current frame
## Math:: ivec2 getRenderResolutionMax () const

Returns the current upper bound of the internal render resolution for the current configuration. With dynamic resolution enabled, the per-frame render resolution moves between the minimum and this bound; otherwise it matches the render resolution.
### Return value

Current upper bound of the internal render resolution
## Math:: ivec2 getRenderResolutionMin () const

Returns the current lower bound of the internal render resolution for the current configuration. With dynamic resolution enabled, the per-frame render resolution moves between this bound and the maximum; otherwise it matches the render resolution.
### Return value

Current lower bound of the internal render resolution
## Ptr < Texture > getTextureGBufferReactiveMask () const

Returns the current reactive mask texture of the G-buffer of the current frame: a single-channel screen texture into which transparent materials with reactivity enabled write their reactivity factor. It is consumed by the temporal upscalers to reduce ghosting on surfaces whose color changes cannot be explained by motion vectors (transparency, particles). The texture exists only while an upscaler is enabled.
### Return value

Current reactive mask texture of the G-buffer
## Ptr < Texture > getTextureGBufferSurfaceID () const

Returns the current surface ID texture of the opaque G-buffer (*R32U*, one surface ID per pixel). The buffer is cleared to the sky ID each frame, so pixels not covered by any opaque surface are marked as sky.
### Return value

Current surface ID texture of the opaque G-buffer
## Ptr < Texture > getTextureSurfaceIDDecal () const

Returns the current surface ID texture of the decal stage (*R32U*). A separate per-stage buffer exists only when *[SurfaceIDMultilayered](../../../api/library/rendering/class.render_cpp.md#isSurfaceIDMultilayered_int)* is enabled; otherwise, the composite scene surface ID texture is returned.
### Return value

Current surface ID texture of the decal stage
## Ptr < Texture > getTextureSurfaceIDScene () const

Returns the current composite scene surface ID texture: the opaque surface IDs with the decal, transparency, and water surface IDs composited on top (*R32U*). When *[SurfaceIDMultilayered](../../../api/library/rendering/class.render_cpp.md#isSurfaceIDMultilayered_int)* is disabled, this is the same texture as the G-buffer surface ID texture.
### Return value

Current composite scene surface ID texture
## Ptr < Texture > getTextureSurfaceIDTransparent () const

Returns the current surface ID texture of the transparent stage (*R32U*). A separate per-stage buffer exists only when *[SurfaceIDMultilayered](../../../api/library/rendering/class.render_cpp.md#isSurfaceIDMultilayered_int)* is enabled; otherwise, the composite scene surface ID texture is returned.
### Return value

Current surface ID texture of the transparent stage
## Ptr < Texture > getTextureSurfaceIDWater () const

Returns the current surface ID texture of the water stage (*R32U*). A separate per-stage buffer exists only when *[SurfaceIDMultilayered](../../../api/library/rendering/class.render_cpp.md#isSurfaceIDMultilayered_int)* is enabled; otherwise, the composite scene surface ID texture is returned.
### Return value

Current surface ID texture of the water stage
---

## void clearStates ( )


Clears rendering states and textures.


> **Notice:** The shader will also be cleared.


## void clearShader ( )

Clears the shader.
## void setBlendFunc ( Render::PASS pass , const Ptr < Material > & material ) const

Sets the light blending function for a given rendering pass and material.
### Arguments

- *[Render::PASS](../../../api/library/rendering/class.render_cpp.md#PASS)* **pass** - Rendering pass. One of the following values:

  - [PASS_AMBIENT](../../../api/library/rendering/class.render_cpp.md#PASS_AMBIENT)
  - [PASS_EMISSION](../../../api/library/rendering/class.render_cpp.md#PASS_EMISSION)
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Material](../../../api/library/rendering/class.material_cpp.md)> &* **material** - Material smart pointer.

## void setBufferMask ( Render::PASS pass , const Ptr < Material > & material ) const


Sets the buffer mask for a given rendering pass and material.


> **Notice:** If the material does not use a depth mask and [ambient pass](../../../api/library/rendering/class.render_cpp.md#PASS_AMBIENT) is specified, the [BUFFER_COLOR](../../../api/library/rendering/class.renderstate_cpp.md#BUFFER_COLOR) mask will be set; otherwise, the [BUFFER_ALL](../../../api/library/rendering/class.renderstate_cpp.md#BUFFER_ALL) mask will be set.


### Arguments

- *[Render::PASS](../../../api/library/rendering/class.render_cpp.md#PASS)* **pass** - Rendering pass. One of the following values:

  - [PASS_DEFERRED](../../../api/library/rendering/class.render_cpp.md#PASS_DEFERRED)
  - [PASS_AMBIENT](../../../api/library/rendering/class.render_cpp.md#PASS_AMBIENT)
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Material](../../../api/library/rendering/class.material_cpp.md)> &* **material** - Material smart pointer.

## void setCameraPosition ( const Math:: Vec3 & position )

Sets a new camera position.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **position** - New camera position.

## Math:: Vec3 getCameraPosition ( ) const

Returns current camera position.
### Return value

Current camera position.
## void setDepthFunc ( Render::PASS pass , const Ptr < Material > & material ) const


Sets depth function for a given rendering pass and material.


> **Notice:** If the *depth_test* option of the material is enabled, the *[DEPTH_GEQUAL](../../../api/library/rendering/class.renderstate_cpp.md#DEPTH_GEQUAL)* function will be used; otherwise the depth comparison function will be disabled.


### Arguments

- *[Render::PASS](../../../api/library/rendering/class.render_cpp.md#PASS)* **pass** - Rendering pass. One of the [PASS_*](../../../api/library/rendering/class.render_cpp.md#PASS_WIREFRAME) variables, except the following: *PASS_DEFERRED, PASS_SHADOW, PASS_DEPTH_PRE_PASS, PASS_EMISSION*.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Material](../../../api/library/rendering/class.material_cpp.md)> &* **material** - Material smart pointer.

## bool hasGeodeticPivot ( )

Returns a value indicating if the rendering scene has a *GeodeticPivot*.
### Return value

true if the rendering scene has a *GeodeticPivot*; otherwise, false.
## Math:: Mat4 getIModelview ( ) const

Returns current inverse view matrix.
### Return value

Returns current inverse view matrix.
## void setMaterial ( Render::PASS pass , const Ptr < Material > & material )

Sets material and initialize all material textures for the specified rendeting pass.
### Arguments

- *[Render::PASS](../../../api/library/rendering/class.render_cpp.md#PASS)* **pass** - Rendering pass. One of the [PASS_*](../../../api/library/rendering/class.render_cpp.md#PASS_WIREFRAME) variables.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Material](../../../api/library/rendering/class.material_cpp.md)> &* **material** - Material smart pointer.

## void setModelview ( const Math:: Mat4 & modelview )

Sets current view matrix.
### Arguments

- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **modelview** - New view matrix to be set.

## Math:: Mat4 getModelview ( ) const

Returns current view matrix.
### Return value

Returns current view matrix.
## bool isNode ( ) const

Returns a value indicating if node rendering is in progress.
### Return value

true if the node rendering is in progress, otherwise false.
## Vector < Ptr < Object >> getObjects ( )

Retrieves the list of all rendering scene objects and puts it to the buffer.
### Return value

Buffer containing all scene objects.
## void setObliqueFrustumPlane ( const Math:: Vec4 & plane )


Sets the oblique near clipping plane of the viewing frustum.


> **Notice:** This method does not affect the projection matrix. To enable the oblique frustum use the *[setObliqueFrustum()](#setObliqueFrustum_int_void)* method.


### Arguments

- *const  Math::[Vec4](../../../api/library/math/class.vec4_cpp.md) &* **plane** - World coordinates of the oblique near clipping plane to set *(Nx, Ny, Nz, D)*, where *Nx, Ny, Nz* - coordinates of the plane normal, *D* - distance from the origin to the plane.

## Math:: Vec4 getObliqueFrustumPlane ( ) const

Returns the oblique near clipping plane of the viewing frustum.
### Return value

World coordinates of the oblique near clipping plane to set *(Nx, Ny, Nz, D)*, where *Nx, Ny, Nz* - coordinates of the plane normal, *D* - distance from the origin to the plane.
## void setOldModelview ( const Math:: Mat4 & modelview )

Updates the old view matrix.
### Arguments

- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **modelview** - Old view matrix to be set.

## Math:: Mat4 getOldModelview ( ) const

Returns the old view matrix.
### Return value

Old view matrix.
## void setOldProjection ( const Math:: mat4 & projection )

Updates the old projection matrix.
### Arguments

- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **projection** - Old projection matrix to be set.

## Math:: mat4 getOldProjection ( ) const

Returns the old projection matrix.
### Return value

Old projection matrix.
## void setPolygonCull ( Render::PASS pass , const Ptr < Material > & material ) const


Sets the polygon culling mode for a given rendering pass and material.


> **Notice:** If the material is one-sided, the back-facing polygons will be culled; otherwise, polygon culling for the material will be disabled.


### Arguments

- *[Render::PASS](../../../api/library/rendering/class.render_cpp.md#PASS)* **pass** - Rendering pass. One of the [RENDER_PASS_*](../../../api/library/rendering/class.render_cpp.md#PASS_WIREFRAME) variables.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Material](../../../api/library/rendering/class.material_cpp.md)> &* **material** - Material smart pointer.

## Math:: mat4 getProjectionWithoutTAA ( ) const

Returns current projection matrix without TAA.
### Return value

Projection matrix without TAA.
## void setProjection ( const Math:: mat4 & projection )


Updates the current projection matrix.


> **Notice:** It is not recommended to use this method for setting obliqueness of the near clipping plane of the frustum, as in this case a number of features (such as clouds, shadows, TAA, a number of engine optimizations, etc.) will not function properly. Please, use the *[setObliqueFrustum()](#setObliqueFrustum_int_void)* method instead.


### Arguments

- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **projection** - Projection matrix to be set.

## Math:: mat4 getProjection ( ) const

Returns current projection matrix.
### Return value

Current projection matrix.
## bool isReflection ( ) const

Returns a value indicating if reflection rendering is in progress.
### Return value

true if reflection rendering is in progress, otherwise false.
## int getReflectionViewportMask ( ) const

Returns the current reflection viewport mask.
### Return value

Current reflection viewport mask.
## void setShaderParameters ( Render::PASS pass , const Ptr < Shader > & shader , bool is_screen_space = 0 )

Sets the parameters of the specified shader for a given rendering pass.
### Arguments

- *[Render::PASS](../../../api/library/rendering/class.render_cpp.md#PASS)* **pass** - Rendering pass. One of the [PASS_*](../../../api/library/rendering/class.render_cpp.md#PASS_WIREFRAME) variables.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Shader](../../../api/library/rendering/class.shader_cpp.md)> &* **shader** - Shader smart pointer.
- *bool* **is_screen_space** - Screenspace flag: **1** to set the parameters for the screen space effect; otherwise 0.

## void setShaderParameters ( Render::PASS pass , const Ptr < Shader > & shader , const Ptr < Material > & material , bool is_screen_space = 0 )

Sets the parameters of the specified shader for a given rendering pass and material.
### Arguments

- *[Render::PASS](../../../api/library/rendering/class.render_cpp.md#PASS)* **pass** - Rendering pass. One of the [PASS_*](../../../api/library/rendering/class.render_cpp.md#PASS_WIREFRAME) variables.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Shader](../../../api/library/rendering/class.shader_cpp.md)> &* **shader** - Shader smart pointer.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Material](../../../api/library/rendering/class.material_cpp.md)> &* **material** - Material smart pointer.
- *bool* **is_screen_space** - Screenspace flag: **1** to set the parameters for the screen space effect; otherwise 0.

## void setShaderParameters ( Render::PASS pass , const Ptr < Shader > & shader , const Ptr < Material > & material , const Ptr < Object > & object , int surface , bool is_screen_space = 0 )

Sets the parameters of the specified shader for a given rendering pass, material, object and surface.
### Arguments

- *[Render::PASS](../../../api/library/rendering/class.render_cpp.md#PASS)* **pass** - Rendering pass. One of the [PASS_*](../../../api/library/rendering/class.render_cpp.md#PASS_WIREFRAME) variables.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Shader](../../../api/library/rendering/class.shader_cpp.md)> &* **shader** - Shader smart pointer.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Material](../../../api/library/rendering/class.material_cpp.md)> &* **material** - Material smart pointer.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Object](../../../api/library/objects/class.object_cpp.md)> &* **object** - Object smart pointer.
- *int* **surface** - Surface number.
- *bool* **is_screen_space** - Screenspace flag: **1** to set the parameters for the screen space effect; otherwise 0.

## void setShaderParameters ( Render::PASS pass , const Ptr < Material > & material , bool is_screen_space = 0 )

Sets the parameters of the shader for a given rendering pass and material.
### Arguments

- *[Render::PASS](../../../api/library/rendering/class.render_cpp.md#PASS)* **pass** - Rendering pass. One of the [PASS_*](../../../api/library/rendering/class.render_cpp.md#PASS_WIREFRAME) variables.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Material](../../../api/library/rendering/class.material_cpp.md)> &* **material** - Material smart pointer.
- *bool* **is_screen_space** - Screenspace flag: **1** to set the parameters for the screen space effect; otherwise 0.

## void setShaderParameters ( Render::PASS pass , const Ptr < Object > & object , int surface , bool is_screen_space = 0 )

Sets the parameters of the shader for a given rendering pass, object and surface.
### Arguments

- *[Render::PASS](../../../api/library/rendering/class.render_cpp.md#PASS)* **pass** - Rendering pass. One of the [PASS_*](../../../api/library/rendering/class.render_cpp.md#PASS_WIREFRAME) variables.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Object](../../../api/library/objects/class.object_cpp.md)> &* **object** - Object smart pointer.
- *int* **surface** - Surface number.
- *bool* **is_screen_space** - Screenspace flag: **1** to set the parameters for the screen space effect; otherwise 0.

## bool isShadow ( ) const

Returns a value indicating if shadows are rendered.
### Return value

true if shadows are rendered; otherwise, false.
## int checkSkipFlags ( int flags ) const

Returns a value indicating if the specified [skip flag](../../../api/library/rendering/class.viewport_cpp.md#SKIP_DYNAMIC_REFLECTIONS) is set.
### Arguments

- *int* **flags** - [Skip flag](../../../api/library/rendering/class.viewport_cpp.md#SKIP_DYNAMIC_REFLECTIONS).

### Return value

true if the specified [skip flag](../../../api/library/rendering/class.viewport_cpp.md#SKIP_DYNAMIC_REFLECTIONS) is set; otherwise, false.
## int getSkipFlags ( ) const

Returns the [skip flag](../../../api/library/rendering/class.viewport_cpp.md#SKIP_DYNAMIC_REFLECTIONS) set for the rendering viewport.
### Return value

[Skip flag](../../../api/library/rendering/class.viewport_cpp.md#SKIP_DYNAMIC_REFLECTIONS).
## bool isStereo ( ) const

Returns a value indicating if stereo rendering is enabled.
### Return value

true if the stereo rendering is enabled; otherwise, false.
## int getStereoMode ( ) const

Returns the current stereo mode.
### Return value

One of the [RENDER_STEREO_*](#RENDER_STEREO_VERTICAL) variables.
## Renderer::RENDER_STEREO_EYE getStereoCurrentEye ( ) const

Returns the current stereo eye.
### Return value

One of the [RENDER_STEREO_EYE_*](#RENDER_STEREO_EYE) variables.
## Ptr < Texture > getTextureAutoExposure ( ) const

Returns the autoexposure texture.
### Return value

Autoexposure texture.
## Ptr < Texture > getTextureAuxiliary ( ) const

Returns the [auxiliary texture](../../../principles/render/sequence/index.md#auxiliary).
### Return value

Auxiliary texture.
## Ptr < Texture > getTextureBentNormal ( ) const

Returns the bent normal texture. This texture is used during the [Screen-Space Global Illumination stage](../../../principles/render/sequence/index.md#ssgi).
### Return value

Bent normal texture.
## Ptr < Texture > getTextureClouds ( ) const

Returns the clouds texture. This texture is rendered during the separate clouds pass.
### Return value

Clouds texture.
## Ptr < Texture > getTextureColor ( ) const

Returns the [color texture](../../../principles/render/sequence/index.md#opaque_deferred).
### Return value

Color texture.
## Ptr < Texture > getTextureColorOld ( ) const

Returns the [color old texture](../../../principles/render/sequence/index.md#linear_depth_for_ss).
### Return value

Color old texture.
## Ptr < Texture > getTextureColorOldReprojection ( ) const

Returns the [color old reprojection texture](../../../principles/render/sequence/index.md#linear_depth_for_ss).
### Return value

Color old reprojection texture.
## Ptr < Texture > getTextureColorOpacity ( ) const

Returns the color opacity texture.
### Return value

Color opacity texture.
## Ptr < Texture > getTextureCurrentDepth ( ) const

Returns the [current depth texture](../../../principles/render/sequence/index.md#depth).
### Return value

Current depth texture.
## Ptr < Texture > getTextureDOFMask ( ) const

Returns the DoF mask texture. This texture is used at the [camera effects stage](../../../principles/render/sequence/index.md#dof).
### Return value

DoF mask texture
## Ptr < Texture > getTextureGBufferFeatures ( ) const

Returns the texture that stores intensity of the [screen-space bevel effect](../../../api/library/rendering/class.render_cpp.md#setSSBevel_int_void).
### Return value

Texture storing intensity of the bevels. The texture is **RGBA8**, the intensity value is written to the **R** channel.
## Ptr < Texture > getTextureGBufferAlbedo ( ) const

Returns the [Gbuffer albedo texture](../../../principles/render/sequence/index.md#albedo).
### Return value

Gbuffer albedo texture.
## Ptr < Texture > getTextureGBufferNormal ( ) const

Returns the [Gbuffer normal texture](../../../principles/render/sequence/index.md#normal).
### Return value

Gbuffer normal texture.
## Ptr < Texture > getTextureGBufferShading ( ) const

Returns the [Gbuffer shading texture](../../../principles/render/sequence/index.md#shading).
### Return value

Gbuffer shading texture.
## Ptr < Texture > getTextureGBufferVelocity ( ) const

Returns the [Gbuffer velocity texture](../../../principles/render/sequence/index.md#velocity).
### Return value

Gbuffer velocity texture.
## Ptr < Texture > getTextureDirectLights ( ) const

Returns the array texture storing contents of the [deferred light buffer](../../../principles/render/sequence/index.md#lights). The texture contains two **RG11B10F** textures: the first layer stores the diffuse light, and the second layer stores the specular light.
### Return value

A texture storing contents of the deferred light buffer.
## Ptr < Texture > getTextureIndirectLights ( ) const

Returns the array texture storing contents of the [deferred reflections buffer](../../../principles/render/sequence/index.md#deferred_reflection). The texture contains two **RG11B10F** textures: the first layer stores the environment reflection color, and the second layer stores the environment ambient light.
### Return value

A texture storing contents of the deferred reflections buffer.
## Ptr < Texture > getTextureOpacityDepth ( ) const

Returns the [opacity depth texture](../../../principles/render/sequence/index.md#depth_pre_pass).
### Return value

Opacity depth texture.
## Ptr < Texture > getTextureRefraction ( ) const

Returns the [refraction texture](../../../principles/render/sequence/index.md#refraction).
### Return value

Refraction texture.
## Ptr < Texture > getTextureSSR ( ) const

Returns the [SSR texture](../../../principles/render/sequence/index.md#ssr).
### Return value

SSR texture.
## Ptr < Texture > getTextureSSAO ( ) const

Returns the [SSAO texture](../../../principles/render/sequence/index.md#ssao).
### Return value

SSAO texture.
## Ptr < Texture > getTextureSSGI ( ) const

Returns the [SSGI texture](../../../principles/render/sequence/index.md#ssgi).
### Return value

SSGI texture.
## Ptr < Texture > getTextureSSShadowShafts ( ) const

Returns the Screen-Space Shadow Shafts texture.
### Return value

Screen-Space Shadow Shafts texture.
## Ptr < Texture > getTextureTransparentBlur ( ) const

Returns the transparent blur texture. This texture is rendered during the transparent blur pass.
### Return value

Transparent blur texture.
## Ptr < RenderTarget > getRenderTarget ( ) const

Returns the [render target](../../../api/library/rendering/class.rendertarget_cpp.md).
### Return value

Render target.
## Ptr < RenderTarget > getPostRenderTarget ( ) const

Returns the post [texture render](../../../api/library/rendering/class.rendertarget_cpp.md).
### Return value

Post render target.
## Ptr < Viewport > getViewport ( ) const

Returns the rendering viewport.
### Return value

Rendering viewport smart pointer.
## int getViewportMask ( ) const

Returns current viewport mask.
### Return value

Returns current viewport mask.
## float getZFar ( ) const

Return current far clipping plane.
### Return value

Returns current far clipping plane.
## float getZNear ( ) const

Returns current near clipping plane.
### Return value

Returns current near clipping plane.
## void saveState ( )

Saves current renderer matrices.
## void restoreState ( )

Restores current renderer matrices.
## bool useDynamicReflections ( ) const

Returns a value indicating if rendering of dynamic reflections is enabled.
### Return value

true if rendering of dynamic reflections is enabled; otherwise, false.
## bool useOcclusionQueries ( ) const

Returns a value indicating if the occlusion query test is enabled.
### Return value

true if the occlusion query test is enabled; otherwise, false.
## bool usePostEffects ( ) const

Returns a value indicating if rendering of post effects is enabled.
### Return value

true if rendering of post effects is enabled; otherwise, false.
## bool useShadows ( ) const

Returns a value indicating if rendering of shadows is enabled.
### Return value

true if rendering of shadows is enabled; otherwise, false.
## bool useTAA ( ) const

Returns a value indicating if the Temporal Anti-Aliasing (TAA) is enabled.
### Return value

true if the Temporal Anti-Aliasing (TAA) is enabled; otherwise, false.
## void setUseTAAOffset ( bool offset )

Sets a value indicating if skipping render mode check is enabled for using TAA. Can be used to ensure proper TAA calculation when rendering mode for the *Viewport* is set to [RENDER_DEPTH](../../../api/library/rendering/class.viewport_cpp.md#RENDER_DEPTH).
### Arguments

- *bool* **offset** - true to enable skipping render mode check and use TAA; otherwise false.

## bool isUseTAAOffset ( ) const

Returns a value indicating if skipping render mode check is enabled for using TAA. Can be used to ensure proper TAA calculation when rendering mode for the *Viewport* is set to [RENDER_DEPTH](../../../api/library/rendering/class.viewport_cpp.md#RENDER_DEPTH).
### Return value

true if skipping render mode check is enabled for using TAA; otherwise false.
## bool useVelocityBuffer ( ) const

Returns a value indicating if rendering to the velocity buffer is enabled.
### Return value

true if rendering to the velocity buffer is enabled; otherwise, false.
## bool useVisualizer ( ) const

Returns a value indicating if rendering of the visualizer is enabled.
### Return value

true if rendering of the visualizer is enabled; otherwise, false.
## Ptr < Texture > getTextureSSCurvature ( ) const

Returns the texture used by the [Screen-Space Dirt (SSDirt) effect](../../../editor2/settings/render_settings/ssdirt/index.md).
### Return value

Curvature texture used by the [Screen-Space Dirt (SSDirt) effect](../../../editor2/settings/render_settings/ssdirt/index.md).
## Ptr < Texture > getTextureAutoWhiteBalance ( ) const

Returns the [auto white balance texture](../../../editor2/settings/render_settings/camera_effects/index.md#white_balance).
### Return value

Auto-white-balance texture.
## Ptr < Texture > getTextureRefractionMask ( ) const

Returns the [refraction](../../../principles/render/sequence/index.md#refraction_apply) mask texture.
### Return value

Refraction mask texture.
## Ptr < Texture > createCustomTexture3D ( const char * name , int width , int height , int depth , int format , int flags = 0 )


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

- *const char ** **name** - Texture name.
- *int* **width** - Texture width, in pixels.
- *int* **height** - Texture height, in pixels.
- *int* **depth** - Texture depth, in pixels.
- *int* **format** - Texture format, one of the [Texture::FORMAT_](../../../api/library/rendering/class.texture_cpp.md#FORMAT_ATI1) values.
- *int* **flags** - Texture flags. A combination of flags (such as [Texture::FORMAT_USAGE_](../../../api/library/rendering/class.texture_cpp.md#FORMAT_USAGE_DYNAMIC), [Texture::SAMPLER_WRAP_](../../../api/library/rendering/class.texture_cpp.md#SAMPLER_WRAP_BORDER), etc.)

### Return value

New created custom 3D texture.
## Ptr < Texture > createCustomTexture2D ( const char * name , int width , int height , int format , int flags = 0 )


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

- *const char ** **name** - Texture name.
- *int* **width** - Texture width, in pixels.
- *int* **height** - Texture height, in pixels.
- *int* **format** - Texture format, one of the [Texture::FORMAT_](../../../api/library/rendering/class.texture_cpp.md#FORMAT_ATI1) values.
- *int* **flags** - Texture flags. A combination of flags (such as [Texture::FORMAT_USAGE_](../../../api/library/rendering/class.texture_cpp.md#FORMAT_USAGE_DYNAMIC), [Texture::SAMPLER_WRAP_](../../../api/library/rendering/class.texture_cpp.md#SAMPLER_WRAP_BORDER), etc.)

### Return value

New created custom 2D texture.
## Ptr < Texture > createCustomTexture2DArray ( const char * name , int width , int height , int depth , int format , int flags = 0 )


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

- *const char ** **name** - Texture name.
- *int* **width** - Texture width, in pixels.
- *int* **height** - Texture height, in pixels.
- *int* **depth** - Number of elements in the array.
- *int* **format** - Texture format, one of the [Texture::FORMAT_](../../../api/library/rendering/class.texture_cpp.md#FORMAT_ATI1) values.
- *int* **flags** - Texture flags. A combination of flags (such as [Texture::FORMAT_USAGE_](../../../api/library/rendering/class.texture_cpp.md#FORMAT_USAGE_DYNAMIC), [Texture::SAMPLER_WRAP_](../../../api/library/rendering/class.texture_cpp.md#SAMPLER_WRAP_BORDER), etc.)

### Return value

New created custom 2D texture array.
## Ptr < Texture > getCustomTexture ( const char * name )

Returns a custom texture by its name. Custom textures can be created using [*createCustomTexture3D()*](#createCustomTexture3D_cstr_int_int_int_int_int_Texture), [*createCustomTexture3D()*](#createCustomTexture3D_cstr_int_int_int_int_int_Texture), and [*createCustomTexture3D()*](#createCustomTexture3D_cstr_int_int_int_int_int_Texture) methods.
### Arguments

- *const char ** **name** - Custom texture name.

### Return value

Custom texture corresponding to the specified name, if it exists, otherwise nullptr.
## Renderer::CBufferCamera getShaderCBufferCamera ( ) const

Returns a buffer containing camera parameters to be passed to a custom shader. This method can be used in a [event handler](../../../api/library/rendering/class.render_cpp.md#getEventBegin_Event) to obtain camera parameters at a certain stage of the rendering sequence and pass them to a custom shader.
### Return value

Buffer containing camera parameters to be passed to a custom shader.
## Renderer::CBufferScattering getShaderCBufferScattering ( ) const

Returns a buffer containing scattering parameters to be passed to a custom shader. This method can be used in a [event handler](../../../api/library/rendering/class.render_cpp.md#getEventBegin_Event) to obtain scattering parameters at a certain stage of the rendering sequence and pass them to a custom shader.
### Return value

Buffer containing scattering parameters to be passed to a custom shader.
## Ptr < Light > getCurrentLight ( ) const

Returns the currently rendered light source. This method can be used to obtain shadow maps for a certain light source in a [event handler](../../../api/library/rendering/class.render_cpp.md#getEventBegin_Event) (see *[BeginShadows](../../../api/library/rendering/class.render_cpp.md#getEventBeginShadows_Event)* event).
### Return value

Currently rendered light source.
## void setOverlapEnvironmentTexture ( const Ptr < Texture > & texture )

Sets a new environment cubemap texture.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Texture](../../../api/library/rendering/class.texture_cpp.md)> &* **texture** - Environment cubemap texture to be used.

## Ptr < Texture > getOverlapEnvironmentTexture ( ) const

Returns the currently used environment cubemap texture.
### Return value

Currently used environment cubemap texture.
## void resetOverlapEnvironmentTexture ( )

Resets the environment cubemap texture to default (no environment texture is used).
## Ptr < Texture > getTextureNormalUnpack ( ) const

Returns the texture that stores unpacked normals. Available for the following post-effects: SSR, SSGI, SSRTGI, Screen-Space Shadows.
### Return value

The texture that stores unpacked normals.
## Ptr < Texture > getTextureLinearDepth ( ) const

Returns the texture that stores linear depth data.
### Return value

The texture that stores linear depth data.
## void renderMesh ( const Ptr < MeshRender > & mesh , const Ptr < Material > & material , const char * pass_name , const Math:: Mat4 & transform , const Ptr < Camera > & camera )

Renders the specified [render mesh](../../../api/library/rendering/class.meshrender_cpp.md) with the specified material applied to it during the specified render pass as viewed from by specified camera.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[MeshRender](../../../api/library/rendering/class.meshrender_cpp.md)> &* **mesh** - Render mesh to be rendered.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Material](../../../api/library/rendering/class.material_cpp.md)> &* **material** - Material to be used to render the mesh.
- *const char ** **pass_name** - Name of the rendering pass during which the mesh is to be rendered.
- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation to be passed to shader for rendering.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Camera](../../../api/library/rendering/class.camera_cpp.md)> &* **camera** - Camera to be used for mesh rendering.

## bool isStereoPeripheral ( ) const

Returns a value indicating if the Stereo Peripheral rendering mode is enabled. This rendering mode is used for HMDs having context (low-res) and focus (high-res) displays.
### Return value

true if stereo peripheral rendering is enabled; otherwise false.
## bool useUpscale ( ) const

Returns a value indicating if the upscaling is enabled. It is a technology to be used to render high-resolution images based on the lower resolution source.
### Return value

true if upscaling (*DLSS or FSR*) is used and the final image is rendered with post-processing; otherwise false.
## bool useDepthPrePass ( ) const

Returns a value indicating if *[depth pre-pass](../../../principles/render/sequence/index.md#depth_pre_pass)* is enabled. In this pre-pass, the GPU performs a depth-test for surface culling.
### Return value

true if depth pre-pass is used; otherwise false.
## bool useReactiveMask ( ) const

Returns a value indicating if the reactive mask of the G-buffer is used in the current rendering, which is the case when a temporal upscaler is enabled.
### Return value

true if the reactive mask is used in the current rendering; otherwise, false.
