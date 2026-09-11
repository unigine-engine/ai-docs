# Asynchronous Data Streaming


Data streaming is an optimization technique intended to reduce spikes caused by loading graphic resources and compiling shaders. With this technique, not all the data is loaded into memory at once. Instead, only the required data is loaded, and the rest is loaded progressively on demand.


![](streaming.gif)


Resource loading is performed and transferred to the *GPU* in separate asynchronous threads. After that, resources are synchronized and added to the virtual scene on the *CPU* side.


[![](streaming_profiler.png)](streaming_profiler_full.png)

*The output of theMicroprofiletool.*


In UNIGINE, asynchronous data streaming is enabled by default. You can **disable asynchronous data streaming** in UnigineEditor or via the console:


- In UnigineEditor, open the *Settings* window and go to the *Streaming* section. Here you can switch the streaming mode for textures and/or meshes.
- In the console, run the [corresponding commands](../../code/console/index.md#render_resources) that switch the streaming mode for textures and/or meshes.


There are two main streaming modes � asynchronous (Async) and forced (Force). The **Force** mode ensures force-loading of all resources required for each frame simultaneously (e.g., grabbing frame sequences, rendering node previews, warmup, etc.).


> **Notice:** The *Force* mode may cause freezes, so use it only if you are sure that the resources in your world fit into the available memory.


The streaming system provides asynchronous loading of the following data to *RAM*:


- All texture [runtime files](../../editor2/assets_workflow/assets_runtimes.md) and textures with the *[Unchanged](../../editor2/assets_workflow/texture_import.md#unchanged)* option enabled, including [cubemaps](../../editor2/assets_workflow/texture_import.md#image_type), [voxel probe maps](../../objects/lights/voxelprobe/index.md#overview), and shadow maps of [baked shadows](../../content/optimization/lights/index.md#static_light).
- Meshes of *[ObjectMeshStatic](../../objects/objects/mesh/index.md), [ObjectMeshClutter](../../objects/objects/mesh_clutter/index.md), [ObjectMeshCluster](../../objects/objects/mesh_cluster/index.md), [ObjectGuiMesh](../../api/library/objects/class.objectguimesh_cpp.md)* objects, and *[DecalMesh](../../api/library/decals/class.decalmesh_cpp.md)*.


Procedurally generated objects such as *ObjectMeshClutter* are generated in a separate thread, significantly reducing performance costs.


You can obtain general information on streamed resources by using the `render_streaming_meshes_info` and `render_streaming_textures_info` console commands.


![](streaming_info.png)

*Therender_streaming_meshes_infooutput.*


It is also possible to print the list of loaded resources and detailed information on them by using the `render_streaming_meshes_list` and `render_streaming_textures_list` console commands.


![](streaming_list.png)

*Therender_streaming_meshes_listoutput.*


## Asynchronous Shader Compilation


In addition to the asynchronous loading of meshes and textures, the streaming system provides **asynchronous shader compilation and loading**.


There are also 2 modes � asynchronous (Async) and forced (Force). In the Force mode, all shaders required for the current frame are compiled and loaded to RAM simultaneously in the current thread. By default, the asynchronous mode is used.


> **Notice:** You can switch the compilation mode in [UnigineEditor](../../editor2/settings/render_settings/streaming/index.md#shaders) or by using the `render_shaders_compile_mode` console command.


The number of compiled and loaded shaders are available in the *[Performance Profiler](../../tools/profiling/profiler/index.md#render)* tool.


![](streaming_shaders_profiler.png)


## Memory Usage Limits


All memory allocations for graphic resources are limited by the *committed memory* size, which includes both RAM and VRAM.


You can limit the memory available to the application to avoid crashes and find the balance between performance and memory consumption. There following parameters allow you to do this:


- *[Usage limits](../../code/console/index.md#render_streaming_usage_limit_ram)* for RAM and VRAM that restrict memory consumption to a specified percentage of the committed memory. However, you should remember that if the streaming system exceeds the VRAM usage limit, it will start using RAM for loading graphic resources. If it exceeds the RAM usage limit, the application will crash.
- *[Free space](../../editor2/settings/render_settings/streaming/index.md#free_space_vram)* for RAM and VRAM that defines how much memory is additionally reserved for allocations per frame. These parameters ensure that there is always enough memory for resource loading in the current frame. The values should be determined empirically, depending on the application.
- *[Cache limits](../../editor2/settings/render_settings/streaming/index.md#cache_ram)* for RAM and VRAM define a hard cap on how much memory can be used specifically for streaming caches. These caches store currently unused but potentially reusable resources to reduce loading times. Setting these limits helps prevent uncontrolled cache growth and reduces the risk of falling back to shared memory or experiencing crashes. However, if the limits are set too low, streaming misses may occur due to insufficient space for fast cache data access. Optimal values depend on the available memory budget and should be adjusted accordingly.


> **Notice:** You can disable VRAM limits if necessary by toggling on the *[VRAM Overcommit](../../code/console/index.md#render_streaming_vram_overcommit)* option. It may lead to spikes and freezes of the application but will ensure continuous loading of graphic resources. This option is unavailable for RAM, as exceeding available RAM will result in the application crash.
>
>
> The *[Committed Memory Overcommit](../../code/console/index.md#render_streaming_committed_memory_overcommit)* option controls how aggressively the engine uses system memory. When enabled (default), the engine can exceed 80% of total committed memory usage, which may improve performance during heavy streaming or memory-intensive scenarios. When disabled, memory usage is limited to 80% of system-committed memory, which can help maintain stability - especially on systems without a pagefile or with constrained disk space.


You can specify the usage limits and free space via UnigineEditor or the console:


- In UnigineEditor, open the *Settings* window, go to the *[Streaming](../../editor2/settings/render_settings/streaming/index.md)* section, and specify the required values.
- In the console, pass the required values to the corresponding commands:

  - `render_streaming_usage_limit_ram` and/or `render_streaming_usage_limit_vram`.
  - `render_streaming_free_space_vram` and/or `render_streaming_free_space_ram`.
  - `render_streaming_cache_ram` and/or `render_streaming_cache_vram`.


> **Notice:** For particle systems, there is a [separate memory limit](../../editor2/settings/render_settings/streaming/index.md#memory_particles) in percentage of the total GPU memory.


## Texture Streaming


The streaming system manages textures automatically. There are two modes of texture streaming:


- *Asynchronous* mode that provides asynchronous loading of textures.
- *Forced* mode for force-loading of textures required for the current frame at once.


For texture streaming optimization, you can enable texture mipmap loading, which significantly improves performance by reducing the memory consumption of texture streaming. This feature allows for the correct mipmap to be loaded at the current moment. When mipmaps loading is enabled, the textures that are not currently in use are unloaded.


To enable and configure mipmaps loading via UnigineEditor, do the following:


1. Open the *Settings* window and go to the *[Streaming](../../editor2/settings/render_settings/streaming/index.md)* section.
2. Toggle on the *[Mipmaps](../../editor2/settings/render_settings/streaming/index.md#textures_mipmaps)* flag and specify the required *[Mipmaps Density](../../editor2/settings/render_settings/streaming/index.md#textures_mipmaps_density)*.


> **Notice:** You can do the same via the console using the `render_streaming_textures_mipmaps` and `render_streaming_textures_mipmaps_density` commands.


*Mipmaps Density* sets the density of mipmaps relative to the screen resolution and helps to define which mipmap should be loaded at the current moment. You can specify different values for different quality presets. For example, you can set the density to less than 1 for the low-quality preset. In this case, the engine will load the low-resolution mipmaps, and the textures will look blurry.


Additionally, you may need to configure the *Texture Streaming Density Multiplier* for each texture in some materials to achieve the desired visual effect.


### Forced Streaming for Textures in Post-Effect Materials


To ensure all textures for your post-effects are available when needed, the forced streaming mode is set for all post materials by default. You can find this setting in *[Material Editor](../../content/materials/graph/index.md#post_effect_settings)*.


However, if some textures in the post material continuously change (via code, Tracker, etc.), it is recommended to specify the forced streaming mode *per texture*:


1. In the *[Material Editor](../../content/materials/graph/index.md#post_effect_settings)*, set Setting For Each Texture in the *Textures Streaming Mode* parameter for your post-effect material.
2. Toggle the forced streaming on and off for each texture individually in the *Parameters* panel of the Material Editor.


These settings override the global texture streaming settings specified in the *Settings* window.


## Mesh Streaming


Meshes can be loaded to RAM and VRAM separately for more efficient work with geometry. This allows eliminating memory leaks: meshes participating in collisions and intersections can be loaded to RAM only, if they are not currently rendered.


There are two modes of mesh streaming to RAM/VRAM:


- *Asynchronous* mode that provides asynchronous loading of meshes.
- *Forced* mode for force-loading of meshes required for the current frame at once.


The asynchronous loading to RAM and VRAM differs. Even if a mesh hasn't been loaded to *video memory* in time, it doesn't affect the application behavior (you may only notice some lag). However, if a mesh hasn't been loaded to *memory* in time, it may lead to incorrect physical behavior of objects in the scene.


First of all, we highly recommend you to use [shapes](../../principles/physics/collision/index.md) for collision and intersection detection as it is faster. If, for some reason, it doesn't suit you, use the following methods:


- Load meshes and hold them in memory while they exist. API of some mesh-based objects provides this functionality out of the box. It may partially solve the problem with incorrect behavior, however, only a few meshes can remain loaded.
- Use the [*prefetch system*](../../editor2/settings/render_settings/streaming/index.md#prefetch_cpu) that allows asynchronous pre-loading of meshes participating in collisions and intersections to memory before they are used: You can also preload all meshes for which collisions and intersections are calculated (the Full prefetch mode), however it will significantly increase RAM usage.

  1. Set the Radius prefetch mode.
  2. Specify the [physics radius](../../editor2/settings/physics_global/index.md#physics_distance) (for collisions) and/or the radius within which intersections are calculated.
  3. Specify the prefetch radius that should exceed the collison and intersection radius values.
- API of some mesh-based objects, as well as the *[MeshRender](../../api/library/rendering/class.meshrender_cpp.md)* class API provides also methods which allow implementing a custom prefetch logic for pre-loading meshes.


> **Notice:** It is highly recommended to use [shapes](../../principles/physics/collision/index.md) for collision and intersection detection.


Asynchronously streamed meshes shouldn't be modified. The only way to change such mesh is to make it procedural. A *procedural mesh* is a mesh created via code, such meshes have a specific streaming mode � they are always kept in memory after creation and never unloaded until the object is destroyed via code or the mesh returns to its normal mode (streaming from a source file). The mesh-based objects API allows switching a mesh to the [procedural mode](../../api/library/objects/class.objectmeshstatic_cpp.md#setMeshProceduralMode_int_int_void) and apply changes.


## Animation Streaming


Skeletal animations of *[ObjectMeshSkinned](../../api/library/objects/class.objectmeshskinned_cpp.md)* and *[ObjectMeshSkinnedLegacy](../../api/library/objects/class.objectmeshskinnedlegacy_cpp.md)* objects are streamed as well. Unlike geometry and textures, an animation only provides bone transforms computed on the CPU side, so it is streamed to **RAM only** and never occupies video memory.


There are two modes of animation streaming:


- *Asynchronous* mode that loads an animation in a **background thread**. Until the animation is loaded, the skeleton holds the **first frame** of this animation.
- *Forced* mode that loads the animation required for the current frame **immediately**, blocking until it is available.


By default, animations use the **forced** mode, so a newly requested animation is available right away. You can switch the mode in *[UnigineEditor Streaming Settings](../../editor2/settings/render_settings/streaming/index.md#animations_streaming_mode)* or via the `render_streaming_animations_mode` console command.


> **Notice:** Because an animation provides bone transforms rather than geometry, a streaming miss does not make an object disappear. The object is rendered in the **first frame** of the animation being loaded, so no bind-pose flash occurs.
>
>
> You can check whether a layer's animation is still **streaming** both on *[ObjectMeshSkinnedLegacy](../../api/library/objects/class.objectmeshskinnedlegacy_cpp.md#isLayerAnimationStreaming_int_int)* and on *[NodeSkeletonPose](../../api/library/nodes/class.nodeskeletonpose_cpp.md#isLayerAnimationStreaming_int_int)*.


### Keeping Animations in Memory


Once an animation is no longer used, it is **not unloaded immediately**. Instead, it stays in the **RAM cache** for a while so that it can be reused without reloading. How long an unused animation remains in the cache is defined, **in frames**, by the `render_streaming_animations_life_time` console command. The default value of -1 keeps animations in memory **permanently** - they are never unloaded. Values below 6 are clamped to 6 frames.


You can also limit the total amount of RAM used by the animation cache with the `render_streaming_animation_cache_ram` console command.


When you need a specific animation to stay loaded **regardless of the lifetime setting**, you can [**hold**](../../api/library/rendering/class.render_cpp.md#holdStreamingAnimation_cstr_int) it explicitly via the *[Render](../../api/library/rendering/class.render_cpp.md)* class API. A held animation remains in memory and is **never unloaded until it is released**. The same class also lets you **preload** animations [in the background](../../api/library/rendering/class.render_cpp.md#loadStreamingAnimationAsync_cstr_MeshSkinnedAnimation) or [immediately](../../api/library/rendering/class.render_cpp.md#loadStreamingAnimationForce_cstr_MeshSkinnedAnimation), and query whether an animation currently [**exists**](../../api/library/rendering/class.render_cpp.md#isStreamingAnimationExist_cstr_int) or is [**loaded**](../../api/library/rendering/class.render_cpp.md#isStreamingAnimationLoaded_cstr_int) in the streaming system.


You can obtain general information on streamed animations and the list of loaded animations with the `render_streaming_animations_info` and `render_streaming_animations_list` console commands.
