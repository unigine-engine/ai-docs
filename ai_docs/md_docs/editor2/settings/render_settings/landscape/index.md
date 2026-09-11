# Landscape


The section contains settings that control rendering of *Landscape Terrain*.


![Landscape rendering settings](landscape.png)

*Landscape Terrainrendering settings*


All the settings are also available via [Console](../../../../code/console/index.md#terrain).


| Operations Per Frame | The maximum number of Landscape texture draw operations (*[asyncTextureDraw](../../../../api/library/objects/landscape_terrain/class.landscape.md#asyncTextureDraw_int_UGUID_ivec2_ivec2_int_VECWorldBoundBox_void)*) that can be performed per frame. Range of values: **[1, 1000]**. The default value is : **10**. `Console access:render_landscape_operations_per_frame` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_landscape_operations_per_frame)) |
|---|---|
| Mask Dithering | The global dither amount multiplier to be used for rendering details of the [Landscape Terrain](../../../../objects/objects/terrain/landscape_terrain/index.md). Dithering enables reduction of graphical artefacts in case of increased Mask Contrast values set for a detail. This is a global multiplier for dithering values set [for each detail mask](../../../../api/library/objects/landscape_terrain/class.terraindetailmask.md#setDithering_float_void). > **Notice:** [Reloads Landscape Terrain graphic data](../../../../objects/objects/terrain/landscape_terrain/settings.md#runtime_safe). Range of values: **[0.0f, 1.0f]**. The default value is : **1.0f**. `Console access:render_landscape_terrain_mask_dithering` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_landscape_terrain_mask_dithering)) |
| Advanced | Exposes the [Advanced Settings](#advanced) for *Landscape Terrain*. |


## Geometry


![Terrain geometry rendering settings](geometry_preset.png)


| Preset | The index of the Landscape Terrain geometry preset used at the moment. > **Notice:** Presets override user-defined custom settings. When any preset other than Custom is active, modification of the parameters via [API](../../../../api/library/rendering/class.render_cpp.md) has no effect. The parameter value set via the last API call shall be used only when the Custom preset is active. When checking the current parameter value via API you'll get the corresponding setting stored in the active preset (default or custom one). One of the following values: - Low (by default) - Medium - High - Ultra - Extreme - Custom `Console access:render_landscape_terrain_geometry_preset` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_landscape_terrain_geometry_preset)) |
|---|---|
| Holes | The value indicating if [decal-based holes](../../../../objects/objects/terrain/landscape_terrain/index.md#decal_holes) for the [Landscape Terrain](../../../../objects/objects/terrain/landscape_terrain/index.md) are enabled. **enabled** by default. `Console access:render_landscape_terrain_geometry_holes` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_landscape_terrain_geometry_holes)) |
| Visibility Distance | The maximum visibility distance for the [Landscape Terrain](../../../../objects/objects/terrain/landscape_terrain/index.md), in meters. The terrain is visible, as long as the distance between the camera and the terrain does not exceed this value. > **Notice:** [Reloads Landscape Terrain graphic data](../../../../objects/objects/terrain/landscape_terrain/settings.md#runtime_safe). Range of values: **[0.0f, inf]**. The default value is : **30000.0f**. `Console access:render_landscape_terrain_visible_distance` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_landscape_terrain_visible_distance)) |
| Detail Max Height | The maximum height for detail displacement clamping. Adjust this value to the highest height value used in details in case of artifacts of stepped geometry caused by insufficient bit depth. > **Notice:** [Reloads Landscape Terrain graphic data](../../../../objects/objects/terrain/landscape_terrain/settings.md#runtime_safe). Range of values: **[0.0f, 10.0f]**. The default value is : **0.5f**. `Console access:render_landscape_terrain_geometry_detail_max_height` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_landscape_terrain_geometry_detail_max_height)) ![](detail_max_height_0.png) ![](detail_max_height_1.png) |


### Customizable Settings


The following settings are available when the [Custom](#geometry_preset) preset is selected.


![Geometry custom settings](geometry.png)

*Geometry Settings*


| Geometry Progression | The progression of [Landscape Terrain](../../../../objects/objects/terrain/landscape_terrain/index.md) geometry tessellation. > **Notice:** [Reloads Landscape Terrain graphic data](../../../../objects/objects/terrain/landscape_terrain/settings.md#runtime_safe). Range of values: **[0.0f, 50.0f]**. The default value is : **1.5f**. `Console access:render_landscape_terrain_geometry_progression` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_landscape_terrain_geometry_progression)) ![](geometry_progression_1.png) ![](geometry_progression_2.png) |
|---|---|
| Geometry Subpixel Reduction | The minimum ratio between the polygon size (in screen space) to the size of an area in the viewport for [skipping polygons rendering](../../../../objects/objects/terrain/landscape_terrain/settings.md#subpixel_reduction) (the ones having a lower ratio will be removed). > **Notice:** Setting too high values may cause small but noticeable visual artifacts when the camera moves. Range of values: **[0.0f, 50.0f]**. The default value is : **6.0f**. `Console access:render_landscape_terrain_geometry_subpixel_reduction` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_landscape_terrain_geometry_subpixel_reduction)) ![](geometry_subpixel_1.png) ![](geometry_subpixel_2.png) |
| Geometry Polygon Size | The size of Landscape Terrain polygons defining the maximum allowed density of Landscape Terrain geometry. > **Notice:** [Reloads Landscape Terrain graphic data](../../../../objects/objects/terrain/landscape_terrain/settings.md#runtime_safe). Range of values: **[0.0f, 1000.0f]**. The default value is : **0.01f**. `Console access:render_landscape_terrain_geometry_polygon_size` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_landscape_terrain_geometry_polygon_size)) ![](geometry_polygon_size_1.png) ![](geometry_polygon_size_2.png) |


## Streaming


![Terrain streaming rendering settings](streaming_preset.png)


| Preset | The index of the Landscape Terrain streaming preset used at the moment. > **Notice:** Presets override user-defined custom settings. When any preset other than Custom is active, modification of the parameters via [API](../../../../api/library/rendering/class.render_cpp.md) has no effect. The parameter value set via the last API call shall be used only when the Custom preset is active. When checking the current parameter value via API you'll get the corresponding setting stored in the active preset (default or custom one). One of the following values: - Low (by default) - Medium - High - Ultra - Extreme - Custom `Console access:render_landscape_terrain_streaming_preset` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_landscape_terrain_streaming_preset)) |
|---|---|
| Detail Albedo Texture Resolution | The resolution of the albedo texture for details of the [Landscape Terrain](../../../../objects/objects/terrain/landscape_terrain/index.md). > **Notice:** [Reloads Landscape Terrain graphic data](../../../../objects/objects/terrain/landscape_terrain/settings.md#runtime_safe). One of the following values: - 64�64 - 128�128 - 256�256 - 512�512 - 1024�1024 (by default) - 2048�2048 - 4096�4096 - 8192�8192 - 16384�16384 `Console access:render_landscape_terrain_detail_resolution_albedo` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_landscape_terrain_detail_resolution_albedo)) |
| Detail Height Texture Resolution | The resolution of the height texture for details of the [Landscape Terrain](../../../../objects/objects/terrain/landscape_terrain/index.md). > **Notice:** [Reloads Landscape Terrain graphic data](../../../../objects/objects/terrain/landscape_terrain/settings.md#runtime_safe). One of the following values: - 64�64 - 128�128 - 256�256 - 512�512 - 1024�1024 (by default) - 2048�2048 - 4096�4096 - 8192�8192 - 16384�16384 `Console access:render_landscape_terrain_detail_resolution_height` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_landscape_terrain_detail_resolution_height)) |
| Detail Additional Mask Texture Resolution | The resolution of the additional mask texture for details of the [Landscape Terrain](../../../../objects/objects/terrain/landscape_terrain/index.md). > **Notice:** [Reloads Landscape Terrain graphic data](../../../../objects/objects/terrain/landscape_terrain/settings.md#runtime_safe). One of the following values: - 64�64 - 128�128 - 256�256 - 512�512 - 1024�1024 (by default) - 2048�2048 - 4096�4096 - 8192�8192 - 16384�16384 `Console access:render_landscape_terrain_detail_resolution_additional_mask` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_landscape_terrain_detail_resolution_additional_mask)) |
| Detail Compression | The mode of detail textures compression. Compressed detail textures take less video memory. One of the following values: - Disabled - Fast Compression (by default) - High Quality `Console access:render_landscape_terrain_detail_compression` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_landscape_terrain_detail_compression)) |
| Texture Filtering | The filtering mode for the [Landscape Terrain](../../../../objects/objects/terrain/landscape_terrain/index.md) textures. The following values are available: - Low - use the lower mip-level - Medium - use the higher mip-level - High - linearly interpolate between adjacent mip-levels Option **#2** is selected by default (see above). `Console access:render_landscape_terrain_vt_filtering` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_landscape_terrain_vt_filtering)) |
| Target Resolution | The [target resolution](../../../../objects/objects/terrain/landscape_terrain/settings.md#target_resolution) (width x height) for the Landscape Terrain, in pixels. **1344 х 756** - (default) `Console access:render_landscape_terrain_vt_target_resolution` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_landscape_terrain_vt_target_resolution)) |


### Customizable Settings


The following settings are available when the [Custom](#streaming_preset) preset is selected.


![Streaming custom settings](streaming.png)

*Streaming Settings*


| Texture Memory Size | The value defining memory consumption for the [Landscape Terrain](../../../../objects/objects/terrain/landscape_terrain/index.md) textures. The value is interpreted as follows: - 0.0f - 3072�3072 (~200 MB of VRAM) - 1.0f - 16384�16384 (~3.1 GB of VRAM) - **0.4f** - 8192�8192 (~860 MB of VRAM) > **Notice:** [Reloads Landscape Terrain graphic data](../../../../objects/objects/terrain/landscape_terrain/settings.md#runtime_safe). Range of values: **[0.0f, 1.0f]**. The default value is : **0.4f**. `Console access:render_landscape_terrain_vt_memory_size` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_landscape_terrain_vt_memory_size)) |
|---|---|
| Detail Level By Angle | The value indicating detail level reduction depending on the inclination of the the Landscape Terrain polygons relative to viewing direction. Can be used to reduce streaming load and memory consumption. The value of 1 corresponds to the pixel-to-pixel quality, and lower values decrease it. Range of values: **[0.0f, 1.0f]**. The default value is : **0.95f**. `Console access:render_landscape_terrain_vt_detail_level_by_angle` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_landscape_terrain_vt_detail_level_by_angle)) ![](detail_by_angle_1.png) ![](detail_by_angle_2.png) |
| Tiles Update Per Frame | The number of tiles passed to the virtual texture of the [Landscape Terrain](../../../../objects/objects/terrain/landscape_terrain/index.md) each frame. Range of values: **[1, 256]**. The default value is : **60**. `Console access:render_landscape_terrain_vt_tiles_update_per_frame` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_landscape_terrain_vt_tiles_update_per_frame)) |
| Tiles Load Per Frame | The number of [Landscape Terrain](../../../../objects/objects/terrain/landscape_terrain/index.md) tiles loaded per frame. You can decrease the value of this parameter to reduce spikes, but in this case streaming becomes slower and more noticeable. Range of values: **[1, 64]**. The default value is : **4**. `Console access:render_landscape_terrain_vt_tiles_load_per_frame` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_landscape_terrain_vt_tiles_load_per_frame)) |
| Tiles Reload Per Frame | The number of tiles to be reloaded per frame after applying changes to the [Landscape Terrain](../../../../objects/objects/terrain/landscape_terrain/index.md) surface. Range of values: **[1, 64]**. The default value is : **4**. `Console access:render_landscape_terrain_vt_tiles_reload_per_frame` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_landscape_terrain_vt_tiles_reload_per_frame)) |
| Texel Size | The texel size of the [Landscape Terrain](../../../../objects/objects/terrain/landscape_terrain/index.md) render textures representing the maximum level of detail for the albedo, normal, and height components of the Landscape Terrain. > **Notice:** [Reloads Landscape Terrain graphic data](../../../../objects/objects/terrain/landscape_terrain/settings.md#runtime_safe). Range of values: **[0.0001f, 1.0f]**. The default value is : **0.001f**. `Console access:render_landscape_terrain_texel_size` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_landscape_terrain_texel_size)) ![](texel_size_1.png) ![](texel_size_2.png) |


## Culling


![](culling.png)


| Culling By Depth | The  value indicating if culling by depth is enabled. Keep this option enabled to get the performance higher due to culling of tiles occluded by geometry and Landscape Terrain itself. **enabled** by default. `Console access:render_landscape_terrain_culling_by_depth` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_landscape_terrain_culling_by_depth)) |
|---|---|
| Culling Frustum Aggressive | The value indicating if frustum culling optimization is enabled for the [Landscape Terrain](../../../../objects/objects/terrain/landscape_terrain/index.md). When enabled, the number of culled polygons increases thereby increasing performance. In case of any issues with polygons rendering, try disabling this option (however, note that performance may drop). **enabled** by default. `Console access:render_landscape_terrain_culling_frustum_aggressive` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_landscape_terrain_culling_frustum_aggressive)) |
| Culling Oblique Frustum | The multiplier for culling of tessellation patches of the [Landscape Terrain](../../../../objects/objects/terrain/landscape_terrain/index.md) beyond the oblique frustum plane. *Higher* values result in more patches culled. Range of values: **[0.0f, 1.0f]**. The default value is : **0.9f**. `Console access:render_landscape_terrain_culling_oblique_frustum` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_landscape_terrain_culling_oblique_frustum)) |


## Cache


![](cache.png)


| CPU Cache Size | The CPU cache size to be used for landscape terrain rendering, in percentage of the total memory. CPU cache size affects intersections, physics, streaming, etc. The size of CPU cache depends on the scene. Range of values: **[1, 100]**. The default value is : **10**. `Console access:render_landscape_cache_cpu_size` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_landscape_cache_cpu_size)) |
|---|---|
| CPU Cache Prefetch Radius | The radius within which heights data is pre-loaded into memory for correct calculation of collisions and intersections. Range of values: **[0.0f, inf]**. The default value is : **0.0f**. `Console access:render_landscape_cache_cpu_prefetch_radius` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_landscape_cache_cpu_prefetch_radius)) |
| GPU Cache Size | The GPU cache size to be used for landscape terrain rendering, in percentage of the total GPU memory. GPU cache is used to accumulate tiles, that are visible to the camera, before streaming them to the megatexture. > **Notice:** High-resolution maps require larger cache capacity. Range of values: **[1, 100]**. The default value is : **4**. `Console access:render_landscape_cache_gpu_size` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_landscape_cache_gpu_size)) |
| GPU Cache Life Time | The lifetime of GPU cache used for Landscape Terrain rendering, in frames. Range of values: **[1, 60]**. The default value is : **4**. `Console access:render_landscape_cache_gpu_life_time` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_landscape_cache_gpu_life_time)) |


## Advanced Settings


The following settings are available when the [Advanced](#option_advanced) option is enabled. The advanced settings do not affect the visual quality of *Landscape Terrain* and intended for fine tuning of data streaming and rendering performance-wise.


> **Warning:** It is not recommended to make changes to the default values without understanding these settings. Improper configuration may lead to major performance issues.


### Advanced Streaming Settings


![Advanced terrain streaming settings](streaming_advanced.png)


| Sampler Feedback Screen Resolution | The resolution of the screen buffer used to detect visible tiles and what MIP-levels to be loaded. > **Notice:** [Reloads Landscape Terrain graphic data](../../../../objects/objects/terrain/landscape_terrain/settings.md#runtime_safe). One of the following values: - Quarter - Half (by default) - Full `Console access:render_landscape_terrain_vt_sampler_feedback_screen_resolution` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_landscape_terrain_vt_sampler_feedback_screen_resolution)) |
|---|---|
| Sampler Feedback Buffer Resolution | The resolution of the buffer used to transfer data about tiles and what MIP-levels to be loaded. > **Notice:** [Reloads Landscape Terrain graphic data](../../../../objects/objects/terrain/landscape_terrain/settings.md#runtime_safe). From **1x1** to **1024x1024** Default: **80x60** `Console access:render_landscape_terrain_vt_sampler_feedback_buffer_resolution` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_landscape_terrain_vt_sampler_feedback_buffer_resolution)) |
| Streaming Threads | The  number of threads used for streaming. Range of values: **[0, 32]**. The default value is : **1**. `Console access:render_landscape_terrain_streaming_threads` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_landscape_terrain_streaming_threads)) |
| Streaming Per Lods | The value indicating if streaming per LODs (MIP maps) is enabled. Disable this option to make streaming faster by skipping loading of intermediate MIP-levels for textures. **enabled** by default. `Console access:render_landscape_terrain_streaming_per_lods` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_landscape_terrain_streaming_per_lods)) |


### Advanced Culling Setings


![](culling_advanced.png)


| Culling Depth Resolution | The  resolution of the buffer used for culling by depth. Range of values: **[4, 2048]**. The default value is : **64**. `Console access:render_landscape_terrain_culling_depth_resolution` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_landscape_terrain_culling_depth_resolution)) |
|---|---|
| Culling Patch Resolution GPU | The  number of subdivisions for patches of [Landscape Terrain](../../../../objects/objects/terrain/landscape_terrain/index.md) culled on the GPU side that are to be tessellated. By lowering this value you reduce the load on CPU, by increasing it you reduce the load on GPU. The point is to find a trade-off between loads in the given conditions on the target hardware. Range of values: **[4, 64]**. The default value is : **32**. `Console access:render_landscape_terrain_culling_patch_resolution_gpu` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_landscape_terrain_culling_patch_resolution_gpu)) |
| Culling Patch Resolution CPU | The  number of subdivisions for patches of [Landscape Terrain](../../../../objects/objects/terrain/landscape_terrain/index.md) culled on the CPU side that are to be passed to GPU. The lowest value of 2 corresponds to no subdivisions at all, i.e. all patched will be culled on the CPU side. By increasing this value you can reduce the load on CPU as more patches will be checked for visibility on the GPU side. Range of values: **[2, 64]**. The default value is : **2**. `Console access:render_landscape_terrain_culling_patch_resolution_cpu` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_landscape_terrain_culling_patch_resolution_cpu)) |
| Culling Patch Batching | The  number of culling patches of [Landscape Terrain](../../../../objects/objects/terrain/landscape_terrain/index.md) processed in a batch. The higher this value, the more patches will be checked for visibility on CPU at once. Range of values: **[1, 64]**. The default value is : **16**. `Console access:render_landscape_terrain_culling_patch_batching` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_landscape_terrain_culling_patch_batching)) |
| Culling Padding Triangles | The  padding between LODs of tessellated polygons. Range of values: **[0.0f, inf]**. The default value is : **1.0f**. `Console access:render_landscape_terrain_culling_padding_triangles` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_landscape_terrain_culling_padding_triangles)) |
| Culling Padding Patch GPU | The  padding between LODs of patches culled on GPU. Range of values: **[0.0f, inf]**. The default value is : **1.0f**. `Console access:render_landscape_terrain_culling_padding_patch_gpu` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_landscape_terrain_culling_padding_patch_gpu)) |
| Culling Padding Patch CPU | The  padding between LODs of patches culled on CPU. Range of values: **[0.0f, inf]**. The default value is : **1.0f**. `Console access:render_landscape_terrain_culling_padding_patch_cpu` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_landscape_terrain_culling_padding_patch_cpu)) |
| Culling Map | The  extent of culling of [Landscape Layer Maps](../../../../objects/objects/terrain/landscape_terrain/landscape_layer_map.md) with the distance. In case small Landscape Layer Maps disappear too soon with the distance, try increasing this value. > **Notice:** [Reloads Landscape Terrain graphic data](../../../../objects/objects/terrain/landscape_terrain/settings.md#runtime_safe). Range of values: **[0.0f, 1.0f]**. The default value is : **0.3f**. `Console access:render_landscape_terrain_culling_map` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_landscape_terrain_culling_map)) |
