# Unigine::Config Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


The **Config** class is used to read values (settings) from the [application configuration file](../../../code/configuration_file_usc.md#config) (`configs/default.config` by default) and write them back to it.


Use the appropriate methods depending on the type of the target item. For example, to get the values of the following items, you should use the *getInt()* and *getString()* methods respectively:


```xml
...
<item name="show_fps" type="int">1</item>
<item name="system_script" type="string">unigine_project/unigine.usc</item>
...

```


### Usage Example


By using the *Config* class, you can save custom settings to the configuration file and then restore it when required. For example:


```cpp
#include <core/unigine.h>

string player_avatar;
int skip_cutscenes;
int blood_enabled;
int bulletshell_lifetime;

int init() {

	// read custom user-defined settings from the configuration file
	player_avatar = engine.config.getString("player_avatar", "usa_soldier1");
	skip_cutscenes = engine.config.getBool("skip_cutscenes", 0);
	blood_enabled = engine.config.getBool("blood_enabled", 0);
	bulletshell_lifetime = engine.config.getInt("bulletshell_lifetime", 100);

	return 1;
}

int shutdown() {

	// check whether data can be written to the configuration file
	if (engine.console.getInt("config_readonly") == 1) engine.console.setInt("config_readonly",0);
	// write the custom settings to the configuration file
	engine.config.setString("player_avatar", player_avatar);
	engine.config.setBool("skip_cutscenes", skip_cutscenes);
	engine.config.setBool("blood_enabled", blood_enabled);
	engine.config.setInt("bulletshell_lifetime", bulletshell_lifetime);

	return 1;
}

```


In UnigineScript, changes made for the configuration file are saved automatically on the application shutdown.


### See Also


- Article on [Configuration Files](../../../code/configuration_file_usc.md).


## Config Class

### Members

## void setAutosave ( )

Sets a new value indicating if current Engine configuration settings are automatically saved to the corresponding config file on loading, closing, and saving the world, as well as on the Engine shutdown.
### Arguments

- **autosave** - The automatic saving of current Engine configuration settings

## isAutosave () const

Returns the current value indicating if current Engine configuration settings are automatically saved to the corresponding config file on loading, closing, and saving the world, as well as on the Engine shutdown.
### Return value

Current automatic saving of current Engine configuration settings
## void setPath ( string path )

Sets a new path to the Engine configuration file (default: `configs/default.config`). The path can be specified as an absolute path or relative to the *[*-data_path*](../../../code/command_line.md#data_path)* or *<project_name>* folder if the *[*-project_name*](../../../code/command_line.md#project_name)* is set.
### Arguments

- *string* **path** - The path to the Engine configuration file.

## const char * getPath () const

Returns the current path to the Engine configuration file (default: `configs/default.config`). The path can be specified as an absolute path or relative to the *[*-data_path*](../../../code/command_line.md#data_path)* or *<project_name>* folder if the *[*-project_name*](../../../code/command_line.md#project_name)* is set.
### Return value

Current path to the Engine configuration file.
---

## static void engine.config. setBool ( string name , int value )

Sets a value of the given boolean setting. If the setting with this name already exists, its value is overwritten.
### Arguments

- *string* **name** - Name of the setting.
- *int* **value** - Boolean value (**0** or **1**). **0** stands for *false*, **1** stands for *true*.

## static int engine.config. getBool ( string name )

Reads the value of the given boolean setting.
### Arguments

- *string* **name** - Name of the setting.

### Return value

Boolean value (**0** or **1**) of the setting. **0** stands for *false*, **1** stands for *true*.
## static int engine.config. getBool ( string name , int value )

Reads the value of the given boolean setting. Returns the value specified as the second argument if the setting isn't found.
### Arguments

- *string* **name** - Name of the setting.
- *int* **value** - Custom value to be returned if the setting isn't found.

### Return value

Boolean value (**0** or **1**) of the setting. **0** stands for *false*, **1** stands for *true*.
## static int engine.config. isExist ( string name )

Checks if the setting with the given name exists.
### Arguments

- *string* **name** - Name of the setting.

### Return value

**1** if the setting exists; otherwise, **0**.
## static void engine.config. setFloat ( string name , float value )

Sets a value of the given float setting. If the setting with this name already exists, its value is overwritten.
### Arguments

- *string* **name** - Name of the setting.
- *float* **value** - Float value of the setting.

## static float engine.config. getFloat ( string name , float value )

Reads the value of the given float setting. Returns the value specified as the second argument if the setting isn't found.
### Arguments

- *string* **name** - Name of the setting.
- *float* **value** - Custom value to be returned if the setting isn't found.

### Return value

Float value of the setting.
## static float engine.config. getFloat ( string name )

Reads the value of the given float setting.
### Arguments

- *string* **name** - Name of the setting.

### Return value

Float value of the setting.
## static void engine.config. setInt ( string name , int value )

Sets a value of the given integer setting. If the setting with this name already exists, its value is overwritten.
### Arguments

- *string* **name** - Name of the setting.
- *int* **value** - Integer value of the setting.

## static int engine.config. getInt ( string name )

Reads the value of the given integer setting.
### Arguments

- *string* **name** - Name of the setting.

### Return value

Integer value of the setting.
## static int engine.config. getInt ( string name , int value )

Reads the value of the given integer setting. Returns the value specified as the second argument if the setting isn't found.
### Arguments

- *string* **name** - Name of the setting.
- *int* **value** - Custom value to be returned if the setting isn't found.

### Return value

Integer value of the setting.
## static void engine.config. setString ( string name , string value )

Sets a value of the given string setting. If the setting with this name already exists, its value is overwritten.
### Arguments

- *string* **name** - Name of the setting.
- *string* **value** - String value of the setting.

## static string engine.config. getString ( string name , string value )

Reads the value of the given string setting. Returns the value specified as the second argument if the setting isn't found.
### Arguments

- *string* **name** - Name of the setting.
- *string* **value** - Custom value to be returned if the setting is found.

### Return value

String value of the setting.
## static string engine.config. getString ( string name )

Reads the value of the given string setting.
### Arguments

- *string* **name** - Name of the setting.

### Return value

String value of the setting.
