# Unigine::Console Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


Controls [console](../../../code/console/index.md)-related parameters.


### Onscreen Console Overlay


By default the console overlay is disabled. To make it output console messages to the application screen it should be [enabled](#isOnscreen_int). You can adjust the overlay�s behavior and appearance as well as specify the messages that will be printed exclusively to the onscreen overlay and will not be written to the console.


![](overlay.png)

*Onscreen Overlay with custom parameters and colored text*


You can customize the console font by using the *[setFontSize()](#setFontSize_int_void), [setMessageColor()](#setMessageColor_vec4_void), [setWarningColor()](#setWarningColor_vec4_void)*, and *[setErrorColor()](#setErrorColor_vec4_void)* methods. See the following example:


### Adding Console Command with Several Arguments


The *Console* class can be used to create custom user console commands with a different number of arguments. This section provides an example of how to create a custom console command with several arguments.

  Prior KnowledgeIt is supposed that you have already [created an empty UnigineScript project](../../../code/uniginescript/application.md#empty_application) by using UNIGINE *SDK Browser*.
In the example below, we perform the following actions:


- Define and implement methods for console commands.
- Add a new command.


##### 1. Implementing Callback Function


In this example, we define 2 functions in the world script (`unigine_project.usc` file): one as a callback for a console command with no arguments and one for a console command with 1 argument.


```cpp
// unigine_project.usc

// a script function to be executed for no arguments input
void console_action_callback() {
	log.message("first action! no arguments!\n");
}

// a script function to be executed for 1 argument input
void console_action_callback(string arg) {
	log.message("second action! the argument is: %s\n",arg);
}

```


##### 2. Adding Custom Console Command


Add a custom command to the `unigine_project.usc` file by using *[engine.console.addCommand()](#addCommand_cstr_cstr_CommandCallback_int)* function. By adding this code into *init()* function, the engine adds a new console command on world initialization.


```cpp
// unigine_project.usc

/* ... */

int init() {
	// add a command
	engine.console.addCommand("console_action","my_command description","console_action_callback");

	return 1;
}

/* ... */

```


##### 3. Running Sample


Run the project and open the console. Write recently created command to check the result:


```text
#if you write "console_action"
console_action
first action! no arguments!

#if you write "console_action arg"
console action arg
second action! the argument is: arg

```


To remove the added console command, use *[removeCommand()](#removeCommand_cstr_int)* method.


### See Also


- C++ sample
- C# Component sample
- HowTo video on [Printing User Messages to Console with C#](../../../videotutorials/how_to/how_to_cs/logging.md)


## Console Class

### Members

## void setLock ( int lock )

Sets a new value showing if the console is disabled.
### Arguments

- *int* **lock** - The value set to **1** (or any positive value) means that the console is disabled; the value of **0** corresponds to the enabled (unlocked) console.

## int getLock () const

Returns the current value showing if the console is disabled.
### Return value

Current value set to **1** (or any positive value) means that the console is disabled; the value of **0** corresponds to the enabled (unlocked) console.
## int getNumCommands () const

Returns the current number of all available console commands, including the custom ones.
### Return value

Current number of available console [commands](../../../code/console/index.md#command).
## int getNumVariables () const

Returns the current number of all available console variables.
### Return value

Current number of available console [variables](../../../code/console/index.md#variable).
## void setActive ( bool active )

Sets a new value indicating if the console is opened or closed.
### Arguments

- *bool* **active** - Set **true** to enable the active (opened) state of the console; **false** - to disable it.

## bool isActive () const

Returns the current value indicating if the console is opened or closed.
### Return value

**true** if the active (opened) state of the console is enabled ; otherwise **false**.
## const char * getLastError () const

Returns the current last error message printed to the console.
### Return value

Current last error message printed to the console.
## const char * getLastWarning () const

Returns the current last warning message printed to the console.
### Return value

Current last warning message printed to the console.
## const char * getLastMessage () const

Returns the current last message printed to the console.
### Return value

Current last message printed to the console.
## void setOnscreenTime ( float time )

Sets a new time during which the text is displayed on the screen.
### Arguments

- *float* **time** - The time during which the text is displayed on the screen, in seconds.

## float getOnscreenTime () const

Returns the current time during which the text is displayed on the screen.
### Return value

Current time during which the text is displayed on the screen, in seconds.
## void setOnscreenHeight ( int height )

Sets a new height for the onscreen overlay.
### Arguments

- *int* **height** - The height of the onscreen overlay in percentage of the window height.

## int getOnscreenHeight () const

Returns the current height for the onscreen overlay.
### Return value

Current height of the onscreen overlay in percentage of the window height.
## void setOnscreenFontSize ( int size )

Sets a new size of the onscreen overlay font.
### Arguments

- *int* **size** - The size of the onscreen overlay font.

## int getOnscreenFontSize () const

Returns the current size of the onscreen overlay font.
### Return value

Current size of the onscreen overlay font.
## void setOnscreen ( int onscreen )

Sets a new value indicating if the onscreen overlay is shown or hidden.
### Arguments

- *int* **onscreen** - The display of the onscreen overlay

## int isOnscreen () const

Returns the current value indicating if the onscreen overlay is shown or hidden.
### Return value

Current display of the onscreen overlay
## void setFontSize ( int size )

Sets a new current font size used for console messages.
### Arguments

- *int* **size** - The current font size used for console messages.

## int getFontSize () const

Returns the current current font size used for console messages.
### Return value

Current current font size used for console messages.
## void setWrapping ( int wrapping )

Sets a new value indicating if the text wrapping is enabled for the console.
### Arguments

- *int* **wrapping** - The text wrapping for the console

## int isWrapping () const

Returns the current value indicating if the text wrapping is enabled for the console.
### Return value

Current text wrapping for the console
## void setHeight ( int height )

Sets a new console height in percentage of the window height.
### Arguments

- *int* **height** - The console height in percentage of the window height.

## int getHeight () const

Returns the current console height in percentage of the window height.
### Return value

Current console height in percentage of the window height.
## void setLimit ( int limit )

Sets a new maximum number of messages the console can output. the default value is **16384**.
### Arguments

- *int* **limit** - The maximum number of messages the console can output. the default value is **16384**.

## int getLimit () const

Returns the current maximum number of messages the console can output. the default value is **16384**.
### Return value

Current maximum number of messages the console can output. the default value is **16384**.
## void setPrompt ( string prompt )

Sets a new console prompt.
### Arguments

- *string* **prompt** - The console prompt text.

## const char * getPrompt () const

Returns the current console prompt.
### Return value

Current console prompt text.
## void setTextColor ( vec4 color )

Sets a new common font color for the console.
### Arguments

- *vec4* **color** - The four-component vector specifying the color in the RGBA format.

## vec4 getTextColor () const

Returns the current common font color for the console.
### Return value

Current four-component vector specifying the color in the RGBA format.
## void setErrorColor ( vec4 color )

Sets a new color for error messages in the console.
### Arguments

- *vec4* **color** - The four-component vector specifying the color in the RGBA format.

## vec4 getErrorColor () const

Returns the current color for error messages in the console.
### Return value

Current four-component vector specifying the color in the RGBA format.
## void setWarningColor ( vec4 color )

Sets a new color for warning messages in the console.
### Arguments

- *vec4* **color** - The four-component vector specifying the color in the RGBA format.

## vec4 getWarningColor () const

Returns the current color for warning messages in the console.
### Return value

Current four-component vector specifying the color in the RGBA format.
## void setMessageColor ( vec4 color )

Sets a new color for ordinary messages in the console.
### Arguments

- *vec4* **color** - The four-component vector specifying the color in the RGBA format.

## vec4 getMessageColor () const

Returns the current color for ordinary messages in the console.
### Return value

Current four-component vector specifying the color in the RGBA format.
## void setBackgroundColor ( vec4 color )

Sets a new background color for the console.
### Arguments

- *vec4* **color** - The four-component vector specifying the color in the RGBA format.

## vec4 getBackgroundColor () const

Returns the current background color for the console.
### Return value

Current four-component vector specifying the color in the RGBA format.
## getEventOutput () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
---

## int engine.console. isCommand ( string name )

Returns a value indicating if a command with a given name exists.
### Arguments

- *string* **name** - The command name.

### Return value

**1** if the command with a given name exists; otherwise, **0**.
## string engine.console. getCommandDescription ( string name )

Returns the description of the console command by its name. If the name isn't specified, an empty string will be returned.
### Arguments

- *string* **name** - The command name.

### Return value

The command description if it exists; otherwise, an empty string.
## string engine.console. getCommandName ( int num )

Returns the name of the console command by its number in the array of the existing commands.
### Arguments

- *int* **num** - The command number.

### Return value

The command name if it is found in the array of the existing commands; otherwise, an empty string.
## void engine.console. setFloat ( string name , float value )

Sets a float value for a given variable.
### Arguments

- *string* **name** - The variable name.
- *float* **value** - Float value of the variable.

## float engine.console. getFloat ( string name )

Returns a float value of a given variable.
### Arguments

- *string* **name** - The variable name.

### Return value

Float value of the variable.
## float engine.console. getFloatMax ( string name )

Returns a maximum float value for a given variable.
### Arguments

- *string* **name** - Variable name.

### Return value

Maximum float value of the variable.
## float engine.console. getFloatMin ( string name )

Returns a minimum float value for a given variable.
### Arguments

- *string* **name** - Variable name.

### Return value

Minimum float value of the variable.
## int engine.console. isFloat ( string name )

Checks if the value set for the given console variable is of the float type.
### Arguments

- *string* **name** - The variable name.

### Return value

True if the variable value is float; otherwise, false.
## void engine.console. setInt ( string name , int value )

Sets an integer value for a given variable.
### Arguments

- *string* **name** - Variable name.
- *int* **value** - Value of the variable.

## int engine.console. getInt ( string name )

Returns an integer value of a given variable.
### Arguments

- *string* **name** - Variable name.

### Return value

Value of the variable.
## int engine.console. getIntMax ( string name )

Returns a maximum integer value for a given variable.
### Arguments

- *string* **name** - Variable name.

### Return value

Maximum integer value of the variable.
## int engine.console. getIntMin ( string name )

Returns a minimum integer value for a given variable.
### Arguments

- *string* **name** - Variable name.

### Return value

Minimum integer value of the variable.
## int engine.console. isInt ( string name )

Checks if the value of the given console variable is of the integer type.
### Arguments

- *string* **name** - The variable name.

### Return value

True if the variable value is int; otherwise, false.
## int engine.console. isPalette ( string name )

Checks for a [palette](../../../api/library/common/class.palette_usc.md) with the specified name.
### Arguments

- *string* **name** - Palette name.

## void engine.console. setPalette ( string name , Palette value )

Sets a color [palette](../../../api/library/common/class.palette_usc.md) by its name.
### Arguments

- *string* **name** - Palette name.
- *[Palette](../../../api/library/common/class.palette_usc.md)* **value** - Palette to be set.

## Palette engine.console. getPalette ( string name )

Returns a color [palette](../../../api/library/common/class.palette_usc.md) by its name.
### Arguments

- *string* **name** - Palette name.

### Return value

Palette with the specified name is it exists; otherwise nullptr.
## void engine.console. setString ( string name , string value )

Sets a string value for a given variable.
### Arguments

- *string* **name** - The variable name.
- *string* **value** - String value of the variable.

## string engine.console. getString ( string name )

Returns the string value of a given variable.
### Arguments

- *string* **name** - The variable name.

### Return value

String value of the variable.
## int engine.console. isString ( string name )

Checks if the value of the given console variable is of the string type.
### Arguments

- *string* **name** - The variable name.

### Return value

True if the variable value is string; otherwise, false.
## int engine.console. isVariable ( string name )

Returns a value indicating if a variable with a given name exists.
### Arguments

- *string* **name** - The variable name.

### Return value

True if the variable exists; otherwise, false.
## string engine.console. getVariableDescription ( string name )

Returns the description of the console variable by its name. If the name isn't specified, an empty string will be returned.
### Arguments

- *string* **name** - The variable name.

### Return value

The variable description if it exists; otherwise, an empty string.
## string engine.console. getVariableName ( int num )

Returns the name of the console variable by its number in the array of the existing variables.
### Arguments

- *int* **num** - The variable number.

### Return value

The variable name if it is found in the array of the existing variables; otherwise, an empty string.
## void engine.console. setVec2 ( string name , vec2 value )

Sets a two component vector for the console variable.
### Arguments

- *string* **name** - Name of the variable.
- *vec2* **value** - Value of the variable.

## vec2 engine.console. getVec2 ( string name )

Returns the two component vector console variable.
### Arguments

- *string* **name** - Name of the variable.

### Return value

Value of the variable.
## int engine.console. isVec2 ( string name )

Returns a value indicating if the console variable is a two component vector.
### Arguments

- *string* **name** - Name of the variable.

### Return value

True if the variable is a two component vector; otherwise, false.
## void engine.console. setVec3 ( string name , vec3 value )

Sets a three component vector for the console variable.
### Arguments

- *string* **name** - Name of the variable.
- *vec3* **value** - Value of the variable.

## vec3 engine.console. getVec3 ( string name )

Returns the three component vector console variable.
### Arguments

- *string* **name** - Name of the variable.

### Return value

Value of the variable.
## int engine.console. isVec3 ( string name )

Returns a value indicating if the console variable is a three component vector.
### Arguments

- *string* **name** - Name of the variable.

### Return value

**True** if the variable is a three component vector; otherwise, **false**.
## void engine.console. setVec4 ( string name , vec4 value )

Sets a four component vector for the console variable.
### Arguments

- *string* **name** - Name of the variable.
- *vec4* **value** - Value of the variable.

## vec4 engine.console. getVec4 ( string name )

Returns the four component vector console variable.
### Arguments

- *string* **name** - Name of the variable.

### Return value

Value of the variable.
## int engine.console. isVec4 ( string name )

Returns a value indicating if the console variable is a four component vector.
### Arguments

- *string* **name**

### Return value

**True** if the variable is a three component vector; otherwise, **false**.
## int engine.console. addCommand ( string name , string desc , string callback )

Adds a [custom console command](#adding_command) bound to a given callback function. The command can have up to 6 arguments, which will be passed to the script function.
### Arguments

- *string* **name** - Name of the new console command.
- *string* **desc** - Short description to be displayed in the console.
- *string* **callback** - Name of the callback function to be run on command execution.

### Return value

1 if the custom command is added successfully; otherwise, 0.
## void engine.console. flush ( )

Forces to execute all queued console commands.
## int engine.console. removeCommand ( )

Removes a custom console command.
### Arguments

### Return value

**1** if the custom command has been removed successfully; otherwise, 0.
## void engine.console. run ( )

Runs the specified console command.
### Arguments

## int engine.console. getNumPresetNames ( string name )

Returns the number of presets registered for the given preset console variable (for example, render_aa_preset), including the trailing custom preset that is always reserved for user-overridden settings.
### Arguments

- *string* **name** - Name of the console variable.

### Return value

Number of presets, or 0 if the variable does not exist or is not a preset variable.
## string engine.console. getPresetName ( string name , int num )

Returns the name of the preset with the given number for the specified preset console variable. The last preset is always named custom.
### Arguments

- *string* **name** - Name of the console variable.
- *int* **num** - Preset number, in the [0; **[getNumPresetNames()()](../../...md#getNumPresetNames_cstr_int)**) range.

### Return value

Name of the preset, or an empty string if the variable is not found, is not a preset variable, or the number is out of range.
