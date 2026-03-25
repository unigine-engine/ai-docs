# Console Migration


## Changed Console Commands


| UNIGINE 2.20 | UNIGINE 2.21 |
|---|---|
| `render_transparent_light` | Removed. |
| `render_transparent_ambient` | Removed. |
| `render_lights_tile_grid_size` | Removed. |
| `render_lights_max_per_batch` | Removed. |
| `render_sssss_taa_max_frames_by_velocity` | Removed. |
| `render_sssss_taa_min_frames_by_velocity` | Removed. |
| `render_taa_max_frames_by_velocity` | Removed. |
| `render_taa_min_frames_by_velocity` | Removed. |
| `render_taa_information_lost_frame_count` | Removed. |
| `render_upscale_post` | Removed. |
| `render_upscale_fsr_auto_reactive_enabled` | Removed. |
| `render_upscale_fsr_auto_reactive_scale` | Removed. |
| `render_upscale_fsr_auto_tc_scale` | Removed. |
| `render_upscale_fsr_auto_tc_threshold` | Removed. |
| `render_upscale_fsr_auto_reactive_max` | Removed. |


## New Console Commands


### Clouds


- `render_clouds_environment_sky`
- `render_clouds_environment_sky_color`
- `render_clouds_environment_color`


### Configurations


- `global_config`
- `global_config_autosave`
- `global_config_load`
- `global_config_save`


### Effects


- `render_sharpen_resolution`


### Environment


- `render_environment_haze_resolution`
- `render_environment_dither_scale`
- `render_environment_haze_dither_scale`


### Lighting and Shadows


- `render_lights_dither_scale`


### Streaming


- `render_streaming_igpu_vram_mode`
- `render_streaming_igpu_vram_size`
- `render_streaming_igpu_vram_balance`


### Upscalers


- `render_upscale_fix_flicker`
- `render_upscale_fsr_custom_resolution_scale`
- `render_upscale_dlss_resolution_scale_enabled`
- `render_upscale_dlss_resolution_scale_value`
- `render_upscale_order`
- `render_upscale_fsr_show_debug_view`


### Visualizer


- `render_show_visualizer_on_invisible_surfaces`
- `render_show_depth_pre_pass`
- `render_show_proj_and_omni_shadow_casters`
- `render_show_transparent_gbuffer`
- `render_show_transparent_lighting_ambient`
- `render_show_transparent_lighting_environment_probe`
- `render_show_transparent_lighting_voxel_probe`
- `render_show_transparent_lighting_planar_probe`
- `render_show_transparent_lighting_light_omni`
- `render_show_transparent_lighting_light_proj`
- `render_show_transparent_lighting_light_world`
- `render_show_vertex_density_enabled`
- `render_show_vertex_density_mode`
- `render_show_vertex_density_depth_test`
- `render_show_vertex_density_search_area`
- `render_show_vertex_density_threshold`
- `render_show_vertex_density_blend`
- `render_show_quad_overdraw_enabled`
- `render_show_quad_overdraw_display_mode`
- `render_show_quad_overdraw_passes`
- `render_show_quad_overdraw_wireframe`
- `render_show_quad_overdraw_landscape_terrain`
- `render_show_quad_overdraw_water_global`
- `render_show_quad_overdraw_threshold`
- `render_show_quad_overdraw_blend`


### Miscellaneous


- `render_occluder_distance`
