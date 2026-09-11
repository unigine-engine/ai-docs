# Unigine::Config Class (CPP)

**Header:** #include <UnigineConfig.h>

> **Notice:** This class is a singleton.


The **Config** class is used to read values (settings) from the [application configuration file](../../../code/configuration_file_cpp.md#config) (`configs/default.config` by default) and write them back to it.


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
<summary>AppSystemLogic.h | Close</summary>

`AppSystemLogic.h`


```cpp
#ifndef __APP_SYSTEM_LOGIC_H__
#define __APP_SYSTEM_LOGIC_H__

#include <UnigineLogic.h>

class AppSystemLogic : public Unigine::SystemLogic
{
public:
	AppSystemLogic();
	~AppSystemLogic() override;

	int init() override;

	int update() override;
	int postUpdate() override;

	int shutdown() override;

private:
	Unigine::String player_avatar;
	bool skip_cutscenes;
	bool blood_enabled;
	int bulletshell_lifetime;
};

#endif // __APP_SYSTEM_LOGIC_H__

```

</details>


<details>
<summary>AppSystemLogic.cpp | Close</summary>

`AppSystemLogic.cpp`


```cpp
#include "AppSystemLogic.h"
#include <UnigineConfig.h>

using namespace Unigine;

/*...*/

int AppSystemLogic::init() {

	// read custom user-defined settings from the configuration file
	player_avatar = Config::getString("player_avatar", "soldier1");
	skip_cutscenes = Config::getBool("skip_cutscenes", false);
	blood_enabled = Config::getBool("blood_enabled", false);
	bulletshell_lifetime = Config::getInt("bulletshell_lifetime", 100);

	return 1;
}

int AppSystemLogic::shutdown() {

	// automatically save the configuration file at shutdown
	Config::setAutosave(true);

	// write the custom settings to the configuration file
	Config::setString("player_avatar", player_avatar.get());
	Config::setBool("skip_cutscenes", skip_cutscenes);
	Config::setBool("blood_enabled", blood_enabled);
	Config::setInt("bulletshell_lifetime", bulletshell_lifetime);
	// save data to the custom configuration file, which is different from the default one
	Config::setPath("configs/my.config");
	Config::save();

	return 1;
}

```

</details>


### See Also


- Article on [Configuration Files](../../../code/configuration_file_cpp.md).


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
## void setPath ( const char * path )

Sets a new path to the Engine configuration file (default: `configs/default.config`). The path can be specified as an absolute path or relative to the *[*-data_path*](../../../code/command_line.md#data_path)* or *<project_name>* folder if the *[*-project_name*](../../../code/command_line.md#project_name)* is set.
### Arguments

- *const char ** **path** - The path to the Engine configuration file.

## const char * getPath () const

Returns the current path to the Engine configuration file (default: `configs/default.config`). The path can be specified as an absolute path or relative to the *[*-data_path*](../../../code/command_line.md#data_path)* or *<project_name>* folder if the *[*-project_name*](../../../code/command_line.md#project_name)* is set.
### Return value

Current path to the Engine configuration file.
---

## static void setBool ( const char * name , int value )

Sets a value of the given boolean setting. If the setting with this name already exists, its value is overwritten.
### Arguments

- *const char ** **name** - Name of the setting.
- *int* **value** - Boolean value (**0** or **1**). **0** stands for *false*, **1** stands for *true*.

## static int getBool ( const char * name )

Reads the value of the given boolean setting.
### Arguments

- *const char ** **name** - Name of the setting.

### Return value

Boolean value (**0** or **1**) of the setting. **0** stands for *false*, **1** stands for *true*.
## static int getBool ( const char * name , int value )

Reads the value of the given boolean setting. Returns the value specified as the second argument if the setting isn't found.
### Arguments

- *const char ** **name** - Name of the setting.
- *int* **value** - Custom value to be returned if the setting isn't found.

### Return value

Boolean value (**0** or **1**) of the setting. **0** stands for *false*, **1** stands for *true*.
## static int isExist ( const char * name )

Checks if the setting with the given name exists.
### Arguments

- *const char ** **name** - Name of the setting.

### Return value

**1** if the setting exists; otherwise, **0**.
## static void setFloat ( const char * name , float value )

Sets a value of the given float setting. If the setting with this name already exists, its value is overwritten.
### Arguments

- *const char ** **name** - Name of the setting.
- *float* **value** - Float value of the setting.

## static float getFloat ( const char * name , float value )

Reads the value of the given float setting. Returns the value specified as the second argument if the setting isn't found.
### Arguments

- *const char ** **name** - Name of the setting.
- *float* **value** - Custom value to be returned if the setting isn't found.

### Return value

Float value of the setting.
## static float getFloat ( const char * name )

Reads the value of the given float setting.
### Arguments

- *const char ** **name** - Name of the setting.

### Return value

Float value of the setting.
## static void setInt ( const char * name , int value )

Sets a value of the given integer setting. If the setting with this name already exists, its value is overwritten.
### Arguments

- *const char ** **name** - Name of the setting.
- *int* **value** - Integer value of the setting.

## static int getInt ( const char * name )

Reads the value of the given integer setting.
### Arguments

- *const char ** **name** - Name of the setting.

### Return value

Integer value of the setting.
## static int getInt ( const char * name , int value )

Reads the value of the given integer setting. Returns the value specified as the second argument if the setting isn't found.
### Arguments

- *const char ** **name** - Name of the setting.
- *int* **value** - Custom value to be returned if the setting isn't found.

### Return value

Integer value of the setting.
## static void setString ( const char * name , const char * value )

Sets a value of the given string setting. If the setting with this name already exists, its value is overwritten.
### Arguments

- *const char ** **name** - Name of the setting.
- *const char ** **value** - String value of the setting.

## static const char * getString ( const char * name , const char * value )

Reads the value of the given string setting. Returns the value specified as the second argument if the setting isn't found.
### Arguments

- *const char ** **name** - Name of the setting.
- *const char ** **value** - Custom value to be returned if the setting is found.

### Return value

String value of the setting.
## static const char * getString ( const char * name )

Reads the value of the given string setting.
### Arguments

- *const char ** **name** - Name of the setting.

### Return value

String value of the setting.
## static int load ( )

***Console*:**`config_load`Loads config from the file. To change the path to the configuration file use the [*setPath()*](#setPath_cstr_void) method.
### Return value

**true** if the config is successfully loaded from the file; otherwise, **false**.
## static void remove ( const char * name )

Removes the setting with the given name from the configuration file.
### Arguments

- *const char ** **name** - Name of the setting.

## static int save ( )

***Console*:**`config_save`Saves the current configuration to the file. To change the path to the configuration file use the [*setPath()*](#setPath_cstr_void) method.
### Return value

**true** if the current configuration is successfully saved to the file; otherwise, **false**.
