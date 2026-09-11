# Startup Command-Line Options


Startup command-line options can be specified on the UNIGINE executable file launching. These options control what rendering API to use, what resolution to set for Unigine window, where resources for initializing the engine are stored, etc. The options are either set in [UNIGINE SDK Browser](../sdk/projects/index_cpp.md#custom_run) or manually via the command line.


> **Notice:** If no command-line options is specified, the options with default values will be used when launching the application.


The syntax of command-line options is as follows: the full name of the binary executable (64-bit development or production version) is specified first and then the start-up options.


```bash
main_* -command argument
```


```bash
main_* -command "argument,argument"
```


```bash
main_* -console_command "command argument"
```


All paths are specified as absolute or relative to the binary executable or the `data` directory.


If the same command is specified multiple times, only the last command will be taken into account by the engine. For example, in the following case, only the *argument3* will be used by the Engine:


```bash
-command "argument1" -command "argument2" -command "argument3"
```


> **Notice:** - An exception is [file system command-line options](#file_system): they can accumulate all the specified values.
> - The CLI options specified on the application start-up always take precedence over the ones stored in the configuration files. Some of the CLI options can be changed through the [console](../code/console/index.md). Such options are automatically stored in the configuration files (this way, after the application is quit, they will be restored on the next start-up). All other CLI options don't change the configuration files.


## Video Settings


| -main_window_size | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
|---|---|
| **Description:** The size of the main application window. | **Arguments:** Usage with the argument: *main_window_size **width height*** (1600 x 900 by default) |
| -main_window_resizable | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** Enables the resizable mode for the main application window (its size can be changed on the fly without restarting the application). | **Arguments:** **0** - disabled **1** - enabled (by default) |
| -main_window_fullscreen | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** The fullscreen mode for the application window. Only one window is available, when the application runs in the fullscreen mode (no other windows or dialogs shall be displayed atop). | **Arguments:** **0** - windowed mode (by default) **1** - full-screen mode |


## Graphics Settings


| -video_app |  |
|---|---|
| **Description:** Graphics API to be used for rendering. The current value of *-video_app* can be obtained via the *[getVideoApp()](../api/library/engine/class.engine_cpp.md#getVideoApp_const_char_ptr)* method of Unigine API. | **Arguments:** - ***"null"*** - no renderer: do not render anything onto the screen (for example, for servers in case of playing over the network) - ***"auto"*** - automatically choose the best option from available ones - ***"direct3d12" / "dx12" / "dx"*** - DirectX12 - ***"vulkan" / "vk"*** - Vulkan |
| -auto_quit |  |
| **Description:** Enables force closing of the Engine when all windows are closed. Enable this option when 0 is passed to [-main_window](#main_window). | **Arguments:** **0** - disabled **1** - enabled (by default) |
| -video_adapter_uuid |  |
| **Description:** The hardware video adapter universal unique identifier (*UUID*) to be used for rendering. Unlike the adapter index (`-video_adapter`), the UUID is persistent across reboots and hardware configuration changes, making it more reliable for multi-GPU setups. If specified, takes priority over *-video_adapter*. ```text -video_adapter_uuid 69cfa97d-d00c-4e5a-9f78-9fa2f5825f98 ``` > **Notice:** The GPU UUID can be obtained from: > > > - Engine / Editor log output at application startup > - *nvidia-smi -L* in the terminal (ships with NVIDIA drivers) > - *vulkaninfo --summary* in the terminal (part of Vulkan SDK / *vulkan-tools*) |  |


| -video_adapter | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
|---|---|
| **Description:** The  the hardware video adapter [ID](../api/library/engine/class.systeminfo_cpp.md#getGPUID_int_int) to be used for rendering. The value must be from 0 to [the number of available video adapters](../api/library/engine/class.systeminfo_cpp.md#getGPUCount_int). To obtain a universal unique identifier (*UUID*), which is persistent across reboots and hardware configuration changes, use `-video_adapter_uuid`. | **Arguments:** **[0; 32]** - available range **0** - by default |
| -video_debug | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** The  video debug mode for graphical API. > **Warning:** Beware of severe slowdown when enabled. | **Arguments:** **0** - release rendering context (no debug) (by default) **1** - debug rendering context **2** - debug rendering context with break on error (only on debug binaries) **3** - GPU side validation (dx12-only, only on debug binaries) |
| -video_debug_shader | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** The status of debug shaders for the application regardless of its binary type (debug or release). This option should be enabled in case you use graphics debugging tools (e.g., the [RenderDoc](https://renderdoc.org/) debugger). | **Arguments:** **0** - disable debug shaders (release shaders are used) (by default) **1** - enable debug shaders |
| -video_offscreen | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** Enables the offscreen mode for the application, making it possible to run UNIGINE Engine in a cloud and use powerful servers (e.g., to generate photorealistic datasets for deep learning and verification of AI algorithms). | **Arguments:** **0** - disabled (by default) **1** - enabled |
| -main_window | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** Enables creating a main window during the application start-up. After starting up the application any window can be created and will work normally. For example, this can be useful in a custom editor or any other application, where there should be no main Engine window. | **Arguments:** **0** - disabled **1** - enabled (by default) |
| -dlss_application_id | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** The DLSS Application ID, provided by NVIDIA. > **Notice:** If no NVIDIA Application ID is available, the Engine uses its own generated project ID instead. | **Arguments:** **[INT_MIN; INT_MAX]** - available range **0** - by default |
| -fsr_max_contexts | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** The number of the FSR contexts. | **Arguments:** **[1; 1024]** - available range **8** - by default |


## File System


| -data_path |  |
|---|---|
| **Description:** Path to the [`data`](../principles/filesystem/index_cpp.md#data_dir) directory with all [resources](../principles/filesystem/index_cpp.md#paths). The path can be specified as an absolute path or relatively to the binary executable. The specified *-data_path* directory can be obtained via the *[getDataPath()](../api/library/engine/class.engine_cpp.md#getDataPath_const_char_ptr)* function. The argument can be passed as follows: - ../RELATIVE_PATH/ - ABSOLUTE_PATH | **Arguments:** **../** (by default) |
| -plugin_path |  |
| **Description:** Path to a directory that contains plugins dynamic libraries. All of the plugins in this directory will be loaded automatically on the start-up. The path can be specified relatively to the binary executable or as an absolute path. The list of the specified *-plugin_path* directories can be obtained via the *[getNumPluginPaths()](../api/library/engine/class.engine_cpp.md#getNumPluginPaths_int)* and *[getPluginPath(int num)](../api/library/engine/class.engine_cpp.md#getPluginPath_int_const_char_ptr)* methods. The argument can be passed as follows: - ../RELATIVE_PATH/ - ABSOLUTE_PATH | **Arguments:** **plugins/** (by default) |


> **Notice:** Unlike other command-line options, the `plugin_path` option can accumulate all specified values. It allows specifying multiple paths, each of which will be used by the Engine.


For several directories or packages you should specify each item separately without commas, for example:


```text
-plugin_path ../RELATIVE_PATH_1/ -plugin_path ../RELATIVE_PATH_2/ -plugin_path ABSOLUTE_PATH
```


## Other Data


| -boot_config |  |
|---|---|
| **Description:** Path to [Startup Configuration File](../code/configuration_file_cpp.md#boot) containing the engine start-up options. The path can be specified as an absolute path or relative to the *[-data_path](#data_path)* or *<project_name>* folder if the *[-project_name](#project_name)* is set. The argument can be passed as follows: - ../RELATIVE_PATH/ - ABSOLUTE_PATH | **Arguments:** **configs/default.boot** (by default) |
| -cache_path |  |
| **Description:** Path to store system and editor cache files (specified by *[system_cache](#system_cache)* and *[editor_cache](#editor_cache)* respectively). The path can be specified as an absolute path or relatively to the *[-data_path](#data_path)*. > **Notice:** For this parameter to take effect you should either delete existing [system](#system_cache) and [editor](#editor_cache) cache files or move them to the new specified location. | **Arguments:** **data/** (by default) |
| -editor_cache |  |
| **Description:** Path to a cache file to be used by the UnigineEditor. The path can be specified as an absolute path or relatively to the *[-data_path](#data_path)*, or to the *[-cache_path](#cache_path)* (if any). | **Arguments:** **editor.cache** (by default) |
| -system_cache |  |
| **Description:** Path to a cache file to be used by the Engine. The path can be specified as an absolute path or relatively to the *[-data_path](#data_path)*, or to the *[-cache_path](#cache_path)* (if any). | **Arguments:** **unigine.cache** (by default) |
| -engine_log |  |
| **Description:** Log file to be created and used. The path can be specified as an absolute path or relatively to the binary executable. For relative paths, if the *[-project_name](#project_name)* is set, the log file with the specified name will be created in the corresponding directory in the User profile (only the name will be used, the remaining part of the relative path will be discarded). | **Arguments:** **log.txt** (by default) |
| -gui_path |  |
| **Description:** Path to a GUI skin to be used for the engine interface. The path can be specified as an absolute path or relatively to the *[-data_path](#data_path)*. | **Arguments:** **core/gui/** (by default) |
| -project_name |  |
| **Description:** Forces the engine to store all changing data (a log file, cache files and configuration files) in the User profile rather than in a directory with binaries. For that, a directory will be created with a specified PROJECT_NAME or a path to the project directory relative to the User profile (for example, `unigine_projects/my_project`). | **Arguments:** PROJECT_NAME, namely: - Name of the project directory. For example, *-project_name my_project* will create the following directory: **Windows**: `C:/Users/<username>/my_project/` **Linux**: `/home/<username>/.my_project/` - Path to the project directory relative to the User profile. For example, *-project_name unigine_projects/my_project* will create `my_project` directory in the following directory: **Windows**: `C:/Users/<username>/unigine_projects/` **Linux**: `/home/<username>/.unigine_projects/` > **Notice:** The specified `unigine_projects` folder must exist in the User profile. |
| -system_script |  |
| **Description:** Path to the [system script](../code/fundamentals/execution_sequence/app_logic_system.md#scripts) (specified relative to the [data directory](#data_path)). | **Arguments:** **core/unigine.usc** (by default) |
| -skip_guidsdb |  |
| **Description:** The Engine ignores the `guids.db` file and searches for GUIDs among all `.meta` files inside the data folder and all mounted external directories and packages. > **Notice:** UnigineEditor uses this argument by default to avoid errors, and always re-generates the `guids.db` file to ensure its validity. |  |


| -mesh_procedural_path | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
|---|---|
| **Description:** - **Variable.** Prints a current path used to store temporary procedural mesh files. - **Command.** Specifies the directory for storing temporary procedural mesh files when *[PROCEDURAL_MODE_FILE](../api/library/objects/class.objectmeshstatic_cpp.md#PROCEDURAL_MODE)* is used. | **Arguments:** `Path` to the directory used for storing temporary procedural mesh files: Default values: - `default.boot`: *data/.unigine_mesh_procedural* - `editor.boot`: *[Cache Directory](../editor2/settings/hotkeys/index.md#cache_directory)/UNIGINE_Editor_Procedural_Mesh* |
| -mesh_procedural_read_only | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** Enables read-only mode for procedural file access. When set to 1, the engine does not write procedural mesh data to disk. Instead all generated meshes are stored and managed entirely in **RAM**, as if *[PROCEDURAL_MODE_BLOB](../api/library/objects/class.objectmeshstatic_cpp.md#PROCEDURAL_MODE)* was active. This helps avoid disk I/O, but procedural meshes will be lost on application exit. | **Arguments:** **0** - disabled (by default) **1** - enabled |


## Engine-Related Settings


| -console_command |  |
|---|---|
| **Description:** [Console command](../code/console/index.md) to be used at the engine start-up. Several commands can be separated using the **&&** sequence. | **Arguments:** command <arguments> |
| -console_history |  |
| **Description:** Sets the path to the file that stores the console command input history. The path to the file and its name should be specified. If the path to the file is not specified, the file will be searched in directories the following sequence: 1. Directory set by the parameter `-project_name` (if specified) 2. Directory where binary executable file is stored 3. Directory set by the parameter `-data_path` (if specified) If the file name is also not specified, the file with the default name `console_history` will be searched in the above-mentioned order. | **Arguments:** - **bin/console_history** (by default) - The argument should be specified as follows: <path_to_file/console_history_file_name> |
| -extern_plugin |  |
| **Description:** Load a [plugin library](../code/cpp/plugin.md) (the path is specified relative to the binary executable). - The library name should go without any prefixes and postfixes. (For example, `libNetwork_x64d.so` should be passed as `"Network"`.) - Several plugins are comma separated (no whitespace). - If you want to clear the list of plugins (they are automatically loaded by the engine once specified on the start-up), simply pass `""` as an argument to this command. | **Arguments:** The arguments can be specified as follows: - PLUGIN_NAME - PLUGIN_NAME_1,PLUGIN_NAME_2,...,PLUGIN_NAME_N |
| -extern_define |  |
| **Description:** External definition to be used. - Several definitions are comma separated (no whitespace). - You can also use the following syntax: `-extern_define "A=B,C=D"`. (For example, `-extern_define �"TEST=42"`.) - If you want to clear all definitions, simply pass `""` as an argument to this command. > **Notice:** Affects UnigineScript only. The current value of *-extern_define* can be obtained via the *[getExternDefine()](../api/library/engine/class.engine_cpp.md#getExternDefine_const_char_ptr)* method of Unigine API. | **Arguments:** The arguments can be specified as follows: - DEFINITION_NAME - DEFINITION_NAME=VALUE - DEFINITION_NAME_1,DEFINITION_NAME_2, DEFINITION_NAME_3=VALUE,...,DEFINITION_NAME_N |
| -async_init |  |
| **Description:** Enables the parallel initialization of meshes, properties, and materials on the engine start-up. If disabled, initialization of meshes, properties, and materials is done in sequence. | **Arguments:** **0** - disabled **1** - enabled (by default) |


| -memory_statistics_enabled | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
|---|---|
| **Description:** Enables gathering memory statistics during the application start-up. After starting up prints the value indicating whether gathering memory statistics is enabled or not. | **Arguments:** **0** - disabled **1** - enabled (by default) |
| -microprofile_enabled |  |
| **Description:** Enables Microprofile. | **Arguments:** **0** - disabled **1** - enabled (by default) |


## Multithreading Functionality


These boot-time options control how many worker threads the Engine creates for each [thread pool](../code/fundamentals/thread_system/index.md). They are applied once at startup and cannot be changed at runtime.


> **Notice:** Setting the thread count higher than the number of available CPU cores will not improve performance - it will increase context switching overhead and may degrade it.


| -num_cores_reserve |  |
|---|---|
| **Description:** The number of CPU cores to exclude from thread pool calculations. The remaining cores are shared among all pools. By default (-1), the Engine reserves 1 core. | **Arguments:** **[-1; 256]** - available range **-1** - by default |
| -num_threads_sync |  |
| **Description:** The number of worker threads to create in the **Sync Pool**. By default (0), the Engine calculates the count automatically based on available CPU cores. Set a positive value to override. Capped by *[num_threads_limit_sync](#num_threads_limit_sync)*. | **Arguments:** **[0; 256]** - available range **0** - by default |
| -num_threads_async |  |
| **Description:** The number of worker threads to create in the **Async Pool**. By default (0), the Engine calculates the count automatically based on available CPU cores. Set a positive value to override. Capped by *[num_threads_limit_async](#num_threads_limit_async)*. | **Arguments:** **[0; 256]** - available range **0** - by default |
| -num_threads_critical |  |
| **Description:** The number of worker threads to create in the **Critical Pool**. By default (0), the Engine creates 1 thread. Set a positive value to override. Capped by *[num_threads_limit_critical](#num_threads_limit_critical)*. | **Arguments:** **[0; 256]** - available range **0** - by default |
| -num_threads_common |  |
| **Description:** The number of worker threads to create in the **Common Pool**. By default (0), the Engine creates 1 thread. Set a positive value to override. Capped by *[num_threads_limit_common](#num_threads_limit_common)*. | **Arguments:** **[0; 256]** - available range **0** - by default |
| -num_threads_background |  |
| **Description:** The number of worker threads to create in the **Background Pool**. By default (0), the Engine creates 1 thread. Set a positive value to override. Capped by *[num_threads_limit_background](#num_threads_limit_background)*. | **Arguments:** **[0; 256]** - available range **0** - by default |
| -num_threads_file_stream |  |
| **Description:** The number of worker threads to create in the **File Stream Pool**. By default (0), the Engine creates 1 thread. Set a positive value to override. Capped by *[num_threads_limit_file_stream](#num_threads_limit_file_stream)*. | **Arguments:** **[0; 256]** - available range **0** - by default |
| -num_threads_limit_sync |  |
| **Description:** The upper limit on the number of worker threads in the **Sync Pool**. The thread count, whether set via *[num_threads_sync](#num_threads_sync)* or calculated by the Engine, cannot exceed this value. | **Arguments:** **[1; 256]** - available range **256** - by default |
| -num_threads_limit_async |  |
| **Description:** The upper limit on the number of worker threads in the **Async Pool**. The thread count, whether set via *[num_threads_async](#num_threads_async)* or calculated by the Engine, cannot exceed this value. | **Arguments:** **[1; 256]** - available range **256** - by default |
| -num_threads_limit_critical |  |
| **Description:** The upper limit on the number of worker threads in the **Critical Pool**. The thread count, whether set via *[num_threads_critical](#num_threads_critical)* or calculated by the Engine, cannot exceed this value. | **Arguments:** **[1; 256]** - available range **256** - by default |
| -num_threads_limit_common |  |
| **Description:** The upper limit on the number of worker threads in the **Common Pool**. The thread count, whether set via *[num_threads_common](#num_threads_common)* or calculated by the Engine, cannot exceed this value. | **Arguments:** **[1; 256]** - available range **256** - by default |
| -num_threads_limit_background |  |
| **Description:** The upper limit on the number of worker threads in the **Background Pool**. The thread count, whether set via *[num_threads_background](#num_threads_background)* or calculated by the Engine, cannot exceed this value. | **Arguments:** **[1; 256]** - available range **256** - by default |
| -num_threads_limit_file_stream |  |
| **Description:** The upper limit on the number of worker threads in the **File Stream Pool**. The thread count, whether set via *[num_threads_file_stream](#num_threads_file_stream)* or calculated by the Engine, cannot exceed this value. | **Arguments:** **[1; 256]** - available range **256** - by default |


## Sound Settings


| -sound_app |  |
|---|---|
| **Description:** Sound API to be used. The current value of *-sound_app* can be obtained via the *[getSoundApp()](../api/library/engine/class.engine_cpp.md#getSoundApp_const_char_ptr)* method of Unigine API. | **Arguments:** - **null** - no sound - **auto** (by default) - automatically choose the best sound library option from available ones (OpenAL) - **openal** - OpenAL sound library |


## VR Settings


| -vr_app |  |
|---|---|
| **Description:** VR to be used. The current value of *-vr_app* can be obtained via the *[getApiName()](../api/library/vr/class.vr_cpp.md#getApiName_cstr)* method of UNIGINE API. | **Arguments:** - **null** (by default) - no VR - **auto** - automatically choose OpenVR - **openvr** - OpenVR - **openxr** - OpenXR - **varjo** - Varjo |
