# Unigine.GlobalConfig Class (CPP)

**Header:** #include <UnigineConfig.h>

> **Notice:** This class is a singleton.


This class is used to manage global configuration - various personal settings, such as helpers (wireframe, profiler, etc.). By default, these settings are stored in the `configs/default.global` [configuration file](../../../code/configuration_file_cpp.md), but you can change file location if necessary.


### See Also


- Article on [Configuration Files](../../../code/configuration_file_cpp.md).


## GlobalConfig Class

### Members

---

## void setPath ( const char * path )

***Console*:**`global_config`Sets a new path to the global configuration file (default: `configs/default.global`). The path can be specified as an absolute path or relative to the *[*-data_path*](../../../code/command_line.md#data_path)* or *<project_name>* folder if the *[*-project_name*](../../../code/command_line.md#project_name)* is set. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *const char ** **path** - New path to the global configuration file to be set.

## const char * getPath ( ) const

***Console*:**`global_config`Returns the current path to the global configuration file (default: `configs/default.global`). This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

Current path to the global configuration file.
## void setAutosave ( bool autosave )

***Console*:**`global_config_autosave`Sets a value indicating if current global configuration settings are automatically saved to the corresponding global config file (`configs/default.global` by default) on loading, closing, and saving the world, as well as on the Engine shutdown.
### Arguments

- *bool* **autosave** - true to enable automatic saving of current global configuration settings; false — to disable it.

## bool isAutosave ( ) const

***Console*:**`global_config_autosave`Returns a value indicating if current global configuration settings are automatically saved to the corresponding global config file (`configs/default.global` by default) on loading, closing, and saving the world, as well as on the Engine shutdown.
### Return value

true if automatic saving of current global configuration settings is enabled; otherwise, 0.
## bool load ( )

***Console*:**`global_config_load`Loads global configuration from the file. To change the path to the configuration file use the [*setPath()*](#setPath_cstr_void) method.
### Return value

**true** if the global configuration is successfully loaded from the file; otherwise, **false**.
## bool save ( ) const

***Console*:**`global_config_save`Saves the current global configuration to the file. To change the path to the configuration file use the [*setPath()*](#setPath_cstr_void) method.
### Return value

**true** if the current global configuration is successfully saved to the file; otherwise, **false**.
## void reset ( )

Resets the settings in the global configuration file to the default.
