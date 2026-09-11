# Unigine.UserConfig Class (CS)

> **Notice:** This class is a singleton.


This class is used to manage user configuration - various personal settings, such as helpers (wireframe, profiler, etc.). By default, these settings are stored in the `configs/default.user` [configuration file](../../../code/configuration_file_cs.md), but you can change file location if necessary.


### See Also


- Article on [Configuration Files](../../../code/configuration_file_cs.md).


## UserConfig Class

### Properties

## bool Autosave

***Console*:**`user_config_autosave`The value indicating if current user configuration settings are automatically saved to the corresponding user config file (`configs/default.user` by default) on loading, closing, and saving the world, as well as on the Engine shutdown.
## string Path

***Console*:**`user_config`The path to the user configuration file (default: `configs/default.user`).
The path can be specified as an absolute path or relative to the *[-data_path](../../../code/command_line.md#data_path)* or `<project_name>` folder if the *[-project_name](../../../code/command_line.md#project_name)* is set.


### Members

---

## bool Load ( )

***Console*:**`user_config_load`Loads user configuration from the file. To change the path to the configuration file use **[Path](../../...md#setPath_cstr_void)**.
### Return value

true if the user configuration is successfully loaded from the file; otherwise, false.
## bool Save ( )

***Console*:**`user_config_save`Saves the current user configuration to the file. To change the path to the configuration file use **[Path](../../...md#setPath_cstr_void)**.
### Return value

true if the current user configuration is successfully saved to the file; otherwise, false.
## void Reset ( )

Resets the settings in the user configuration file to the default.
