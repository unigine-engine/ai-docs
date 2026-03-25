# Unigine.GlobalConfig Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


This class is used to manage global configuration - various personal settings, such as helpers (wireframe, profiler, etc.). By default, these settings are stored in the `configs/default.global` [configuration file](../../../code/configuration_file_usc.md), but you can change file location if necessary.


### See Also


- Article on [Configuration Files](../../../code/configuration_file_usc.md).


## GlobalConfig Class

### Members

---

## void engine.global_config. setPath ( string path )

***Console*:**`global_config`Sets a new path to the global configuration file (default: `configs/default.global`). The path can be specified as an absolute path or relative to the *[*-data_path*](../../../code/command_line.md#data_path)* or *<project_name>* folder if the *[*-project_name*](../../../code/command_line.md#project_name)* is set. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *string* **path** - New path to the global configuration file to be set.

## string engine.global_config. getPath ( )

***Console*:**`global_config`Returns the current path to the global configuration file (default: `configs/default.global`). This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

Current path to the global configuration file.
## void engine.global_config. setAutosave ( int autosave )

***Console*:**`global_config_autosave`Sets a value indicating if current global configuration settings are automatically saved to the corresponding global config file (`configs/default.global` by default) on loading, closing, and saving the world, as well as on the Engine shutdown.
### Arguments

- *int* **autosave** - **1** to enable automatic saving of current global configuration settings; **0** — to disable it.

## int engine.global_config. isAutosave ( )

***Console*:**`global_config_autosave`Returns a value indicating if current global configuration settings are automatically saved to the corresponding global config file (`configs/default.global` by default) on loading, closing, and saving the world, as well as on the Engine shutdown.
### Return value

**1** if automatic saving of current global configuration settings is enabled; otherwise, 0.
## int engine.global_config. load ( )

***Console*:**`global_config_load`Loads global configuration from the file. To change the path to the configuration file use the [*setPath()*](#setPath_cstr_void) method.
### Return value

**1** if the global configuration is successfully loaded from the file; otherwise, **0**.
## int engine.global_config. save ( )

***Console*:**`global_config_save`Saves the current global configuration to the file. To change the path to the configuration file use the [*setPath()*](#setPath_cstr_void) method.
### Return value

**1** if the current global configuration is successfully saved to the file; otherwise, **0**.
## void engine.global_config. reset ( )

Resets the settings in the global configuration file to the default.
