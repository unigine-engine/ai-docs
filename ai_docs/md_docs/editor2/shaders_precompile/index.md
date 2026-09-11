# Pre-Compiling Shaders


A **shader** is a small program executed on the GPU, and of course it takes some time to get compiled and loaded. Usually, compiling and loading a single GPU program does not take much time, but shaders often have a lot of "variants". Complex shaders have multiple preprocessor directives (defines) for various cases, each combination of these directives defines a shader variant. So we end up having to compile many thousands of slightly different GPU programs. Compiling shaders on demand at runtime can cause visual artifacts - objects or their individual surfaces may **pop in** (appear suddenly or partially as shaders become ready) or the application may **freeze**. To avoid this, all required shader combinations are precompiled and stored in the **shader cache**. Loading precompiled shaders from cache is much faster.


> **Notice:** - A shader cache generated for **debug** builds should not be used for **release** builds, as shaders are compiled without optimizations (both DirectX and Vulkan). Re-generate it for your release build for maximum performance.
> - **Float-** and **double-precision** builds each use their own shader cache. If your application ships with both, generate the cache for each build separately.


## Generating the Most Complete Shader Cache


**Precompilation of all shaders** is an important feature that ensures you will have the most complete shader cache possible at the time your project is completed and final builds are ready to be handed over to customers. This significantly reduces the number of visual artifacts (pop-ins and freezes) in the final release build and smooths your application's framerate. Shaders are precompiled for all materials in the project.


This feature is available via the ***Precompile All Shaders*** button on the toolbar near the **Play** button or via the *Editor* section of the *Settings* window when a world is loaded.


![](precompile_option.png)

*Precompile All Shadersoption on the toolbar and in theEditorsection of theSettingswindow*


You can use it in one of the following ways:


- **Constant background precompilation** When this button is enabled, each time you create a new material, you'll see the following message on shader compilation in the viewport: ![](compile_process.png) > **Notice:** In case the UnigineEditor's UI response has become too slow, you can stop the process of shader cache generation via the corresponding button right on the compilation message. Objects whose shaders are not yet compiled will temporarily pop in or appear white/reflective until all required render passes are compiled. This may take a couple of seconds depending on your computer's performance.
- **Precompilation on demand** Sometimes constant background compilation of shaders may disturb and slow down your work. You can disable shaders precompilation and enable it just before measuring performance of your final build. In this case shader cache generation will take much more time (up to half an hour) depending on your project's complexity and selected graphics API, but it will be performed only once. > **Notice:** This mode is recommended for graphics programmers to save time on recompilation when changing states of materials.


The precompilation described above covers all shader variants for all materials in the project. However, some objects (geodetic pivot, terrain, water, clouds) have material states that the Engine changes automatically at runtime, which produces new shader variants requiring additional compilation.


> **Notice:** Certain objects (terrain, water, clouds, geodetic pivot) require special attention because the Engine automatically changes internal material **states** based on runtime conditions (e.g., camera position relative to water surface, or altitude relative to clouds and terrain). Each state change introduces different preprocessor defines, resulting in distinct shader variants that must be compiled separately.


The following actions should be performed to generate the most complete shader cache for your project:


1. Open all worlds, that contain geodetic pivot, terrain, water, or clouds.
2. For each of these worlds perform the following:

  - **water** - put a scene camera over water, under water and at the waterline between the two media.
  - **terrain** - put a scene camera high above the terrain and move it to the terrain surface.
  - **clouds** - put a scene camera over above the clouds, under the clouds and inside the clouds.
3. Create and launch [tracks](../../editor2/tools/tracker/index.md) for all material states that you plan to switch via your application's logic.


> **Notice:** To minimize run-time recompilation of shaders for materials, whose states are to be changed via the application logic, you can also create separate materials having the required state values and switch between these materials instead of changing states.


Output shader cache for DirectX / Vulkan is generated inside the `data` folder:


- DirectX 12 - `shader_d3d12_dxc.cache`, `pso_log_d3d12_dxc.cache`, `d3d12_<gpu_name>_dxc.gpu_cache`
- Vulkan - `shader_vk.cache`, `pso_log_vk.cache`, `vk_<gpu_name>.gpu_cache`


See the [Shader Cache Types](#shader_cache_types) section below for a detailed description of each file type.


> **Warning:** Do not put shader cache files to UNG archives! You will not have a substantial file size reduction, as cache files already use LZ4 compression. Moreover, in this case, any new shaders generated on the end user's side will not be added to the cache.


As your project is completed and final builds are ready to be handed over to customers, you should copy **portable** shader cache files ([Shader Bytecode Cache](#cache_type_shader) and [PSO Log](#cache_type_pso_log)) to the `data` directory of the final build. Do not distribute GPU pipeline cache files (`.gpu_cache`) - they are GPU-specific and will be generated automatically on each end user's system.


If you pass a [project name](../../code/command_line.md#project_name) via the command line or on Engine initialization:

```bash
-project_name "YourProject"
```

 you should copy shader cache files to the following directory:
- Windows - `C:/Users/<username>/YourProject/`
- Linux - `/home/<username>/.YourProject/`


## From Materials to Shaders


In UNIGINE, you mostly work with **materials** rather than writing shaders directly. A material (whether built from a [Material Graph](../../content/materials/graph/index.md) or written as a [base material](../../code/uusl/index.md) with custom UUSL shaders) defines how a surface should be rendered: which textures to use, how lighting is applied, whether the object is transparent, and so on.


Behind the scenes, each material contains shader source code and a set of **[states](../../api/library/rendering/class.material_cpp.md#getState_int_int)** - switches that control its rendering behavior (e.g., enabling a normal map, turning on transparency, or switching to two-sided rendering). The current states are translated into preprocessor **defines** that are passed to the shader compiler, producing a compiled shader tailored to that specific configuration.


Every material must produce compiled shaders for each **[render pass](../../api/library/rendering/class.render_cpp.md#PASS)** it participates in (depth pre-pass, deferred, shadow, etc.) and for each **[node type](../../api/library/nodes/class.node_cpp.md#TYPE)** it supports (static mesh, skinned mesh, terrain, etc.). Each combination of base material + **states** + render pass + node type = one **shader variant**. Each variant is a [**Shader**](../../api/library/rendering/class.shader_cpp.md) object containing independently compiled bytecode for its subshaders (vertex, fragment, geometry, etc.).


Two material instances using the same base but with different states will produce different defines - and therefore different compiled bytecode. Multiply this by many materials in a typical project, and you can end up with **tens of thousands of shader variants** that need to be compiled. This is why shader precompilation and caching exist - to ensure all these variants are compiled ahead of time, not during gameplay.


## From Shaders to PSOs


A [**Shader**](../../api/library/rendering/class.shader_cpp.md) object contains compiled bytecode, but the GPU cannot use it alone. Modern graphics APIs (DirectX 12, Vulkan) require a **Pipeline State Object (PSO)** - a single object that combines the shader bytecode with the full set of **render state** parameters: blend mode, depth test, cull mode, render target formats, vertex layout, topology, and so on.


Much of this render state comes from the material itself - its transparency settings, two-sided mode, depth testing configuration. The rest is determined by the rendering context - which render targets are active, what multisample level is used, etc.


This means that the same **Shader** object can produce **different PSOs** when used with different render state configurations. The total number of PSOs in a scene depends not only on the number of shader variants, but also on the variety of render state combinations the Engine encounters at runtime.


Creating a PSO is an expensive operation - it involves the GPU driver compiling and validating the full pipeline configuration. This is why the Engine maintains a **PSO cache** in memory and supports **PSO precompilation** (see [Step 2](#lifecycle_pso_precompile) and [Step 6](#lifecycle_runtime_pso) of the Shader Lifecycle).


## Shader Cache Types


The term "Shader Cache" can be confusing because UNIGINE actually uses several types of cached data at different stages. Each type serves a distinct purpose in the shader compilation pipeline.


### Shader Bytecode Cache


Files: `shader_d3d12_dxc.cache`, `shader_vk.cache`


This is the primary shader cache. It stores compiled **shader bytecode** - an intermediate representation (**DXIL** for **DirectX 12**, **SPIR-V** for **Vulkan**) produced by the shader compiler. This is **not** native GPU machine code, but a platform-specific bytecode that the GPU driver translates into native code at a later stage.


Each entry in the cache corresponds to a unique shader variant, determined by the combination of shader source, material states, rendering settings, and compiler options. The cache uses compression to reduce disk space. When a required shader variant is not found in the cache, it is compiled from source and added to the cache automatically.


This cache is **GPU-independent** and can be distributed with your application.


### PSO Log Cache


Files: `pso_log_d3d12_dxc.cache`, `pso_log_vk.cache`


A **Pipeline State Object (PSO)** is a concept required by modern graphics APIs (DirectX 12, Vulkan). A PSO combines a compiled shader with a set of render state parameters (blend mode, depth test, cull mode, render target formats, vertex layout, topology, etc.) into a single pre-validated object. Creating a PSO involves the GPU driver compiling and validating the full pipeline configuration under the hood, which is why doing this at runtime can cause noticeable hitches.


The PSO Log does not store PSOs themselves - it records **which PSO configurations were needed** during previous runs. When *[pso_preload](../../code/console/index.md#pso_preload)* is enabled, the Engine creates these PSOs at startup (the driver still does the same heavy work, but during the loading screen rather than runtime). See [Step 2](#lifecycle_pso_precompile) and [Step 6](#lifecycle_runtime_pso) of the **[Shader Lifecycle](#shader_lifecycle_detailed)** for details.


This cache is **GPU-independent** and can be distributed with your application.


### GPU Pipeline Cache


Files: `d3d12_<gpu_name>_dxc.gpu_cache`, `vk_<gpu_name>.gpu_cache`


This cache is managed by the **Engine** using the graphics API (**D3D12 Pipeline Library** / **VkPipelineCache**). During a session, the driver accumulates compiled PSO data in a cache object in memory. When the Engine shuts down, it serializes this object to disk. On subsequent runs, the Engine loads the file and passes it back to the driver, allowing it to skip recompilation and return ready PSOs almost instantly.


The file name includes the GPU model name, making it **specific to a particular GPU and driver version**. The data may become invalid when the GPU driver is updated.


> **Warning:** GPU cache files are **not portable** between different GPUs. They are generated automatically and should not be distributed with your application. Each end user's system will generate its own GPU cache after the first run.


### Driver PSO Cache


Independently of the Engine, GPU drivers maintain their own internal shader/pipeline caches stored in system directories:


- NVIDIA - `%LOCALAPPDATA%/NVIDIA/DXCache` (DirectX), `%LOCALAPPDATA%/NVIDIA/GLCache` (Vulkan)
- AMD - `%LOCALAPPDATA%/AMD/DxcCache` (DirectX), `%LOCALAPPDATA%/AMD/VkCache` (Vulkan)
- Intel - `%APPDATA%/../LocalLow/Intel/ShaderCache` (DirectX only)


These caches are fully managed by the GPU driver and are normally invisible to the application.


> **Notice:** Developers typically have populated caches and may not experience the same PSO creation hitches that end users encounter on their **first run**. Use the *[video_debug_clear_driver_pso_cache](../../code/console/index.md#video_debug_clear_driver_pso_cache)* boot command to temporarily bypass both the GPU Pipeline Cache and the Driver Cache at startup to accurately test first-run performance. The driver cache files are restored when the Engine shuts down.


## Step-by-Step Shader Lifecycle


The following describes the complete shader lifecycle from render initialization through runtime rendering.


### 1. Render Initialization


When the Renderer is created, two things happen: the shader cache is opened and the PSO cache is initialized.


#### Opening the Shader Cache


The Engine opens the [Shader Bytecode Cache](#cache_type_shader). From this point on, whenever a shader variant is needed, the Engine can check whether compiled bytecode already exists in the cache. Whether the bytecode is also loaded into memory at this stage is determined by the following console variables:


| -shader_cache_immediate_flush |  |
|---|---|
| **Description:** Controls how the Engine works with the [Shader Bytecode Cache](../../editor2/shaders_precompile/index.md#cache_type_shader) file. When enabled (default), the file stays on disk and each newly compiled shader is written to it immediately. When disabled, the **raw cache file** is loaded into a RAM buffer at startup and all I/O goes through this buffer, which is faster for bulk operations like shader cache generation. The buffer is flushed to disk on shutdown. | **Arguments:** **0** - disabled **1** - enabled (by default) |
| -shader_cache_preload | Config file: [*.boot](../../code/configuration_file_cpp.md#boot) |
| **Description:** When enabled, all compiled shader bytecode is **decompressed** and loaded into RAM from the [Shader Bytecode Cache](../../editor2/shaders_precompile/index.md#cache_type_shader) at startup, ready to use without any disk access. When disabled (default), each shader's bytecode is read from the cache and decompressed on demand. | **Arguments:** **0** - disabled (by default) **1** - enabled |


#### PSO Cache Initialization


The Engine also loads the [GPU Pipeline Cache](#cache_type_gpu) and passes it to the GPU driver. This cache will be actively used later both during PSO precompilation and at runtime to accelerate PSO creation.


### 2. PSO Precompilation at Startup


When enabled, the Engine reads the [PSO Log](#cache_type_pso_log) (a list of PSO configurations recorded during previous Engine runs) and creates these PSOs at startup. Shader bytecode is read from the **Shader Bytecode Cache** on demand, and the **GPU Pipeline Cache** accelerates creation through the driver.


PSO precompilation is controlled by:


| -pso_preload | Config file: [*.boot](../../code/configuration_file_cpp.md#boot) |
|---|---|
| **Description:** Enables PSO (Pipeline State Object) preloading at Engine startup. When enabled, the Engine records every PSO created during rendering into the [PSO Log](../../editor2/shaders_precompile/index.md#cache_type_pso_log). On the next launch, all recorded PSOs are pre-created before rendering begins (multi-threaded, blocks startup until complete). When disabled, no PSO Log is written or read, and all PSOs are created on demand during rendering. | **Arguments:** **0** - disabled (by default) **1** - enabled |


### 3. Loading Materials and Their Variants


The Engine locates all material files (`.abstmat`, `.basemat`, `.mat`) and creates [**Material**](../../api/library/rendering/class.material_cpp.md) objects. When enabled, the Engine also creates additional material variants needed for rendering - each with a modified set of states, meaning its own set of shader variants in the next step.


Creation of material variants is controlled by:


| -materials_preload | Config file: [*.boot](../../code/configuration_file_cpp.md#boot) |
|---|---|
| **Description:** Enables [creation of material variants](../../editor2/shaders_precompile/index.md#lifecycle_load_materials) at Engine startup. For each loaded material, the Engine creates additional internal copies with modified states (e.g. different culling or blending modes) to handle specific rendering scenarios. Each variant requires its own set of shader variants. When enabled, all material variants are created at startup, ensuring that subsequent shader preloading (see *[shaders_preload](#shaders_preload)*) covers the full set of required shaders. When disabled, material variants are created on demand at runtime - useful for faster iteration during development, but may cause additional shader compilation hitches. | **Arguments:** **0** - disabled **1** - enabled (by default) |


### 4. Creating Shaders at Startup


For each loaded material, [**Shader**](../../api/library/rendering/class.shader_cpp.md) objects can be created for every combination of [Render Pass](../../api/library/rendering/class.render_cpp.md#PASS) and [Node Type](../../api/library/nodes/class.node_cpp.md#TYPE) supported by the material.


This behavior is controlled by:


| -shaders_preload | Config file: [*.boot](../../code/configuration_file_cpp.md#boot) |
|---|---|
| **Description:** The shaders creation strategy at Engine startup. For each loaded material (including material variants), the Engine goes through all required render pass and node type combinations. | **Arguments:** **0** - No Shader objects are created at startup. Everything is deferred to runtime - Shader objects are created from the [Shader Bytecode Cache](../../editor2/shaders_precompile/index.md#cache_type_shader) or compiled from source on demand during rendering. Fastest startup, but may cause pop-in or freezes. **1** - Shader objects are created for all variants that have compiled bytecode in the [Shader Bytecode Cache](../../editor2/shaders_precompile/index.md#cache_type_shader). Variants not found in the cache are skipped and will be handled at runtime on demand. (by default) **2** - Same as 1, but variants not found in the cache are also compiled from source. Creating a Shader object from cached bytecode is always synchronous; compilation from source is asynchronous by default (controlled by *[render_shaders_compile_mode](#render_shaders_compile_mode)*). |


When *shaders_preload* is **2**, the behavior of uncached shader compilation is controlled by:


| render_shaders_compile_mode |  |
|---|---|
| **Description:** - **Variable.** � Prints the current compilation mode for shaders that are used in the loaded world. - **Command.** � Sets the compilation mode for shaders that are used in the loaded world. The following modes are available: > **Notice:** This setting does not affect post-processing shaders, lightmap data shaders, and materials with forced compilation - these are always compiled synchronously regardless of this setting. - *Async* - shaders are compiled in a background thread. Objects whose shaders are not yet ready are not rendered (pop-in effect). - *Force* - shaders are compiled synchronously on the main thread. The application freezes until the shader is ready, but objects are rendered immediately. | **Arguments:** **0** - Asynchronous compilation. Objects whose shaders are not yet ready are not rendered (pop-in). (by default) **1** - Forced synchronous compilation. The application freezes until the shader is ready. |


> **Notice:** If shader bytecode is already in the [Shader Bytecode Cache](#cache_type_shader), creating a **Shader** object from it is fast (load + decompress) and always done synchronously. *render_shaders_compile_mode* only affects shaders that require full compilation from source.


### 5. Runtime: Shader Creation on Demand


During rendering, when the Engine needs a **Shader** object that was not created at [step 4](#lifecycle_shader_objects), it must create one on the fly to proceed with PSO creation. If bytecode exists in the [Shader Bytecode Cache](#cache_type_shader), creation is fast (load + decompress). If not - the shader is compiled from UUSL source and the result is added to the cache.


The *[render_shaders_compile_mode](../../code/console/index.md#render_shaders_compile_mode)* variable controls whether this happens in the background or blocks the main thread.


> **Warning:** Certain render passes (post-processing, lightmap data) and materials with forced compilation are **always compiled synchronously** regardless of *render_shaders_compile_mode*. The only way to avoid freezes from these shaders is to have them pre-compiled in the [Shader Bytecode Cache](#cache_type_shader).


### 6. Runtime: PSO Creation and Rendering


To render an object, the Engine needs a ready PSO. If the PSO already exists - rendering is instant. If not, it must be created through the GPU driver. The [GPU Pipeline Cache](#cache_type_gpu) accelerates this process.


The *[render_shaders_compile_mode](../../code/console/index.md#render_shaders_compile_mode)* variable determines the user-visible behavior when a **Shader** object or PSO is not ready:


- **0** - compilation happens in the background. The object is **not rendered** until ready (**pop-in**).
- **1** - compilation is synchronous. The application **freezes** until ready, but the object is rendered immediately.


When *pso_preload* is **enabled**, every new PSO configuration is recorded in the [PSO Log](#cache_type_pso_log). On the next launch it will be precompiled at startup. For this reason, the [**PSO Log Cache**](#cache_type_pso_log) should be distributed alongside the [**Shader Bytecode Cache**](#cache_type_shader) - so that end users benefit from precompilation on their first run.


## Compiling Shaders from API


While the Engine manages shader compilation automatically based on console variables (as described in the [Shader Lifecycle](#shader_lifecycle_detailed) above), you can also trigger these operations manually through the API. The methods below control the same process - creating **Shader** objects and populating the [Shader Bytecode Cache](#cache_type_shader).


### Materials Class


The  class provides methods for managing shaders across all loaded materials:


| Method | Console Equivalent | Description |
|---|---|---|
|  | - | Creates render material variants (for dynamic objects, alpha fade, decals, etc.), each requiring its own set of shaders. Must be called before creating shaders - otherwise not all required shader variants will be found. |
|  | *[shaders_create](../../code/console/index.md#shaders_create)* | Creates **Shader** objects for all variants of all loaded materials. Compiles from source if bytecode is not found in the [Shader Bytecode Cache](#cache_type_shader), and updates the cache with new results. |
|  | *[shaders_create_from_cache](../../code/console/index.md#shaders_create_from_cache)* | Creates **Shader** objects only for variants that have compiled bytecode in the [Shader Bytecode Cache](#cache_type_shader). Variants not found in the cache are skipped. |
|  | *[shaders_create_cache_async](../../code/console/index.md#shaders_create_cache_async)* | Asynchronously creates **Shader** objects for all variants not yet in the [Shader Bytecode Cache](#cache_type_shader), and saves the compiled bytecode to the cache. Use  to wait for completion. |
|  | *[shaders_create_cache_force](../../code/console/index.md#shaders_create_cache_force)* | Immediately creates **Shader** objects for all variants not yet in the [Shader Bytecode Cache](#cache_type_shader), and saves the compiled bytecode to the cache. |
|  | *[shaders_destroy](../../code/console/index.md#shaders_destroy)* | Destroys all **Shader** objects, freeing their memory. |
|  | *[materials_reload](../../code/console/index.md#materials_reload)* | Reloads all loaded materials and their shaders. Shader variables are updated automatically. |


> **Notice:** The console commands *shaders_create* and *shaders_create_from_cache* automatically call  before creating shaders. When using the API directly, you must call it yourself.


### Material Class


The  class provides methods for managing shaders of an individual material:


| Method | Description |
|---|---|
|  | Synchronously creates a **Shader** object for a specific render pass and node type. Blocks the calling thread until the object is ready. |
|  | Starts asynchronous creation of a **Shader** object for a specific render pass and node type. Returns immediately. |
|  | Returns the **Shader** object for a specific render pass and node type. If it does not exist yet, it is created synchronously (may cause a freeze). |
|  | Returns the **Shader** object for a specific render pass and node type if it is ready, or **nullptr** if it is still being compiled asynchronously. |
|  | Returns **true** if compiled bytecode for the given pass and node type is not yet in the [Shader Bytecode Cache](#cache_type_shader) and needs to be compiled. |
|  | Returns **true** if compiled bytecode for the given pass and node type already exists in the [Shader Bytecode Cache](#cache_type_shader). |


The **pass** parameter is a  enum value (e.g., PASS_DEFERRED, PASS_SHADOW, PASS_DEPTH_PRE_PASS). The **node_type** parameter is a  value representing the type of object being rendered.


> **Warning:** and  block the calling thread until the **Shader** object is ready. Use them with caution in production code, as they may cause noticeable freezes, especially when bytecode is not in the [Shader Bytecode Cache](#cache_type_shader).


## Force Streaming Does Not Affect Shaders


The *render_streaming_force* console command (or the  method in API) forces synchronous loading of **meshes and textures only**. It has **no effect** on shader compilation or loading.


Even when a shader exists in the cache, it is loaded **lazily** - only when the material is first used for rendering. By default this happens asynchronously (controlled by *render_shaders_compile_mode*), meaning objects may appear suddenly, look white/reflective, or be temporarily invisible until shaders for all required render passes are ready.


To ensure all shaders are loaded synchronously and no placeholders appear, use one of the following approaches:


- Set *render_shaders_compile_mode 1* to force synchronous shader compilation (may cause freezes).
- Set *shaders_preload 2* to compile all shaders at Engine startup.
- Use the *shaders_create* or *shaders_create_from_cache* console commands after loading your world.
