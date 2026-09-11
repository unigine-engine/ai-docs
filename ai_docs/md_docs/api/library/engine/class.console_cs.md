# Unigine::Console Class (CS)

> **Notice:** This class is a singleton.


Controls [console](../../../code/console/index.md)-related parameters.


### Onscreen Console Overlay


By default the console overlay is disabled. To make it output console messages to the application screen it should be [enabled](#isOnscreen_int). You can adjust the overlay�s behavior and appearance as well as specify the messages that will be printed exclusively to the onscreen overlay and will not be written to the console.


![](overlay.png)

*Onscreen Overlay with custom parameters and colored text*


You can customize the console font by using the *[setFontSize()](#setFontSize_int_void), [setMessageColor()](#setMessageColor_vec4_void), [setWarningColor()](#setWarningColor_vec4_void)*, and *[setErrorColor()](#setErrorColor_vec4_void)* methods. See the following example:


```csharp
private void Init()
{

	// enable the onscreen overlay
	Unigine.Console.Onscreen = true;
	// increase the size of the console's font
	Unigine.Console.FontSize = 20;

	// change the color for different types of messages
	Unigine.Console.MessageColor = vec4.GREEN;
	Unigine.Console.WarningColor = vec4.RED;
	Unigine.Console.ErrorColor = vec4.BLUE;

	// send messages to the console
	Unigine.Log.Message("Message!\n");
	Unigine.Log.Warning("Warning!\n");
	Unigine.Log.Error("Error!\n");

}


```


### Adding Console Command with Several Arguments


The *Console* class can be used to create custom user console commands with a different number of arguments. This section provides an example of how to create a custom console command with several arguments.

  Prior KnowledgeIt is supposed that you have already [created an empty C# project](../../../code/csharp/application.md#empty_application) by using UNIGINE *SDK Browser*.
In the example below, we perform the following actions:


- Define and implement *[AppWorldLogic](../../../code/fundamentals/execution_sequence/app_logic_system.md)* instance methods for console commands.
- Get the console instance (which has a singleton implementation) and add a new command.


##### 1. Adding Instance Methods


In this example, we define three methods in the `AppWorldLogic.cs` file: one as a callback for a console command and another two methods for actions depending on the number of arguments:


- *choose_command()* selects the appropriate method.
- *action_no_args()* is called if there are no console arguments.
- *action_one_arg()* is called if an argument was passed.


```csharp
public static void choose_command(int argc, string[] argv)
{
for (int i = 0; i < argc; i++) {
	Log.Message("arg[{0}]: {1}\n", i, argv[i]);
}
// note: the first element of argv is the name of console command
if (argc == 1) {
	action_no_args();
}
else if (argc == 2) {
	 action_one_arg(argv[1]);
}
// for more arguments:
//else if (...) {
	//	// etc
//}
}

// write the message into console, if there are no arguments
public static void action_no_args()
{
Log.Message("first action! no arguments!\n");
}
// write the message into console, if an argument was passed
public static void action_one_arg(string s)
{
Log.Message("second action! the argument is:{0} \n", s);
}


```


Arguments ***argc*** and ***argv*** are used to get the *arguments count* and *arguments vector*.


> **Notice:** The first element of `argv` always keeps the name of a console command. Thus, `argc` is always >= **1**. To get the first passed argument, you should use *argv[1]*.


##### 2. Adding Custom Console Command


Add a custom command to the `AppWorldLogic.cs` file by using *[addCommand()](#addCommand_cstr_cstr_CommandCallback_int)* function. By adding this code into *init()* function of the AppWorldLogic class, the engine adds a new console command on AppWorldLogic class instance initialization.


```csharp
private void Init()
{

	// add a command
	Unigine.Console.AddCommand("console_action","Performs custom console action",choose_command);

}


```


##### 3. Running Sample


After building the project, run it and open the console. Write recently created command to check the result:


```text
#if you write "console_action"
arg[0]: console_action
first action! no arguments!

#if you write "console_action arg"
arg[0]: console action
arg[1]: arg
second action! the argument is:arg

```


To remove the added console command, use *[removeCommand()](#removeCommand_cstr_int)* method.


### See Also


- C++ sample
- C# Component sample
- HowTo video on [Printing User Messages to Console with C#](../../../videotutorials/how_to/how_to_cs/logging.md)


## Console Class

### Enums

## LEVEL

| Name | Description |
|---|---|
| **NORMAL** = 0 | An ordinary message. |
| **WARNING** = 1 | A warning. |
| **ERROR** = 2 | An error message. |

### Properties

## int Lock

The value showing if the console is disabled.
## 🔒︎ int NumCommands

The number of all available console commands, including the custom ones.
## 🔒︎ int NumVariables

The number of all available console variables.
## bool Active

The value indicating if the console is opened or closed.
## 🔒︎ string LastError

The last error message printed to the console.
## 🔒︎ string LastWarning

The last warning message printed to the console.
## 🔒︎ string LastMessage

The last message printed to the console.
## float OnscreenTime

The time during which the text is displayed on the screen.
## int OnscreenHeight

The height for the onscreen overlay.
## int OnscreenFontSize

The size of the onscreen overlay font.
## bool Onscreen

The value indicating if the onscreen overlay is shown or hidden.
## int FontSize

The current font size used for console messages.
## bool Wrapping

The value indicating if the text wrapping is enabled for the console.
## int Height

The console height in percentage of the window height.
## int Limit

The maximum number of messages the console can output. the default value is **16384**.
## string Prompt

The console prompt.
## vec4 TextColor

The common font color for the console.
## vec4 ErrorColor

The color for error messages in the console.
## vec4 WarningColor

The color for warning messages in the console.
## vec4 MessageColor

The color for ordinary messages in the console.
## vec4 BackgroundColor

The background color for the console.
## 🔒︎ Event<string, Console.LEVEL > EventOutput

The event triggered when a text is output to the console. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

<details>
<summary>See Example | Close</summary>

**Usage Example**


```csharp
// implement the Output event handler
void output_handler(string text,  Console.LEVEL level)
{
	switch (level)
	{
		case Unigine.Console.LEVEL.NORMAL:
			// logic for ordinary messages
			break;
		case Unigine.Console.LEVEL.WARNING:
			// logic for warnings
			break;
		case Unigine.Console.LEVEL.ERROR:
			// logic for error messages
			break;
	}
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections output_event_connections = new EventConnections();

// link to this instance when subscribing for an event (subscription for various events can be linked)
Console.EventOutput.Connect(output_event_connections, output_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Console.EventOutput.Connect(output_event_connections, (string text,  Console.LEVEL level) => {
		Log.Message("Handling Output event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
output_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe for the Output event with a handler function
Console.EventOutput.Connect(output_event_handler);

// remove subscription for the Output event later by the handler function
Console.EventOutput.Disconnect(output_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection output_event_connection;

// subscribe for the Output event with a lambda handler function and keeping the connection
output_event_connection = Console.EventOutput.Connect((string text,  Console.LEVEL level) => {
		Log.Message("Handling Output event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
output_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
leave_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
output_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Output events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Console.EventOutput.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Console.EventOutput.Enabled = true;
```

</details>


> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(string **text**, Console.LEVEL **level**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Output event handler
void output_event_handler(string text,  Console.LEVEL level)
{
	Log.Message("\Handling Output event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections output_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventOutput.Connect(output_event_connections, output_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventOutput.Connect(output_event_connections, (string text,  Console.LEVEL level) => {
		Log.Message("Handling Output event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
output_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Output event with a handler function
publisher.EventOutput.Connect(output_event_handler);

// remove subscription to the Output event later by the handler function
publisher.EventOutput.Disconnect(output_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection output_event_connection;

// subscribe to the Output event with a lambda handler function and keeping the connection
output_event_connection = publisher.EventOutput.Connect((string text,  Console.LEVEL level) => {
		Log.Message("Handling Output event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
output_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
output_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
output_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Output events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventOutput.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventOutput.Enabled = true;

```

</details>

### Members

---

## bool IsCommand ( string name )

Returns a value indicating if a command with a given name exists.
### Arguments

- *string* **name** - The command name.

### Return value

**true** if the command with a given name exists; otherwise, **false**.
## string GetCommandDescription ( string name )

Returns the description of the console command by its name. If the name isn't specified, an empty string will be returned.
### Arguments

- *string* **name** - The command name.

### Return value

The command description if it exists; otherwise, an empty string.
## string GetCommandName ( int num )

Returns the name of the console command by its number in the array of the existing commands.
### Arguments

- *int* **num** - The command number.

### Return value

The command name if it is found in the array of the existing commands; otherwise, an empty string.
## void SetFloat ( string name , float value )

Sets a float value for a given variable.
### Arguments

- *string* **name** - The variable name.
- *float* **value** - Float value of the variable.

## float GetFloat ( string name )

Returns a float value of a given variable.
### Arguments

- *string* **name** - The variable name.

### Return value

Float value of the variable.
## float GetFloatMax ( string name )

Returns a maximum float value for a given variable.
### Arguments

- *string* **name** - Variable name.

### Return value

Maximum float value of the variable.
## float GetFloatMin ( string name )

Returns a minimum float value for a given variable.
### Arguments

- *string* **name** - Variable name.

### Return value

Minimum float value of the variable.
## bool IsFloat ( string name )

Checks if the value set for the given console variable is of the float type.
### Arguments

- *string* **name** - The variable name.

### Return value

True if the variable value is float; otherwise, false.
## void SetInt ( string name , int value )

Sets an integer value for a given variable.
### Arguments

- *string* **name** - Variable name.
- *int* **value** - Value of the variable.

## int GetInt ( string name )

Returns an integer value of a given variable.
### Arguments

- *string* **name** - Variable name.

### Return value

Integer value of the variable.
## int GetIntMax ( string name )

Returns a maximum integer value for a given variable.
### Arguments

- *string* **name** - Variable name.

### Return value

Maximum integer value of the variable.
## int GetIntMin ( string name )

Returns a minimum integer value for a given variable.
### Arguments

- *string* **name** - Variable name.

### Return value

Minimum integer value of the variable.
## bool IsInt ( string name )

Checks if the value of the given console variable is of the integer type.
### Arguments

- *string* **name** - The variable name.

### Return value

True if the variable value is int; otherwise, false.
## bool IsPalette ( string name )

Checks for a [palette](../../../api/library/common/class.palette_cs.md) with the specified name.
### Arguments

- *string* **name** - Palette name.

## void SetPalette ( string name , Palette value )

Sets a color [palette](../../../api/library/common/class.palette_cs.md) by its name.
### Arguments

- *string* **name** - Palette name.
- *[Palette](../../../api/library/common/class.palette_cs.md)* **value** - Palette to be set.

## void SetPalette ( string name , int index , float value )

Sets a value for the specified [palette](../../../api/library/common/class.palette_cs.md) color by its index.
### Arguments

- *string* **name** - Palette name.
- *int* **index** - Palette color index.
- *float* **value** - Value to be set for the color with the specified index.

## void SetPalette ( string name , string color , float value )

Sets a value for the specified [palette](../../../api/library/common/class.palette_cs.md) color by the color name.
### Arguments

- *string* **name** - Palette name.
- *string* **color** - Palette color name.
- *float* **value** - Value to be set for the color with the specified name.

## Palette GetPalette ( string name )

Returns a color [palette](../../../api/library/common/class.palette_cs.md) by its name.
### Arguments

- *string* **name** - Palette name.

### Return value

Palette with the specified name is it exists; otherwise nullptr.
## void SetString ( string name , string value )

Sets a string value for a given variable.
### Arguments

- *string* **name** - The variable name.
- *string* **value** - String value of the variable.

## string GetString ( string name )

Returns the string value of a given variable.
### Arguments

- *string* **name** - The variable name.

### Return value

String value of the variable.
## bool IsString ( string name )

Checks if the value of the given console variable is of the string type.
### Arguments

- *string* **name** - The variable name.

### Return value

True if the variable value is string; otherwise, false.
## bool IsVariable ( string name )

Returns a value indicating if a variable with a given name exists.
### Arguments

- *string* **name** - The variable name.

### Return value

True if the variable exists; otherwise, false.
## string GetVariableDescription ( string name )

Returns the description of the console variable by its name. If the name isn't specified, an empty string will be returned.
### Arguments

- *string* **name** - The variable name.

### Return value

The variable description if it exists; otherwise, an empty string.
## string GetVariableName ( int num )

Returns the name of the console variable by its number in the array of the existing variables.
### Arguments

- *int* **num** - The variable number.

### Return value

The variable name if it is found in the array of the existing variables; otherwise, an empty string.
## void SetVec2 ( string name , vec2 value )

Sets a two component vector for the console variable.
### Arguments

- *string* **name** - Name of the variable.
- *vec2* **value** - Value of the variable.

## vec2 GetVec2 ( string name )

Returns the two component vector console variable.
### Arguments

- *string* **name** - Name of the variable.

### Return value

Value of the variable.
## bool IsVec2 ( string name )

Returns a value indicating if the console variable is a two component vector.
### Arguments

- *string* **name** - Name of the variable.

### Return value

True if the variable is a two component vector; otherwise, false.
## void SetVec3 ( string name , vec3 value )

Sets a three component vector for the console variable.
### Arguments

- *string* **name** - Name of the variable.
- *vec3* **value** - Value of the variable.

## vec3 GetVec3 ( string name )

Returns the three component vector console variable.
### Arguments

- *string* **name** - Name of the variable.

### Return value

Value of the variable.
## bool IsVec3 ( string name )

Returns a value indicating if the console variable is a three component vector.
### Arguments

- *string* **name** - Name of the variable.

### Return value

**True** if the variable is a three component vector; otherwise, **false**.
## void SetVec4 ( string name , vec4 value )

Sets a four component vector for the console variable.
### Arguments

- *string* **name** - Name of the variable.
- *vec4* **value** - Value of the variable.

## vec4 GetVec4 ( string name )

Returns the four component vector console variable.
### Arguments

- *string* **name** - Name of the variable.

### Return value

Value of the variable.
## bool IsVec4 ( string name )

Returns a value indicating if the console variable is a four component vector.
### Arguments

- *string* **name**

### Return value

**True** if the variable is a three component vector; otherwise, **false**.
## void addCommand ( string name , string desc , CommandCallback callback )

Adds a [custom console command](#adding_command) bound to a given callback function.
### Arguments

- *string* **name** - Name of the new console command.
- *string* **desc** - Short description to be displayed in the console.
- *CommandCallback* **callback** - The callback function to be run on command execution. The callback arguments must be (*int* **argc**, *string[]* **argv**,...).

### Return value

1 if the custom command is added successfully; otherwise, 0.
## void Flush ( )

Forces to execute all queued console commands.
## bool RemoveCommand ( string name )

Removes a custom console command.
### Arguments

- *string* **name** - Name of the custom console command.

### Return value

true if the custom command has been removed successfully; otherwise, 0.
## void Run ( string command )

Runs the specified console command.
### Arguments

- *string* **command** - A console command with arguments.

## void Write ( string text )

Writes the specified text to the console and displays it on the screen (onscreen overlay).
> **Notice:** The [onscreen overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen.


### Arguments

- *string* **text** - Text to output to the console.

## void Write ( vec4 color , string text )

Writes the specified text to the console and displays it on the screen (onscreen overlay).
> **Notice:** The [onscreen overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen.


### Arguments

- *vec4* **color** - Four-component vector specifying the text color in the RGBA format.
- *string* **text** - Text to output to the console.

## void Write ( Console.LEVEL level , string text )

Writes the specified text to the console and displays it on the screen (onscreen overlay).
> **Notice:** The [onscreen overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen.


### Arguments

- *[Console.LEVEL](../../../api/library/engine/class.console_cs.md#LEVEL)* **level** - Type of the message.
- *string* **text** - Text to output to the console.

## static void GetMessages ( ICollection<string> messages , int limit )

Gets the messages written to the console and the onscreen overlay.
### Arguments

- *ICollection<string>* **messages** - Vector to populate with messages.
- *int* **limit** - Maximum number of messages to retrieve.

## void GetMessages ( string[] OUT_messages , int[] OUT_levels , int limit )

### Arguments

- *string[]* **OUT_messages** - Vector to populate with messages. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int[]* **OUT_levels** - Types of messages to retrieve. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int* **limit** - Maximum number of messages to retrieve.

## static void GetWarnings ( ICollection<string> messages , int limit )

Gets the warning messages written to the console and the onscreen overlay.
### Arguments

- *ICollection<string>* **messages** - Vector to populate with messages.
- *int* **limit** - Maximum number of messages to retrieve.

## void GetErrors ( ICollection<string> messages , int limit )

Gets the error messages written to the console and the onscreen overlay.
### Arguments

- *ICollection<string>* **messages** - Vector to populate with messages.
- *int* **limit** - Maximum number of messages to retrieve.

## static void WriteLine ( string text )


Writes the text followed by the line terminator to the console and the onscreen overlay.


> **Notice:** The [onscreen overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen.


### Arguments

- *string* **text** - Text to output to the console.

## static void WriteLine ( vec4 color , string text )


Writes the text followed by the line terminator to the console and the onscreen overlay.


> **Notice:** The [onscreen overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen.


### Arguments

- *vec4* **color** - Four-component vector specifying the text color in the RGBA format.
- *string* **text** - Text to output to the console.

## static void WriteLine ( Console.LEVEL level , string text )


Writes the text followed by the line terminator to the console and the onscreen overlay.


> **Notice:** The [onscreen overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen.


### Arguments

- *[Console.LEVEL](../../../api/library/engine/class.console_cs.md#LEVEL)* **level** - Type of the message.
- *string* **text** - Text to output to the console.

## static void OnscreenWrite ( string text )


Writes the text to the onscreen overlay only.


> **Notice:** The [onscreen overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen.


### Arguments

- *string* **text** - Text to output to the console.

## static void OnscreenWrite ( vec4 color , string text )


Writes the text to the onscreen overlay only.


> **Notice:** The [onscreen overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen.


### Arguments

- *vec4* **color** - Four-component vector specifying the text color in the RGBA format.
- *string* **text** - Text to output to the console.

## static void OnscreenWrite ( Console.LEVEL level , string text )


Writes the text to the onscreen overlay only.


> **Notice:** The [onscreen overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen.


### Arguments

- *[Console.LEVEL](../../../api/library/engine/class.console_cs.md#LEVEL)* **level** - Type of the message.
- *string* **text** - Text to output to the console.

## static void OnscreenWriteLine ( string text )


Writes the text only to the onscreen overlay followed by the line terminator.


> **Notice:** The [console overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen on the screen.


### Arguments

- *string* **text** - Text to output to the console.

## static void OnscreenWriteLine ( vec4 color , string text )


Writes the text only to the onscreen overlay followed by the line terminator.


> **Notice:** The [console overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen on the screen.


### Arguments

- *vec4* **color** - Four-component vector specifying the text color in the RGBA format.
- *string* **text** - Text to output to the console.

## static void OnscreenWriteLine ( Console.LEVEL level , string text )


Writes the text only to the onscreen overlay followed by the line terminator.


> **Notice:** The [console overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen on the screen.


### Arguments

- *[Console.LEVEL](../../../api/library/engine/class.console_cs.md#LEVEL)* **level** - Type of the message.
- *string* **text** - Text to output to the console.

## static void Message ( vec4 color , string format , ... )


Writes the ordinary message to the console and the onscreen overlay.


> **Notice:** The [onscreen overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen.


### Arguments

- *vec4* **color** - Four-component vector specifying the text color in the RGBA format.
- *string* **format** - Formatted text.
- *...*  - Arguments, multiple allowed.

## static void Message ( string format , ... )


Writes the ordinary message to the console and the onscreen overlay.


> **Notice:** The [onscreen overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen.


### Arguments

- *string* **format** - Formatted text.
- *...*  - Arguments, multiple allowed.

## static void Warning ( string format , ... )


Writes the warning message to the console and the onscreen overlay.


> **Notice:** The [onscreen overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen.


### Arguments

- *string* **format** - Formatted text.
- *...*  - Arguments, multiple allowed.

## static void Error ( string format , ... )


Writes the error message to the console and the onscreen overlay.


> **Notice:** The [onscreen overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen.


### Arguments

- *string* **format** - Formatted text.
- *...*  - Arguments, multiple allowed.

## static void MessageLine ( vec4 color , string format , ... )


Writes the ordinary message to the console and the onscreen overlay followed by the line terminator.


> **Notice:** The [onscreen overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen.


### Arguments

- *vec4* **color** - Four-component vector specifying the text color in the RGBA format.
- *string* **format** - Formatted text.
- *...*  - Arguments, multiple allowed.

## static void MessageLine ( string format , ... )


Writes the ordinary message to the console and the onscreen overlay followed by the line terminator.


> **Notice:** The [onscreen overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen.


### Arguments

- *string* **format** - Formatted text.
- *...*  - Arguments, multiple allowed.

## static void WarningLine ( string format , ... )


Writes the warning message to the console and the onscreen overlay followed by the line terminator.


> **Notice:** The [onscreen overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen.


### Arguments

- *string* **format** - Formatted text.
- *...*  - Arguments, multiple allowed.

## static void ErrorLine ( string format , ... )


Writes the error message to the console and the onscreen overlay followed by the line terminator.


> **Notice:** The [onscreen overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen.


### Arguments

- *string* **format** - Formatted text.
- *...*  - Arguments, multiple allowed.

## static void OnscreenMessage ( vec4 color , string format , ... )


Writes the ordinary message to the onscreen overlay only.


> **Notice:** The [console overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen on the screen.


### Arguments

- *vec4* **color** - Four-component vector specifying the text color in the RGBA format.
- *string* **format** - Formatted text.
- *...*  - Arguments, multiple allowed.

## static void OnscreenMessage ( string format , ... )


Writes the ordinary message to the onscreen overlay only.


> **Notice:** The [console overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen on the screen.


### Arguments

- *string* **format** - Formatted text.
- *...*  - Arguments, multiple allowed.

## static void OnscreenWarning ( string format , ... )


Writes the warning message to the onscreen overlay only.


> **Notice:** The [console overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen on the screen.


### Arguments

- *string* **format** - Formatted text.
- *...*  - Arguments, multiple allowed.

## static void OnscreenError ( string format , ... )


Writes the error message to the onscreen overlay only.


> **Notice:** The [console overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen on the screen.


### Arguments

- *string* **format** - Formatted text.
- *...*  - Arguments, multiple allowed.

## static void OnscreenMessageLine ( vec4 color , string format , ... )


Writes the ordinary message only to the onscreen overlay followed by the line terminator.


> **Notice:** The [console overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen on the screen.


### Arguments

- *vec4* **color** - Four-component vector specifying the text color in the RGBA format.
- *string* **format** - Formatted text.
- *...*  - Arguments, multiple allowed.

## static void OnscreenMessageLine ( string format , ... )


Writes the ordinary message only to the onscreen overlay followed by the line terminator.


> **Notice:** The [console overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen on the screen.


### Arguments

- *string* **format** - Formatted text.
- *...*  - Arguments, multiple allowed.

## static void OnscreenWarningLine ( string format , ... )


Writes the warning message only to the onscreen overlay followed by the line terminator.


> **Notice:** The [console overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen on the screen.


### Arguments

- *string* **format** - Formatted text.
- *...*  - Arguments, multiple allowed.

## static void OnscreenErrorLine ( string format , ... )


Writes the error message only to the onscreen overlay followed by the line terminator.


> **Notice:** The [console overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen on the screen.


### Arguments

- *string* **format** - Formatted text.
- *...*  - Arguments, multiple allowed.

## int GetNumPresetNames ( string name )

Returns the number of presets registered for the given preset console variable (for example, render_aa_preset), including the trailing custom preset that is always reserved for user-overridden settings.
### Arguments

- *string* **name** - Name of the console variable.

### Return value

Number of presets, or 0 if the variable does not exist or is not a preset variable.
## string GetPresetName ( string name , int num )

Returns the name of the preset with the given number for the specified preset console variable. The last preset is always named custom.
### Arguments

- *string* **name** - Name of the console variable.
- *int* **num** - Preset number, in the [0; **[GetNumPresetNames()](../../...md#getNumPresetNames_cstr_int)**) range.

### Return value

Name of the preset, or an empty string if the variable is not found, is not a preset variable, or the number is out of range.
