# Unigine.GlobalConfig Class (CS)

> **Notice:** This class is a singleton.


This class is used to manage global configuration - global project settings, such as declarations of custom surface and material parameters and custom render parameters along with their values. By default, these settings are stored in the `configs/default.global` [configuration file](../../../code/configuration_file_cs.md#global), but you can change file location if necessary.


### See Also


- Article on [Configuration Files](../../../code/configuration_file_cs.md).


## GlobalConfig Class

### Properties

## bool Autosave

***Console*:**`global_config_autosave`The value indicating if current global configuration settings are automatically saved to the corresponding global config file (`configs/default.global` by default) on loading, closing, and saving the world, as well as on the Engine shutdown.
## string Path

***Console*:**`global_config`The path to the global configuration file (default: `configs/default.global`).
The path can be specified as an absolute path or relative to the *[-data_path](../../../code/command_line.md#data_path)* or `<project_name>` folder if the *[-project_name](../../../code/command_line.md#project_name)* is set.

### Members

---

## bool Load ( )

***Console*:**`global_config_load`Loads global configuration from the file. To change the path to the configuration file use **[Path](../../...md#setPath_cstr_void)**.
### Return value

true if the global configuration is successfully loaded from the file; otherwise, false.
## bool Save ( )

***Console*:**`global_config_save`Saves the current global configuration to the file. To change the path to the configuration file use **[Path](../../...md#setPath_cstr_void)**.
### Return value

true if the current global configuration is successfully saved to the file; otherwise, false.
## void Reset ( )

Resets the settings in the global configuration file to the default.
