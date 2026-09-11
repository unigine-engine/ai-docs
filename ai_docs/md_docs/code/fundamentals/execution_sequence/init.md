# Engine Initialization


This article describes in detail the steps performed by the UNIGINE Engine during **initialization**.


At this stage, the Engine prepares all core subsystems required for application startup and further execution. This includes parsing command-line arguments, initializing hardware interfaces and APIs, setting up configuration files, log and data paths, creating internal threads, and connecting to graphics, audio, and input systems.


Once all initialization steps are completed, the Engine is fully ready to start the **[main loop](../../../code/fundamentals/execution_sequence/main_loop.md)**.


> **Notice:** Initialization steps are accompanied by log messages. For example, when opening the Editor, these messages can be observed in the *Console* tab, and when running the application, they are displayed in the in-game console (opened by default with the **~** key).
>
>
> Log files are also created by default in the `/bin` folder of your project.


The **first frame** is processed in a special way, as it finalizes the setup of core systems and scripts. For this reason, its steps are also listed in this article and considered as a part of the initialization process.


For other steps and general information about execution sequence, see the [Execution Sequence](../../../code/fundamentals/execution_sequence/index.md) article.


## Initialization steps


| Engine Initialization |  |
|---|---|
| 1. | The main application thread is identified and stored to ensure [thread safety](../../../code/fundamentals/thread_safety/index.md) for operations that must be executed on the main thread only. |
| 2. | **[Command-line options](../../../code/command_line.md)** provided at start-up are parsed and stored for later configuration. > **Notice:** Command-line values override the default values and values specified in the [configuration files](../../../code/configuration_file_cpp.md). |
| 3. | The **[System Info](../../../api/library/engine/class.systeminfo_cpp.md)** is initialized to provide access to information about the current hardware configuration. |
| 4. | The UNIGINE API is initialized. |
| 5. | The home directory and the application directory are determined. A path to the folder where all application data will be saved by default: - If you pass a [*project name*](../../../code/command_line.md#project_name) via the command line or on engine initialization, all data (such as log files, cache, and configuration files) are stored in the user's home directory as follows: - On Windows, in the `C:/Users/<username>/<project_name>/` folder - On Linux, in the `/home/<username>/.<project_name>/` folder - Otherwise, data is stored in the application folder (`<PROJECT_DIRECTORY>/bin/` with the binary executable file). |
| 6. | The *[Console](../../../code/console/index.md)* history is restored. |
| 7. | [Third-Party Notices](../../../third_party.md) are written to the log. |
| 8. | [Configuration files](../../../code/configuration_file_cpp.md) and additional dependencies are loaded and processed (command-line arguments have higher priority); a corresponding message is written to the log: ```text ---- Configs ---- Loading boot config "D:/UNIGINE/UNIGINE Projects/MyProject/data/configs/editor.boot"... Loading user config "D:/UNIGINE/UNIGINE Projects/MyProject/data/configs/default.user"... Using config file "configs/default.config" Using boot config file "configs/editor.boot" Using user config file "configs/default.user" Using controls config file "configs/default.controls" Loading "dxgi.dll"... ``` |
| 9. | Remaining **[command-line options](../../../code/command_line.md)** are parsed (the ones that haven't been parsed [previously](#cli_paths)). These options specify basic video settings, such as a graphics API to be used for rendering (DirectX or Vulkan; also you can disable the graphics API), size of the application window, and so on. You can also pass any external *[#define](../../../code/command_line.md#extern_define)* directives and [console variables](../../../code/console/index.md#operation) via the command line. > **Notice:** Command-line values override the default values and values specified in the [configuration files](../../../code/configuration_file_cpp.md). |
| 10. | The UNIGINE custom [Memory Allocator](../../../principles/allocator/index.md) is initialized for faster and more optimal allocations compared to the default system allocator. In the engine code, it is set via the *USE_MEMORY* directive. |
| 11. | The GPU is initialized, and full information about the current hardware [is written to the log](../../../api/library/engine/class.systeminfo_cpp.md#logInfo_void) (Engine info, OS, CPU and GPU). |
| 12. | [Microprofile](../../../tools/profiling/microprofile/index_cpp.md) and [Memory Profiler](../../../tools/profiling/profiler/index.md) are initialized. The *Microprofile* web server status is written to the log (if enabled): ```text ---- Engine Microprofile ---- Microprofile initialization (Time: 0.6ms, Memory: 1.4KB) MicroProfile: Web server started on port 1338 ``` |
| 13. | The [general-purpose thread pools](../../../code/fundamentals/thread_system/index.md#thread_pools) are initialized. |
| 14. | Internal Engine threads for specialized tasks are initialized. See the [Threading](../../../code/fundamentals/thread_system/index.md) article for details. |
| 15. | The default *[System Proxy](../../../api/library/engine/class.customsystemproxy_cpp.md)* is initialized. The Engine connects to the graphics subsystem, audio devices, and input systems. Corresponding message is written to the log: ```text ---- System Proxy ---- SystemProxy initialization (Time: 0.0ms, Memory: 0B) ``` |
| 16. | [VR API](../../../code/command_line.md#vr_app) is initialized. Corresponding message is written to the log: ```text ---- VR ---- VR initialization (Time: 0.0ms, Memory: 896B) ``` |
| 17. | [Rendering API](../../../code/command_line.md#video_app) is initialized. Corresponding message is written to the log: ```text ---- Render ---- Renderer API: Direct3D 12.0 Maximum texture size: 16384 Maximum texture units: 16 DLSS is supported DLSS Streamline version: 2.8.12 FSR is supported FSR Version: 3.1.3 FSR Max Contexts: 8 Render initialization (Time: 5.2s, Memory: 25.6MB) ``` |
| 18. | The Window Manager is initialized (see the *[WindowManager](../../../api/library/gui/class.windowmanager_cpp.md)* class for details). |
| 19. | The Input System is initialized. |
| 20. | Displays are initialized (see the *[Displays](../../../api/library/gui/class.displays_cpp.md)* class for details). |
| 21. | VR Subsystems are initialized. Corresponding message is written to the log: ```text ---- VR Subsystems ---- VR Subsystems initialization (Time: 0.1ms, Memory: 17.4KB) ``` |
| 22. | The [Boot screen](../../../code/gui/screens/index.md#boot) is shown based on the `default.boot` [configuration file](../../../code/configuration_file_cpp.md). |
| 23. | The [File System](../../../principles/filesystem/index_cpp.md) is initialized. Corresponding message is written to the log: ```text ---- Filesystem begin ---- App path:  D:/UNIGINE/UNIGINE Projects/MyProject/bin/ Data path: D:/UNIGINE/UNIGINE Projects/MyProject/data/ Save path: D:/UNIGINE/UNIGINE Projects/MyProject/bin/ Runtimes loaded: 7 (Time: 13.3ms, Memory: 245.8KB) Filesystem initialization (Time: 422.4ms, Memory: 1.6MB) ``` |
| 24. | Render presets are loaded, including default ones (*Low, Medium, High*, etc.) as well as any custom presets. |
| 25. | Console and Profiler fonts are loaded. |
| 27. | The sound system is initialized. Corresponding message is written to the log: ```text ---- Sound ---- Loading "openal32.dll"... Renderer: OpenAL Soft on Realtek Digital Output (2- Realtek(R) Audio) OpenAL vendor: OpenAL Community ... Sound: openal Sound initialization (Time: 110.6ms, Memory: 6.9KB) ``` |
| 28. | A set of internal managers is created (e.g., *[Game](../../../api/library/engine/class.game_cpp.md), [Physics](../../../api/library/physics/class.physics_cpp.md), [Materials](../../../api/library/rendering/class.materials_cpp.md), [Properties](../../../api/library/engine/class.properties_cpp.md), [Animations](../../../api/library/animations/class.animations_cpp.md)*, etc.). Each of these classes exists as a single global instance (singleton). |
| 29. | [Asynchronous data streaming](../../../principles/data_streaming/index.md) is started. |
| 30. | Meshes, materials, and properties are loaded. If preload-related console variables are specified in the Engine startup configuration file, PSOs, shaders, and materials are compiled and cached. ```text ---- Materials begin---- ---- MeshManager begin ---- Initialization meshes (Time: 18.7ms, Memory: 580.4KB) Total resources: 28 ---- MeshManager end ---- ---- Properties begin ---- Properties loaded: 2/2 (Time: 0.7ms, Memory: 36.0KB) ---- Properties end ---- Base materials loaded: 196/196 Materials loaded: 88/88 Load Materials (Time: 145.4ms, Memory: 3.6MB) Preload materials loaded: 81 (Time: 8.5ms, Memory: 768.1KB) Shaders compiled: 54 (Time: 71.9ms, Memory: 797.4KB) Total materials loaded: 365 (Time: 225.9ms, Memory: 5.1MB) ---- Materials end ---- ``` |
| 31. | [Animations](../../../api/library/animations/class.animations_cpp.md) are loaded. |
| 32. | [Loading screen](../../../code/gui/screens/index.md#loading) is set. |
| 33. | The main application window is initialized and properly configured. |
| 34. | The Engine initialization statistics are written to the logs: ```text Engine initialization (Time: 4.4s, Memory: 587.1MB) ``` |
| 35. | Plugins are loaded from the *[plugin_path](../../../code/command_line.md#plugin_path)* (the `/bin/plugins` folder of your project's folder by default) The *[init()](../../../api/library/common/class.plugin_cpp.md#init_int)* method of all plugins is called after loading. The corresponding message is written to the log: ```text ---- Plugins ---- EnginePlugins: "UnigineFbxImporter" plugin is initialized EnginePlugins: "UnigineGLTFImporter" plugin is initialized EnginePlugins: "UnigineFbxExporter" plugin is initialized EnginePlugins: "UnigineUsdExchanger" plugin is initialized Plugins initialization (Time: 318.0ms, Memory: 9.0KB) ``` |
| First Frame |  |
| 1. | [Interpreter](../../../api/library/common/class.interpreter_cpp.md) is initialized. |
| 2. | Console commands provided as command-line arguments are executed. |
| 3. | The [System Script](../../../code/fundamentals/execution_sequence/app_logic_system.md#usc_system_logic) is loaded. |
| 4. | [System Logics](../../../code/fundamentals/execution_sequence/app_logic_system.md#systemlogic_init) are initialized. - The System script *[init()](../../../code/fundamentals/execution_sequence/app_logic_system.md#systemlogic_init)* method is called. - The SystemLogic *[init()](../../../code/fundamentals/execution_sequence/app_logic_system.md#systemlogic_init)* method is called. |
| 5. | The console command queue is flushed to ensure all pending commands are processed. |
