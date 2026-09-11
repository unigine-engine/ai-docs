# Streaming


This section contains settings related to resource streaming.


![Streaming settings](streaming.png)

*Streaming Settings*


| Free Space VRAM | The amount of VRAM that the Engine will always keep free and never allocate for its own use, in Mbytes. Range of values: **[0, INT_MAX]**. The default value is : **512**. `Console access:render_streaming_free_space_vram` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_streaming_free_space_vram)) |
|---|---|
| Free Space RAM | The amount of physical memory that the Engine will always keep free and never allocate for its own use, in Mbytes. Range of values: **[0, INT_MAX]**. The default value is : **1024**. `Console access:render_streaming_free_space_ram` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_streaming_free_space_ram)) |
| Particles Memory Limit (%) | The cache memory limit for vertices of particle systems, in percentage of the total GPU memory. > **Notice:** Setting a too low limit for a huge number of particle systems in the scene may lead to rendering only some of them. Works only with the **Vulkan** graphics API. Range of values: **[0, 100]**. The default value is : **3**. `Console access:render_streaming_particles_memory_limit` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_streaming_particles_memory_limit)) |
| VRAM Budget | The mode for determining the amount of available VRAM. The following modes are available: - *System* - the available VRAM size is obtained from the operating system. - *Driver* - the VRAM available for the application is determined by the video driver. - *Full GPU Memory* - all VRAM is available for the application. One of the following values: - System - Driver (by default) - Full GPU Memory `Console access:render_streaming_vram_budget` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_streaming_vram_budget)) |
| VRAM Overcommit | The value indicating whether VRAM limits (both the usage limit and free space) are applied. **disabled** by default. `Console access:render_streaming_vram_overcommit` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_streaming_vram_overcommit)) |
| Committed Memory Overcommit | The value indicating whether the Engine enforces internal limits on committed memory usage. - When **disabled**, the Engine respects the **Free Space Committed RAM** setting and will not allocate more committed memory than the configured limit allows. In this mode, the amount of physical RAM and VRAM available to the Engine is effectively reduced to the portion of committed memory accessible within this limit. - When **enabled** (default), the Engine ignores the **Free Space Committed RAM** restriction and can use **all available committed memory** provided by the system. This may improve streaming performance, especially under high memory pressure (for example, when browsers or other background applications are running, or after long system uptime), but it also increases the risk of instability if the system runs out of virtual memory. > **Warning:** With overcommit enabled, crashes may occur if: > > > - the system has no page file > - there is insufficient free disk space on the drive where the page file is located. > > > If system committed memory is fully exhausted, this may affect not only the Engine, but also **other running applications**. **enabled** by default. `Console access:render_streaming_committed_memory_overcommit` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_streaming_committed_memory_overcommit)) |
| Usage Limit VRAM | The percentage of the committed video memory available for streaming. If the streaming exceeds the VRAM usage limit, it will start using RAM for loading graphic resources. Range of values: **[10, 100]**. The default value is : **80**. `Console access:render_streaming_usage_limit_vram` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_streaming_usage_limit_vram)) |
| Usage Limit RAM | The percentage of the total physical memory (RAM) that the Engine is allowed to use for streaming. If the streaming exceeds the RAM usage limit, the application may become unstable or crash. Range of values: **[10, 100]**. The default value is : **80**. `Console access:render_streaming_usage_limit_ram` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_streaming_usage_limit_ram)) |
| Cache VRAM | The  maximum size of VRAM available for streaming caches. When set to -1, caches grow freely up to [engine limits](#render_streaming_usage_limit_vram). When limited, caches will grow only up to the defined value. If the limit is too low, not all resources will fit into the cache in time, which may cause streaming to stutter. Range of values: **[-1, inf]**. The default value is : **-1**. `Console access:render_streaming_cache_vram` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_streaming_cache_vram)) |
| Cache RAM | The  maximum size of RAM available for streaming caches. When set to -1, caches grow freely up to [engine limits](#render_streaming_usage_limit_ram). When limited, caches will grow only up to the defined value. If the limit is too low, not all resources will fit into the cache in time, which may cause streaming to stutter. Range of values: **[-1, inf]**. The default value is : **-1**. `Console access:render_streaming_cache_ram` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_streaming_cache_ram)) |


## Shaders


| Compile Mode | The compilation mode for shaders that are used in the loaded world. The following modes are available: - *Async* - shaders are compiled in a background thread. Objects whose shaders are not yet ready are not rendered (pop-in effect). - *Force* - shaders are compiled synchronously on the main thread. The application freezes until the shader is ready, but objects are rendered immediately. > **Notice:** This setting does not affect post-processing shaders, lightmap data shaders, and materials with forced compilation - these are always compiled synchronously regardless of this setting. Option **#1** is selected by default (see above). `Console access:render_shaders_compile_mode` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_shaders_compile_mode)) |
|---|---|


## Textures


| Streaming Mode | The streaming mode for textures. The following modes are available: - *Async* - asynchronous loading of textures. - *Force* - force-loading of textures required for each frame at ones. Option **#1** is selected by default (see above). `Console access:render_streaming_textures_mode` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_streaming_textures_mode)) |
|---|---|
| Mipmaps | The value indicating whether texture mipmap loading is enabled. **disabled** by default. `Console access:render_streaming_textures_mipmaps` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_streaming_textures_mipmaps)) |
| Mipmaps Density | The density of mipmaps relative to the screen resolution. This value helps to define which mipmap should be loaded at the current moment. You can specify different values for different quality presets. Range of values: **[0.0f, 1000000.0f]**. The default value is : **2.0f**. `Console access:render_streaming_textures_mipmaps_density` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_streaming_textures_mipmaps_density)) |


## Meshes GPU


| Streaming Mode | The streaming mode for loading meshes to video memory (VRAM). The following modes are available: - *Async* - asynchronous loading of meshes. - *Force* - force-loading of meshes required for the current frame at once. Option **#1** is selected by default (see above). `Console access:render_streaming_meshes_mode_vram` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_streaming_meshes_mode_vram)) |
|---|---|


## Meshes CPU


| Streaming Mode | The streaming mode for loading meshes to memory (RAM). The following modes are available: - *Async* - asychronous loading of meshes. - *Force* - force-loading of meshes required for the current frame at once. Option **#1** is selected by default (see above). `Console access:render_streaming_meshes_mode_ram` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_streaming_meshes_mode_ram)) |
|---|---|


## Animations


| Streaming Mode | The streaming mode for skinned mesh animations. The following modes are available: - *Async* - asynchronous loading of animations. - *Force* - force-loading of animations required for the current frame at once. Option **#2** is selected by default (see above). `Console access:render_streaming_animations_mode` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_streaming_animations_mode)) |
|---|---|
| Life Time | The lifetime of the RAM cache used for animation streaming, in frames. When an animation is no longer used, it remains in the cache for this number of frames before being unloaded, so that it can be reused without reloading. The default value of -1 keeps animations in memory permanently - they are never unloaded. Values below 6 are clamped to 6 frames. Range of values: **[-1, INT_MAX]**. The default value is : **-1**. `Console access:render_streaming_animations_life_time` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_streaming_animations_life_time)) |


## Prefetch CPU


| Collision Mode | The mode of asynchronous pre-loading of meshes to memory before they are used. Pre-loading is available only for meshes, which have at least one surface with the *Collision* flag set. There are 2 modes of loading such meshes to RAM: - *Disable* - loading is disabled. - *Radius* - meshes within the prefetch radius are loaded. This method should be used when the *Async* streaming mode for meshes is set. Option **#1** is selected by default (see above). `Console access:render_streaming_meshes_prefetch_collision` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_streaming_meshes_prefetch_collision)) |
|---|---|
| Intersection Mode | The mode of asynchronous pre-loading of meshes into memory before they are used. Pre-loading is available only for meshes, which have at least one surface with the *Intersection* flag set. There are 2 modes of loading such meshes to RAM: - *Disable* - loading is disabled. - *Radius* - all meshes within the prefetch radius are loaded. This method should be used when the *Async* streaming mode for meshes is set. Option **#1** is selected by default (see above). `Console access:render_streaming_meshes_prefetch_intersection` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_streaming_meshes_prefetch_intersection)) |
| Radius | The radius within which meshes are pre-loaded into memory. The value should exceed the physics radius (for collisions) and/or the radius within which intersections are calculated. Range of values: **[0.0f, inf]**. The default value is : **0.0f**. `Console access:render_streaming_meshes_prefetch_radius` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_streaming_meshes_prefetch_radius)) |
