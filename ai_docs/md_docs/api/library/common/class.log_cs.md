# Unigine::Log Class (CS)


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


```csharp
// auxiliary variables for messages
string file_name = "file.txt";
int ID = 10;

// reporting an error message
Log.Error("Loading mesh: can't open \"{0}\" file\n", file_name);

// reporting a message
Log.Message("-> Added {0} UI elements.\n", ID);

// reporting a warning message
Log.Warning("ID of the \"{0}\" file: {1}.\n", file_name, ID);

// reporting a fatal error message to the log file and closing the application (Windows only)
Log.Fatal("FATAL ERROR reading \"{0}\" file!\n", file_name);


```


### Handling Events


You can [subscribe for events](#getEventMessage_Event) to define custom actions on various types of messages printed to the Log. The signature of the handler function must be as follows:


```csharp
void handler_function_name(string message_text);
```


Here is an example of tracking error messages via event handlers:


```csharp
public void error_handler(string message_text)
{
	Unigine.Console.MessageLine("The following error message has been printed: \"{0}\".", message_text);
	// ...
}

// somewhere in the code

// setting our callback function on an error message
Log.EventError.Connect(error_callback);

// printing an error message to the Log
Log.Error("An ERROR has occurred!");

```


## Log Class

### Properties

## bool DialogFatalEnabled

The value indicating if displaying *Fatal* dialog messages is enabled (when disabled, the corresponding message will be printed to the log).
Can be used, for example, to disable when running console tools like *[Runtimes Generator](../../../tools/runtimes_generator/index.md)* or *[Build Tool](../../../editor2/projects/build_project.md#console_build)* (use the `-dialog_fatal_enabled` command).


> **Notice:** Available for Windows OS only.

## 🔒︎ Event<string> EventMessage

The event triggered when a message has been printed to the log. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

<details>
<summary>See Example | Close</summary>

**Usage Example**


```csharp
// implement the Message event handler
void message_handler(string text)
{
	// Handling Message event...
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections message_event_connections = new EventConnections();

// link to this instance when subscribing for an event (subscription for various events can be linked)
Log.EventMessage.Connect(message_event_connections, message_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Log.EventMessage.Connect(message_event_connections, (string text) => {
		Log.Message("Handling Message event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
message_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe for the Message event with a handler function
Log.EventMessage.Connect(message_event_handler);

// remove subscription for the Message event later by the handler function
Log.EventMessage.Disconnect(message_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection message_event_connection;

// subscribe for the Message event with a lambda handler function and keeping the connection
message_event_connection = Log.EventMessage.Connect((string text) => {
		Log.Message("Handling Message event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
message_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
leave_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
message_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Message events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Log.EventMessage.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Log.EventMessage.Enabled = true;
```

</details>


> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(string **text**)*
## 🔒︎ Event<string> EventWarning

The event triggered when a warning has been printed to the log. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

<details>
<summary>See Example | Close</summary>

**Usage Example**


```csharp
// implement the Warning event handler
void warning_handler(string text)
{
	// Handling Warning event...
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections warning_event_connections = new EventConnections();

// link to this instance when subscribing for an event (subscription for various events can be linked)
Log.EventWarning.Connect(warning_event_connections, warning_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Log.EventWarning.Connect(warning_event_connections, (string text) => {
		Log.Message("Handling Warning event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
warning_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe for the Warning event with a handler function
Log.EventWarning.Connect(warning_event_handler);

// remove subscription for the Warning event later by the handler function
Log.EventWarning.Disconnect(warning_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection warning_event_connection;

// subscribe for the Warning event with a lambda handler function and keeping the connection
warning_event_connection = Log.EventWarning.Connect((string text) => {
		Log.Message("Handling Warning event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
warning_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
leave_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
warning_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Warning events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Log.EventWarning.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Log.EventWarning.Enabled = true;
```

</details>


> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(string **text**)*
## 🔒︎ Event<const char *> EventError

The event triggered when an error message has been printed to the log. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

<details>
<summary>See Example | Close</summary>

**Usage Example**


```csharp
// implement the Error event handler
void error_handler(string text)
{
	// Handling Error event...
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections error_event_connections = new EventConnections();

// link to this instance when subscribing for an event (subscription for various events can be linked)
Log.EventError.Connect(error_event_connections, error_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Log.EventError.Connect(error_event_connections, (string text) => {
		Log.Message("Handling Error event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
error_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe for the Error event with a handler function
Log.EventError.Connect(error_event_handler);

// remove subscription for the Error event later by the handler function
Log.EventError.Disconnect(error_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection error_event_connection;

// subscribe for the Error event with a lambda handler function and keeping the connection
error_event_connection = Log.EventError.Connect((string text) => {
		Log.Message("Handling Error event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
error_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
leave_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
error_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Error events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Log.EventError.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Log.EventError.Enabled = true;
```

</details>


> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(string **text**)*
## 🔒︎ Event<const char *> EventFatal

The event triggered when a fatal error message has been printed to the log. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

<details>
<summary>See Example | Close</summary>

**Usage Example**


```csharp
// implement the Fatal event handler
void fatal_handler(string text)
{
	// Handling Fatal event...
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections fatal_event_connections = new EventConnections();

// link to this instance when subscribing for an event (subscription for various events can be linked)
Log.EventFatal.Connect(fatal_event_connections, fatal_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Log.EventFatal.Connect(fatal_event_connections, (string text) => {
		Log.Message("Handling Fatal event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
fatal_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe for the Fatal event with a handler function
Log.EventFatal.Connect(fatal_event_handler);

// remove subscription for the Fatal event later by the handler function
Log.EventFatal.Disconnect(fatal_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection fatal_event_connection;

// subscribe for the Fatal event with a lambda handler function and keeping the connection
fatal_event_connection = Log.EventFatal.Connect((string text) => {
		Log.Message("Handling Fatal event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
fatal_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
leave_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
fatal_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Fatal events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Log.EventFatal.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Log.EventFatal.Enabled = true;
```

</details>


> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.


> **Notice:** Available for Windows OS only.

The event handler signature is as follows: *myhandler(string **text**)*
### Members

---

## void Error ( string format , ... )

Prints an error message to the console and the log file.
### Arguments

- *string* **format** - Error message to print.
- *...*  - Arguments, multiple allowed.

## void ErrorLine ( formating format , ... )

Prints an error message followed by the line terminator to the console and the log file.
### Arguments

- *formating* **format** - Error message to print.
- *...*  - Arguments, multiple allowed.

## void Fatal ( string format , ... )

Prints a fatal error message to the log file and quits the engine.

> **Notice:** Available for Windows OS only.

### Arguments

- *string* **format** - Fatal error message to print.
- *...*  - Arguments, multiple allowed.

## void FatalLine ( string format , ... )

Prints a fatal error message followed by the line terminator to the log file and quits the engine.

> **Notice:** Available for Windows OS only.

### Arguments

- *string* **format** - Fatal error message to print.
- *...*  - Arguments, multiple allowed.

## void Message ( string format , ... )

Prints a message to the console and the log file.
### Arguments

- *string* **format** - Message to print.
- *...*  - Arguments, multiple allowed.

## void MessageLine ( string format , ... )

Prints a message followed by the line terminator to the console and the log file.
### Arguments

- *string* **format** - Message to print.
- *...*  - Arguments, multiple allowed.

## void Warning ( string format , ... )

Prints a warning to the console and the log file.
### Arguments

- *string* **format** - Warning to print.
- *...*  - Arguments, multiple allowed.

## void WarningLine ( string format , ... )

Prints a warning followed by the line terminator to the console and the log file.
### Arguments

- *string* **format** - Warning to print.
- *...*  - Arguments, multiple allowed.
