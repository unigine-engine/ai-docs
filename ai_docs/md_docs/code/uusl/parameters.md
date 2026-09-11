# UUSL Parameters


UUSL defines parameters that are passed by the engine to the shader. These parameters can be used in your shader programs to get the necessary data from the engine.


## Common Parameters


| UUSL parameter | Type | Description |
|---|---|---|
| *s_viewport* | *float4* | Viewport sizes: width, height, 1/width, 1/height. |
| *s_viewport_coords* | *float4* | Viewport position: x, y, 1/x, 1/y. |
| *s_stereo_hidden_area* | *float4* | [Stereo hidden area transform](../../api/library/rendering/class.render_cpp.md#StereoHiddenAreaTransform) parameter. |
| *s_depth_range* | *float4* | Depth range: near, far, 1/near, 1/far. |
| *s_solid_color* | *float4* | Solid color. |
| *s_frame* | *int* | The current frame number. |
| *s_polygon_front* | *float* | Polygon front. |


## Camera Parameters


| UUSL parameter | Type | Description |
|---|---|---|
| *s_projection* | *float4x4* | Projection matrix. |
| *s_iprojection* | *float4x4* | Inverse projection matrix. |
| *s_oblique_frustum_plane* | *float4* | Oblique frustum culling plane. |
| *s_modelview* | *float4x4* | Model-View matrix. |
| *s_old_modelview* | *float4x4* | Old Model-View matrix. |
| *s_imodelview* | *float4x4* | Inverse Model-View matrix. |
| *s_old_imodelview* | *float4x4* | Old inverse Model-View matrix. |
| *s_old_imodelview_delta* | *float4x4* | Delta of old inverse Model-View matrix. |
| *s_camera_offset* | *float3* | Camera position. |
| *s_camera_position* | *float3* | Camera position in world space. |
| *s_camera_direction* | *float3* | Camera direction vector. |
| *s_camera_projection* | *float4x4* | Projection matrix of camera (not renderstate). For example: post have ortographic projection, but camera projection is perspective. |
| *s_camera_iprojection* | *float4x4* | Inverse projection matrix of camera (not renderstate). For example: post have ortographic projection, but camera projection is perspective. |
| *s_camera_fov* | *float* | Camera vertical field of view. |


## Material Deferred Parameters


| UUSL parameter | Type | Description |
|---|---|---|
| *s_material_mask* | *int* | Material mask. |


## Time Parameters


| UUSL parameter | Type | Description |
|---|---|---|
| *s_ifps* | *float* | Delta frame time. |
| *s_time* | *float* | Engine global time. |
| *s_old_time* | *float* | Engine time in the previous frame. |


## Game Time Parameters


| UUSL parameter | Type | Description |
|---|---|---|
| *s_game_scale* | *float* | Game time scale. |
| *s_game_time* | *float* | Game time. |
| *s_game_old_time* | *float* | Game time in the previous frame. |


## Animation Time Parameters


| UUSL parameter | Type | Description |
|---|---|---|
| *s_animation_time* | *float* | Animation time in the previous frame. |
| *s_animation_old_time* | *float* | Animation time. |


## Scattering Parameters


| UUSL parameter | Type | Description |
|---|---|---|
| *s_scattering_sun_dir* | *float3* | The direction of the sun scattering. |
| *s_scattering_moon_dir* | *float3* | The direction of the moon scattering. |
| *s_environment_ambient_intensity* | *float* | [Environment ambient intensity](../../api/library/rendering/class.render_cpp.md#getEnvironmentAmbientIntensity_float) parameter. |
| *s_environment_reflection_intensity* | *float* | [Environment reflection intensity](../../api/library/rendering/class.render_cpp.md#getEnvironmentReflectionIntensity_float) parameter. |
| *s_environment_sky_intensity* | *float* | [Sky intensity](../../api/library/rendering/class.render_cpp.md#getEnvironmentSkyIntensity_float) parameter. |
| *s_environment_mipmaps* | *float* | Environment texture mipmap. |
| *s_haze_color* | *float4* | The [color of the haze](../../api/library/rendering/class.render_cpp.md#getEnvironmentHazeColor_vec4). |
| *s_haze_max_distance* | *float* | [Haze maximum visible distance](../../api/library/rendering/class.render_cpp.md#getEnvironmentHazeMaxDistance_float). |
| *s_haze_density* | *float* | The [haze density](../../api/library/rendering/class.render_cpp.md#getEnvironmentHazeDensity_float). |
| *s_haze_solid* | *float* | 1 if the [Environment Haze Mode](../../api/library/rendering/class.render_cpp.md#setEnvironmentHazeMode_int_void) is set to Solid, otherwise � 0. |
| *s_haze_visibility* | *float* | 1 if haze is enabled, otherwise � 0. |
| *s_haze_gradient* | *float* | [Environment haze gradient](../../api/library/rendering/class.render_cpp.md#setEnvironmentHazeGradient_int_void). |
| *s_sky_up* | *float3* | Sky up vector. |
| *s_sky_altitude* | *float* | Sky altitude. |
| *s_sky_transform* | *float4x4* | Sky transform matrix. |
| *s_sun_color* | *float3* | Sun color. |
| *s_sun_rotation* | *float4x4* | Sun rotation matrix. |
| *s_moon_rotation* | *float4x4* | Moon rotation matrix. |
| *s_haze_physical* | *float* | 1 if the [Environment Haze Mode](../../api/library/rendering/class.render_cpp.md#setEnvironmentHazeMode_int_void) is set to Physical, otherwise � 0. |
| *s_haze_physical_start_height* | *float* | [Reference height value](../../api/library/rendering/class.render_cpp.md#getEnvironmentHazePhysicalStartHeight_float) for the two parameters ([Half Visibility Distance](../../api/library/rendering/class.render_cpp.md#getEnvironmentHazePhysicalHalfVisibilityDistance_float) and *s_haze_physical_falloff*). |
| *s_haze_physical_density* | *float* | [Haze density](../../api/library/rendering/class.render_cpp.md#getEnvironmentHazeDensity_float) for the *Physical* preset. |
| *s_haze_physical_falloff* | *float* | [Height of the haze density gradient](../../api/library/rendering/class.render_cpp.md#getEnvironmentHazePhysicalHalfFalloffHeight_float). |
| *s_haze_physical_zero_visibility_height* | *float* | The height at which the haze makes completely overlaps the scene. |
| *s_haze_physical_screen_space_global_illumination* | *float* | Flag indicating if the [Screen-Space Haze Global Illumination effect is enabled](../../api/library/rendering/class.render_cpp.md#setEnvironmentHazeScreenSpaceGlobalIllumination_int_void). |
| *s_haze_physical_ambient_light_intensity* | *float* | [Intensity of the impact of the ambient lighting on haze](../../api/library/rendering/class.render_cpp.md#getEnvironmentHazePhysicalAmbientLightIntensity_float). |
| *s_haze_physical_ambient_color_saturation* | *float* | [Intensity of the ambient color's contribution to the haze](../../api/library/rendering/class.render_cpp.md#getEnvironmentHazePhysicalAmbientColorSaturation_float). |
| *s_haze_physical_sun_light_intensity* | *float* | [Intensity of the impact of the sunlight on haze](../../api/library/rendering/class.render_cpp.md#getEnvironmentHazePhysicalSunLightIntensity_float). |
| *s_haze_physical_sun_color_saturation* | *float* | [Intensity of the impact of the sunlight on haze](../../api/library/rendering/class.render_cpp.md#getEnvironmentHazePhysicalSunColorSaturation_float). |
| *s_haze_scattering_mie_intensity* | *float* | Minimum [Mie intensity](../../api/library/rendering/class.renderenvironmentpreset_cpp.md#getHazeScatteringMieIntensity_float) value for geometry-occluded areas. |
| *s_haze_scattering_mie_front_side_intensity* | *float* | [Falloff](../../api/library/rendering/class.renderenvironmentpreset_cpp.md#getHazeScatteringMieFrontSideIntensity_float) of the Fresnel effect for Mie intensity. |
| *s_haze_scattering_mie_fresnel_power* | *float* | [Power](../../api/library/rendering/class.renderenvironmentpreset_cpp.md#getHazeScatteringMieFresnelPower_float) of the Fresnel effect for Mie visibility. |


## Tesselation Parameters


| UUSL parameter | Type | Description |
|---|---|---|
| *s_tessellation_density_multiplier* | *float* | Global [density multiplier for the adaptive hardware-accelerated tessellation](../../api/library/rendering/class.render_cpp.md#setTessellationDensityMultiplier_float_void). Higher values produce denser meshes. |
| *s_tessellation_shadow_density_multiplier* | *float* | Global [Shadow Density multiplier for the Tessellated Displacement effect](../../api/library/rendering/class.render_cpp.md#getTessellationShadowDensityMultiplier_float). Higher values produce more detailed shadows. You can make shadows from tessellated meshes simpler to save performance. |
| *s_tessellation_distance_multiplier* | *float* | Global [multiplier for all distance parameters of the adaptive hardware-accelerated tessellation](../../api/library/rendering/class.render_cpp.md#setTessellationDistanceMultiplier_float_void) used for distance-dependent optimization. Higher values make tessellation visible at longer distances from the camera (consuming more resources). |


## Antialiasing Parameters


| UUSL parameter | Type | Description |
|---|---|---|
| *s_taa* | *float* | TAA flag. |
| *s_supersampling* | *float* | [Number of samples per pixel used for supersampling.](../../api/library/rendering/class.render_cpp.md#setSupersampling_float_void). |
