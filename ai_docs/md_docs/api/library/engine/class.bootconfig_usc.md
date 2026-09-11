# Unigine.BootConfig Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


A singleton that controls the Engine [startup configuration](../../../code/configuration_file_usc.md#boot) and enables you to customize the [boot screen](../../../code/gui/screens/index.md#boot).


> **Notice:** Fonts, textures, or any other resources used in the boot screen **cannot be packed into an UNG archive**.


### See Also


- Article on [Configuration Files](../../../code/configuration_file_usc.md).


## BootConfig Class

### Members

## void setScreenEnabled ( bool enabled )

Sets a new value indicating if the boot screen is enabled.
### Arguments

- *bool* **enabled** - Set **true** to enable the boot screen; **false** - to disable it.

## bool isScreenEnabled () const

Returns the current value indicating if the boot screen is enabled.
### Return value

**true** if the boot screen is enabled ; otherwise **false**.
## void setScreenMessageShadersCompilation ( string compilation )

Sets a new message displayed on shaders compilation. The message is set the same way as the [screen text](#setScreenText_cstr_void).
### Arguments

- *string* **compilation** - The message for shaders compilation.

## const char * getScreenMessageShadersCompilation () const

Returns the current message displayed on shaders compilation. The message is set the same way as the [screen text](#setScreenText_cstr_void).
### Return value

Current message for shaders compilation.
## void setScreenMessageEngineInit ( string init )

Sets a new message to be displayed on the engine initialization. The message is set the same way as the [screen text](#setScreenText_cstr_void).
### Arguments

- *string* **init** - The Message for the engine initialization.

## const char * getScreenMessageEngineInit () const

Returns the current message to be displayed on the engine initialization. The message is set the same way as the [screen text](#setScreenText_cstr_void).
### Return value

Current Message for the engine initialization.
## void setScreenMessageFileSystemInit ( string init )

Sets a new message to be displayed on the file system initialization. The message is set the same way as the [screen text](#setScreenText_cstr_void).
### Arguments

- *string* **init** - The Message for the file system initialization.

## const char * getScreenMessageFileSystemInit () const

Returns the current message to be displayed on the file system initialization. The message is set the same way as the [screen text](#setScreenText_cstr_void).
### Return value

Current Message for the file system initialization.
## void setScreenMessagePropertiesInit ( string init )

Sets a new message displayed on properties initialization.The message is set the same way as the [screen text](#setScreenText_cstr_void).
### Arguments

- *string* **init** - The message for properties initialization.

## const char * getScreenMessagePropertiesInit () const

Returns the current message displayed on properties initialization.The message is set the same way as the [screen text](#setScreenText_cstr_void).
### Return value

Current message for properties initialization.
## void setScreenMessageStaticMeshesInit ( )

Sets a new message to be displayed on static meshes initialization. The message is set the same way as the [screen text](#setScreenText_cstr_void).
### Arguments

- **init** - The Message for static meshes initialization.

## const char * getScreenMessageStaticMeshesInit () const

Returns the current message to be displayed on static meshes initialization. The message is set the same way as the [screen text](#setScreenText_cstr_void).
### Return value

Current Message for static meshes initialization.
## void setScreenMessageMaterialsInit ( string init )

Sets a new message to be displayed on materials initialization. The message is set the same way as the [screen text](#setScreenText_cstr_void).
### Arguments

- *string* **init** - The Message for materials initialization.

## const char * getScreenMessageMaterialsInit () const

Returns the current message to be displayed on materials initialization. The message is set the same way as the [screen text](#setScreenText_cstr_void).
### Return value

Current Message for materials initialization.
## void setScreenMessageMaterialsPreloading ( )

Sets a new message to be displayed on materials preloading.
### Arguments

- **preloading** - The Message for materials preloading.

## const char * getScreenMessageMaterialsPreloading () const

Returns the current message to be displayed on materials preloading.
### Return value

Current Message for materials preloading.
## void setScreenText ( string text )

Sets a new text of the boot screen.
### Arguments

- *string* **text** - The text of the boot screen. Can be either a plain or [rich text](../../../code/gui/ui/index.md#rich_text). A number of aliases is provided:

  - UNIGINE_COPYRIGHT � the UNIGINE copyright text.
  - UNIGINE_VERSION � the current UNIGINE version.
  - LOADING_PROGRESS � the loading progress going from 0 to 100.

## const char * getScreenText () const

Returns the current text of the boot screen.
### Return value

Current text of the boot screen. Can be either a plain or [rich text](../../../code/gui/ui/index.md#rich_text). A number of aliases is provided:
- UNIGINE_COPYRIGHT � the UNIGINE copyright text.
- UNIGINE_VERSION � the current UNIGINE version.
- LOADING_PROGRESS � the loading progress going from 0 to 100.


## void setScreenFont ( string font )

Sets a new path to the font for text rendering.
> **Notice:** Fonts or any other resources used in the Boot screen **cannot be packed into an UNG archive**.


### Arguments

- *string* **font** - The path to the font for text rendering.

## const char * getScreenFont () const

Returns the current path to the font for text rendering.
> **Notice:** Fonts or any other resources used in the Boot screen **cannot be packed into an UNG archive**.


### Return value

Current path to the font for text rendering.
## void setScreenTexture ( string texture )

Sets a new path to the boot screen texture.
> **Notice:** Textures or any other resources used in the Boot screen **cannot be packed into an UNG archive**.


### Arguments

- *string* **texture** - The path to the boot screen texture.

## const char * getScreenTexture () const

Returns the current path to the boot screen texture.
> **Notice:** Textures or any other resources used in the Boot screen **cannot be packed into an UNG archive**.


### Return value

Current path to the boot screen texture.
## void setScreenThreshold ( int threshold )

Sets a new threshold for blending based on the alpha-channel.
### Arguments

- *int* **threshold** - The threshold for blending based on the alpha-channel.

## int getScreenThreshold () const

Returns the current threshold for blending based on the alpha-channel.
### Return value

Current threshold for blending based on the alpha-channel.
## void setScreenTransform ( vec4 transform )

Sets a new transformation of the boot screen texture. The default value is vec4(1.0f, 1.0f, 0.5f, 0.5f).
### Arguments

- *vec4* **transform** - The transformation of the screen defined by a vector of four numbers in the [0; 1] range:

  1. Texture size multiplier
  2. Window size multiplier
  3. Horizontal position
  4. Vertical position

## vec4 getScreenTransform () const

Returns the current transformation of the boot screen texture. The default value is vec4(1.0f, 1.0f, 0.5f, 0.5f).
### Return value

Current transformation of the screen defined by a vector of four numbers in the [0; 1] range:
1. Texture size multiplier
2. Window size multiplier
3. Horizontal position
4. Vertical position


## void setScreenBackgroundColor ( vec4 color )

Sets a new background color of the screen.
### Arguments

- *vec4* **color** - The background color defined by a vector of four numbers in the [0; 1] range.

## vec4 getScreenBackgroundColor () const

Returns the current background color of the screen.
### Return value

Current background color defined by a vector of four numbers in the [0; 1] range.
## void setScreenHeight ( int height )

Sets a new height of the boot screen window, in pixels.
### Arguments

- *int* **height** - The height of the boot screen window, in pixels.

## int getScreenHeight () const

Returns the current height of the boot screen window, in pixels.
### Return value

Current height of the boot screen window, in pixels.
## void setScreenWidth ( int width )

Sets a new width of the boot screen window.
### Arguments

- *int* **width** - The width of the boot screen window, in pixels.

## int getScreenWidth () const

Returns the current width of the boot screen window.
### Return value

Current width of the boot screen window, in pixels.
## int getNumExternPlugins () const

Returns the current  number of plugin libraries to be automatically loaded at the Engine startup. These plugins are specified in the `.boot` configuration file via the [`extern_plugin`](../../../code/configuration_file_usc.md#boot) element. The list of these plugin paths can be obtained via the *getNumExternPlugins()* and [*getExternPlugin(int num)*](#getExternPlugin_int_cstr) methods. The order of loading plugins matters, you can rearrange them via [*swapPluginPath()*](#swapPluginPath_int_int_void).
### Return value

Current number of plugin libraries to be loaded at the Engine startup.
## int getNumPluginPaths () const

Returns the current  number of directory(ies) containing plugins to be automatically loaded at the Engine startup. These directories are specified in the `.boot` configuration file via the [`plugin_path`](../../../code/configuration_file_usc.md#boot) element. The list of these plugin paths can be obtained via the *getNumPluginPaths()* and [*getPluginPath(int num)*](../../../api/library/engine/class.engine_usc.md#getPluginPath_int_const_char_ptr) methods. The order of loading plugins matters, you can rearrange the paths via [*swapPluginPath()*](#swapPluginPath_int_int_void)
### Return value

Current number of plugin directories.
## void setConsoleCommand ( string command )

Sets a new  console command(s) used at the Engine startup (corresponds to the [`console_command`](../../../code/configuration_file_usc.md#boot) element of the `.boot` configuration file).
### Arguments

- *string* **command** - The console command(s) used at the Engine startup. Several commands can be separated using the && sequence.

## const char * getConsoleCommand () const

Returns the current  console command(s) used at the Engine startup (corresponds to the [`console_command`](../../../code/configuration_file_usc.md#boot) element of the `.boot` configuration file).
### Return value

Current console command(s) used at the Engine startup. Several commands can be separated using the && sequence.
## void setExternDefine ( string define )

Sets a new  extern define(s) used at the Engine startup (corresponds to the [`extern_define`](../../../code/configuration_file_usc.md#boot) element of the `.boot` configuration file).
### Arguments

- *string* **define** - The external definition(s) used at the Engine startup. Several definitions are comma separated (no whitespaces). Definitions can be specified as follows:

  - DEFINITION_NAME
  - DEFINITION_NAME=VALUE
  - DEFINITION_NAME_1,DEFINITION_NAME_2, DEFINITION_NAME_3=VALUE,...,DEFINITION_NAME_N

## const char * getExternDefine () const

Returns the current  extern define(s) used at the Engine startup (corresponds to the [`extern_define`](../../../code/configuration_file_usc.md#boot) element of the `.boot` configuration file).
### Return value

Current external definition(s) used at the Engine startup. Several definitions are comma separated (no whitespaces). Definitions can be specified as follows:
- DEFINITION_NAME
- DEFINITION_NAME=VALUE
- DEFINITION_NAME_1,DEFINITION_NAME_2, DEFINITION_NAME_3=VALUE,...,DEFINITION_NAME_N


## void setSoundApp ( string app )

Sets a new  sound API used (corresponds to the [`sound_app`](../../../code/configuration_file_usc.md#boot) element of the `.boot` configuration file).
### Arguments

- *string* **app** - The sound API used for rendering: *nosound, auto*, or *openal*.

## const char * getSoundApp () const

Returns the current  sound API used (corresponds to the [`sound_app`](../../../code/configuration_file_usc.md#boot) element of the `.boot` configuration file).
### Return value

Current sound API used for rendering: *nosound, auto*, or *openal*.
## void setVideoApp ( string app )

Sets a new  graphics API used for rendering (corresponds to the [`video_app`](../../../code/configuration_file_usc.md#boot) element of the `.boot` configuration file).
### Arguments

- *string* **app** - The graphics API used for rendering: *null, auto, dx, dx12, direct3d12, vk, vulkan*.

## const char * getVideoApp () const

Returns the current  graphics API used for rendering (corresponds to the [`video_app`](../../../code/configuration_file_usc.md#boot) element of the `.boot` configuration file).
### Return value

Current graphics API used for rendering: *null, auto, dx, dx12, direct3d12, vk, vulkan*.
## void setSystemCache ( string cache )

Sets a new  path to a cache file used by the Engine (corresponds to the [`system_cache`](../../../code/configuration_file_usc.md#boot) element of the `.boot` configuration file).
### Arguments

- *string* **cache** - The path to a cache file used by the Engine. Can be an absolute path or a path relative to the [`data path`](../../../api/library/engine/class.engine_usc.md#getDataPath_const_char_ptr), or to the [`cache path`](#setCachePath_cstr_void) (if any).

## const char * getSystemCache () const

Returns the current  path to a cache file used by the Engine (corresponds to the [`system_cache`](../../../code/configuration_file_usc.md#boot) element of the `.boot` configuration file).
### Return value

Current path to a cache file used by the Engine. Can be an absolute path or a path relative to the [`data path`](../../../api/library/engine/class.engine_usc.md#getDataPath_const_char_ptr), or to the [`cache path`](#setCachePath_cstr_void) (if any).
## void setEditorCache ( string cache )

Sets a new  path to a cache file used by the UnigineEditor (corresponds to the [`editor_cache`](../../../code/configuration_file_usc.md#boot) element of the `.boot` configuration file).
### Arguments

- *string* **cache** - The path to a cache file used by the UnigineEditor. Can be an absolute path or a path relative to the [`data path`](../../../api/library/engine/class.engine_usc.md#getDataPath_const_char_ptr), or to the [`cache path`](#setCachePath_cstr_void) (if any).

## const char * getEditorCache () const

Returns the current  path to a cache file used by the UnigineEditor (corresponds to the [`editor_cache`](../../../code/configuration_file_usc.md#boot) element of the `.boot` configuration file).
### Return value

Current path to a cache file used by the UnigineEditor. Can be an absolute path or a path relative to the [`data path`](../../../api/library/engine/class.engine_usc.md#getDataPath_const_char_ptr), or to the [`cache path`](#setCachePath_cstr_void) (if any).
## void setCachePath ( string path )

Sets a new  path to the store system and Editor cache files(corresponds to the [`cache_path`](../../../code/configuration_file_usc.md#boot) element of the `.boot` configuration file).
### Arguments

- *string* **path** - The path to the store system and Editor cache files. Can be an absolute path or a relative path to the [`data path`](../../../api/library/engine/class.engine_usc.md#getDataPath_const_char_ptr).

## const char * getCachePath () const

Returns the current  path to the store system and Editor cache files(corresponds to the [`cache_path`](../../../code/configuration_file_usc.md#boot) element of the `.boot` configuration file).
### Return value

Current path to the store system and Editor cache files. Can be an absolute path or a relative path to the [`data path`](../../../api/library/engine/class.engine_usc.md#getDataPath_const_char_ptr).
## void setEditorScript ( string script )

Sets a new  path to the [editor script](../../../code/fundamentals/execution_sequence/app_logic_system.md#editor_logic) (corresponds to the [`system_script`](../../../code/configuration_file_usc.md#boot) element of the `.boot` configuration file).
### Arguments

- *string* **script** - The path to the [editor script](../../../code/fundamentals/execution_sequence/app_logic_system.md#editor_logic) (specified relative to the `data` folder).

## const char * getEditorScript () const

Returns the current  path to the [editor script](../../../code/fundamentals/execution_sequence/app_logic_system.md#editor_logic) (corresponds to the [`system_script`](../../../code/configuration_file_usc.md#boot) element of the `.boot` configuration file).
### Return value

Current path to the [editor script](../../../code/fundamentals/execution_sequence/app_logic_system.md#editor_logic) (specified relative to the `data` folder).
## void setSystemScript ( string script )

Sets a new  path to the [system script](../../../code/fundamentals/execution_sequence/app_logic_system.md#system_logic) (corresponds to the [`system_script`](../../../code/configuration_file_usc.md#boot) element of the `.boot` configuration file).
### Arguments

- *string* **script** - The path to the [system script](../../../code/fundamentals/execution_sequence/app_logic_system.md#system_logic) (specified relative to the `data` folder).

## const char * getSystemScript () const

Returns the current  path to the [system script](../../../code/fundamentals/execution_sequence/app_logic_system.md#system_logic) (corresponds to the [`system_script`](../../../code/configuration_file_usc.md#boot) element of the `.boot` configuration file).
### Return value

Current path to the [system script](../../../code/fundamentals/execution_sequence/app_logic_system.md#system_logic) (specified relative to the `data` folder).
## void setEngineLog ( string log )

Sets a new  log file (in TXT format) used by the Engine. The path can be absolute or relative to the binary executable. For relative paths, if the **Project Name** startup parameter is set, the log file with the specified name will be created in the corresponding directory in the User profile (only the name will be used, the remaining part of the relative path will be discarded).
### Arguments

- *string* **log** - The log file (in TXT format) used by the Engine.

## const char * getEngineLog () const

Returns the current  log file (in TXT format) used by the Engine. The path can be absolute or relative to the binary executable. For relative paths, if the **Project Name** startup parameter is set, the log file with the specified name will be created in the corresponding directory in the User profile (only the name will be used, the remaining part of the relative path will be discarded).
### Return value

Current log file (in TXT format) used by the Engine.
## void setGuiPath ( string path )

Sets a new path to a GUI skin used for the engine interface. The path can be specified as absolute or relatively to the `data` folder.
### Arguments

- *string* **path** - The path to a GUI skin used for the Engine interface (absolute path or path relative to the `data` folder).

## const char * getGuiPath () const

Returns the current path to a GUI skin used for the engine interface. The path can be specified as absolute or relatively to the `data` folder.
### Return value

Current path to a GUI skin used for the Engine interface (absolute path or path relative to the `data` folder).
## void setAutosave ( int autosave )

Sets a new value indicating if the startup configuration settings are automatically saved to the corresponding config file on loading, closing, and saving the world, as well as on the Engine shutdown.
### Arguments

- *int* **autosave** - The automatic saving of current startup configuration settings

## int isAutosave () const

Returns the current value indicating if the startup configuration settings are automatically saved to the corresponding config file on loading, closing, and saving the world, as well as on the Engine shutdown.
### Return value

Current automatic saving of current startup configuration settings
## void setPath ( string path )

Sets a new path to the startup configuration file (default: `configs/default.boot`). The path can be specified as an absolute path or relative to the *[-data_path](../../../code/command_line.md#data_path)* or *<project_name>* folder if the *[-project_name](../../../code/command_line.md#project_name)* is set. To run the application with another boot configuration file, specify the path to it using the [`-boot_config`](../../../code/command_line.md#boot_config) command-line option.
### Arguments

- *string* **path** - The path to the startup configuration file.

## const char * getPath () const

Returns the current path to the startup configuration file (default: `configs/default.boot`). The path can be specified as an absolute path or relative to the *[-data_path](../../../code/command_line.md#data_path)* or *<project_name>* folder if the *[-project_name](../../../code/command_line.md#project_name)* is set. To run the application with another boot configuration file, specify the path to it using the [`-boot_config`](../../../code/command_line.md#boot_config) command-line option.
### Return value

Current path to the startup configuration file.
## void setWindowTitle ( string title )

Sets a new title of the application window.
### Arguments

- *string* **title** - The application window title.

## const char * getWindowTitle () const

Returns the current title of the application window.
### Return value

Current application window title.
## void setWindowIconPath ( string path )

Sets a new path to the custom icon for the final application's window.
### Arguments

- *string* **path** - The path to the custom icon for the final application's window.

## const char * getWindowIconPath () const

Returns the current path to the custom icon for the final application's window.
### Return value

Current path to the custom icon for the final application's window.
## void setVideoQuadroSync ( bool sync )

***Console*:**`video_quadro_sync`Sets a new value indicating whether NVIDIA Quadro Sync feature is enabled, providing support for synchronization of frame rendering across multiple displays. Enabling this option automatically sets the view to fullscreen, enables [VSYNC](../../../api/library/rendering/class.render_usc.md#VSync) and sets the [MaxFPS](../../../api/library/rendering/class.render_usc.md#MaxFPS) value to 0.
### Arguments

- *bool* **sync** - Set **true** to enable NVIDIA Quadro Sync feature; **false** - to disable it. The default value is **false**.

## bool isVideoQuadroSync () const

***Console*:**`video_quadro_sync`Returns the current value indicating whether NVIDIA Quadro Sync feature is enabled, providing support for synchronization of frame rendering across multiple displays. Enabling this option automatically sets the view to fullscreen, enables [VSYNC](../../../api/library/rendering/class.render_usc.md#VSync) and sets the [MaxFPS](../../../api/library/rendering/class.render_usc.md#MaxFPS) value to 0.
### Return value

**true** if NVIDIA Quadro Sync feature is enabled ; otherwise **false**. The default value is **false**.
## void setVideoOffscreen ( bool offscreen )

***Console*:**`video_offscreen`Sets a new value indicating if the offscreen mode is enabled for the application. Offscreen mode makes it possible to run UNIGINE Engine in a cloud and use powerful servers (e.g., to generate photorealistic datasets for deep learning and verification of AI algorithms).
> **Notice:** Available only during the Engine initialization (startup), has no effect at run time.


### Arguments

- *bool* **offscreen** - Set **true** to enable usage of the offscreen mode for the application; **false** - to disable it. The default value is **false**.

## bool isVideoOffscreen () const

***Console*:**`video_offscreen`Returns the current value indicating if the offscreen mode is enabled for the application. Offscreen mode makes it possible to run UNIGINE Engine in a cloud and use powerful servers (e.g., to generate photorealistic datasets for deep learning and verification of AI algorithms).
> **Notice:** Available only during the Engine initialization (startup), has no effect at run time.


### Return value

**true** if usage of the offscreen mode for the application is enabled ; otherwise **false**. The default value is **false**.
## void setVideoAdapter ( int adapter )

***Console*:**`video_adapter`Sets a new hardware video adapter [ID](../../../api/library/engine/class.systeminfo_usc.md#getGPUID_int_int) to be used for rendering.
> **Notice:** Available only during the Engine initialization (startup), has no effect at run time.


### Arguments

- *int* **adapter** - The hardware video adapter [ID](../../../api/library/engine/class.systeminfo_usc.md#getGPUID_int_int), value from 0 to [the number of available video adapters](../../../api/library/engine/class.systeminfo_usc.md#getGPUCount_int). Range of values: **[0, 32]**. The default value is : **0**.

## int getVideoAdapter () const

***Console*:**`video_adapter`Returns the current hardware video adapter [ID](../../../api/library/engine/class.systeminfo_usc.md#getGPUID_int_int) to be used for rendering.
> **Notice:** Available only during the Engine initialization (startup), has no effect at run time.


### Return value

Current hardware video adapter [ID](../../../api/library/engine/class.systeminfo_usc.md#getGPUID_int_int), value from 0 to [the number of available video adapters](../../../api/library/engine/class.systeminfo_usc.md#getGPUCount_int).
Range of values: **[0, 32]**. The default value is : **0**.
## void setVideoDebugShader ( bool shader )

***Console*:**`video_debug_shaders`Sets a new the value indicating if the debug shader shall be used for the application regardless of its binary type (debug or release). This option should be enabled in case you use graphics debugging tools (e.g., the [RenderDoc](https://renderdoc.org/) debugger).
### Arguments

- *bool* **shader** - Set **true** to enable debug shader for the application; **false** - to disable it.

## bool isVideoDebugShader () const

***Console*:**`video_debug_shaders`Returns the current the value indicating if the debug shader shall be used for the application regardless of its binary type (debug or release). This option should be enabled in case you use graphics debugging tools (e.g., the [RenderDoc](https://renderdoc.org/) debugger).
### Return value

**true** if debug shader for the application is enabled ; otherwise **false**.
## void setVideoDebug ( int debug )

***Console*:**`video_debug`Sets a new video debug mode for graphical API.
> **Notice:** Beware of severe slowdown when enabled. Available only during the Engine initialization (startup), has no effect at run time.


### Arguments

- *int* **debug** - The video debug mode for graphical API. One of the following values:

  - **0** - release rendering context (no debug) (by default)
  - **1** - debug rendering context
  - **2** - debug rendering context with break on error (only on debug binaries)
  - **3** - GPU side validation (dx12-only, only on debug binaries)

## int getVideoDebug () const

***Console*:**`video_debug`Returns the current video debug mode for graphical API.
> **Notice:** Beware of severe slowdown when enabled. Available only during the Engine initialization (startup), has no effect at run time.


### Return value

Current video debug mode for graphical API. One of the following values:
- **0** - release rendering context (no debug) (by default)
- **1** - debug rendering context
- **2** - debug rendering context with break on error (only on debug binaries)
- **3** - GPU side validation (dx12-only, only on debug binaries)

## int getNumFallbackFonts () const

Returns the current number of per-font fallback entries in the boot configuration (fonts for which an individual list of fallback fonts is defined). Fallback fonts are used by the GUI when the primary font lacks a glyph.
### Return value

Current number of per-font fallback entries
## int getNumGlobalFontFallbacks () const

Returns the current number of global fallback fonts in the boot configuration. Global fallbacks apply to every font and are checked after the font's own fallback list.
### Return value

Current number of global fallback fonts
---

## int engine.boot_config. load ( )

***Console*:**`boot_config_load`Loads Engine startup configuration from the file. To change the path to the configuration file use the [*setPath()*](#setPath_cstr_void) method.
### Return value

**1** if the config is successfully loaded from the file; otherwise, **0**.
## int engine.boot_config. save ( )

***Console*:**`boot_config_save`Saves the current Engine startup configuration to the file. To change the path to the configuration file use the [*setPath()*](#setPath_cstr_void) method.
### Return value

**1** if the current configuration is successfully saved to the file; otherwise, **0**.
## void engine.boot_config. reset ( )

Resets the settings in the Engine startup configuration file to the default.
## void engine.boot_config. removePluginPath ( int num )

 Removes a plugin path with the specified number from the list of the plugin paths specified in the `.boot` configuration file via the [`plugin_path`](../../../code/configuration_file_usc.md#boot) element.A plugin path is a directory containing plugins to be automatically loaded at the Engine startup.
### Arguments

- *int* **num** - Number of the plugin path to be removed from the list of the specified plugin paths, in the range from 0 to the [total number of plugin paths specified](#getNumPluginPaths_int).

## void engine.boot_config. swapPluginPath ( int num0 , int num1 )

 Swaps two plugin paths with the given numbers specified in the `.boot` configuration file.A plugin path is a directory containing plugins to be automatically loaded at the Engine startup. The list of these plugin paths can be obtained via the [*getNumPluginPaths()*](../../../api/library/engine/class.engine_usc.md#getNumPluginPaths_int) and [*getPluginPath(int num)*](../../../api/library/engine/class.engine_usc.md#getPluginPath_int_const_char_ptr) methods. The order of loading plugins matters, you can rearrange the paths via [*swapPluginPath()*](#swapPluginPath_int_int_void)
### Arguments

- *int* **num0** - Number of the first plugin path in the list of the specified plugin paths to be swapped, in the range from 0 to the [total number of plugin paths specified](#getNumPluginPaths_int).
- *int* **num1** - Number of the second plugin path in the list of the specified plugin paths to be swapped, in the range from 0 to the [total number of plugin paths specified](#getNumPluginPaths_int).

## string engine.boot_config. getPluginPath ( int num )

 Returns a plugin path with the given number specified in the `.boot` configuration file via the [`plugin_path`](../../../code/configuration_file_usc.md#boot) element.A plugin path is a directory containing plugins to be automatically loaded at the Engine startup. The order of loading plugins matters, you can rearrange the paths via [*swapPluginPath()*](#swapPluginPath_int_int_void).
### Arguments

- *int* **num** - Plugin path number in the list of the specified plugin paths, in the range from 0 to the [total number of plugin paths specified](#getNumPluginPaths_int).

### Return value

Path to the plugins directory with the given number in the list of the plugin paths. Сan be absolute or specified relatively to the binary executable.
## void engine.boot_config. setPluginPath ( int num , string value )

 Sets a new path for the item of the list of the plugin paths with the given number specified in the `.boot` configuration file via the [`plugin_path`](../../../code/configuration_file_usc.md#boot) element.A plugin path is a directory containing plugins to be automatically loaded at the Engine startup. The order of loading plugins matters, you can rearrange the paths via [*swapPluginPath()*](#swapPluginPath_int_int_void).
### Arguments

- *int* **num** - Plugin path number in the list of the specified plugin paths.
- *string* **value** - New path to be set for the specified item of the list of the plugin paths. Сan be specified relatively to the binary executable or as an absolute path.

## void engine.boot_config. removeExternPlugin ( int num )

 Removes a plugin with the specified number from the list of the plugins specified in the `.boot` configuration file via the [`extern_plugin`](../../../code/configuration_file_usc.md#boot) element.
### Arguments

- *int* **num** - Number of the plugin to be removed from the list of the specified plugins, in the range from 0 to the [total number of plugins specified](#getNumExternPlugins_int).

## void engine.boot_config. swapExternPlugin ( int num0 , int num1 )

 Swaps two plugins with the given numbers specified in the `.boot` configuration file.The list of these plugins can be obtained via the [*getNumExternPlugins()*](#getNumExternPlugins_int) and [*getExternPlugin(int num)*](#getExternPlugin_int_cstr) methods. The order of loading plugins matters, this method enables you to rearrange plugins to change loading order.
### Arguments

- *int* **num0** - Number of the first plugin in the list of the specified plugins to be swapped, in the range from 0 to the [total number of plugins specified](#getNumExternPlugins_int).
- *int* **num1** - Number of the second plugin in the list of the specified plugins to be swapped, in the range from 0 to the [total number of plugins specified](#getNumExternPlugins_int).

## string engine.boot_config. getExternPlugin ( int num )

 Returns the name of the plugin with the given number specified in the `.boot` configuration file via the [`extern_plugin`](../../../code/configuration_file_usc.md#boot) element.The order of loading plugins matters, you can rearrange the paths via [*swapExternPlugin()*](#swapExternPlugin_int_int_void).
### Arguments

- *int* **num** - Number of the plugin in the list of the specified plugins, in the range from 0 to the [total number of plugins specified](#getNumExternPlugins_int).

### Return value

Name of the plugin with the given number specified in the `.boot` configuration file. Plugin library name goes without any prefixes and postfixes (e.g., `libNetwork_x64d.so` is listed as "**Network**").
## void engine.boot_config. setExternPlugin ( int num , string value )

Sets a new name of the plugin with the given number specified in the `.boot` configuration file via the [`extern_plugin`](../../../code/configuration_file_usc.md#boot) element.The order of loading plugins matters, you can rearrange the paths via [*swapExternPlugin()*](#swapExternPlugin_int_int_void).
### Arguments

- *int* **num** - Number of the plugin to be set in the list of the specified plugins, in the range from 0 to the [total number of plugins specified](#getNumExternPlugins_int).
- *string* **value** - Name of the plugin with the given number specified in the `.boot` configuration file. Plugin library name goes without any prefixes and postfixes (e.g., `libNetwork_x64d.so` is listed as "**Network**").

## int engine.boot_config. addFallbackFont ( string font )

Appends a new per-font fallback entry for the specified font, with an initially empty fallback list (populate it via **[addFontFallback()()](../../...md#addFontFallback_int_cstr_void)**).
### Arguments

- *string* **font** - Path to the font file the new entry is created for.

### Return value

Index of the new entry.
## void engine.boot_config. addFontFallback ( int font , string fallback_font )

Appends a fallback font to the list of the per-font entry with the specified index.
### Arguments

- *int* **font** - Index of the per-font fallback entry.
- *string* **fallback_font** - Path to the fallback font file to append.

## void engine.boot_config. addGlobalFontFallback ( string fallback_font )

Appends a font to the global fallback list applied to every font.
### Arguments

- *string* **fallback_font** - Path to the fallback font file to append.

## string engine.boot_config. getFallbackFontName ( int num )

Returns the font path of the per-font fallback entry with the specified index.
### Arguments

- *int* **num** - Index of the per-font fallback entry, in the [0; **[getNumFallbackFonts()()](../../...md#getNumFallbackFonts_int)**) range.

### Return value

Path to the font file the entry is defined for.
## string engine.boot_config. getFontFallback ( int font , int fallback )

Returns the path of the fallback font with the specified index in the given per-font entry.
### Arguments

- *int* **font** - Index of the per-font fallback entry.
- *int* **fallback** - Index of the fallback font within the entry.

### Return value

Path to the fallback font file.
## string engine.boot_config. getGlobalFontFallback ( int num )

Returns the path of the global fallback font with the specified index.
### Arguments

- *int* **num** - Index of the global fallback font, in the [0; **[getNumGlobalFontFallbacks()()](../../...md#getNumGlobalFontFallbacks_int)**) range.

### Return value

Path to the global fallback font file.
## int engine.boot_config. getNumFontFallbacks ( int font )

Returns the number of fallback fonts registered for the per-font entry with the specified index.
### Arguments

- *int* **font** - Index of the per-font fallback entry.

### Return value

Number of fallback fonts in the entry.
## void engine.boot_config. removeFontFallback ( int font , int fallback )

Removes the fallback font with the specified index from the given per-font entry.
### Arguments

- *int* **font** - Index of the per-font fallback entry.
- *int* **fallback** - Index of the fallback font within the entry.

## void engine.boot_config. removeGlobalFontFallback ( int num )

Removes the global fallback font with the specified index.
### Arguments

- *int* **num** - Index of the global fallback font.

## void engine.boot_config. setFontFallback ( int font , int fallback , string fallback_font )

Replaces the fallback font with the specified index in the given per-font entry.
### Arguments

- *int* **font** - Index of the per-font fallback entry.
- *int* **fallback** - Index of the fallback font within the entry.
- *string* **fallback_font** - Path to the new fallback font file.

## void engine.boot_config. setGlobalFontFallback ( int num , string fallback_font )

Replaces the global fallback font with the specified index.
### Arguments

- *int* **num** - Index of the global fallback font.
- *string* **fallback_font** - Path to the new fallback font file.
