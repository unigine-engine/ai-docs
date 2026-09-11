# Unigine::Console Class (CPP)

**Header:** #include <UnigineConsole.h>

> **Notice:** This class is a singleton.


Controls [console](../../../code/console/index.md)-related parameters.


### Onscreen Console Overlay


By default the console overlay is disabled. To make it output console messages to the application screen it should be [enabled](#isOnscreen_int). You can adjust the overlay�s behavior and appearance as well as specify the messages that will be printed exclusively to the onscreen overlay and will not be written to the console.


![](overlay.png)

*Onscreen Overlay with custom parameters and colored text*


You can customize the console font by using the *[setFontSize()](#setFontSize_int_void), [setMessageColor()](#setMessageColor_vec4_void), [setWarningColor()](#setWarningColor_vec4_void)*, and *[setErrorColor()](#setErrorColor_vec4_void)* methods. See the following example:


```cpp
#include "AppWorldLogic.h"
#include <UnigineConsole.h>

using namespace Unigine;

int AppWorldLogic::init()
{

	// enable the onscreen overlay
	Console::setOnscreen(true);
	// increase the size of the console's font
	Console::setFontSize(20);

	// change the color for different types of messages
	Console::setMessageColor(Unigine::Math::vec4_green);
	Console::setWarningColor(Unigine::Math::vec4_red);
	Console::setErrorColor(Unigine::Math::vec4_blue);

	// send messages to the console
	Log::message("Message!\n");
	Log::warning("Warning!\n");
	Log::error("Error!\n");

	return 1;
}


```


### Adding Console Command with Several Arguments


The *Console* class can be used to create custom user console commands with a different number of arguments. This section provides an example of how to create a custom console command with several arguments.

  Prior KnowledgeIt is supposed that you have already [created an empty C++ project](../../../code/cpp/application.md#empty_application) by using UNIGINE *SDK Browser*.
In the example below, we perform the following actions:


- Define and implement *[AppWorldLogic](../../../code/fundamentals/execution_sequence/app_logic_system.md)* instance methods for console commands.
- Get the console instance (which has a singleton implementation) and add a new command.


##### 1. Adding Instance Methods


In this example, we define three methods in the `AppWorldLogic.h` header file � one as a callback for a console command and another two methods for actions depending on the number of arguments:


```cpp
/* ... */

class AppWorldLogic : public Unigine::WorldLogic
{

public:
	AppWorldLogic();

	/* ... */

private:
	// choose the method to run on the console command call
	void choose_command(int argc, char** argv);
	// perform an action if there are no arguments
	void action_no_args();
	// perform another action if an argument was passed
	void action_one_arg(const char* s);

};


```


- *choose_command()* selects the appropriate method.
- *action_no_args()* is called if there are no console arguments.
- *action_one_arg()* is called if an argument was passed.


In the `AppWorldLogic.cpp` file implement recently defined methods:


```cpp
// check the number of arguments and call the corresponding method
void AppWorldLogic::choose_command(int argc, char** argv) {
	for (int i = 0; i < argc; i++) {
		Log::message("arg[%d]: %s\n", i, argv[i]);
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
void AppWorldLogic::action_no_args() {
	Log::message("first action! no arguments!\n");
}
// write the message into console, if an argument was passed
void AppWorldLogic::action_one_arg(const char* s) {
	Log::message("second action! the argument is:%s \n", s);
}


```


Arguments ***argc*** and ***argv*** are used to get the *arguments count* and *arguments vector*.


> **Notice:** The first element of `argv` always keeps the name of a console command. Thus, `argc` is always >= **1**. To get the first passed argument, you should use *argv[1]*.


##### 2. Adding Custom Console Command


Add custom command to the `AppWorldLogic.cpp` file by using *[addCommand()](#addCommand_cstr_cstr_CommandCallback_int)* function. By adding this code into *AppWorldLogic::init()* function, the engine adds a new console command on AppWorldLogic class instance initialization.


```cpp
#include "AppWorldLogic.h"
#include <UnigineConsole.h>

#include <UnigineCallback.h>

using namespace Unigine;

int AppWorldLogic::init()
{

	// get the existing singleton Console instance and add a command
	Console::addCommand(
		"console_action",
		"Performs custom console action",
		MakeCallback(this, &AppWorldLogic::choose_command)
	);

	return 1;
}


```


##### 3. Running Sample


After building the project, run it and open the console. Write recently created command to see the result:


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
| **LEVEL_NORMAL** = 0 | An ordinary message. |
| **LEVEL_WARNING** = 1 | A warning. |
| **LEVEL_ERROR** = 2 | An error message. |

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
## void setOnscreen ( bool onscreen )

Sets a new value indicating if the onscreen overlay is shown or hidden.
### Arguments

- *bool* **onscreen** - Set **true** to enable display of the onscreen overlay; **false** - to disable it.

## bool isOnscreen () const

Returns the current value indicating if the onscreen overlay is shown or hidden.
### Return value

**true** if display of the onscreen overlay; otherwise **false**.
## void setFontSize ( int size )

Sets a new current font size used for console messages.
### Arguments

- *int* **size** - The current font size used for console messages.

## int getFontSize () const

Returns the current current font size used for console messages.
### Return value

Current current font size used for console messages.
## void setWrapping ( bool wrapping )

Sets a new value indicating if the text wrapping is enabled for the console.
### Arguments

- *bool* **wrapping** - Set **true** to enable text wrapping for the console; **false** - to disable it.

## bool isWrapping () const

Returns the current value indicating if the text wrapping is enabled for the console.
### Return value

**true** if text wrapping for the console is enabled ; otherwise **false**.
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
## void setPrompt ( const char * prompt )

Sets a new console prompt.
### Arguments

- *const char ** **prompt** - The console prompt text.

## const char * getPrompt () const

Returns the current console prompt.
### Return value

Current console prompt text.
## void setTextColor ( const Math:: vec4 & color )

Sets a new common font color for the console.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **color** - The four-component vector specifying the color in the RGBA format.

## Math:: vec4 getTextColor () const

Returns the current common font color for the console.
### Return value

Current four-component vector specifying the color in the RGBA format.
## void setErrorColor ( const Math:: vec4 & color )

Sets a new color for error messages in the console.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **color** - The four-component vector specifying the color in the RGBA format.

## Math:: vec4 getErrorColor () const

Returns the current color for error messages in the console.
### Return value

Current four-component vector specifying the color in the RGBA format.
## void setWarningColor ( const Math:: vec4 & color )

Sets a new color for warning messages in the console.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **color** - The four-component vector specifying the color in the RGBA format.

## Math:: vec4 getWarningColor () const

Returns the current color for warning messages in the console.
### Return value

Current four-component vector specifying the color in the RGBA format.
## void setMessageColor ( const Math:: vec4 & color )

Sets a new color for ordinary messages in the console.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **color** - The four-component vector specifying the color in the RGBA format.

## Math:: vec4 getMessageColor () const

Returns the current color for ordinary messages in the console.
### Return value

Current four-component vector specifying the color in the RGBA format.
## void setBackgroundColor ( const Math:: vec4 & color )

Sets a new background color for the console.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **color** - The four-component vector specifying the color in the RGBA format.

## Math:: vec4 getBackgroundColor () const

Returns the current background color for the console.
### Return value

Current four-component vector specifying the color in the RGBA format.
## Event<const char *, Console::LEVEL > getEventOutput () const

event triggered when a text is output to the console. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

<details>
<summary>See Example | Close</summary>

**Usage Example**


```cpp
// implement the Output event handler
void output_event_handler(const char * text,  Console::LEVEL level)
{
	switch (level) {
	case Console::LEVEL_NORMAL:
		// logic for ordinary messages
	case Console::LEVEL_WARNING:
		// logic for warnings
	case Console::LEVEL_ERROR:
		// logic for error messages
	}
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections output_event_connections;

// link to this instance when subscribing for an event (subscription for various events can be linked)
Console::getEventOutput().connect(output_event_connections, output_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Console::getEventOutput().connect(output_event_connections, [](const char * text,  Console::LEVEL level) {
		Log::message("\Handling Output event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
output_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection output_event_connection;

// subscribe for the Output event with a handler function keeping the connection
Console::getEventOutput().connect(output_event_connection, output_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
output_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
output_event_connection.setEnabled(true);

// ...

// remove subscription for the Output event via the connection
output_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A Output event handler implemented as a class member
	void event_handler(const char * text,  Console::LEVEL level)
	{
		Log::message("\Handling Output event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Console::getEventOutput().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//  4. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe for the Output event with a handler function
Console::getEventOutput().connect(output_event_handler);

// remove subscription for the Output event later by the handler function
Console::getEventOutput().disconnect(output_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   5. Subscribe to an event saving an ID and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////

// define a connection ID to be used to unsubscribe later
EventConnectionId output_handler_id;

// subscribe for the Output event with a lambda handler function and keeping connection ID
output_handler_id = Console::getEventOutput().connect([](const char * text,  Console::LEVEL level) {
		Log::message("\Handling Output event (lambda).\n");
	}
);

// remove the subscription later using the ID
Console::getEventOutput().disconnect(output_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   6. Ignoring all Output events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Console::getEventOutput().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Console::getEventOutput().setEnabled(true);
```

</details>


> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const char * **text**, Console::LEVEL **level**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Output event handler
void output_event_handler(const char * text,  Console::LEVEL level)
{
	Log::message("\Handling Output event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections output_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventOutput().connect(output_event_connections, output_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventOutput().connect(output_event_connections, [](const char * text,  Console::LEVEL level) {
		Log::message("\Handling Output event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
output_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection output_event_connection;

// subscribe to the Output event with a handler function keeping the connection
publisher->getEventOutput().connect(output_event_connection, output_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
output_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
output_event_connection.setEnabled(true);

// ...

// remove subscription to the Output event via the connection
output_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A Output event handler implemented as a class member
	void event_handler(const char * text,  Console::LEVEL level)
	{
		Log::message("\Handling Output event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventOutput().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId output_handler_id;

// subscribe to the Output event with a lambda handler function and keeping connection ID
output_handler_id = publisher->getEventOutput().connect(e_connections, [](const char * text,  Console::LEVEL level) {
		Log::message("\Handling Output event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventOutput().disconnect(output_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Output events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventOutput().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventOutput().setEnabled(true);

```

</details>

### Return value

Event instance.
---

## bool isCommand ( const char * name ) const

Returns a value indicating if a command with a given name exists.
### Arguments

- *const char ** **name** - The command name.

### Return value

**true** if the command with a given name exists; otherwise, **false**.
## const char * getCommandDescription ( const char * name ) const

Returns the description of the console command by its name. If the name isn't specified, an empty string will be returned.
### Arguments

- *const char ** **name** - The command name.

### Return value

The command description if it exists; otherwise, an empty string.
## const char * getCommandName ( int num ) const

Returns the name of the console command by its number in the array of the existing commands.
### Arguments

- *int* **num** - The command number.

### Return value

The command name if it is found in the array of the existing commands; otherwise, an empty string.
## void setFloat ( const char * name , float value )

Sets a float value for a given variable.
### Arguments

- *const char ** **name** - The variable name.
- *float* **value** - Float value of the variable.

## float getFloat ( const char * name ) const

Returns a float value of a given variable.
### Arguments

- *const char ** **name** - The variable name.

### Return value

Float value of the variable.
## float getFloatMax ( const char * name ) const

Returns a maximum float value for a given variable.
### Arguments

- *const char ** **name** - Variable name.

### Return value

Maximum float value of the variable.
## float getFloatMin ( const char * name ) const

Returns a minimum float value for a given variable.
### Arguments

- *const char ** **name** - Variable name.

### Return value

Minimum float value of the variable.
## bool isFloat ( const char * name ) const

Checks if the value set for the given console variable is of the float type.
### Arguments

- *const char ** **name** - The variable name.

### Return value

True if the variable value is float; otherwise, false.
## void setInt ( const char * name , int value )

Sets an integer value for a given variable.
### Arguments

- *const char ** **name** - Name of the variable.
- *int* **value** - Integer value of the variable.

## int getInt ( const char * name ) const

Returns an integer value of a given variable.
### Arguments

- *const char ** **name** - Name of the variable.

### Return value

Integer value of the variable.
## int getIntMax ( const char * name ) const

Returns a maximum integer value for a given variable.
### Arguments

- *const char ** **name** - Variable name.

### Return value

Maximum integer value of the variable.
## int getIntMin ( const char * name ) const

Returns a minimum integer value for a given variable.
### Arguments

- *const char ** **name** - Variable name.

### Return value

Minimum integer value of the variable.
## bool isInt ( const char * name ) const

Checks if the value of the given console variable is of the integer type.
### Arguments

- *const char ** **name** - The variable name.

### Return value

True if the variable value is int; otherwise, false.
## bool isPalette ( const char * name ) const

Checks for a [palette](../../../api/library/common/class.palette_cpp.md) with the specified name.
### Arguments

- *const char ** **name** - Palette name.

## void setPalette ( const char * name , const Palette& value )

Sets a color [palette](../../../api/library/common/class.palette_cpp.md) by its name.
### Arguments

- *const char ** **name** - Palette name.
- *const Palette&* **value** - Palette to be set.

## void setPalette ( const char * name , int index , float value )

Sets a value for the specified [palette](../../../api/library/common/class.palette_cpp.md) color by its index.
### Arguments

- *const char ** **name** - Palette name.
- *int* **index** - Palette color index.
- *float* **value** - Value to be set for the color with the specified index.

## void setPalette ( const char * name , const char * color , float value )

Sets a value for the specified [palette](../../../api/library/common/class.palette_cpp.md) color by the color name.
### Arguments

- *const char ** **name** - Palette name.
- *const char ** **color** - Palette color name.
- *float* **value** - Value to be set for the color with the specified name.

## Palette getPalette ( const char * name ) const

Returns a color [palette](../../../api/library/common/class.palette_cpp.md) by its name.
### Arguments

- *const char ** **name** - Palette name.

### Return value

Palette with the specified name is it exists; otherwise nullptr.
## void setString ( const char * name , const char * value )

Sets a string value for a given variable.
### Arguments

- *const char ** **name** - The variable name.
- *const char ** **value** - String value of the variable.

## const char * getString ( const char * name ) const

Returns the string value of a given variable.
### Arguments

- *const char ** **name** - The variable name.

### Return value

String value of the variable.
## bool isString ( const char * name ) const

Checks if the value of the given console variable is of the string type.
### Arguments

- *const char ** **name** - The variable name.

### Return value

True if the variable value is string; otherwise, false.
## bool isVariable ( const char * name ) const

Returns a value indicating if a variable with a given name exists.
### Arguments

- *const char ** **name** - The variable name.

### Return value

True if the variable exists; otherwise, false.
## const char * getVariableDescription ( const char * name ) const

Returns the description of the console variable by its name. If the name isn't specified, an empty string will be returned.
### Arguments

- *const char ** **name** - The variable name.

### Return value

The variable description if it exists; otherwise, an empty string.
## const char * getVariableName ( int num ) const

Returns the name of the console variable by its number in the array of the existing variables.
### Arguments

- *int* **num** - The variable number.

### Return value

The variable name if it is found in the array of the existing variables; otherwise, an empty string.
## void setVec2 ( const char * name , const Math:: vec2 & value )

Sets a two component vector for the console variable.
### Arguments

- *const char ** **name** - Name of the variable.
- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **value** - Value of the variable.

## Math:: vec2 getVec2 ( const char * name ) const

Returns the two component vector console variable.
### Arguments

- *const char ** **name** - Name of the variable.

### Return value

Value of the variable.
## bool isVec2 ( const char * name ) const

Returns a value indicating if the console variable is a two component vector.
### Arguments

- *const char ** **name** - Name of the variable.

### Return value

True if the variable is a two component vector; otherwise, false.
## void setVec3 ( const char * name , const Math:: vec3 & value )

Sets a three component vector for the console variable.
### Arguments

- *const char ** **name** - Name of the variable.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **value** - Value of the variable.

## Math:: vec3 getVec3 ( const char * name ) const

Returns the three component vector console variable.
### Arguments

- *const char ** **name** - Name of the variable.

### Return value

Value of the variable.
## bool isVec3 ( const char * name ) const

Returns a value indicating if the console variable is a three component vector.
### Arguments

- *const char ** **name** - Name of the variable.

### Return value

**True** if the variable is a three component vector; otherwise, **false**.
## void setVec4 ( const char * name , const Math:: vec4 & value )

Sets a four component vector for the console variable.
### Arguments

- *const char ** **name** - Name of the variable.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **value** - Value of the variable.

## Math:: vec4 getVec4 ( const char * name ) const

Returns the four component vector console variable.
### Arguments

- *const char ** **name** - Name of the variable.

### Return value

Value of the variable.
## bool isVec4 ( const char * name ) const

Returns a value indicating if the console variable is a four component vector.
### Arguments

- *const char ** **name**

### Return value

**True** if the variable is a three component vector; otherwise, **false**.
## int addCommand ( const char * name , const char * desc , CallbackBase * callback )

Adds a [custom console command](#adding_command) bound to a given callback function.
### Arguments

- *const char ** **name** - Name of the new console command.
- *const char ** **desc** - Short description to be displayed in the console.
- *[CallbackBase](../../../api/library/common/callbacks/class.callbackbase_cpp.md) ** **callback** - The callback pointer. The callback arguments must be (*int* **argc**, *char*** **argv**,...).

### Return value

1 if the custom command is added successfully; otherwise, 0.
## void flush ( )

Forces to execute all queued console commands.
## bool removeCommand ( const char * name )

Removes a custom console command.
### Arguments

- *const char ** **name** - Name of the custom console command.

### Return value

true if the custom command has been removed successfully; otherwise, 0.
## void run ( const char * command )

Runs the specified console command.
### Arguments

- *const char ** **command** - A console command with arguments.

## void write ( const char * text )

Writes the specified text to the console and displays it on the screen (onscreen overlay).
> **Notice:** The [onscreen overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen.


### Arguments

- *const char ** **text** - Text to output to the console.

## void write ( const Math:: vec4 & color , const char * text )

Writes the specified text to the console and displays it on the screen (onscreen overlay).
> **Notice:** The [onscreen overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen.


### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Four-component vector specifying the text color in the RGBA format.
- *const char ** **text** - Text to output to the console.

## void write ( Console::LEVEL level , const char * text )

Writes the specified text to the console and displays it on the screen (onscreen overlay).
> **Notice:** The [onscreen overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen.


### Arguments

- *[Console::LEVEL](../../../api/library/engine/class.console_cpp.md#LEVEL)* **level** - Type of the message.
- *const char ** **text** - Text to output to the console.

## static void getMessages ( Vector < String > & messages , int limit )

Gets the messages written to the console and the onscreen overlay.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md) < [String](../../../api/library/common/class.string_cpp.md) > &* **messages** - Vector to populate with messages.
- *int* **limit** - Maximum number of messages to retrieve.

## void getMessages ( Vector < String > & OUT_messages , Vector < int > & OUT_levels , int limit ) const

### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)< [String](../../../api/library/common/class.string_cpp.md) > &* **OUT_messages** - Vector to populate with messages. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)< int > &* **OUT_levels** - Types of messages to retrieve. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int* **limit** - Maximum number of messages to retrieve.

## static void getWarnings ( Vector < String > & messages , int limit )

Gets the warning messages written to the console and the onscreen overlay.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md) < [String](../../../api/library/common/class.string_cpp.md) > &* **messages** - Vector to populate with messages.
- *int* **limit** - Maximum number of messages to retrieve.

## void getErrors ( Vector < String > & messages , int limit )

Gets the error messages written to the console and the onscreen overlay.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md) < [String](../../../api/library/common/class.string_cpp.md) > &* **messages** - Vector to populate with messages.
- *int* **limit** - Maximum number of messages to retrieve.

## static void writeLine ( const char * text )


Writes the text followed by the line terminator to the console and the onscreen overlay.


> **Notice:** The [onscreen overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen.


### Arguments

- *const char ** **text** - Text to output to the console.

## static void writeLine ( const Math:: vec4 & color , const char * text )


Writes the text followed by the line terminator to the console and the onscreen overlay.


> **Notice:** The [onscreen overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen.


### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Four-component vector specifying the text color in the RGBA format.
- *const char ** **text** - Text to output to the console.

## static void writeLine ( Console::LEVEL level , const char * text )


Writes the text followed by the line terminator to the console and the onscreen overlay.


> **Notice:** The [onscreen overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen.


### Arguments

- *[Console::LEVEL](../../../api/library/engine/class.console_cpp.md#LEVEL)* **level** - Type of the message.
- *const char ** **text** - Text to output to the console.

## static void onscreenWrite ( const char * text )


Writes the text to the onscreen overlay only.


> **Notice:** The [onscreen overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen.


### Arguments

- *const char ** **text** - Text to output to the console.

## static void onscreenWrite ( const Math:: vec4 color , const char * text )


Writes the text to the onscreen overlay only.


> **Notice:** The [onscreen overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen.


### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)* **color** - Four-component vector specifying the text color in the RGBA format.
- *const char ** **text** - Text to output to the console.

## static void onscreenWrite ( Console::LEVEL level , const char * text )


Writes the text to the onscreen overlay only.


> **Notice:** The [onscreen overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen.


### Arguments

- *[Console::LEVEL](../../../api/library/engine/class.console_cpp.md#LEVEL)* **level** - Type of the message.
- *const char ** **text** - Text to output to the console.

## static void onscreenWriteLine ( const char * text )


Writes the text only to the onscreen overlay followed by the line terminator.


> **Notice:** The [console overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen on the screen.


### Arguments

- *const char ** **text** - Text to output to the console.

## static void onscreenWriteLine ( Math:: vec4 & color , const char * text )


Writes the text only to the onscreen overlay followed by the line terminator.


> **Notice:** The [console overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen on the screen.


### Arguments

- *Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Four-component vector specifying the text color in the RGBA format.
- *const char ** **text** - Text to output to the console.

## static void onscreenWriteLine ( Console::LEVEL level , const char * text )


Writes the text only to the onscreen overlay followed by the line terminator.


> **Notice:** The [console overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen on the screen.


### Arguments

- *[Console::LEVEL](../../../api/library/engine/class.console_cpp.md#LEVEL)* **level** - Type of the message.
- *const char ** **text** - Text to output to the console.

## static void message ( const Unigine:: Math:: vec4 & color , const char * format , ... )


Writes the ordinary message to the console and the onscreen overlay.


> **Notice:** The [onscreen overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen.


### Arguments

- *const  Unigine:: Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Four-component vector specifying the text color in the RGBA format.
- *const char ** **format** - Formatted text.
- *...*  - Arguments, multiple allowed.

## static void message ( const char * format , ... )


Writes the ordinary message to the console and the onscreen overlay.


> **Notice:** The [onscreen overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen.


### Arguments

- *const char ** **format** - Formatted text.
- *...*  - Arguments, multiple allowed.

## static void warning ( const char * format , ... )


Writes the warning message to the console and the onscreen overlay.


> **Notice:** The [onscreen overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen.


### Arguments

- *const char ** **format** - Formatted text.
- *...*  - Arguments, multiple allowed.

## static void error ( const char * format , ... )


Writes the error message to the console and the onscreen overlay.


> **Notice:** The [onscreen overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen.


### Arguments

- *const char ** **format** - Formatted text.
- *...*  - Arguments, multiple allowed.

## static void messageLine ( const Unigine:: Math:: vec4 & color , const char * format , ... )


Writes the ordinary message to the console and the onscreen overlay followed by the line terminator.


> **Notice:** The [onscreen overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen.


### Arguments

- *const  Unigine:: Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Four-component vector specifying the text color in the RGBA format.
- *const char ** **format** - Formatted text.
- *...*  - Arguments, multiple allowed.

## static void messageLine ( const char * format , ... )


Writes the ordinary message to the console and the onscreen overlay followed by the line terminator.


> **Notice:** The [onscreen overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen.


### Arguments

- *const char ** **format** - Formatted text.
- *...*  - Arguments, multiple allowed.

## static void warningLine ( const char * format , ... )


Writes the warning message to the console and the onscreen overlay followed by the line terminator.


> **Notice:** The [onscreen overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen.


### Arguments

- *const char ** **format** - Formatted text.
- *...*  - Arguments, multiple allowed.

## static void errorLine ( const char * format , ... )


Writes the error message to the console and the onscreen overlay followed by the line terminator.


> **Notice:** The [onscreen overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen.


### Arguments

- *const char ** **format** - Formatted text.
- *...*  - Arguments, multiple allowed.

## static void onscreenMessage ( const Unigine:: Math:: vec4 & color , const char * format , ... )


Writes the ordinary message to the onscreen overlay only.


> **Notice:** The [console overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen on the screen.


### Arguments

- *const  Unigine:: Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Four-component vector specifying the text color in the RGBA format.
- *const char ** **format** - Formatted text.
- *...*  - Arguments, multiple allowed.

## static void onscreenMessage ( const char * format , ... )


Writes the ordinary message to the onscreen overlay only.


> **Notice:** The [console overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen on the screen.


### Arguments

- *const char ** **format** - Formatted text.
- *...*  - Arguments, multiple allowed.

## static void onscreenWarning ( const char * format , ... )


Writes the warning message to the onscreen overlay only.


> **Notice:** The [console overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen on the screen.


### Arguments

- *const char ** **format** - Formatted text.
- *...*  - Arguments, multiple allowed.

## static void onscreenError ( const char * format , ... )


Writes the error message to the onscreen overlay only.


> **Notice:** The [console overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen on the screen.


### Arguments

- *const char ** **format** - Formatted text.
- *...*  - Arguments, multiple allowed.

## static void onscreenMessageLine ( const Unigine:: Math:: vec4 & color , const char * format , ... )


Writes the ordinary message only to the onscreen overlay followed by the line terminator.


> **Notice:** The [console overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen on the screen.


### Arguments

- *const  Unigine:: Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Four-component vector specifying the text color in the RGBA format.
- *const char ** **format** - Formatted text.
- *...*  - Arguments, multiple allowed.

## static void onscreenMessageLine ( const char * format , ... )


Writes the ordinary message only to the onscreen overlay followed by the line terminator.


> **Notice:** The [console overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen on the screen.


### Arguments

- *const char ** **format** - Formatted text.
- *...*  - Arguments, multiple allowed.

## static void onscreenWarningLine ( const char * format , ... )


Writes the warning message only to the onscreen overlay followed by the line terminator.


> **Notice:** The [console overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen on the screen.


### Arguments

- *const char ** **format** - Formatted text.
- *...*  - Arguments, multiple allowed.

## static void onscreenErrorLine ( const char * format , ... )


Writes the error message only to the onscreen overlay followed by the line terminator.


> **Notice:** The [console overlay](#onscreen_console_overlay) must be [enabled](#isOnscreen_int) for the text to be seen on the screen.


### Arguments

- *const char ** **format** - Formatted text.
- *...*  - Arguments, multiple allowed.

## int getNumPresetNames ( const char * name ) const

Returns the number of presets registered for the given preset console variable (for example, render_aa_preset), including the trailing custom preset that is always reserved for user-overridden settings.
### Arguments

- *const char ** **name** - Name of the console variable.

### Return value

Number of presets, or 0 if the variable does not exist or is not a preset variable.
## const char * getPresetName ( const char * name , int num ) const

Returns the name of the preset with the given number for the specified preset console variable. The last preset is always named custom.
### Arguments

- *const char ** **name** - Name of the console variable.
- *int* **num** - Preset number, in the [0; **[getNumPresetNames()](../../...md#getNumPresetNames_cstr_int)**) range.

### Return value

Name of the preset, or an empty string if the variable is not found, is not a preset variable, or the number is out of range.
