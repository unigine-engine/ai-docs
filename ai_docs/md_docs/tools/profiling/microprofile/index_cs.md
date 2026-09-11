# Microprofile (CS)


UNIGINE has support for **[Microprofile](https://github.com/zeux/microprofile)**, an advanced external embeddable CPU/GPU profiler with support for per-frame inspection.


[![](microprofile_sm.jpg)](microprofile.jpg)

*MicroprofileTool*


The profiler features the following:


- Profiling operations performed by the engine on CPU and GPU
- Profiling the engine threads
- Profiling up to 1000 frames
- The performance data output to a local web server or to an HTML file


## Running Microprofile


The *Microprofile* tool is available **only for the *Development* builds** of UNIGINE Engine: it won't be compiled for the *Debug* and *Release* ones. You can use the `microprofile_info` console command to check if the *Microprofile* is included into the compilation.


The performance data obtained by the *Microprofile* can be output to a local web server or to an HTML file.


> **Notice:** *Microprofile* shows valid information only after the first 1000 frames are rendered (e.g. at the framerate of 60 FPS, such "warmup" time comprises about 16 seconds).


### Enabling and Disabling Microprofile


> **Warning:** *Microprofile* is performance-consuming, that's why we recommend you to **enable it only when you work with it and keep disabled otherwise**.


1. Make sure that your project [runs on the *Development* build](../../../sdk/projects/index_cs.md#engine_build). The *Microprofile* tool is available for the *Development* build only. If your project runs on a *Release* build, [reconfigure](../../../sdk/projects/index_cs.md#update_config) it via *SDK Browser*.
2. Toggle *Microprofile*.

  - One way to toggle *Microprofile* is to toggle the corresponding option before running [UnigineEditor](../../../sdk/projects/index_cs.md#customize_edit) or the [application](../../../sdk/projects/index_cs.md#customize_run): ![Disabling Microprofile via SDK Browser](disable_microprofile.png)
  - Another way is to use the `microprofile_enabled` console command. > **Notice:** If you change the *Microprofile* status via the console, this setting is saved in the `<Project_Name>/data/configs/default.user` file. The state set in the user configuration file will override the state defined via SDK Browser.
3. Run the Editor or application.


### Saving Performance Data to File


Microprofile allows saving the performance data to an `HTML` file and then analyzing it offline.


To output the performance data to the HTML file, perform the following:


1. In the console, set the the number of frames to be profiled via the `microprofile_dump_frames` console command. You can skip this step: by default, 500 frames will be profiled.
2. Run the `microprofile_dump_html` console command.


The performance data will be saved to the specified `HTML` file.


> **Notice:** If the path isn't specified, the dump is saved to `data/microprofile_dump_html` folder.


Using profiling dumps simplifies capturing performance "spikes": the engine continues rendering the application in the background even when it is out of focus, so the frame where the spike has occurred can be overwritten in case of [using the Web server](#web_browser_visualization) for performance data visualization. Also it can be used to estimate the optimization results: you can dump frames before and after optimization and compare them.


### Visualization Using Built-In Server


To visualize the performance data using the local web server, do the following:


1. In the console, check the current state of Microprofile using the `microprofile_info` console command. The displayed web server port is required for data visualization. Adjust the [number of frames](../../../code/console/index.md#microprofile_webserver_frames), if required.
2. In the Web browser address bar, type `localhost:1337` (number is the web server port, provided in the info). You can display only a part of the profiled frames: add **/<number_of_frames>** to the current URL. For example, if you specify `localhost:1337/100`, only the first 100 frames will be displayed. In the Editor, Microprofile is also accessible via the toolbar (*Tools -> Microprofile*): ![](microprofile_editor.png)


The performance data will be displayed in your Web browser.


> **Notice:** Use **F5** to refresh profiling data as there is no automatic update.


All console commands related to performance profiling are available [here](../../../code/console/index.md#microprofile).


## Performance Data


The *Microprofile* visualizes the detailed per frame performance data on the operations performed by the engine on CPU and GPU and on the engine threads. In the *Microprofile* main menu, you can change the visualization mode: click *Mode* and choose the required one. By default, the *Detailed* mode is set.


![](groups.jpg)

*Profiling Groups Displayed inDetailedMode*


In the *Detailed* mode, each operation (function) and thread is displayed as a separate colored region. The regions are hierarchical: the function called by the other function is displayed under the last one. The size of the region is determined by the time the corresponding operation takes.


In the picture below, the *Engine::do_render()* function calls the *RenderRenderer::renderWorld()* functions and so on:


![](regions.jpg)


To view the data on a certain operation or a thread, point to the corresponding region. To zoom in/out the displayed regions, scroll the mouse wheel.


### CPU Data


In the **Main** group of the performance data, the call stack of the operations (e.g., *update, rendering*, etc.) performed by the engine on CPU is displayed.


![](cpu_data.jpg)

*Performance Data onWorld UpdateFunction*


### GPU Data


In the **GPU** group of the performance data, the call stack of the operations performed by the engine on GPU is displayed. In addition to the main performance data, for each function (e.g. environment rendering, post materials rendering and so on), the number of DIP calls and rendered triangles is shown. Also there can be the number of surfaces, lights, shadows rendered by this function, the number of materials and shaders used; the information on the node or material for which the function is called (identifier, name, etc.).


![](gpu_data.jpg)

*Performance Data on Deferred Lighting Rendering*


When the region that corresponds to the certain function is pointed, the *Microprofile* displays when this function is called on CPU and how much time is spent on its performing.


Vulkan or DirectX commands can be combined into GPU Debug groups that are created automatically when defining a profiling scope. All graphic resources loaded from external files, such as textures, shaders, static or skinned meshes, as well as the Engine's internal resources, have their own debug names to simplify identification. This information can be useful when using Graphics API debuggers, such as *NVIDIA Nsight* or *RenderDoc*.


[![](renderdoc.png)](renderdoc.png)

*Example of debug data viewed inRenderDoc*


### Engine Threads Data


The performance data on the engine threads is visualized in the **CPUThread*, *SoundThread*, *AsyncQueueThread*, *WorldSpawnMeshClutterThread*, *WorldSpawnGrassThread** groups.


![](thread_data.jpg)

*Performance Data on Physics Thread*


## Using Microprofile For Application Logic


You can use the *Microprofile* to inspect performance of your application logic.


1. Open the source code of your application.
2. Find a function or a scope in the code you want to inspect.
3. In the beginning of the function (or the scope), call *[Profiler.Begin()](../../../api/library/engine/class.profiler_cs.md#begin_cstr_void)*. Specify a name for the capture to be displayed in the *Microprofile*. > **Notice:** You can specify the *__FUNCTION__* macro to automatically use the class and the function name as the capture.
4. In the end of the function, call *[Profiler.End()](../../../api/library/engine/class.profiler_cs.md#end_float)*. <details> <summary>Microprofile.cs | Close</summary> ```csharp private void Update() { // start profiling Profiler.Begin("Component Update"); float time = Game.Time; Vec3 pos = new Vec3(MathLib.Sin(time) * RADIUS, MathLib.Cos(time) * RADIUS, 0.0f); trigger.Enabled = pos.x > 0.0f || pos.y > 0.0f; trigger.WorldPosition = pos; // stop profiling Profiler.End(); } ``` </details>
5. Run the project.
6. Open the console and run the `microprofile_enabled 1` command.
7. Go to the *Microprofile* and find the region with the specified name.


![](user_microprofile_cs.png)


The *[Begin()](../../../api/library/engine/class.profiler_cs.md#begin_cstr_void)* and *[End()](../../../api/library/engine/class.profiler_cs.md#end_float)* functions make the profiling scope available for **both** the [Profiler](../../../tools/profiling/profiler/index.md) and the *Microprofile*.


![](user_profiler_cs.png)


If you want to use the Microprofile only, create the counter via the *[Profiler.BeginMicro()](../../../api/library/engine/class.profiler_cs.md#beginMicro_cstr_int_int)* and *[Profiler.EndMicro()](../../../api/library/engine/class.profiler_cs.md#endMicro_int_void)* functions.


> **Notice:** *BeginMicro()* returns an identifier that should be passed to *EndMicro()*. Thus, [several nested counters](#nested_cs) can be created.


<details>
<summary>Microprofile.cs | Close</summary>

```csharp
private void Update()
{

	// start profiling
	int id = Profiler.BeginMicro("Component Update");

	float time = Game.Time;

	Vec3 pos = new Vec3(MathLib.Sin(time) * RADIUS, MathLib.Cos(time) * RADIUS, 0.0f);

	trigger.Enabled = pos.x > 0.0f || pos.y > 0.0f;
	trigger.WorldPosition = pos;

	// stop profiling
	Profiler.EndMicro(id);

}


```

</details>


### Creating Nested Counters for Profiling


To create several nested counters, you should use the *[Profiler.BeginMicro()](../../../api/library/engine/class.profiler_cs.md#beginMicro_cstr_int_int)* and *[Profiler.EndMicro()](../../../api/library/engine/class.profiler_cs.md#endMicro_int_void)* functions. *BeginMicro()* returns an identifier that should be passed to *EndMicro()*. This enables to create nested and intersecting profiler counters.


In the following example, combination of *Begin()/End()* and *BeginMicro()/EndMicro()* is used. So, profiling of the *Update()* function will be available in both the Profiler and the *Microprofile*.


<details>
<summary>Microprofile.cs | Close</summary>

```csharp
private void Update()
{

	// start profiling
	Profiler.Begin("Component Update");

	float time = Game.Time;

	// start a nested counter
	int id_0 = Profiler.BeginMicro("Trigger Position");

	Vec3 pos = new Vec3(MathLib.Sin(time) * RADIUS, MathLib.Cos(time) * RADIUS, 0.0f);

	// stop the counter
	Profiler.EndMicro(id_0);

	trigger.Enabled = pos.x > 0.0f || pos.y > 0.0f;
	trigger.WorldPosition = pos;

	// stop profiling
	Profiler.End();

}


```

</details>


![](user_microprofile_nested_cs.png)


> **Notice:** Use only *BeginMicro()/EndMicro()*, if you don't need the [Profiler](../../../tools/profiling/profiler/index.md) tool.


### Profiling Logic Using Macros


There are special **macros** to mark fragments of your code that should be inspected. They can be used instead of the *[BeginMicro()](../../../api/library/engine/class.profiler_cs.md#beginMicro_cstr_int_int)* and *[EndMicro()](../../../api/library/engine/class.profiler_cs.md#endMicro_int_void)* functions:


- *UNIGINE_PROFILER_FUNCTION* to inspect performance of the function. | Using Macro | Using Functions | |---|---| | ```csharp void myFunction() { UNIGINE_PROFILER_FUNCTION; // your function code } ``` | ```csharp void myFunction() { int id = Profiler.BeginMicro(__FUNCTION__); // your function code Profiler.EndMicro(id); } ``` |
- *UNIGINE_PROFILER_SCOPED* to inspect only a certain part of the code. | Using Macro | Using Functions | |---|---| | ```csharp void myFunction() { // your function code { UNIGINE_PROFILER_SCOPED("Scope name"); // your function code } } ``` | ```csharp void myFunction() { // your function code { int id = Profiler.BeginMicro("Scope name"); // your function code Profiler.EndMicro(id); } } ``` |


## Video Tutorial: Performance Inspection with Microprofile
