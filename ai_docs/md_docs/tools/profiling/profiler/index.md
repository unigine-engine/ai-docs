# Performance Profiler


A performance profiler displays performance data in a timeline. It reports how much time is spent per each frame for updating all aspects of your project: rendering nodes that are in view, updating their states, executing scripts with game logic, calculating physics, etc.


With the profiler, you can:


- Detect the bottlenecks of your application
- Check if art assets optimization is required
- Check if code optimization is required
- Compare the profiling results before and after the changes


![](profiler.png)

*Performance Profiler*


## Activating Profiler


To show profiler statistics in runtime, type the *[`show_profiler 1`](../../../code/console/index.md#show_profiler)* command in the console. To disable the profiler in runtime, type *`show_profiler 0`* in the console.


You can configure the information displayed by the profiler by using the corresponding *[console commands](../../../code/console/index.md#show_profiler)*.


The following profiling modes are available:


- *[Generic](#generic)* shows only the general statistics data.
- *[Rendering](#render)* shows the detailed rendering statistics.
- *[Memory](#memory)* shows the detailed visualization of the memory consumption data.
- *[Physics](#physics)* shows the detailed physics-related statistics (within the [Physics radius](../../../editor2/settings/physics_global/index.md#physics_distance)).
- *[World Management](#world)* shows the statistics on the whole loaded world.
- *[Thread](#thread)* shows the statistics on loading threaded resources.
- Visualization of the *[table](../../../code/console/index.md#show_profiler_table)* and *[timeline charts](../../../code/console/index.md#show_profiler_charts)* is also configurable by the console commands.


In the Editor, the profiler is also accessible via the toolbar (*Tools -> Performance Profiler*):


![](profiler_run.png)


> **Notice:** You can also set a hot key (or a key combination) that will run the profiler in the *Hotkeys* section of the *[Settings](../../../editor2/settings/hotkeys/index.md)* window. However, you will have to create a [custom preset](../../../editor2/settings/hotkeys/index.md#custom_presets).


## Generic Profiler


![](generic_profiler.png)

*Generic Profiler Enabled*


| Resolution: |  |
|---|---|
| Resolution | Output display resolution used for presenting the final rendered image. |
| Render Resolution | Internal resolution at which the scene is rendered before upscaling is applied. (Displayed only when [DLSS](../../../principles/render/upscaling/index.md#dlss_use) or [FSR](../../../principles/render/upscaling/index.md#fsr2_use) is enabled.) |
| Upscaler | Current upscaling method in use (FSR or DLSS), including the active mode, preset, and custom scale (if specified). |
| Charts: |  |
| FPS | Current Engine framerate. Shown only if [Profiler Dump](../../../tools/profiling/profiler_dump/index_cpp.md) is being recorded. |
| Total | Total time in milliseconds taken to both calculate and render the current frame. This is the duration of the [main loop](../../../code/fundamentals/execution_sequence/main_loop.md) in the application [execution sequence](../../../code/fundamentals/execution_sequence/index.md). |
| Total CPU | Total time in milliseconds taken to prepare the current frame (including *update, render*, and *swap*). |
| Total GPU | GPU execution time measured using timestamp queries from the graphics API. Represents the duration of GPU work for a single frame. > **Notice:** Since the data is taken from the graphics API, therefore, convergence with the other timings received by the engine itself is not guaranteed. |
| Update | Time taken to update application logic. This includes executing all steps in the [***update()***](../../../code/fundamentals/execution_sequence/main_loop.md#update) function of the world script. It also includes the update of states of all nodes (for example, update of the skinned animation or of a particle system to spawn new particles). - If the Update time is too high, it signals that you need to optimize the application logic executed each frame. - You may also need to decrease the number of objects in the world, as updating their states (spawn particles by the particle systems, play skinned mesh animation, etc.) increases the load. |
| Render CPU | Time taken to prepare all data to be rendered in the current frame and feed rendering commands from the CPU to the GPU. If Render CPU time is too high, it signals that art assets may need to be optimized, for example: - [LOD](../../../principles/world_management/index.md#lods) system should be used; - polygon count of models should be reduced. |
| Waiting GPU | Time between completing all calculations on the CPU up to the moment when the GPU has finished rendering the frame. (See the [illustration](../../../code/fundamentals/execution_sequence/index.md#waiting_gpu)). This counter is useful to analyze the bottleneck in your application's performance. - When Waiting GPU time is equal to **0**, it signals that scripts take too long to be updated and calculations are too intensive for CPU to perform them fast enough. In this case, your application has a CPU bottleneck. Optimize your update block in the world scripts or reduce the number of objects updated each frame. - High Waiting GPU time means one of the following: - low framerate signals that there exists a GPU bottleneck. The art content needs to be optimized in this case. - consistently high framerate means you have free CPU resources available to process more numbers in the *update()* of the world script. |
| Waiting FPS Lock | Time taken to maintain a fixed frame rate when an FPS limit is set. This represents the idle time the Engine spends waiting to synchronize with the specified frame rate target. > **Notice:** This metric is not displayed if no FPS limit is set. In that case, the Engine immediately starts processing the next frame. |
| Interface | Time taken to render all GUI widgets. |
| Total Physics | Time taken to perform all physics calculations. |
| Waiting Physics | Time period during which the physics module waits for the completion of rendering process to return to the Main thread and execute the rest of the physics ticks. > **Notice:** In addition to the individual values listed above, average characteristics are also calculated and displayed. |
| Flush Physics | Time taken to synchronize all physics states. |
| CPU RAM General: |  |
| CPU ram free | Unused available physical RAM in the system. |
| CPU ram usage | Amount of system RAM used by the engine process. `CPU ram active+CPU ram cache` |
| CPU ram limit | Maximum amount of physical RAM available to the engine, considering both *[render_streaming_free_space_ram](../../../api/library/rendering/class.render_cpp.md#render_streaming_free_space_ram)* and *[render_streaming_usage_limit_ram](../../../code/console/index.md#render_streaming_usage_limit_ram)*. |
| CPU ram active | Amount of system RAM actively used by the engine excluding cached memory (CPU ram cache). `CPU ram usage-CPU ram cache` |
| CPU ram cache | Amount of system RAM used to cache streamed assets, including skinned meshes, static meshes, and textures. `CPU ram usage-CPU ram active` |
| CPU RAM Committed (**available only for Windows**): |  |
| CPU ram committed free | Amount of committed system memory currently available for use, excluding the portion reserved for streaming. When [render_streaming_committed_memory_overcommit](../../../api/library/rendering/class.render_cpp.md#render_streaming_committed_memory_overcommit) is enabled, the value represents the full free committed memory of the system. Otherwise, it is adjusted by [render_streaming_free_space_ram_committed](../../../api/library/rendering/class.render_cpp.md#render_streaming_free_space_ram_committed). |
| CPU ram committed usage | Amount of committed memory currently used by the engine process. |
| CPU ram committed background | Amount of committed memory currently used by all background processes. |
| CPU ram committed limit | Amount of committed system memory that the engine process is allowed to commit. This value is available only when [render_streaming_committed_memory_overcommit](../../../api/library/rendering/class.render_cpp.md#render_streaming_committed_memory_overcommit) is disabled and represents the total committed system memory minus the portion reserved for streaming ([render_streaming_free_space_ram_committed](../../../api/library/rendering/class.render_cpp.md#render_streaming_free_space_ram_committed)). |
| CPU ram committed total | Total amount of committed system memory. |
| CPU Memory Allocations: |  |
| CPU ram malloc | The amount of memory allocated by the UNIGINE custom allocator. |
| Frame Allocations | The number of allocations made per frame. The UNIGINE allocator allocates memory in [pools](../../../principles/allocator/index.md#memory_pools) which allows the allocation to be faster and more efficient. |
| Live Allocations | The current number of allocations made / The maximum number of allocations made during runtime (peak consumption). |
| GPU RAM General: |  |
| GPU ram usage | Amount of RAM currently used by GPU for the engine process. |
| GPU ram background | Amount of RAM currently used by GPU for all background processes. |
| GPU VRAM General: |  |
| GPU vram free | Amount of GPU video memory currently available for use, calculated based on configured streaming limits and budget. |
| GPU vram usage | Amount of VRAM currently available for use, calculated based on configured streaming limits and budget. `GPU vram active+GPU vram cache` |
| GPU vram background | Current amount of VRAM used by all background processes. |
| GPU vram limit | Amount of VRAM available to the engine process based on: - *[render_streaming_vram_budget](../../../api/library/rendering/class.render_cpp.md#render_streaming_vram_budget)* - *[render_streaming_usage_limit_vram](../../../api/library/rendering/class.render_cpp.md#render_streaming_usage_limit_vram)* - *[render_streaming_free_space_vram](../../../api/library/rendering/class.render_cpp.md#render_streaming_free_space_vram)* |
| GPU vram budget | OS-provided VRAM budget. |
| GPU vram total | Total amount of VRAM available in the system. |
| GPU vram active | Amount of GPU video memory currently in active use, excluding cached resources. `GPU vram usage-GPU vram cache` |
| GPU vram cache | Amount of GPU memory used to store cached streamed assets, including skinned meshes, static meshes, and textures. `VRAM Textures Unused + VRAM Meshes Static Unused + VRAM Meshes Skinned unused` You can limit maximum size of VRAM Caches using *[render_streaming_cache_vram](../../../api/library/rendering/class.render_cpp.md#render_streaming_cache_vram)* |


## Memory Profiler


![](memory_profiler.png)

*Memory Profiler Enabled*


The following statistics are displayed in addition to the [generic](#generic) one:


| CPU RAM Pools: |  |
|---|---|
| CPU ram static pool | Memory pool pre-allocated at engine startup for small-sized allocations (features fixed-size blocks, e.g., 16, 32, 48 bytes). Static pools must be configured and tuned using memory statisctics (*[memory_info](../../../code/console/index.md#memory_info)* and *[memory_optimize_static_pools](../../../code/console/index.md#memory_optimize_static_pools)*) |
| CPU ram dynamic pool | Flexible memory pool that grows and shrinks dynamically for allocation sizes beyond configured static pools capacity. Available on Windows only. |
| CPU ram instance pool | Developer-defined memory pools, share allocator behavior with dynamic pools but with no size limitations. > **Notice:** Learn more about **pools** here: **[Memory Allocator](../../../principles/allocator/index.md)** |
| GPU Memory Allocations: |  |
| GPU vram alloc | The amount of vram allocated made by the engine on the GPU side. |
| GPU ram alloc | The amount of ram allocated made by the engine on the GPU side. |
| GPU Frame Allocations | The number of video memory allocations made per frame. |
| GPU Live Allocations | The current number of allocations made / The maximum number of allocations made during runtime (peak consumption). |
| GPU Allocator small pool size | The maximum size of the VRAM pool for small allocations. |
| GPU Allocator small pool usage | Actual usage of the video memory pool for small allocations. |
| RAM Usage Advanced: |  |
| RAM ImagePool | RAM usage managed by the ImagePool, which handles all Image class instances. |
| RAM StringPool | RAM usage managed by the StringPool, which handles all String instances. The string pool increases performance, as it stores only one string instead of its several duplicates. However, this pool is cleared only on the engine shutdown, so it is important to keep its size at the adequate level during runtime. |
| RAM GUI | Amount of RAM currently used for GUI. |
| RAM FFP | Amount of RAM currently used for FFP. |
| RAM Sounds | Amount of RAM currently used for sound assets. Cache limits for sounds can be adjusted using: - *[sound_manager_sample_static_memory](../../../code/console/index.md#sound_manager_sample_static_memory)* - *[sound_manager_sample_stream_memory](../../../code/console/index.md#sound_manager_sample_stream_memory)* |
| RAM Terrain | Memory (RAM) amount currently used for terrain streaming, and the memory limit set for it. The memory limit is the maximum amount of RAM that can be used for terrain streaming. Limit is adjustable via *[render_landscape_cache_cpu_size](../../../api/library/rendering/class.render_cpp.md#render_landscape_cache_cpu_size)*. |
| RAM Animations | Memory (RAM) amount currently used for animations (stored in the `.anim` files). |
| RAM Meshes Static | Total amount of RAM currently used for streaming static meshes. > **Notice:** The same static mesh will use more RAM than [VRAM](#vram_meshes_static), as additional data is generated in RAM to calculate collisions, intersections, spatial trees and so on. |
| RAM Meshes Procedural Dynamic | The total amount of RAM currently used for streaming procedural dynamic meshes. |
| RAM Meshes Skinned | Total amount of RAM currently used for streaming skinned meshes. |
| RAM Meshes Static Used | Amount of RAM actively used for static meshes rendering. |
| RAM Meshes Static Unused | Amount of RAM reserved for cached static meshes that are currently not in use. |
| RAM Meshes Skinned Used | Amount of RAM actively used for skinned meshes rendering. |
| RAM Meshes Skinned Unused | Amount of RAM reserved for skinned meshes that are currently not in use. |
| RAM Animations Used | Amount of RAM, in megabytes, currently used by animations that are actively in use. |
| RAM Animations Unused | Amount of RAM, in megabytes, used by animations that are no longer in use but are kept in the streaming cache for possible reuse (see the [animation lifetime](../../../principles/data_streaming/index.md#animation_streaming)). |
| RAM Animations Held | Amount of RAM, in megabytes, used by animations that are explicitly held in memory and are never unloaded until released. |
| VRAM Usage Advanced: |  |
| VRAM Render Buffers Used | Amount of VRAM actively used for rendering buffers (Gbuffer, post-effects, etc.). |
| VRAM Render Buffers Unused | Amount of VRAM currently reserved for rendering buffers (Gbuffer, post-effects, etc.) that are currently not in use. |
| VRAM Textures | Total amount of VRAM currently used for textures. |
| VRAM GUI | Amount of VRAM currently used for GUI. Visible only if GUI is present in the world. |
| VRAM Geometry Grass | Amount of VRAM currently used for vertices of grass. Visible only if Grass present in the world. |
| VRAM Geometry Particles | Amount of VRAM currently used for vertices of particle systems, and the maximum amount of VRAM that can be used for them. Visible only if Particle Systems are present in the world. Avaiable only when using **Vulkan** API. This values are adjustable via: - *[render_streaming_particles_memory_limit](../../../api/library/rendering/class.render_cpp.md#render_streaming_particles_memory_limit)* - *[particles_memory_preload](../../../code/console/index.md#particles_memory_preload)* |
| VRAM Geometry Decals | Amount of VRAM currently used for decals. |
| VRAM Meshes Static | Total amount of VRAM currently used for streaming static meshes. |
| VRAM Meshes Procedural Dynamic | Total amount of VRAM currently used for procedural meshes. |
| VRAM Meshes Skinned | Total amount of VRAM currently used for skinned meshes. |
| VRAM Terrain | Total amount of VRAM currently used for terrain: [Cache](#vram_terrain_cache) + [Virtual Texture](#vram_terrain_virtual_texture) + [Detail Textures](#vram_terrain_detail_textures) |
| VRAM Usage Upscaler (FSR or DLSS) | Total amount of VRAM currently used by the active upscaler ([DLSS](../../../principles/render/upscaling/index.md#dlss_use) or [FSR](../../../principles/render/upscaling/index.md#fsr2_use)). The value may remain constant, as the upscaler allocates fixed-size textures to avoid reallocation and excessive VRAM usage during dynamic changes. Shown only if the corresponding upscaler is enabled. |
| VRAM Small Pool unallocated | Free VRAM on the Small Pool `GPU Allocator small pool size-GPU Allocator small pool usage`. |
| VRAM Unaccounted | Represents VRAM not allocated through the engine. `GPU VRAM Usage-GPU VRAM Alloc` |
| VRAM Textures Used | Amount of VRAM actively used for textures rendering. |
| VRAM Textures Unused | Amount of VRAM currently used for textures cache. |
| VRAM Meshes Static Used | Amount of VRAM actively used for static meshes rendering. |
| VRAM Meshes Static Unused | Amount of VRAM used for cached static meshes. |
| VRAM Meshes Skinned Used | Amount of VRAM actively used for skinned meshes rendering. |
| VRAM Meshes Skinned Unused | Amount of VRAM used for cached skinned meshes. |
| VRAM Meshes Skinned Allocator: |  |
| VRAM Meshes Skinned Allocator Size | Total allocated video memory reserved for skinned mesh data; if usage exceeds current size, the allocator expands. You can configure the size of a skinned mesh chunk using the *[skinned_mesh_pool_chunk_size](../../../code/console/index.md#skinned_pool_chunk_size)* setting. Reducing the chunk size may lead to performance degradation, as it's more efficient to perform skinning when the geometry fits within a single chunk. |
| VRAM Meshes Skinned Allocator Usage | Amount of video memory currently in use for storing skinned mesh data; reflects how much of the reserved allocator space is actively occupied. |
| VRAM Meshes Decals Allocator: |  |
| VRAM Meshes Decals Allocator Size | Total video memory allocated for decal mesh data; defines the reserved memory pool size used specifically for rendering mesh-based decals. You can configure the size of a decal chunk using the *[decal_pool_chunk_size](../../../code/console/index.md#decal_pool_chunk_size)* setting. Unlike skinned meshes, reducing the chunk size does not negatively impact performance. |
| VRAM Meshes Decals Allocator Usage | Amount of allocated video memory currently used by mesh decals; indicates how much of the decal memory pool is actively occupied. |
| VRAM Terrain: |  |
| VRAM Terrain Cache | GPU memory used for cached terrain tiles (landscape data) and the VRAM cache limit for terrain. Visible only if ObjectLandscapeTerrain is present. Limit is adjustable via: . |
| VRAM Terrain Virtual Texture | Amount of VRAM currently used for the *Landscape Terrain* virtual texture. Visible only if ObjectLandscapeTerrain is present. The amount of VRAM allocated for virtual textures can be adjusted using the *[render_landscape_terrain_vt_memory_size](../../../api/library/rendering/class.render_cpp.md#render_landscape_terrain_vt_memory_size)* command. Note that this value is stored in a custom preset, which is activated by setting *[render_landscape_terrain_streaming_preset](../../../api/library/rendering/class.render_cpp.md#render_landscape_terrain_streaming_preset)* to 5. |
| VRAM Terrain Detail Textures | Amount of VRAM currently used for *Landscape Terrain* details. Visible only if ObjectLandscapeTerrain is present. |
| Streaming needs: |  |
| RAM Streaming need | Amount of system RAM additionally needed to load currently required assets. A positive value indicates that the engine is short on RAM for streaming and will start freeing caches to load new assets. |
| VRAM Streaming need | Amount of system VRAM additionally needed to load currently required assets. A positive value indicates that the engine is short on VRAM for streaming and will start freeing caches to load new assets. |


## Rendering Profiler


![](rendering_profiler.png)

*Rendering Profiler Enabled*


The following statistics are displayed in addition to the [generic](#generic) and [memory](#memory) statistics:


| Render Terrain: |  |
|---|---|
| Terrain Reload Tiles | Number of Landscape Terrain tiles that are currently awaiting reloading after being modified. |
| Terrain Reload Bounds | Number of events causing reloading of tiles (one bound may cause reloading of multiple tiles). |
| Lights: |  |
| Lights All | Number of light passes rendered per frame. This means that the counter displays the number of all light sources that are currently seen illuminating something in the viewport. This value also includes additional passes for rendering lights in the reflecting surfaces (if dynamical reflections are used). Plain 2D reflection will multiply the number of rendering passes by two, while cubemap-based reflection with six faces updated each frame will multiply the number of rendering passes by six. > **Notice:** Each light redraws mesh polygons it illuminates. That is why the higher the number of light sources, the higher the number of polygons the graphics card has to render, and the lower the performance. For example, using two omni lights will as much as double the rendered geometry they shine on. |
| Lights Omni (Viewports) | Number of rendered [Omni lights](../../../objects/lights/omni/index.md) visible in the main viewport. |
| Lights Proj (Viewports) | Number of rendered [Projected lights](../../../objects/lights/proj/index.md) visible in the main viewport. |
| Lights World (Viewports) | Number of rendered [World lights](../../../objects/lights/world/index.md) visible in the main viewport. |
| Lights Environment Probe (Viewports) | Number of rendered [Environment probes](../../../objects/lights/envprobe/index.md) in the main viewport. |
| Lights Voxel Probe (Viewports) | Number of rendered [Voxel probes](../../../objects/lights/voxelprobe/index.md) in the main viewport. |
| Lights Planar Probe (Viewports) | Number of rendered [Planar probes](../../../objects/lights/planar/index.md) in the main viewport. |
| Lights Omni (Reflections) | Number of [Omni lights](../../../objects/lights/omni/index.md) rendered in reflection passes. |
| Lights Proj (Reflections) | Number of [Projected lights](../../../objects/lights/proj/index.md) rendered in reflection passes. |
| Lights World (Reflections) | Number of [World lights](../../../objects/lights/world/index.md) rendered in reflection passes. |
| Lights Environment Probe (Reflections) | Number of [Environment probes](../../../objects/lights/envprobe/index.md) rendered in reflection passes. |
| Lights Voxel Probe (Reflections) | Number of [Voxel probes](../../../objects/lights/voxelprobe/index.md) rendered in reflection passes. |
| Lights Planar Probe (Reflections) | Number of [Planar probes](../../../objects/lights/planar/index.md) rendered in reflection passes. > **Notice:** Planar probes reflect other lights, but do not reflect each other. |
| Decals: |  |
| Decals All | Number of decals rendered per frame (in all [rendering passes](../../../principles/render/sequence/index.md)). If a decal has any additional effect (is transparent, emits light, lit by a light source, or has any other visual effect) that involves an additional rendering pass for this decal, this decal will be rendered additionally in every corresponding pass, thus the total number of rendered decals will increase. |
| Decals Ortho (Viewports) | Number of [Orthographic](../../../objects/decals/ortho/index.md) decals rendered in the main viewport. |
| Decals Proj (Viewports) | Number of [Projected](../../../objects/decals/proj/index.md) decals rendered in the main viewport. |
| Decals Mesh (Viewports) | Number of [Mesh](../../../objects/decals/mesh/index.md) decals rendered in the main viewport. |
| Decals Ortho (Reflections) | Number of [Orthographic](../../../objects/decals/ortho/index.md) decals rendered in reflection passes. |
| Decals Proj (Reflections) | Number of [Projected](../../../objects/decals/proj/index.md) decals rendered in reflection passes. |
| Decals Mesh (Reflections) | Number of [Mesh](../../../objects/decals/mesh/index.md) decals rendered in reflection passes. |
| Surfaces: |  |
| Surfaces All | Number of surfaces rendered per frame (in all [rendering passes](../../../principles/render/sequence/index.md)). If a surface has any additional effect (is transparent, emits light, lit by a light source, or has any other visual effect) that involves an additional rendering pass for this surface, this surface will be rendered additionally in every corresponding pass, thus the total number of rendered surfaces will increase. |
| Surfaces (Shadows) | Number of surfaces rendered in shadow map passes. |
| Surfaces (Viewports) | Number of surfaces rendered in the main viewport. |
| Surfaces (Reflections) | Number of surfaces rendered in reflection passes. |
| Dynamic Reflections | The number of dynamic reflections drawn per frame. In case of cubemap reflections, if all six faces are updated, six reflections are rendered each frame. |
| Shadows | Number of shadow passes rendered per frame. Each light requires a shadow pass to calculate the shadows. Again, if there are reflecting surfaces with shadows drawn reflected, this will increase the number of shadow passes. |
| Triangles: |  |
| Triangles All | Total number of triangles rendered per frame including all polygons that are currently visible in the viewport as well as the ones rendered in the process of shadows rendering. |
| Triangles (Shadows) | Number of triangles rendered per frame in the process of shadows rendering. Each light source has to redraw the geometry it illuminates, increasing the overall count of rendered triangles. In order to avoid GPU bottleneck, keep the number of dynamic light sources and their radius as low, as possible. |
| Triangles (Viewports) | Number of triangles rendered per frame. This includes all polygons that are currently visible in the viewport (geometry). |
| Triangles (Reflections) | Number of triangles rendered for reflective surfaces; includes geometry drawn in reflection passes such as planar probes or planar water surfaces. |
| Render Counters: |  |
| Primitives | Number of geometric primitives rendered per frame. This includes points, lines, triangles, and polygons. The visualizer and the profiler itself also add to this counter. The value differs dramatically if tessellation is used. In this case, *Triangles* reports the number of triangles in the coarse mesh, while *Primitives* shows statistics on the number of tessellated primitives. |
| Dips | The number of draw calls. The higher the number of identical mesh surfaces with the same material, the more effective the instancing is (enabled by default). This means, the number of draw calls is minimized offloading both the CPU and the GPU. You can compare the number of surfaces (*Surfaces*) and the number of DIPs used to render them. For example, if there are 30000 surfaces and 1000 DIPs, it means that 30 instanced surfaces of meshes are rendered per only one draw call (Surfaces/Dips). Thus the instancing provides performance boost. |
| Barriers | The number of barriers per frame represents how many times GPU resources change states during a single rendering frame. Each transition ensures proper synchronization when a resource is accessed differently, such as switching from rendering to shader reading. This metric reflects the complexity and efficiency of the rendering pipeline - higher counts may indicate frequent state changes, which can lead to pipeline stalls and reduced performance. Reducing unnecessary transitions can improve frame consistency and GPU utilization. |
| Material Counters: |  |
| Materials | Number of materials set per frame. (Materials are set in each of the [rendering passes](../../../principles/render/sequence/index.md).) |
| Shaders | Number of shaders set per frame. (Shaders are set in each of the [rendering passes](../../../principles/render/sequence/index.md); hence if only one material used, its shader still needs to be set several times. When nothing is visible and the screen is black, even in this case the composite shader is still used.) |
| PSO Counters: |  |
| Compiled PSO | Number of pipeline state objects currently being compiled. This value decreases as compilation progresses and reaches zero when all PSOs are ready. A non-zero value during gameplay indicates runtime PSO creation, which may cause stuttering. |
| Compiled Global PSO | Number of global pipeline state objects currently being compiled. Global PSOs are not tied to specific materials and are used by internal engine render passes. |
| Loaded PSO | Total number of pipeline state objects currently in memory. Includes both PSOs loaded from cache at startup and PSOs compiled at runtime. |
| Shader Counters: |  |
| Compiled Shaders | Number of shaders currently in the compilation queue. This value decreases as compilation progresses and reaches zero when all shaders are ready. |
| Loaded Shaders | Total number of shader objects currently in memory. Includes both shaders loaded from cache and shaders compiled at runtime. |
| Resource Streaming Counters: |  |
| CPU Loading resources | Number of resources currently being streamed or loaded by the CPU. Represents how many assets are actively being prepared on the CPU side for rendering. |
| GPU Loading resources | Number of resources currently being streamed or loaded by the GPU. Represents how many assets are actively being prepared on the GPU side for rendering. |


> **Notice:** Values less then 1 Mb are displayed as **0**.


## Physics Profiler


This profiler shows statistics within the [Physics radius](../../../editor2/settings/physics_global/index.md#physics_distance).


> **Notice:** You can enable this profiler via the UnigineEditor interface (*Tools -> Performance Profiler -> Physics*) and via the [`show_profiler_physics 1`](../../../code/console/index.md#show_profiler_physics) console command.


![](physics_profiler.png)

*Physics Profiler Enabled*


The following statistics are displayed in addition to the [generic](#generic) one:


| PIslands | Number of independent physics [islands](../../../principles/physics/collision/index.md#islands) (groups of bodies that can simulate without interacting with others) within the physics simulation [radius](../../../editor2/settings/physics_global/index.md#physics_distance). More islands allow better multi-threading of physics; very few islands mean most objects are inter-connected in one simulation group |
|---|---|
| PBodies | Number of [bodies](../../../principles/physics/bodies/index.md) within the physics [radius](../../../editor2/settings/physics_global/index.md#physics_distance). |
| PJoints | Number of [joints](../../../principles/physics/joints/index.md) within the physics [radius](../../../editor2/settings/physics_global/index.md#physics_distance). |
| PContacts | Total number of contacts within the physics [radius](../../../editor2/settings/physics_global/index.md#physics_distance); this includes contacts between the bodies (their shapes) and body-mesh contacts. |
| PCollision | Duration of the [collision detection phase](../../../principles/physics/simulation.md#collision_detection) of physic simulation when collisions between objects are found. |
| PSimulation | Duration of all simulation phases added together. |


Watch an overview of the Physics Profiler options in our [video tutorial on physics](https://youtu.be/w_GJrE-6HtI?t=1568s).


## World Management Profiler


This profiler shows statistics on the whole world.


> **Notice:** When in the editor mode, enabling and disabling of the node, body or a joint can increase values of world profiler counters, as a (limited) number of clones are created for undo/redo purposes.


![](world_profiler.png)

*World Management Profiler Enabled*


> **Notice:** You can enable this profiler via the UnigineEditor interface (*Tools -> Performance Profiler -> World Management*) and via the [`show_profiler_world 1`](../../../code/console/index.md#show_profiler_world) console command.


The following statistics is displayed in addition to the [generic](#generic) one:


| WNodes | Total number of nodes in the world (both enabled and disabled). |
|---|---|
| WBodies | Total number of [bodies](../../../principles/physics/bodies/index.md) in the world. |
| WShapes | Total number of [shapes](../../../principles/physics/shapes/index.md) in the world. |
| WJoints | Total number of [joints](../../../principles/physics/joints/index.md) in the world. |
| WSpawn | Time in milliseconds that the engine spends on generating content in procedural nodes (such as grass, clutters, world layers). |


## Thread Profiler


![](thread_profiler.png)

*Thread Profiler Enabled*


> **Notice:** You can enable this profiler via the UnigineEditor interface (*Tools -> Performance Profiler -> Thread*) and via the [`show_profiler_thread 1`](../../../code/console/index.md#show_profiler_thread) console command.


The following statistics are displayed in addition to the [generic](#generic) one:


| CPUShaders Sync Threads | Number of internal engine threads used to execute tasks in synchronous mode. |
|---|---|
| CPUShaders Async Threads | Number of internal engine threads used to execute tasks in asynchronous mode. |
| AsyncQueue | Time of asynchronous loading of resources (files/meshes/images/nodes), in milliseconds. In addition to timing metrics, you can also inspect detailed information about files, images, meshes, and nodes using the *[async_queue_info](../../../code/console/index.md#async_queue_info)* console command. |
| Sound | Time of asynchronous loading of sounds, in milliseconds. |
| PathFind | Time of asynchronous pathfinding calculations, in milliseconds. |
| Profiler Dump | Time taken to serialize and write profiler data for the current frame into the [Profiler Dump](../../../tools/profiling/profiler_dump/index_cpp.md). This value is shown only if the Profiler Dump is being recorded. |


## Experimental Navigation Profiler


This profiler shows what the experimental navigation system holds in memory and how much of a frame it takes.


> **Notice:** You can enable this profiler via the UnigineEditor interface (*Tools -> Performance Profiler -> Experimental Navigation*) and via the [`show_profiler_experimental_navigation 1`](../../../code/console/index.md#show_profiler_experimental_navigation) console command.


Counters of the data the system currently keeps:


| ExperimentalNavigation Meshes | Number of [navigation meshes](../../../objects/navigations/experimental/navigation_mesh/index.md) in the world. |
|---|---|
| ExperimentalNavigation Tiles | Number of tiles currently loaded, out of the number of tiles all navigation meshes are cut into. The two differ when streaming is on: a tile that no [invoker](../../../objects/navigations/experimental/invoker/index.md) asks for is not loaded. |
| ExperimentalNavigation Polygons | Number of polygons in the loaded tiles. This is what path searches walk over. |
| ExperimentalNavigation Path Tasks | Number of path searches running in the background right now. |


Memory, in bytes:


| ExperimentalNavigation RAM | Memory the whole system takes, the rows below added together. |
|---|---|
| ExperimentalNavigation Data RAM | Memory the streamed data takes. The second value is the [Streaming Memory Limit](../../../editor2/settings/navigation/index.md#streaming_memory_limit): once the first reaches it, streaming stops loading and the navigation mesh is left with holes. |
| ExperimentalNavigation Tiles RAM | Memory the polygons of the loaded tiles take. |
| ExperimentalNavigation Voxels RAM | Memory the loaded voxel data takes. Navigation meshes keep it to rebuild tiles without reading the world again. |
| ExperimentalNavigation Query RAM | Memory the search structures take. |
| ExperimentalNavigation Thread Query RAM | Memory the per-thread copies of the search structures take. It grows with the number of threads that run path searches. |
| ExperimentalNavigation Obstacle Snapshots RAM | Memory the snapshots of [obstacles](../../../objects/navigations/obstacle/index.md) take. Queries read obstacles from a snapshot instead of the scene. |
| ExperimentalNavigation Corridors RAM | Memory all *[corridors](../../../api/library/pathfinding/class.experimentalnavigationmeshcorridor_cpp.md)* take together. |
| ExperimentalNavigation Avoidance RAM | Memory all *[avoidance](../../../api/library/pathfinding/class.experimentalnavigationavoidance_cpp.md)* solvers take together. |


Time per frame, in milliseconds:


| ExperimentalNavigation Streaming | Time spent loading and unloading tiles. It is capped by the [Streaming Budget](../../../editor2/settings/navigation/index.md#streaming_budget). |
|---|---|
| ExperimentalNavigation Invalidate | Time spent rebuilding the tiles that changed. It is capped by the [Invalidate Budget](../../../editor2/settings/navigation/index.md#invalidate_budget). |
| ExperimentalNavigation Path | Time spent searching for paths. |
| ExperimentalNavigation Corridors | Time spent moving agents along their corridors. |
| ExperimentalNavigation Avoidance | Time spent computing velocities that keep agents apart. |


> **Notice:** Corridors are timed only while this profiler is on. Turning it on costs a pair of timer calls per corridor call, so the numbers it reports for corridors are not free.
