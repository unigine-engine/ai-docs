# Console Migration


## Changed Console Commands


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| `shaders_create_cache` | Removed. Use `shaders_create_cache_async` or `shaders_create_cache_force` instead. |
| `render_dof_bokeh_mode` | Default value changed from 0 to 1. |
| `render_dof_focal_distance` | Default value changed from 1.0f to 4.0f. |
| `render_streaming_textures_mipmaps` | Default value changed to false. |
| `render_upscale_mode` | Value range changed. |
| `render_white_balance_adaptation_time` | Value range changed. |


## New Console Commands


### Clouds Rendering


- `render_clouds_async_compute`


### Dynamic Resolution Scaling


- `render_dynamic_resolution_alignment_enabled`
- `render_dynamic_resolution_cooldown_frames`
- `render_dynamic_resolution_debug`
- `render_dynamic_resolution_dimension`
- `render_dynamic_resolution_down_frames`
- `render_dynamic_resolution_down_threshold`
- `render_dynamic_resolution_enabled`
- `render_dynamic_resolution_scale_max`
- `render_dynamic_resolution_scale_min`
- `render_dynamic_resolution_step`
- `render_dynamic_resolution_target_fps`
- `render_dynamic_resolution_up_frames`
- `render_dynamic_resolution_up_threshold`
- `render_dynamic_resolution_warmup_frames`


### Effects and Postprocesses


- `render_dof_jitter_samples`
- `render_dof_mipmap_by_blur_intensity`
- `render_dof_sampling_mode`
- `render_dof_taa_frame_count`
- `render_dof_taa_frames_velocity_threshold`
- `render_gpu_resource_aliasing`
- `render_indirect_specular_temporal_filtering_angle_dependence`
- `render_indirect_specular_temporal_filtering_color_clamping_grazing`
- `render_indirect_specular_temporal_filtering_frame_count_grazing`
- `render_local_tonemapper_detail_contrast_intensity`
- `render_local_tonemapper_detail_contrast_radius`
- `render_local_tonemapper_use_detail_contrast`
- `render_oblique_frustum_enabled`
- `render_surface_id_multilayered`


### Graphics Settings


- `vk_frame_pool_gpu_upload`
- `vk_frame_pool_upload`
- `vk_gpu_upload_heap`


### ObjectWaterGlobal Rendering


- `render_water_geometry_progression_fov_min`
- `render_water_geometry_progression_fov_scale`


### Output Modes


- `render_panorama_fisheye_kannala_brandt_chromatic_aberration`
- `render_panorama_fisheye_kannala_brandt_coefficients`
- `render_panorama_fisheye_kannala_brandt_focal_length`
- `render_panorama_fisheye_kannala_brandt_image_circle_radius`
- `render_panorama_fisheye_kannala_brandt_image_dimensions`
- `render_panorama_fisheye_kannala_brandt_principal_point`
- `render_panorama_fisheye_kannala_brandt_skew`
- `render_panorama_fisheye_kannala_brandt_tangential_distortion`
- `render_panorama_fisheye_kannala_brandt_vignetting_coefficient_5`
- `render_panorama_fisheye_kannala_brandt_vignetting_coefficients`
- `render_panorama_force_disable_screen_space_effects`


### Performance Profiling


- `show_profiler_memory_object`


### Rendering Resources


- `render_streaming_animation_cache_ram`
- `render_streaming_animations_info`
- `render_streaming_animations_list`
- `render_streaming_animations_mode`
- `render_streaming_animations_reload`
- `render_streaming_mesh_cache_ram`
- `render_streaming_mesh_cache_vram`
- `render_streaming_mesh_skinned_cache_ram`
- `render_streaming_mesh_skinned_cache_vram`
- `render_streaming_skinned_mesh_reload`
- `render_streaming_texture_cache_vram`


### Shaders


- `shaders_create_cache_async`
- `shaders_create_cache_force`


### Shadows


- `render_shadows_penumbra_max_radius_omni`
- `render_shadows_penumbra_max_radius_proj`
- `render_shadows_penumbra_max_radius_world`


### Stereo Rendering


- `render_stereo_hidden_area_enabled`


### VR


- `vr_emulation_mirror_crop`
- `vr_emulation_mirror_crop_offset`
- `vr_emulation_mirror_mode`
- `vr_mirror_crop`
- `vr_mirror_crop_offset`
- `vr_peripheral_rendering_debug_gaze_override_coord`
- `vr_peripheral_rendering_debug_gaze_override_mode`
- `vr_profiler_background_alpha`
- `vr_profiler_position`
- `vr_show_profiler`
- `vr_show_profiler_memory`
- `vr_show_profiler_misc`
- `vr_show_profiler_performance`


### Miscellaneous


- `render_upscale_fsr_use_old_frame_reactivity`
- `rtsp_streamer_profiling`
- `rtsp_streamer_show_debug_info`
- `scenario_manager_log`
- `scenario_manager_server`
