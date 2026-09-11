# Unigine.BootConfig Class (CS)

> **Notice:** This class is a singleton.


A singleton that controls the Engine [startup configuration](../../../code/configuration_file_cs.md#boot) and enables you to customize the [boot screen](../../../code/gui/screens/index.md#boot).


> **Notice:** Fonts, textures, or any other resources used in the boot screen **cannot be packed into an UNG archive**.


### Usage Example


By using the BootConfig class, you can customize the boot screen and change the startup settings and save them to the configuration file for the next engine start-up. For example:


<details>
<summary>AppSystemLogic.cs | Close</summary>

`AppSystemLogic.cs`


```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Reflection;
using System.Runtime.InteropServices;
using System.Text;
using Unigine;

namespace UnigineApp
{
	internal class AppSystemLogic : SystemLogic
	{

		public override bool Shutdown()
		{

			// set the window title
            BootConfig.WindowTitle = "Project Name";
            Unigine.Console.SetString("starting_world", "my_world");

            // customize the boot screen
            BootConfig.ScreenWidth = 960;
            BootConfig.ScreenHeight = 540;

            BootConfig.ScreenBackgroundColor = vec4.BLACK;
            BootConfig.ScreenTransform = new vec4(1.0f, 1.0f, 0.5f, 0.5f);

            BootConfig.ScreenThreshold = 16;
            BootConfig.ScreenTexture = "textures/boot_screen.png";

            BootConfig.ScreenText = @"
			<p align=""center"">
				<font color=""#ffffff"" size=""64"">
					<xy x=""%10"" y=""%50""/>Helicopter
				</font>
			</p>";

            BootConfig.ScreenMessageEngineInit = @"
			<p><font size=""24"" color=""#777777"">
				Engine initialization.
			</font></p>";

            BootConfig.ScreenMessageFileSystemInit = "Custom message for file system initialization.";
            BootConfig.ScreenMessageMaterialsInit = "Custom message for materials initialization.";
            BootConfig.ScreenMessagePropertiesInit = "Custom message for properties initialization.";
            BootConfig.ScreenMessageShadersCompilation = "Custom message for shaders compilation.";

            BootConfig.Save();

			return true;
		}


	}
}

```

</details>


### See Also


- Article on [Configuration Files](../../../code/configuration_file_cs.md).


## BootConfig Class

### Properties

## bool ScreenEnabled

The value indicating if the boot screen is enabled.
## string ScreenMessageShadersCompilation

The message displayed on shaders compilation. The message is set the same way as the [screen text](#setScreenText_cstr_void).
## string ScreenMessageEngineInit

The message to be displayed on the engine initialization. The message is set the same way as the [screen text](#setScreenText_cstr_void).
## string ScreenMessageFileSystemInit

The message to be displayed on the file system initialization. The message is set the same way as the [screen text](#setScreenText_cstr_void).
## string ScreenMessagePropertiesInit

The message displayed on properties initialization.The message is set the same way as the [screen text](#setScreenText_cstr_void).
## string ScreenMessageStaticMeshesInit

The message to be displayed on static meshes initialization. The message is set the same way as the [screen text](#setScreenText_cstr_void).
## string ScreenMessageMaterialsInit

The message to be displayed on materials initialization. The message is set the same way as the [screen text](#setScreenText_cstr_void).
## string ScreenMessageMaterialsPreloading

The message to be displayed on materials preloading.
## string ScreenText

The text of the boot screen.
## string ScreenFont

The path to the font for text rendering.
> **Notice:** Fonts or any other resources used in the Boot screen **cannot be packed into an UNG archive**.


## string ScreenTexture

The path to the boot screen texture.
> **Notice:** Textures or any other resources used in the Boot screen **cannot be packed into an UNG archive**.


## int ScreenThreshold

The threshold for blending based on the alpha-channel.
## vec4 ScreenTransform

The transformation of the boot screen texture. The default value is vec4(1.0f, 1.0f, 0.5f, 0.5f).
## vec4 ScreenBackgroundColor

The background color of the screen.
## int ScreenHeight

The height of the boot screen window, in pixels.
## int ScreenWidth

The width of the boot screen window.
## 🔒︎ int NumExternPlugins

The  number of plugin libraries to be automatically loaded at the Engine startup. These plugins are specified in the `.boot` configuration file via the [`extern_plugin`](../../../code/configuration_file_cs.md#boot) element. The list of these plugin paths can be obtained via the *getNumExternPlugins()* and [*getExternPlugin(int num)*](#getExternPlugin_int_cstr) methods. The order of loading plugins matters, you can rearrange them via [*swapPluginPath()*](#swapPluginPath_int_int_void).
## 🔒︎ int NumPluginPaths

The  number of directory(ies) containing plugins to be automatically loaded at the Engine startup. These directories are specified in the `.boot` configuration file via the [`plugin_path`](../../../code/configuration_file_cs.md#boot) element. The list of these plugin paths can be obtained via the *getNumPluginPaths()* and [*getPluginPath(int num)*](../../../api/library/engine/class.engine_cs.md#getPluginPath_int_const_char_ptr) methods. The order of loading plugins matters, you can rearrange the paths via [*swapPluginPath()*](#swapPluginPath_int_int_void)
## string ConsoleCommand

The  console command(s) used at the Engine startup (corresponds to the [`console_command`](../../../code/configuration_file_cs.md#boot) element of the `.boot` configuration file).
## string ExternDefine

The  extern define(s) used at the Engine startup (corresponds to the [`extern_define`](../../../code/configuration_file_cs.md#boot) element of the `.boot` configuration file).
## string SoundApp

The  sound API used (corresponds to the [`sound_app`](../../../code/configuration_file_cs.md#boot) element of the `.boot` configuration file).
## string VideoApp

The  graphics API used for rendering (corresponds to the [`video_app`](../../../code/configuration_file_cs.md#boot) element of the `.boot` configuration file).
## string SystemCache

The  path to a cache file used by the Engine (corresponds to the [`system_cache`](../../../code/configuration_file_cs.md#boot) element of the `.boot` configuration file).
## string EditorCache

The  path to a cache file used by the UnigineEditor (corresponds to the [`editor_cache`](../../../code/configuration_file_cs.md#boot) element of the `.boot` configuration file).
## string CachePath

The  path to the store system and Editor cache files(corresponds to the [`cache_path`](../../../code/configuration_file_cs.md#boot) element of the `.boot` configuration file).
## string EditorScript

The  path to the [editor script](../../../code/fundamentals/execution_sequence/app_logic_system.md#editor_logic) (corresponds to the [`system_script`](../../../code/configuration_file_cs.md#boot) element of the `.boot` configuration file).
## string SystemScript

The  path to the [system script](../../../code/fundamentals/execution_sequence/app_logic_system.md#system_logic) (corresponds to the [`system_script`](../../../code/configuration_file_cs.md#boot) element of the `.boot` configuration file).
## string EngineLog

The  log file (in TXT format) used by the Engine. The path can be absolute or relative to the binary executable. For relative paths, if the **Project Name** startup parameter is set, the log file with the specified name will be created in the corresponding directory in the User profile (only the name will be used, the remaining part of the relative path will be discarded).
## string GuiPath

The path to a GUI skin used for the engine interface. The path can be specified as absolute or relatively to the `data` folder.
## bool Autosave

The value indicating if the startup configuration settings are automatically saved to the corresponding config file on loading, closing, and saving the world, as well as on the Engine shutdown.
## string Path

The path to the startup configuration file (default: `configs/default.boot`). The path can be specified as an absolute path or relative to the *[-data_path](../../../code/command_line.md#data_path)* or *<project_name>* folder if the *[-project_name](../../../code/command_line.md#project_name)* is set. To run the application with another boot configuration file, specify the path to it using the [`-boot_config`](../../../code/command_line.md#boot_config) command-line option.
## string WindowTitle

The title of the application window.
## string WindowIconPath

The path to the custom icon for the final application's window.
## bool VideoQuadroSync

***Console*:**`video_quadro_sync`The value indicating whether NVIDIA Quadro Sync feature is enabled, providing support for synchronization of frame rendering across multiple displays. Enabling this option automatically sets the view to fullscreen, enables [VSYNC](../../../api/library/rendering/class.render_cs.md#VSync) and sets the [MaxFPS](../../../api/library/rendering/class.render_cs.md#MaxFPS) value to 0.
## bool VideoOffscreen

***Console*:**`video_offscreen`The value indicating if the offscreen mode is enabled for the application. Offscreen mode makes it possible to run UNIGINE Engine in a cloud and use powerful servers (e.g., to generate photorealistic datasets for deep learning and verification of AI algorithms).
> **Notice:** Available only during the Engine initialization (startup), has no effect at run time.


## int VideoAdapter

***Console*:**`video_adapter`The hardware video adapter [ID](../../../api/library/engine/class.systeminfo_cs.md#getGPUID_int_int) to be used for rendering.
> **Notice:** Available only during the Engine initialization (startup), has no effect at run time.


## bool VideoDebugShader

***Console*:**`video_debug_shaders`The the value indicating if the debug shader shall be used for the application regardless of its binary type (debug or release). This option should be enabled in case you use graphics debugging tools (e.g., the [RenderDoc](https://renderdoc.org/) debugger).
## int VideoDebug

***Console*:**`video_debug`The video debug mode for graphical API.
> **Notice:** Beware of severe slowdown when enabled. Available only during the Engine initialization (startup), has no effect at run time.


## 🔒︎ int NumFallbackFonts

The number of per-font fallback entries in the boot configuration (fonts for which an individual list of fallback fonts is defined). Fallback fonts are used by the GUI when the primary font lacks a glyph.
## 🔒︎ int NumGlobalFontFallbacks

The number of global fallback fonts in the boot configuration. Global fallbacks apply to every font and are checked after the font's own fallback list.
### Members

---

## bool Load ( )

***Console*:**`boot_config_load`Loads Engine startup configuration from the file. To change the path to the configuration file use the [*setPath()*](#setPath_cstr_void) method.
### Return value

**true** if the config is successfully loaded from the file; otherwise, **false**.
## bool Save ( )

***Console*:**`boot_config_save`Saves the current Engine startup configuration to the file. To change the path to the configuration file use the [*setPath()*](#setPath_cstr_void) method.
### Return value

**true** if the current configuration is successfully saved to the file; otherwise, **false**.
## void Reset ( )

Resets the settings in the Engine startup configuration file to the default.
## void RemovePluginPath ( int num )

 Removes a plugin path with the specified number from the list of the plugin paths specified in the `.boot` configuration file via the [`plugin_path`](../../../code/configuration_file_cs.md#boot) element.A plugin path is a directory containing plugins to be automatically loaded at the Engine startup.
### Arguments

- *int* **num** - Number of the plugin path to be removed from the list of the specified plugin paths, in the range from 0 to the [total number of plugin paths specified](#getNumPluginPaths_int).

## void SwapPluginPath ( int num0 , int num1 )

 Swaps two plugin paths with the given numbers specified in the `.boot` configuration file.A plugin path is a directory containing plugins to be automatically loaded at the Engine startup. The list of these plugin paths can be obtained via the [*getNumPluginPaths()*](../../../api/library/engine/class.engine_cs.md#getNumPluginPaths_int) and [*getPluginPath(int num)*](../../../api/library/engine/class.engine_cs.md#getPluginPath_int_const_char_ptr) methods. The order of loading plugins matters, you can rearrange the paths via [*swapPluginPath()*](#swapPluginPath_int_int_void)
### Arguments

- *int* **num0** - Number of the first plugin path in the list of the specified plugin paths to be swapped, in the range from 0 to the [total number of plugin paths specified](#getNumPluginPaths_int).
- *int* **num1** - Number of the second plugin path in the list of the specified plugin paths to be swapped, in the range from 0 to the [total number of plugin paths specified](#getNumPluginPaths_int).

## string GetPluginPath ( int num )

 Returns a plugin path with the given number specified in the `.boot` configuration file via the [`plugin_path`](../../../code/configuration_file_cs.md#boot) element.A plugin path is a directory containing plugins to be automatically loaded at the Engine startup. The order of loading plugins matters, you can rearrange the paths via [*swapPluginPath()*](#swapPluginPath_int_int_void).
### Arguments

- *int* **num** - Plugin path number in the list of the specified plugin paths, in the range from 0 to the [total number of plugin paths specified](#getNumPluginPaths_int).

### Return value

Path to the plugins directory with the given number in the list of the plugin paths. Сan be absolute or specified relatively to the binary executable.
## void SetPluginPath ( int num , string value )

 Sets a new path for the item of the list of the plugin paths with the given number specified in the `.boot` configuration file via the [`plugin_path`](../../../code/configuration_file_cs.md#boot) element.A plugin path is a directory containing plugins to be automatically loaded at the Engine startup. The order of loading plugins matters, you can rearrange the paths via [*swapPluginPath()*](#swapPluginPath_int_int_void).
### Arguments

- *int* **num** - Plugin path number in the list of the specified plugin paths.
- *string* **value** - New path to be set for the specified item of the list of the plugin paths. Сan be specified relatively to the binary executable or as an absolute path.

## void RemoveExternPlugin ( int num )

 Removes a plugin with the specified number from the list of the plugins specified in the `.boot` configuration file via the [`extern_plugin`](../../../code/configuration_file_cs.md#boot) element.
### Arguments

- *int* **num** - Number of the plugin to be removed from the list of the specified plugins, in the range from 0 to the [total number of plugins specified](#getNumExternPlugins_int).

## void SwapExternPlugin ( int num0 , int num1 )

 Swaps two plugins with the given numbers specified in the `.boot` configuration file.The list of these plugins can be obtained via the [*getNumExternPlugins()*](#getNumExternPlugins_int) and [*getExternPlugin(int num)*](#getExternPlugin_int_cstr) methods. The order of loading plugins matters, this method enables you to rearrange plugins to change loading order.
### Arguments

- *int* **num0** - Number of the first plugin in the list of the specified plugins to be swapped, in the range from 0 to the [total number of plugins specified](#getNumExternPlugins_int).
- *int* **num1** - Number of the second plugin in the list of the specified plugins to be swapped, in the range from 0 to the [total number of plugins specified](#getNumExternPlugins_int).

## string GetExternPlugin ( int num )

 Returns the name of the plugin with the given number specified in the `.boot` configuration file via the [`extern_plugin`](../../../code/configuration_file_cs.md#boot) element.The order of loading plugins matters, you can rearrange the paths via [*swapExternPlugin()*](#swapExternPlugin_int_int_void).
### Arguments

- *int* **num** - Number of the plugin in the list of the specified plugins, in the range from 0 to the [total number of plugins specified](#getNumExternPlugins_int).

### Return value

Name of the plugin with the given number specified in the `.boot` configuration file. Plugin library name goes without any prefixes and postfixes (e.g., `libNetwork_x64d.so` is listed as "**Network**").
## void SetExternPlugin ( int num , string value )

Sets a new name of the plugin with the given number specified in the `.boot` configuration file via the [`extern_plugin`](../../../code/configuration_file_cs.md#boot) element.The order of loading plugins matters, you can rearrange the paths via [*swapExternPlugin()*](#swapExternPlugin_int_int_void).
### Arguments

- *int* **num** - Number of the plugin to be set in the list of the specified plugins, in the range from 0 to the [total number of plugins specified](#getNumExternPlugins_int).
- *string* **value** - Name of the plugin with the given number specified in the `.boot` configuration file. Plugin library name goes without any prefixes and postfixes (e.g., `libNetwork_x64d.so` is listed as "**Network**").

## int AddFallbackFont ( string font )

Appends a new per-font fallback entry for the specified font, with an initially empty fallback list (populate it via **[AddFontFallback()](../../...md#addFontFallback_int_cstr_void)**).
### Arguments

- *string* **font** - Path to the font file the new entry is created for.

### Return value

Index of the new entry.
## void AddFontFallback ( int font , string fallback_font )

Appends a fallback font to the list of the per-font entry with the specified index.
### Arguments

- *int* **font** - Index of the per-font fallback entry.
- *string* **fallback_font** - Path to the fallback font file to append.

## void AddGlobalFontFallback ( string fallback_font )

Appends a font to the global fallback list applied to every font.
### Arguments

- *string* **fallback_font** - Path to the fallback font file to append.

## string GetFallbackFontName ( int num )

Returns the font path of the per-font fallback entry with the specified index.
### Arguments

- *int* **num** - Index of the per-font fallback entry, in the [0; **[NumFallbackFonts](../../...md#getNumFallbackFonts_int)**) range.

### Return value

Path to the font file the entry is defined for.
## string GetFontFallback ( int font , int fallback )

Returns the path of the fallback font with the specified index in the given per-font entry.
### Arguments

- *int* **font** - Index of the per-font fallback entry.
- *int* **fallback** - Index of the fallback font within the entry.

### Return value

Path to the fallback font file.
## string GetGlobalFontFallback ( int num )

Returns the path of the global fallback font with the specified index.
### Arguments

- *int* **num** - Index of the global fallback font, in the [0; **[NumGlobalFontFallbacks](../../...md#getNumGlobalFontFallbacks_int)**) range.

### Return value

Path to the global fallback font file.
## int GetNumFontFallbacks ( int font )

Returns the number of fallback fonts registered for the per-font entry with the specified index.
### Arguments

- *int* **font** - Index of the per-font fallback entry.

### Return value

Number of fallback fonts in the entry.
## void RemoveFontFallback ( int font , int fallback )

Removes the fallback font with the specified index from the given per-font entry.
### Arguments

- *int* **font** - Index of the per-font fallback entry.
- *int* **fallback** - Index of the fallback font within the entry.

## void RemoveGlobalFontFallback ( int num )

Removes the global fallback font with the specified index.
### Arguments

- *int* **num** - Index of the global fallback font.

## void SetFontFallback ( int font , int fallback , string fallback_font )

Replaces the fallback font with the specified index in the given per-font entry.
### Arguments

- *int* **font** - Index of the per-font fallback entry.
- *int* **fallback** - Index of the fallback font within the entry.
- *string* **fallback_font** - Path to the new fallback font file.

## void SetGlobalFontFallback ( int num , string fallback_font )

Replaces the global fallback font with the specified index.
### Arguments

- *int* **num** - Index of the global fallback font.
- *string* **fallback_font** - Path to the new fallback font file.
