# Unigine::Config Class (CS)

> **Notice:** This class is a singleton.


The **Config** class is used to read values (settings) from the [application configuration file](../../../code/configuration_file_cs.md#config) (`configs/default.config` by default) and write them back to it.


Use the appropriate methods depending on the type of the target item. For example, to get the values of the following items, you should use the *getInt()* and *getString()* methods respectively:


```xml
...
<item name="show_fps" type="int">1</item>
<item name="system_script" type="string">unigine_project/unigine.usc</item>
...

```


### Usage Example


By using the *Config* class, you can save custom settings to the configuration file and then restore it when required. For example:


<details>
<summary>ConfigClass.cs | Close</summary>

`ConfigClass.cs`


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

public partial class ConfigClass : Component
{
	private string player_avatar;
	private bool skip_cutscenes;
	private bool blood_enabled;
	private int bulletshell_lifetime;

	private void Init()
	{
		// read custom user-defined settings from the configuration file
		player_avatar = Config.GetString("player_avatar", "soldier1");
		skip_cutscenes = Config.GetBool("skip_cutscenes", false);
		blood_enabled = Config.GetBool("blood_enabled", false);
		bulletshell_lifetime = Config.GetInt("bulletshell_lifetime", 100);

	}

	private void Shutdown()
	{
		// automatically save the configuration file at shutdown
		Config.Autosave = true;

		// write the custom settings to the configuration file
		Config.SetString("player_avatar", player_avatar);
		Config.SetBool("skip_cutscenes", skip_cutscenes);
		Config.SetBool("blood_enabled", blood_enabled);
		Config.SetInt("bulletshell_lifetime", bulletshell_lifetime);
		// save data to the custom configuration file, which is different from the default one
		Config.Path = "configs/my.config";
		Config.Save();

	}
}

```

</details>


### See Also


- Article on [Configuration Files](../../../code/configuration_file_cs.md).


## Config Class

### Properties

## bool Autosave

The value indicating if current Engine configuration settings are automatically saved to the corresponding config file on loading, closing, and saving the world, as well as on the Engine shutdown.
## string Path

The path to the Engine configuration file (default: `configs/default.config`). The path can be specified as an absolute path or relative to the *[*-data_path*](../../../code/command_line.md#data_path)* or *<project_name>* folder if the *[*-project_name*](../../../code/command_line.md#project_name)* is set.
### Members

---

## static void SetBool ( string name , bool value )

Sets a value of the given boolean setting. If the setting with this name already exists, its value is overwritten.
### Arguments

- *string* **name** - Name of the setting.
- *bool* **value** - Boolean value (**0** or **1**). **0** stands for *false*, **1** stands for *true*.

## static bool GetBool ( string name )

Reads the value of the given boolean setting.
### Arguments

- *string* **name** - Name of the setting.

### Return value

Boolean value (**0** or **1**) of the setting. **0** stands for *false*, **1** stands for *true*.
## static bool GetBool ( string name , bool value )

Reads the value of the given boolean setting. Returns the value specified as the second argument if the setting isn't found.
### Arguments

- *string* **name** - Name of the setting.
- *bool* **value** - Custom value to be returned if the setting isn't found.

### Return value

Boolean value (**0** or **1**) of the setting. **0** stands for *false*, **1** stands for *true*.
## static bool IsExist ( string name )

Checks if the setting with the given name exists.
### Arguments

- *string* **name** - Name of the setting.

### Return value

**1** if the setting exists; otherwise, **0**.
## static void SetFloat ( string name , float value )

Sets a value of the given float setting. If the setting with this name already exists, its value is overwritten.
### Arguments

- *string* **name** - Name of the setting.
- *float* **value** - Float value of the setting.

## static float GetFloat ( string name , float value )

Reads the value of the given float setting. Returns the value specified as the second argument if the setting isn't found.
### Arguments

- *string* **name** - Name of the setting.
- *float* **value** - Custom value to be returned if the setting isn't found.

### Return value

Float value of the setting.
## static float GetFloat ( string name )

Reads the value of the given float setting.
### Arguments

- *string* **name** - Name of the setting.

### Return value

Float value of the setting.
## static void SetInt ( string name , int value )

Sets a value of the given integer setting. If the setting with this name already exists, its value is overwritten.
### Arguments

- *string* **name** - Name of the setting.
- *int* **value** - Integer value of the setting.

## static int GetInt ( string name )

Reads the value of the given integer setting.
### Arguments

- *string* **name** - Name of the setting.

### Return value

Integer value of the setting.
## static int GetInt ( string name , int value )

Reads the value of the given integer setting. Returns the value specified as the second argument if the setting isn't found.
### Arguments

- *string* **name** - Name of the setting.
- *int* **value** - Custom value to be returned if the setting isn't found.

### Return value

Integer value of the setting.
## static void SetString ( string name , string value )

Sets a value of the given string setting. If the setting with this name already exists, its value is overwritten.
### Arguments

- *string* **name** - Name of the setting.
- *string* **value** - String value of the setting.

## static string GetString ( string name , string value )

Reads the value of the given string setting. Returns the value specified as the second argument if the setting isn't found.
### Arguments

- *string* **name** - Name of the setting.
- *string* **value** - Custom value to be returned if the setting is found.

### Return value

String value of the setting.
## static string GetString ( string name )

Reads the value of the given string setting.
### Arguments

- *string* **name** - Name of the setting.

### Return value

String value of the setting.
## static bool Load ( )

***Console*:**`config_load`Loads config from the file. To change the path to the configuration file use the [*setPath()*](#setPath_cstr_void) method.
### Return value

**true** if the config is successfully loaded from the file; otherwise, **false**.
## static void Remove ( string name )

Removes the setting with the given name from the configuration file.
### Arguments

- *string* **name** - Name of the setting.

## static bool Save ( )

***Console*:**`config_save`Saves the current configuration to the file. To change the path to the configuration file use the [*setPath()*](#setPath_cstr_void) method.
### Return value

**true** if the current configuration is successfully saved to the file; otherwise, **false**.
