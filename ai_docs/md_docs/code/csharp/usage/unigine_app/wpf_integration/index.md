# WPF Integration


**[WPF (Windows Presentation Foundation)](https://learn.microsoft.com/en-us/dotnet/desktop/wpf/overview/)** is a UI framework for building desktop applications on Windows. This article provides instructions for running and integrating the WPF sample located in `<UnigineSDK>/source/csharp/proxy/wpf`, which demonstrates how to embed a UNIGINE rendering window into a WPF application with full support for mouse, keyboard, window management, and display handling.


![](wpf_proj_temp.png)


The core of this integration is the `SystemProxyWPF.cs`, which implements the *SystemProxyWPF* class (inherited from *[CustomSystemProxy](../../../../../api/library/engine/class.customsystemproxy_cpp.md)*). This class acts as a proxy layer between the UNIGINE Engine and the Windows system via WPF, providing:


- **Window management** - creation, fullscreen mode, resizing, positioning, icons, and window styles.
- **Input handling** - mouse, keyboard, scroll wheel, raw input, and custom cursor support.
- **Display and DPI management** - multi-monitor support, display resolution, and DPI queries.
- **Clipboard and dialogs** - reading/writing clipboard text and showing modal messages, warnings, or errors.
- **System interaction** - leveraging Windows APIs via *[P/Invoke](https://learn.microsoft.com/en-us/dotnet/standard/native-interop/pinvoke)* for low-level window, input, and DPI operations.


The sample uses **.NET 8**, taking advantage of the latest C# 12 features, with UNIGINE loaded as a `.dll` library. This integration allows WPF applications to host UNIGINE rendering while preserving native input and window behavior.


## Running the Sample


To run the sample:


1. Open the solution `<UnigineSDK>\source\csharp\proxy\wpf\main.csproj` in Visual Studio 2022 and *[build](../../../../../code/rebuild/index.md#build_vs)* it. All required dependencies are automatically resolved from `<UnigineSDK>\bin`.
2. Click *Start* or *Ctrl+F5* to launch the application.


## Integrating WPF into Your Own Project


To integrate WPF support into your own project, follow these steps:


1. Create a new C# project specifying the path to store project files, the SDK version, and precision settings to be used. ![](../../../../../start/quick_start/setup_project/create_new_cs.png)
2. From `<UnigineSDK>\source`, copy the `\csharp` and `\common` folders and paste them into the `\source` folder of your project. ![](wpf_files_0.png) > **Notice:** You can quickly access your project folder via the SDK Browser. Click the ellipsis button to the right of your project's name and select *Open Folder*.
3. Open the project file `your_project_name\source\csharp\proxy\wpf\main.csproj` in Visual Studio 2022.
4. Specify the solution configuration (*Debug, Debug-Double, Release, Release-Double*) **that matches your *[project settings](#new_project)***. ![](../../../../../code/rebuild/configuration_p.png)
5. Build and run the project by hitting ***Ctrl + F5***.
6. Use the *[console](../../../../../code/console/index.md)* to load the world: `world_load world_name`.


> **Warning:** The default C# template includes the `FirstPersonController.cs` component, which automatically creates and assigns its own camera. In the WPF integration setup, this automatic camera creation is not applied, so the scene may appear black because no active camera is assigned.


### Use New Empty World


If you **don't need the default template world**, you can *[create and load](../../../../../editor2/worlds/index.md#create_world)* a new empty world in your project. In the Editor's *Main Menu* click *File -> Create New World*, or press **CTRL + N**.


![](../../../../../editor2/worlds/create_new_world.png)


Change the default world to load by specifying the `-console_command "world_load world_name"` parameter in *Debug -> main Debug Properties* in Visual Studio 2022 or *[via the SDK Browser](../../../../../sdk/projects/index_cpp.md#custom_run)*.


![](wpf_custom_world.png)


### Keep Default C# Template


If you prefer to keep the default C# template:


1. Move the `your_project_name\source\common` folder and the contents of the `your_project_name\source\csharp\proxy\wpf` folder into your project's root. ![](wpf_files.png)
2. Open the `main.csproj` file and update **all** relative paths to library directories by removing unnecessary parent directory traversals (`..\..\..\..\bin`): | Before | After | |---|---| | ```text ..\..\..\..\junk\main_proxy_wpf\$(Configuration)\ ..\..\..\..\bin ..\..\..\common\Unigine.ico ..\..\..\..\bin\UnigineSharp_x64d.dll ..\..\..\..\bin\UnigineSharp_x64.dll ..\..\..\..\bin\UnigineSharp_double_x64d.dll ..\..\..\..\bin\UnigineSharp_double_x64.dll ``` | ```text junk\main_proxy_wpf\$(Configuration)\ bin common\Unigine.ico bin\UnigineSharp_x64d.dll bin\UnigineSharp_x64.dll bin\UnigineSharp_double_x64d.dll bin\UnigineSharp_double_x64.dll ``` |
3. Save `main.csproj` and open the project in Visual Studio 2022.
4. Build and run `main.csproj`. The camera will now work correctly in the default C# template world.


This setup allows the Editor to correctly parse all dependencies, letting you run the project directly from the Editor and build a working WPF integration.
