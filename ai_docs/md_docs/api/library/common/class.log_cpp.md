# Unigine::Log Class (CPP)

**Header:** #include <UnigineLog.h>


This class represents an interface for printing various types of messages to the [console](../../../code/console/index.md) and to the Engine's log file. It can be useful to monitor overall progress of application execution and report errors which can be helpful in the process of debugging.


> **Notice:** To enable displaying system messages in the Console use the following command: [`console_onscreen 1`](../../../code/console/index.md#console_onscreen)


There are two custom color schemes highlighting log syntax for Notepad++ included in the SDK:


- `<SDK>/utils/log_styles/notepad_light.xml`
- `<SDK>/utils/log_styles/notepad_dark.xml`


> **Notice:** By default all logged messages are saved to the Engine's log file, and printed to stdout, the latter **may significantly affect peformance** in case of much logging. If logging causes performance issues, you can control the two logging targets via the following console commands:
> - [`log_stdout`](../../../code/console/index.md#log_stdout)
> - [`log_file`](../../../code/console/index.md#log_file)


### Example


The following code demonstrates how to print various types of messages.


```cpp
using namespace Unigine;

// auxiliary variables for messages
const char* file_name = "file.txt";
int ID = 10;

	// reporting an error message
	Log::error("Loading mesh: can't open \"%s\" file\n", file_name);

	// reporting a message
	Log::message("-> Added %d UI elements.\n", ID);

	// reporting a warning message
	Log::warning("ID of the \"%s\" file: %d.\n", file_name, ID);

	// reporting a fatal error message to the log file and closing the application (Windows only)
	Log::fatal("FATAL ERROR reading \"%s\" file!\n", file_name);


```


### Handling Events


You can [subscribe for events](#getEventMessage_Event) to define custom actions on various types of messages printed to the *Log*. The signature of the handler function must be as follows:


```cpp
void handler_function_name(const char * message_text);
```


Here is an example of tracking error messages via event handlers:


```cpp
void error_handler(const char * message_text)
{
	std::cout<<"My message is: "<<message_text<<std::endl;
    // ...
}

// somewhere in the code

// subscribing for the Error event with our handler function
Log::getEventError().connect(error_handler);

// printing an error message to the Log
Log::error("An ERROR has occurred!\n");

```


## Log Class

### Members

## void setDialogFatalEnabled ( bool enabled )

Sets a new value indicating if displaying *Fatal* dialog messages is enabled (when disabled, the corresponding message will be printed to the log).
Can be used, for example, to disable when running console tools like *[Runtimes Generator](../../../tools/runtimes_generator/index.md)* or *[Build Tool](../../../editor2/projects/build_project.md#console_build)* (use the `-dialog_fatal_enabled` command).


> **Notice:** Available for Windows OS only.

### Arguments

- *bool* **enabled** - Set **true** to enable displaying *Fatal* dialog messages; **false** - to disable it.

## bool isDialogFatalEnabled () const

Returns the current value indicating if displaying *Fatal* dialog messages is enabled (when disabled, the corresponding message will be printed to the log).
Can be used, for example, to disable when running console tools like *[Runtimes Generator](../../../tools/runtimes_generator/index.md)* or *[Build Tool](../../../editor2/projects/build_project.md#console_build)* (use the `-dialog_fatal_enabled` command).


> **Notice:** Available for Windows OS only.

### Return value

**true** if displaying *Fatal* dialog messages is enabled ; otherwise **false**.
## Event<const char*> getEventMessage () const

event triggered when a message has been printed to the log. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

<details>
<summary>See Example | Close</summary>

**Usage Example**


```cpp
// implement the Message event handler
void message_event_handler(const char * text)
{
	// Handling Message event...
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections message_event_connections;

// link to this instance when subscribing for an event (subscription for various events can be linked)
Log::getEventMessage().connect(message_event_connections, message_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Log::getEventMessage().connect(message_event_connections, [](const char * text) {
		// Handling Message event (lambda)...
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
message_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection message_event_connection;

// subscribe for the Message event with a handler function keeping the connection
Log::getEventMessage().connect(message_event_connection, message_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
message_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
message_event_connection.setEnabled(true);

// ...

// remove subscription for the Message event via the connection
message_event_connection.disconnect();

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

	// A Message event handler implemented as a class member
	void event_handler(const char * text)
	{
		// Handling Message event...
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Log::getEventMessage().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//  4. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe for the Message event with a handler function
Log::getEventMessage().connect(message_event_handler);

// remove subscription for the Message event later by the handler function
Log::getEventMessage().disconnect(message_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   5. Subscribe to an event saving an ID and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////

// define a connection ID to be used to unsubscribe later
EventConnectionId message_handler_id;

// subscribe for the Message event with a lambda handler function and keeping connection ID
message_handler_id = Log::getEventMessage().connect([](const char * text) {
		// Handling Message event (lambda)...
	}
);

// remove the subscription later using the ID
Log::getEventMessage().disconnect(message_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   6. Ignoring all Message events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Log::getEventMessage().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Log::getEventMessage().setEnabled(true);
```

</details>


> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const char * **text**)*
### Return value

Event instance.
## Event<const char*> getEventWarning () const

event triggered when a warning has been printed to the log. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

<details>
<summary>See Example | Close</summary>

**Usage Example**


```cpp
// implement the Warning event handler
void warning_event_handler(const char * text)
{
	// Handling Warning event...
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections warning_event_connections;

// link to this instance when subscribing for an event (subscription for various events can be linked)
Log::getEventWarning().connect(warning_event_connections, warning_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Log::getEventWarning().connect(warning_event_connections, [](const char * text) {
		// Handling Warning event (lambda)...
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
warning_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection warning_event_connection;

// subscribe for the Warning event with a handler function keeping the connection
Log::getEventWarning().connect(warning_event_connection, warning_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
warning_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
warning_event_connection.setEnabled(true);

// ...

// remove subscription for the Warning event via the connection
warning_event_connection.disconnect();

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

	// A Warning event handler implemented as a class member
	void event_handler(const char * text)
	{
		// Handling Warning event...
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Log::getEventWarning().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//  4. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe for the Warning event with a handler function
Log::getEventWarning().connect(warning_event_handler);

// remove subscription for the Warning event later by the handler function
Log::getEventWarning().disconnect(warning_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   5. Subscribe to an event saving an ID and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////

// define a connection ID to be used to unsubscribe later
EventConnectionId warning_handler_id;

// subscribe for the Warning event with a lambda handler function and keeping connection ID
warning_handler_id = Log::getEventWarning().connect([](const char * text) {
		// Handling Warning event (lambda)...
	}
);

// remove the subscription later using the ID
Log::getEventWarning().disconnect(warning_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   6. Ignoring all Warning events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Log::getEventWarning().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Log::getEventWarning().setEnabled(true);
```

</details>


> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const char * **text**)*
### Return value

Event instance.
## Event<const char*> getEventError () const

event triggered when an error message has been printed to the log. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

<details>
<summary>See Example | Close</summary>

**Usage Example**


```cpp
// implement the Error event handler
void error_event_handler(const char * text)
{
	// Handling Error event...
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections error_event_connections;

// link to this instance when subscribing for an event (subscription for various events can be linked)
Log::getEventError().connect(error_event_connections, error_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Log::getEventError().connect(error_event_connections, [](const char * text) {
		// Handling Error event (lambda)...
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
error_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection error_event_connection;

// subscribe for the Error event with a handler function keeping the connection
Log::getEventError().connect(error_event_connection, error_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
error_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
error_event_connection.setEnabled(true);

// ...

// remove subscription for the Error event via the connection
error_event_connection.disconnect();

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

	// A Error event handler implemented as a class member
	void event_handler(const char * text)
	{
		// Handling Error event...
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Log::getEventError().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//  4. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe for the Error event with a handler function
Log::getEventError().connect(error_event_handler);

// remove subscription for the Error event later by the handler function
Log::getEventError().disconnect(error_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   5. Subscribe to an event saving an ID and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////

// define a connection ID to be used to unsubscribe later
EventConnectionId error_handler_id;

// subscribe for the Error event with a lambda handler function and keeping connection ID
error_handler_id = Log::getEventError().connect([](const char * text) {
		// Handling Error event (lambda)...
	}
);

// remove the subscription later using the ID
Log::getEventError().disconnect(error_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   6. Ignoring all Error events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Log::getEventError().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Log::getEventError().setEnabled(true);
```

</details>


> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const char * **text**)*
### Return value

Event instance.
## Event<const char*> getEventFatal () const

event triggered when a fatal error message has been printed to the log. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

<details>
<summary>See Example | Close</summary>

**Usage Example**


```cpp
// implement the Fatal event handler
void fatal_event_handler(const char * text)
{
	// Handling Fatal event...
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections fatal_event_connections;

// link to this instance when subscribing for an event (subscription for various events can be linked)
Log::getEventFatal().connect(fatal_event_connections, fatal_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Log::getEventFatal().connect(fatal_event_connections, [](const char * text) {
		// Handling Fatal event (lambda)...
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
fatal_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection fatal_event_connection;

// subscribe for the Fatal event with a handler function keeping the connection
Log::getEventFatal().connect(fatal_event_connection, fatal_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
fatal_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
fatal_event_connection.setEnabled(true);

// ...

// remove subscription for the Fatal event via the connection
fatal_event_connection.disconnect();

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

	// A Fatal event handler implemented as a class member
	void event_handler(const char * text)
	{
		// Handling Fatal event...
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Log::getEventFatal().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//  4. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe for the Fatal event with a handler function
Log::getEventFatal().connect(fatal_event_handler);

// remove subscription for the Fatal event later by the handler function
Log::getEventFatal().disconnect(fatal_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   5. Subscribe to an event saving an ID and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////

// define a connection ID to be used to unsubscribe later
EventConnectionId fatal_handler_id;

// subscribe for the Fatal event with a lambda handler function and keeping connection ID
fatal_handler_id = Log::getEventFatal().connect([](const char * text) {
		// Handling Fatal event (lambda)...
	}
);

// remove the subscription later using the ID
Log::getEventFatal().disconnect(fatal_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   6. Ignoring all Fatal events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Log::getEventFatal().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Log::getEventFatal().setEnabled(true);
```

</details>


> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.


> **Notice:** Available for Windows OS only.

The event handler signature is as follows: *myhandler(const char * **text**)*
### Return value

Event instance.
---

## void error ( const char * format , ... )

Prints an error message to the console and the log file.
### Arguments

- *const char ** **format** - Error message to print.
- *...*  - Arguments, multiple allowed.

## void fatal ( const char * format , ... )

Prints a fatal error message to the log file and quits the engine.

> **Notice:** Available for Windows OS only.

### Arguments

- *const char ** **format** - Fatal error message to print.
- *...*  - Arguments, multiple allowed.

## void message ( const char * format , ... )

Prints a message to the console and the log file.
### Arguments

- *const char ** **format** - Message to print.
- *...*  - Arguments, multiple allowed.

## void warning ( const char * format , ... )

Prints a warning to the console and the log file.
### Arguments

- *const char ** **format** - Warning to print.
- *...*  - Arguments, multiple allowed.
