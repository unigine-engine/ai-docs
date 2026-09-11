# Memory Allocator


*Allocator* is responsible for managing memory allocation for an application. For example, RAM allocation is required when creating a new node.


By default, a standard system *malloc* dynamically allocates memory on the heap. However, using the standard allocator may result in performance drop: each allocation requires an additional amount of memory. In other words, the operating system stores data about memory allocations, and this can consume large amount of RAM. Moreover, the standard system allocator provides inaccurate information regarding statistics on memory consumption.


That is why UNIGINE provides a **custom allocator** in addition to a standard system *malloc*. It allocates memory in ***pools***, making the allocation process faster and more efficient. Also, it enables gathering statistics on memory consumption, including information on the total number of allocations and the number of allocations per frame.


> **Notice:** The UNIGINE allocator gathers statistics for small allocations, as memory leaks mostly occur with small allocation up to 4000 bytes in size. To check statistics, run the [`memory_info`](../../code/console/index.md#memory_info) console command.


## Memory Pools


The UNIGINE custom allocator provides *two main memory pools* for allocations: **static** and **dynamic**.


- The **[static pool](#static_pool)** is allocated only once on the engine start-up and cannot be changed.
- The **[dynamic pool](#dynamic_pool)** increases dynamically and comes into play when the memory allocated in the static pool is full.


> **Notice:** There can be several pools of each type. The size of a pool is always a multiple of 16.


There are also additional **instance pools** that store allocations defined by developers. Usually, these are the allocations which are required regularly. They work the same way as the dynamic pools, but the instance pools have no size limitation.


### Static Pool


The static pools are essential for optimizing memory consumption. In other words, each allocation consumes approximately zero additional memory when using the static pools. Additionaly, it optimizes the allocations themselves, making them faster.


#### Configuring Static Pools


The static pools are limited by the size values you should specify in advance. To do so, you need to know the amount of required memory and its layout. To put it simply, you need to know how much memory of each type (16, 32, 48 bytes, etc.) to allocate. For example, the picture below demonstrates four static pools that contain allocations of 16, 32, 48, and 64 bytes:


![](static_allocs.png)


> **Notice:** UNIGINE provides functionality for configuring the static pools automatically. However, we recommend setting up the static pools according to your project needs.


Configuration of the static pools should be done for the specific hardware that corresponds to the minimum specifications. The static pool settings are stored in the `.boot` configuration file.


> **Notice:** This procedure must be performed for the release build, when the content is finalized. Any changes made after this point can make the static pools configuration inoptimal.


In general, the process is as follows:


1. In your project, identify a location that demands a significant amount of memory.
2. Set up your project so that it starts with this location.
3. Run the application with the [*-memory_statistics_enabled 1*](../../code/command_line.md#memory_statistics_enabled) command line option. It will enable gathering memory statistics required for pool configuration. > **Notice:** The statistics are collected only if there are no static pools configured before.
4. In the console, run the [`memory_optimize_static_pools`](../../code/console/index.md#memory_optimize_static_pools) console command to update and optimize the static pools.
5. Right after that, run the [`boot_config_save`](../../code/console/index.md#boot_config_save) console command to save the static pools settings to the `.boot` configuration file so that they can be used on the next application launch.
6. Restart the application to use the updated static pool configurations.


> **Notice:** The static pools cannot function if the limits are exceeded. In such cases, the [*dynamic pools*](#dynamic_pool) are activated.


### Dynamic Pool


> **Notice:** The dynamic pools are **unavailable on Linux**.


The **dynamic pools** also can optimize performance, but they cannot optimize memory consumption. However, they are restricted only by the size of RAM, which is an advantage. Moreover, the dynamic pools are more flexible as they can both expand and shrink their size as needed.


> **Notice:** If you haven't set up the size of the static pools according to your project's needs, the dynamic pools will be used primarily.


#### Configuring Dynamic Pools


Each dynamic pool stores allocations of a certain type � 16, 32, 48 bytes allocations, etc. So, you can always check how much memory of each type is allocated in the dynamic pools. These values are always a multiple of 16. For example, in the picture below, there are 16 pools of different sizes:


![](dynamic_allocs.png)


To configure the dynamic pools, you can use the [`memory_dynamic_pool`](../../code/console/index.md#memory_dynamic_pool) console command. It defines the number of the dynamic pools by specifying the maximum size of allocations. By default, it is set to 256 bytes, which means that there are 16 pools containing allocations from 16 to 256 bytes in size.


> **Notice:** As the size of allocations is a multiple of 16, the specified value will be automatically adjusted if necessary.


### Analyzing Pools Statistics


To get information on all the allocated static and dynamic memory pools, use the [`memory_info`](../../code/console/index.md#memory_info) console command.


It displays statistics on small allocations as a table, where each row corresponds to one memory pool.


| **Static pools allocations** ![](static_allocs.png) | - The *first value* indicates the type of allocations stored in the pool. - The *second value* displays the current memory allocation in the pool. - The *third value* represents maximum memory consumption that has occurred in the pool. This value indicates the maximum amount of memory the engine has requested (peak consumption). - The *fourth value* indicates the initial memory allocation at the engine start-up that defines the maximum amount of memory the engine can consume from the pool. - The *fifth value* represents the overhead RAM expenses required for maintaining the pool. - The *sixth value* indicates the current number of allocations made, in millions. |
|---|---|
| **Dynamic pools allocations** ![](dynamic_allocs.png) | - The *first value* indicates the type of allocations stored in the pool. - The *second value* indicates how many allocations are hold in the pool for further use. This value is limited to 2 Mb. - The *third value* displays the amount of free allocations in the pool. |
| **Total allocations** ![](total_allocs.png) | The values in the table provides statistics on all memory allocations that have occurred in all the pools |


## Video Memory Allocations


In addition to the custom RAM allocator, UNIGINE provides an option for managing VRAM allocations using memory pools.


> **Notice:** Video memory pools are used for PC applications only, as the process of working with video memory on consoles is different from that on PCs.


There are at least two reasons for using video memory allocations:


- The minimum block of memory that can be allocated by default is **64 Kb**. To avoid allocating such a large amount of memory for significantly smaller graphic resources (for example, textures that require much less than 64 Kb), we need to use memory pools.
- The process of allocation is extremely slow, so we have to allocate video memory in advance and then distribute it as needed.


> **Notice:** VRAM allocations are enabled by default.


### Configuring Pools


There is a console command that allows you to configure the pools for video memory allocations:


| d3d12_small_pool_enabled | Config file: [*.boot](../../code/configuration_file_cpp.md#boot) |
|---|---|
| **Description:** - Toggles small pool allocations on and off. By default, allocations are enabled. However, you can disable them via the console, save the `.boot` configuration file, and restart the application to apply changes. |  |


When configuring chunk sizes, a balance must be found between spikes, performance, and memory consumption. The larger the chunk size, the more stable the frame rate and performance, but the greater the memory consumption. So, we recommend running tests and fine-tuning the values.


### Analyzing Pools Statistics


To get information on all the allocated video memory pools, use the [`video_memory_info`](../../code/console/index.md#video_memory_info) console command. It will provide you with the following information:


> **Notice:** The number of pools may vary depending on the graphics card.


| **Heap Default** | The values in the table display statistics on the default heap, including the current VRAM consumption, the amount of allocated VRAM, the number of allocations in the pool, and so on. |
|---|---|
| **Heap Upload** | The values in the table display statistics on the heap used for uploading. |
| **Heap Readback** | The values in the table display statistics on the heap used for reading back. |


For more details, please refer to [this article](https://learn.microsoft.com/en-us/windows/win32/api/d3d12/ne-d3d12-d3d12_heap_type).


## Profiling Allocations


UNIGINE provides statistics on RAM and VRAM usage and allocation profiling. To get access to this information, run the [*Generic Performance Profiler*](../../tools/profiling/profiler/index.md#generic) and take a look at the following values:


> **Notice:** Statistics will differ depending on the operating system.


### RAM Allocations Statistics


| **CPU ram free** | The amount of currently available memory. |
|---|---|
| **CPU ram usage physics** | The current size of the working set. The working set is the set of memory pages currently visible in physical RAM ([check the source](https://learn.microsoft.com/en-us/windows/win32/api/memoryapi/nf-memoryapi-getprocessworkingsetsize#remarks)). |
| **CPU ram usage committed** | The total amount of private memory that the memory manager has committed for a running process ([check the source](https://learn.microsoft.com/en-us/windows/win32/api/psapi/ns-psapi-process_memory_counters_ex)). |
| **CPU ram malloc** | The amount of memory allocated by the UNIGINE custom allocator. |
| **CPU ram static pool** | The amount of memory allocated in static pools. |
| **CPU ram dynamic pool** | The amount of memory allocated in dynamic pools. Available on Windows only. |
| **CPU ram instance pool** | The amount of memory allocated in instance pools. |
| **Frame Allocations** | The number of allocations made per frame. |
| **Live Allocations** | The current/maximum number of allocations made during runtime (peak consumption). |


### VRAM Allocations Statistics


| **GPU vram free** | The amount of currently available video memory. |
|---|---|
| **GPU vram usage** | The amount of VRAM used by GPU. This value is provided by a graphics driver. |
| **GPU ram usage** | The amount of RAM used by GPU. This value is provided by a graphics driver. |
| **GPU alloc** | The number of allocations made by the engine on GPU. |
| **GPU Frame Allocations** | The number of video memory allocations made per frame. |
| **GPU Live Allocations** | The current/maximum number of allocations made during runtime (peak consumption). |
| **GPU Allocator small pool size** | The maximum size of the VRAM pool. |
| **GPU Allocator small usage** | Actual usage of the video memory pool. |


There is also a separate statistics block that tracks allocations for [*skinned meshes*](../../objects/objects/mesh_skinned/index.md) and [*decals*](../../objects/decals/index.md).


| **GPU Allocator skinned** | The amount of video memory allocated for skinned meshes. |
|---|---|
| **GPU Allocator decals** | The amount of video memory allocated for Decals. |


Each skinned mesh in the scene allocates memory independently. The VRAM for a skinned mesh is allocated in chunks within a separate pool. UNIGINE allows for configuring the size of the chunks via the [`skinned_pool_chunk_size`](../../code/console/index.md#skinned_pool_chunk_size) console command. By default, it is 64 Mb.


> **Notice:** The larger the chunk size, the higher the performance of the skinned meshes.


The same goes with the decals. To configure the chunk size for the decals, use the [`decal_pool_chunk_size`](../../code/console/index.md#decal_pool_chunk_size) console command.
