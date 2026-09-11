# Unigine.UserConfig Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


This class is used to manage user configuration - various personal settings, such as helpers (wireframe, profiler, etc.). By default, these settings are stored in the `configs/default.user` [configuration file](../../../code/configuration_file_usc.md), but you can change file location if necessary.


### See Also


- Article on [Configuration Files](../../../code/configuration_file_usc.md).


## UserConfig Class

### Members

## void setAutosave ( int autosave )

***Console*:**`user_config_autosave`Sets a new value indicating if current user configuration settings are automatically saved to the corresponding user config file (`configs/default.user` by default) on loading, closing, and saving the world, as well as on the Engine shutdown. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *int* **autosave** - The automatic saving of current user configuration settings The default value is **true**.

## int isAutosave () const

***Console*:**`user_config_autosave`Returns the current value indicating if current user configuration settings are automatically saved to the corresponding user config file (`configs/default.user` by default) on loading, closing, and saving the world, as well as on the Engine shutdown. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

Current automatic saving of current user configuration settings The default value is **true**.
## void setPath ( string path )

***Console*:**`user_config`Sets a new path to the user configuration file (default: `configs/default.user`).
The path can be specified as an absolute path or relative to the *[-data_path](../../../code/command_line.md#data_path)* or `<project_name>` folder if the *[-project_name](../../../code/command_line.md#project_name)* is set.

 This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *string* **path** - The path to the user configuration file (default: `configs/default.user`). `Path` to the user configuration file (`configs/default.user` by default)

## const char * getPath () const

***Console*:**`user_config`Returns the current path to the user configuration file (default: `configs/default.user`).
The path can be specified as an absolute path or relative to the *[-data_path](../../../code/command_line.md#data_path)* or `<project_name>` folder if the *[-project_name](../../../code/command_line.md#project_name)* is set.

 This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

Current path to the user configuration file (default: `configs/default.user`). `Path` to the user configuration file
 (`configs/default.user` by default)
---

## int engine.user_config. load ( )

***Console*:**`user_config_load`Loads user configuration from the file. To change the path to the configuration file use **[setPath()()](../../...md#setPath_cstr_void)**.
### Return value

**1** if the user configuration is successfully loaded from the file; otherwise, **0**.
## int engine.user_config. save ( )

***Console*:**`user_config_save`Saves the current user configuration to the file. To change the path to the configuration file use **[setPath()()](../../...md#setPath_cstr_void)**.
### Return value

**1** if the current user configuration is successfully saved to the file; otherwise, **0**.
## void engine.user_config. reset ( )

Resets the settings in the user configuration file to the default.
