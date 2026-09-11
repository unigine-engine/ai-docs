# VR Profiler


![](index.jpg)


**VR Profiler** is a built-in overlay for monitoring rendering statistics directly in VR mode. The profiler is displayed only inside the VR headset and does not obstruct the main application output on the monitor. It can be used to quickly check the current rendering state, analyze performance, track memory usage, and monitor dynamic resolution behavior without leaving the VR session.


**VR Profiler** supports several display modes and can be configured depending on how much information you need during debugging or profiling.


> **Notice:** **VR Profiler** is only available for the *[Development](../../sdk/projects/index_cpp.md#engine_build)* build.


## Enabling VR Profiler


VR Profiler is toggled using the `vr_show_profiler` console command. Two modes are available:


- **Basic** mode (`vr_show_profiler 1`) - a compact overview of the most important VR rendering metrics. It is intended for quick checks during development or testing when you only need to verify the general rendering state without displaying detailed diagnostic data. ![](basic_mode.jpg) This mode is useful for checking that VR rendering general performance is not bound by any substantial degradations while keeping the overlay as lightweight as possible.
- **Advanced** mode (`vr_show_profiler 2`) - extended profiling information for deeper analysis of VR rendering. It includes detailed data such as rendering resolution, Dynamic Resolution Scaling graphs, performance statistics, and memory usage broken down by data type. ![](advanced_mode.jpg) This mode is useful when investigating performance issues, analyzing GPU load, checking how resolution changes over time, or monitoring memory consumption during a VR session.


## Configuring Advanced Profiler Sections


**[Advanced](#advanced)** mode may display a large amount of information. If you want to focus only on a specific category of profiling data, unnecessary sections can be hidden using the following console commands:


Available sections:


![](vr_profiler_sections.png)


| Command | Description |
|---|---|
| `vr_show_profiler_misc` | Shows or hides miscellaneous VR rendering information. |
| `vr_show_profiler_performance` | Shows or hides performance-related profiling data. |
| `vr_show_profiler_memory` | Shows or hides memory usage information. |


## VR Profiler Metrics


**VR Profiler** displays the following information by default:


| Metric | Description |
|---|---|
| **Miscellaneous** |  |
| **Context Resolution** | The resolution of the VR rendering context used for the current frame. |
| **Focus Resolution** | The resolution of the high-detail focus area used for foveated rendering. |
| **Materials** | Number of materials set per frame. (Materials are set in each of the [rendering passes](../../principles/render/sequence/index.md).) |
| **DIPs** | The number of draw calls submitted for rendering. The higher the number of identical mesh surfaces with the same material, the fewer is the number of draw calls, offloading both the CPU and the GPU. |
| **Foveated** | Shows the current foveated rendering mode: - **Disabled** - foveated rendering is disabled. - **Fixed** - fixed foveation when foveated rendering is active, but no Eye Tracking is available. - **Dynamic** - dynamic foveation using Eye Tracking, if available. |
| **ASW** | Shows whether Asynchronous Reprojection is currently enabled. Enabled by default. |
| **Dynamic Resolution Scaling** | Shows whether Dynamic Resolution Scaling is currently enabled. When enabled, the chart displays *Context Resolution* and *Focus Resolution* scale multipliers over time. - 1.0x means the GPU keeps up with the original target resolution; - values above 1.0x indicate GPU performance headroom; - values below 1.0x mean the resolution is reduced because the GPU cannot maintain the target performance. |
| **Performance** |  |
| **Total** | Total time in milliseconds taken to both calculate and render the current frame. This is the duration of the [main loop](../../code/fundamentals/execution_sequence/main_loop.md) in the application [execution sequence](../../code/fundamentals/execution_sequence/index.md). |
| **Total CPU** | Total time in milliseconds taken to prepare the current frame (including *update, render*, and *swap*). |
| **Total GPU** | GPU execution time measured using timestamp queries from the graphics API. Represents the duration of GPU work for a single frame. > **Notice:** Since the data is taken from the graphics API, therefore, convergence with the other timings received by the engine itself is not guaranteed. |
| **Update** | Time taken to update application logic. This includes executing all steps in the [***update()***](../../code/fundamentals/execution_sequence/main_loop.md#update) function of the world script. It also includes the update of states of all nodes (for example, update of the skinned animation or of a particle system to spawn new particles). - If the Update time is too high, it signals that you need to optimize the application logic executed each frame. - You may also need to decrease the number of objects in the world, as updating their states (spawn particles by the particle systems, play skinned mesh animation, etc.) increases the load. |
| **Waiting GPU** | Time between completing all calculations on the CPU up to the moment when the GPU has finished rendering the frame. (See the [illustration](../../code/fundamentals/execution_sequence/index.md#waiting_gpu)). This counter is useful to analyze the bottleneck in your application's performance. - When Waiting GPU time is equal to **0**, it signals that scripts take too long to be updated and calculations are too intensive for CPU to perform them fast enough. In this case, your application has a CPU bottleneck. Optimize your update block in the world scripts or reduce the number of objects updated each frame. - High Waiting GPU time means one of the following: - low framerate signals that there exists a GPU bottleneck. The art content needs to be optimized in this case. - consistently high framerate means you have free CPU resources available to process more numbers in the *update()* of the world script. |
| **Target** | The target frame time required to maintain the current VR refresh rate. Uses *VR::getHMDRefreshRate* to get target value. |
| **Memory** |  |
| **VRAM Utilization** | Amount of VRAM currently available for use, calculated based on configured streaming limits and budget. This value includes the amount of GPU video memory currently in active use and the amount of GPU memory used to store cached streamed assets, including skinned meshes, static meshes, and textures. |
| **Render Buffers** | The amount of video memory currently reserved for rendering buffers (Gbuffer, post-effects, etc.). |
| **Textures** | Total amount of VRAM currently used by textures. |
| **Meshes** | The amount of video memory currently used by loaded geometry data. |
| **RAM Usage** | The amount of system memory currently used by the application. This value includes the amount of system memory currently in active use and the amount of system memory used to cache streamed assets, including skinned meshes, static meshes, and textures. |


## Changing the Profiler Position


[![Position set to 4](position_4.jpg)](position_4.jpg)

*Profiler position set to 4*


The profiler position can be changed using the `vr_profiler_position` command with the values from 1 to 9. The value selects one of the predefined screen position presets. Presets 1-9 correspond to the NumPad layout:


![](layout.png)

*Presets location*


Type in the corresponding number key either on the main keyboard or on the NumPad, to move the profiler to the selected position.


Shifting the profiler's position is useful when the overlay overlaps important scene elements or UI controls.


## Adjusting the Profiler Background


The opacity of the profiler background can be changed with `vr_profiler_background_alpha <0-1>`.

  ![](alpha_02.jpg)
vr_profiler_background_alpha 0.2

  ![](alpha_08.jpg)
vr_profiler_background_alpha 0.8

  ![](alpha_1.jpg)
vr_profiler_background_alpha 1.0


Adjusting the background opacity can help reduce visual distraction or improve readability depending on the scene brightness and complexity.


## Adding Custom Values via Profiler API


Custom values can be added to the *VR Profiler* using the Profiler API. This makes it possible to display project-specific metrics, counters, or graphs directly in the VR profiling overlay (the option is currently available only in **[Advanced](#advanced)** mode). This can be useful when you need to monitor custom rendering, simulation, streaming, or gameplay-related values alongside built-in engine metrics.


```cpp
Math::vec4 color = Math::vec4_blue;

Profiler::setValue("My Metric", "ms", my_metric_ms, 50.0f, color.get(), Profiler::COUNTER_VR_FLAG_PERFORMANCE_ADVANCED, true);

```
