# Unigine.GlobalConfig Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


This class is used to manage global configuration - global project settings, such as declarations of custom surface and material parameters and custom render parameters along with their values. By default, these settings are stored in the `configs/default.global` [configuration file](../../../code/configuration_file_usc.md#global), but you can change file location if necessary.


### See Also


- Article on [Configuration Files](../../../code/configuration_file_usc.md).


## GlobalConfig Class

### Members

## void setAutosave ( int autosave )

***Console*:**`global_config_autosave`Sets a new value indicating if current global configuration settings are automatically saved to the corresponding global config file (`configs/default.global` by default) on loading, closing, and saving the world, as well as on the Engine shutdown. This parameter is stored in the following configuration file: **[*.global](../../../code/configuration_file_cpp.md#global)**.
### Arguments

- *int* **autosave** - The automatic saving of current global configuration settings The default value is **false**.

## int isAutosave () const

***Console*:**`global_config_autosave`Returns the current value indicating if current global configuration settings are automatically saved to the corresponding global config file (`configs/default.global` by default) on loading, closing, and saving the world, as well as on the Engine shutdown. This parameter is stored in the following configuration file: **[*.global](../../../code/configuration_file_cpp.md#global)**.
### Return value

Current automatic saving of current global configuration settings The default value is **false**.
## void setPath ( string path )

***Console*:**`global_config`Sets a new path to the global configuration file (default: `configs/default.global`).
The path can be specified as an absolute path or relative to the *[-data_path](../../../code/command_line.md#data_path)* or `<project_name>` folder if the *[-project_name](../../../code/command_line.md#project_name)* is set.

### Arguments

- *string* **path** - The path to the global configuration file (default: `configs/default.global`). `Path` to the global configuration file (`configs/default.global` by default)

## const char * getPath () const

***Console*:**`global_config`Returns the current path to the global configuration file (default: `configs/default.global`).
The path can be specified as an absolute path or relative to the *[-data_path](../../../code/command_line.md#data_path)* or `<project_name>` folder if the *[-project_name](../../../code/command_line.md#project_name)* is set.

### Return value

Current path to the global configuration file (default: `configs/default.global`). `Path` to the global configuration file
 (`configs/default.global` by default)
---

## int engine.global_config. load ( )

***Console*:**`global_config_load`Loads global configuration from the file. To change the path to the configuration file use **[setPath()()](../../...md#setPath_cstr_void)**.
### Return value

**1** if the global configuration is successfully loaded from the file; otherwise, **0**.
## int engine.global_config. save ( )

***Console*:**`global_config_save`Saves the current global configuration to the file. To change the path to the configuration file use **[setPath()()](../../...md#setPath_cstr_void)**.
### Return value

**1** if the current global configuration is successfully saved to the file; otherwise, **0**.
## void engine.global_config. reset ( )

Resets the settings in the global configuration file to the default.
