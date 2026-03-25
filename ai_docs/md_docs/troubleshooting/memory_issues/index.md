# Memory and Rendering-Related Issues


> **Notice:** This article describes methods and best practices for optimizing memory usage of the UNIGINE-application running in the **Windows operating system**.


When operating, the Engine utilizes various types of memory available on your device to load, process, and render resources. The path from your model and texture files on disk to their final display on screen goes through several stages of memory use and data transfer.


In the context of Windows operating systems, all types of memory are ultimately limited by the total amount of **Committed memory** available on the system. Committed memory represents the sum of **physical RAM** and the **Page File**, which together define how much data can be held in active use.


| ![](dataflow.svg) *While Total Committed Memory = Physical RAM + Page File, the Committed Usage represents all memory allocations made by the system and applications. If the Committed Usage approaches or exceeds the Total Committed Limit, the system will begin to fail memory allocations.* |
|---|


It is essential **that all required types of memory remain available** during the Engine operation. If any memory **becomes exhausted**, this may lead to:


- **Invisible objects and missing meshes** - geometry fails to appear when there is no space to load it.
- **Unloaded or blurry textures** - materials might appear black, low-resolution, or lose details.
- **Sudden framerate dropping** - caused by operating system attempting to recover and manage memory under a heavy load.
- **Unexpected crashes or scene instability** - when the memory pools become completely exhausted.

 ![](non_streamed_1.png)
*Example of unstreamed meshes and low-resolution textures caused by a lack of available committed memory. The Windows memory manager attempts to allocate additional resources to the Engine, but cannot always succeed.*

![](non_streamed_2.png)
*Example of unstreamed meshes and low-resolution textures caused by a lack of available committed memory. The Windows memory manager attempts to allocate additional resources to the Engine, but cannot always succeed.*

![](non_streamed_3.png)
*Example of unstreamed meshes and low-resolution textures caused by a lack of available committed memory. The Windows memory manager attempts to allocate additional resources to the Engine, but cannot always succeed.*

![](non_streamed_4.png)
*The expected result.*


## Profiling Memory


If you encounter missing assets, unloaded textures, or reduced frame rates, use the **[Profiler Tool](../../tools/profiling/profiler/index.md)** to inspect the Engine and locate possible memory bottlenecks.


By opening the *[Profiler](../../tools/profiling/profiler/index.md) - [Generic](../../tools/profiling/profiler/index.md#generic)* section, you can monitor the system-wide memory distribution and determine how much memory is currently being used by the Engine.


| ![](../../tools/profiling/profiler/profiler_run.png) *You can also enable the profiler display using the console commandshow_profiler* | ![](generic_profiler.png) *Generic Profiler Enabled* |
|---|---|


Some of the values displayed in the **Profiler** are read **directly from the operating system**, while others are **calculated by the Engine** based on statistics collected by its [Custom Memory Allocator](../../principles/allocator/index.md).


On Windows, your system memory is not limited solely to the RAM chips or modules, installed on a computer's motherboard. It is effectively extended by the ***Page File*** (also known as *virtual memory*), which allows the operating system to allocate more memory than is physically available.


In ***Task Manager***, open the ***Performance*** tab to monitor the total amount of memory currently available in your system.


You will find two values labeled ***Committed Memory***. The first shows the total amount of virtual memory allocated by all running processes, while the second indicates the total amount of virtual memory available on the system.


![](task_manager_ram.png)


> **Warning:** The **most important metric to monitor** is ***Committed Memory***, as it reflects the **actual state of system memory** and should be used to assess memory usage accurately.
>
>
> The ***In Use*** value displayed in *Task Manager* provides only an approximate estimate of actual memory usage.
>
>
> Additionally, VRAM allocations are also reflected in committed memory, so when performance drops or instability occur, **Committed Memory should be the first metric to check!**


Here is the short descriptions of RAM metrics displayed in the Profiler. Among them, the most important are the **FREE** metrics, which indicate how much memory is still available for the Engine to allocate. When new assets are being loaded, you may notice that the **RAM FREE** values in the Profiler begin to decrease. If this value **becomes negative**, it means that the Engine has exceeded its allocated memory budget, which can lead to unstreamed objects and unpredictable behavior (as shown in the pictures above).


| Physical RAM | Committed RAM |
|---|---|
| - ***FREE***: Available physical memory within the Engine's limit. (LIMIT - USAGE) - ***USAGE***: Physical RAM used by the Engine. (COMMITTED USAGE - GPU VRAM USAGE) - ***LIMIT***: Max physical RAM the Engine can use. Calculated as minimum of (**TOTAL** * [usage_limit_ram](#usage_limit_ram)) or (**TOTAL** - [free_space_ram](#free_space_ram)). - ***TOTAL***: Physical RAM installed on your computer. - ***CACHE***: Amount of RAM actively used by the engine excluding cached memory. - ***ACTIVE***: Amount of RAM used to cache streamed assets, including skinned meshes, static meshes, and textures. | - ***FREE***: How much committed memory the Engine can still use. Limited by *[Free Space Committed RAM](#free_space_ram_committed)* - ***USAGE***: How much committed memory the Engine is currently using. - ***BACKGROUND***: Committed memory used by other processes and the system. Calculated as TOTAL - USAGE - FREE - ***LIMIT** ([optional](#committed_memory_overcommit))*: The maximum committed memory the Engine can use. Limited by *[Free Space Committed RAM](#free_space_ram_committed)* - ***TOTAL***: Total committed memory available in the system. |


In the screenshot above, the system has 20.0 GB of total committed memory, of which 16.8 GB is already allocated. The Engine currently uses about 1.8 GB, while other processes take the remaining 15.4 GB, leaving around 3.3 GB of committed memory free.


For physical memory, **a usage limit is applied**. The Engine cannot allocate more RAM than this limit allows (shown by the *LIMIT* metric), and this **limit can be [adjusted in the settings](#advanced_memory_configuration)**.


> **Notice:** When the system runs out of committed memory, Windows cannot allocate additional memory pages, which may cause applications (including the Engine) to become unstable or even crash.


The other type of memory, that the Engine uses is VRAM - the memory used by the GPU to store textures, meshes, render targets, and other graphics resources.


Windows displays two main VRAM usage metrics in ***Task Manager - Performance - GPU***:


- **Dedicated GPU Memory** - the physical memory located on a graphics card. This is the fastest and most efficient type of memory for rendering operations.
- **Shared GPU Memory** - a portion of the system's physical RAM that the GPU can use when dedicated VRAM is exhausted.


![](task_manager_vram.png)


Once *dedicated VRAM* is fully utilized, the GPU automatically starts using *shared system memory*. This results in reduced performance, increased frame time, and longer asset loading times.


The Engine may use a small amount of shared memory by design, which is normal and does not affect performance, but excessive use usually indicates that VRAM is running out. For this reason, you should **always aim to stay within the limits of your dedicated GPU memory** to maintain stable performance and smooth asset streaming.


> **Notice:** In systems equipped with an **integrated GPU**, system RAM is used as VRAM. You can try to adjust the amount of memory allocated to the GPU in the **BIOS** or **vendor's software**. Allocating too little memory may cause rendering issues, while allocating too much will reduce the RAM available to the operating system and other processes.


## Editor and Runtime Memory Difference


Most development work is done directly in UnigineEditor, where the Viewport window usually takes up only part of the screen and operates at a lower resolution. Because of this, the overall **memory usage in the Editor is typically lower** than during the actual runtime.


If your project targets VR, the memory usage grows even further, as both eyes require separate high-resolution frames.


You can estimate the final runtime memory usage without building the project by experimenting with the following settings in the Editor:

 ![](virtual_resolution_1.png)
*Low Viewport Resolution*

![](virtual_resolution_2.png)
*Full HD Rendering (Virtual Resolution)*

![](virtual_resolution_5.png)
*4K Rendering (Virtual Resolution)*

![](virtual_resolution_3.png)
*VR Emulation - Quest Pro*

![](virtual_resolution_4.png)
*VR Emulation - Varjo VR-4*


## Possible Solutions


If memory exhaustion has been confirmed based on data from the **[Profiler](../../tools/profiling/profiler/index.md)** and **Task Manager**, consider applying one or more of the following methods to resolve the issue:


### Closing Background Processes


Since the Engine is not the only process running on your device, it is important to monitor memory usage across the entire system. Background applications, for example, web browsers, can consume a significant amount of memory.


![](background_processes.png)


Use Task Manager to monitor active processes and close those that are not required. Reducing background activity frees up system resources and allows the Engine to allocate more memory for streaming operations.


> **Notice:** Closing an application does not always release its memory immediately. Some recources may remain allocated for a short period of time. To ensure a clean state, use the *[memory_clear](../../code/console/index.md)* console command or, preferably, restart the Engine.


### Ensuring Sufficient Disk Space


Make sure there is enough **free space** on the **drive where the Page File is located**.


![](no_disk_space.png)


If the disk is nearly full, **Windows cannot expand the Page File**, which leads to memory allocation failures and system instability.


### Manually Increasing the Page File Size


On Windows, you can manually define the size of your page file or configure it to expand automatically when needed.


> **Warning:** It is strongly **recommended not to disable the page file**, as it essential for system stability.

 ![](advanced_system_settings.png)
*Windows 11 Virtual Memory Settings location*

![](virtual_memory.png)
*Windows 11 Virtual Memory Settings location*


A generally optimal page file size can be calculated as: (RAM + VRAM) * 2.


This ensures sufficient committed memory for both the Engine and other system processes.


### Turning Off Microprofile Tool


If you are running a **Development build of the engine**, you can disable the Microprofile tool at startup to free several gigabytes of RAM. To do this, add the following parameter to the Engine's startup command line:


```text
-microprofile_enabled 0

```


### Optimizing Content


Optimizing the content of your world can also have a significant positive impact on memory usage and overall performance. Reducing the number of high-resolution textures, merging meshes, optimizing materials, and using efficient [Level of Detail](../../content/optimization/geometry/lods/index.md) (LOD) setups can greatly lower both RAM and VRAM consumption.


For more detailed guidance, refer to the **[Content Optimization](../../content/optimization/index.md)** article series, which covers best practices for asset creation, scene organization, and streaming efficiency.


> **Notice:** In VR application development, performance and memory requirements are significantly more demanding due to higher frame rate targets and stereo rendering overhead. For recommended settings and detailed optimization strategies specific to VR projects, see the **[VR Best Practices](../../content/vr/index.md)** article.


### Advanced Engine Memory Configuration


In the *Settings - Runtime - Render - Streaming* section, you can find parameters that control how the Engine allocates and manages different types of memory. These options define how much physical RAM, committed memory, and VRAM the Engine is allowed to use.


These settings are tuned for optimal performance by default, but changing them might help to achieve a better balance between memory usage and application stability. Incorrect values may lead to slowdowns or crashes.


> **Notice:** For example, if you have two projects running simultaneously, it might be a good idea to allow each Engine instance to consume around 40% of the total system memory by configuring the corresponding limits. The most approptiate values, however, will depend on your specific project, background processes, and hardware configuration.


#### Committed RAM Configuration


| Free Space Committed RAM | The amount of committed memory that the Engine will always keep free and never allocate for its own use, in Mbytes. Range of values: **[0, INT_MAX]**. The default value is : **512**. `Console access:render_streaming_free_space_ram_committed` ([API control](../../api/library/rendering/class.render_cpp.md#render_streaming_free_space_ram_committed)) |
|---|---|
| Committed Memory Overcommit | The value indicating whether the Engine enforces internal limits on committed memory usage. - When **disabled**, the Engine respects the **Free Space Committed RAM** setting and will not allocate more committed memory than the configured limit allows. In this mode, the amount of physical RAM and VRAM available to the Engine is effectively reduced to the portion of committed memory accessible within this limit. - When **enabled** (default), the Engine ignores the **Free Space Committed RAM** restriction and can use **all available committed memory** provided by the system. This may improve streaming performance, especially under high memory pressure (for example, when browsers or other background applications are running, or after long system uptime), but it also increases the risk of instability if the system runs out of virtual memory. > **Warning:** With overcommit enabled, crashes may occur if: > > > - the system has no page file > - there is insufficient free disk space on the drive where the page file is located. > > > If system committed memory is fully exhausted, this may affect not only the Engine, but also **other running applications**. **enabled** by default. `Console access:render_streaming_committed_memory_overcommit` ([API control](../../api/library/rendering/class.render_cpp.md#render_streaming_committed_memory_overcommit)) |


#### RAM Configuration


| Free Space RAM | The amount of physical memory that the Engine will always keep free and never allocate for its own use, in Mbytes. Range of values: **[0, INT_MAX]**. The default value is : **1024**. `Console access:render_streaming_free_space_ram` ([API control](../../api/library/rendering/class.render_cpp.md#render_streaming_free_space_ram)) |
|---|---|
| Usage Limit RAM | The percentage of the total physical memory (RAM) that the Engine is allowed to use for streaming. If the streaming exceeds the RAM usage limit, the application may become unstable or crash. Range of values: **[10, 100]**. The default value is : **80**. `Console access:render_streaming_usage_limit_ram` ([API control](../../api/library/rendering/class.render_cpp.md#render_streaming_usage_limit_ram)) |
| Cache RAM | The  maximum size of RAM available for streaming caches. When set to -1, caches grow freely up to [engine limits](#render_streaming_usage_limit_ram). When limited, caches will grow only up to the defined value. If the limit is too low, not all resources will fit into the cache in time, which may cause streaming to stutter. Range of values: **[-1, inf]**. The default value is : **-1**. `Console access:render_streaming_cache_ram` ([API control](../../api/library/rendering/class.render_cpp.md#render_streaming_cache_ram)) |


#### VRAM Configuration


| VRAM Overcommit | The value indicating whether VRAM limits (both the usage limit and free space) are applied. **disabled** by default. `Console access:render_streaming_vram_overcommit` ([API control](../../api/library/rendering/class.render_cpp.md#render_streaming_vram_overcommit)) |
|---|---|
| Free Space VRAM | The amount of VRAM that the Engine will always keep free and never allocate for its own use, in Mbytes. Range of values: **[0, INT_MAX]**. The default value is : **512**. `Console access:render_streaming_free_space_vram` ([API control](../../api/library/rendering/class.render_cpp.md#render_streaming_free_space_vram)) |
| Cache VRAM | The  maximum size of VRAM available for streaming caches. When set to -1, caches grow freely up to [engine limits](#render_streaming_usage_limit_vram). When limited, caches will grow only up to the defined value. If the limit is too low, not all resources will fit into the cache in time, which may cause streaming to stutter. Range of values: **[-1, inf]**. The default value is : **-1**. `Console access:render_streaming_cache_vram` ([API control](../../api/library/rendering/class.render_cpp.md#render_streaming_cache_vram)) |


### Upgrading Hardware


If memory or performance issues persist even after optimizing content and adjusting all of the settings related to system and the Engine described above, consider upgrading your hardware.


Refer to the **[System Requirements](../../start/requirements.md)** for detailed information on recommended configurations and hardware specifications.


In general, having more system memory available is always beneficial, for example, 64 GB of **RAM** and 16 GB of **VRAM** can provide a noticeably smoother experience and greater stability when working with complex projects.
