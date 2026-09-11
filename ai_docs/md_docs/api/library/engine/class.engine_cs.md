# Unigine::Engine Class (CS)


The Engine class is required for the engine [initialization](../../../code/fundamentals/execution_sequence/init.md) and executing the [main loop](../../../code/fundamentals/execution_sequence/main_loop.md) of the program. Also, you can get the engine [startup options](../../../code/command_line.md) through this class.


The **InitParameters** structure provides the way to set the following parameters to initialize a new Engine instance:.


| Parameter | Description |
|---|---|
| **window_title** | Title of the window. |
| **window_icon_path** | Path to the window icon. |
| **app_path** | Path to a directory where binary executable file is stored. |
| **home_path** | Path to the user's home directory. |
| **project** | Project name. |
| **password** | Password for the filesystem archives. |
| **system_proxy** | Instance of the [CustomSystemProxy](../../../api/library/engine/class.customsystemproxy_cs.md) class. |


## Engine Class

### Enums

## BUILD_CONFIG

Engine build configuration.
| Name | Description |
|---|---|
| **BUILD_CONFIG_DEBUG** = 0 | Debug build configuration. |
| **BUILD_CONFIG_DEVELOPMENT** = 1 | Development build configuration. |
| **BUILD_CONFIG_RELEASE** = 2 | Release build configuration. |

## GCMODE

Garbage collection mode. For more information on garbage collection for C# please refer to the [Garbage Collector](../../../code/csharp/garbage_collector.md) article.
| Name | Description |
|---|---|
| **DEFAULT** = 0 | Default C# garbage collector mode. In this case heavy spikes and excessive memory consumption are imminent if you don't manage your objects properly and do not use the *Dispose()* method. |
| **USE_MEMORY_PRESSURE** = 1 | Passes the information about C++ memory consumption to C#. This results in more frequent GC calls preventing the application from eating too much memory right after startup and removing heavy spikes. |
| **EVERY_FRAME** = 2 | The garbage collector is called every frame. This results in overall performance reduction, but removes heavy spikes. |
| **WORLD_SHUTDOWN** = 3 | The garbage collector is called on closing the world. This mode is ideal if the number of memory allocations is your code is insignificant. |

## BACKGROUND_UPDATE

Engine background update mode.
| Name | Description |
|---|---|
| **BACKGROUND_UPDATE_DISABLED** = 0 | Background update is disabled. |
| **BACKGROUND_UPDATE_RENDER_NON_MINIMIZED** = 1 | Background update is enabled (rendering is performed when the window is out of focus, but stops if the window is minimized). |
| **BACKGROUND_UPDATE_RENDER_ALWAYS** = 2 | Background update is always enabled (rendering is performed all the time, regardless of the window state. |

## PRECISION

engine precision type.
| Name | Description |
|---|---|
| **PRECISION_FLOAT** = 0 | Float precision type. |
| **PRECISION_DOUBLE** = 1 | Double precision type. |

### Properties

## 🔒︎ bool IsInitialized

The value indicating whether the engine is initialized.
## 🔒︎ Engine.GCMODE GCMode_

The garbage collection mode.
## 🔒︎ string AppPath

The path to a directory where binary executable file is stored.
## 🔒︎ string DataPath

The path to the data directory.
## 🔒︎ string HomePath

The path to the user's home directory.
## 🔒︎ string SavePath

The path to a directory with the default configuration file, saved files, etc.
## 🔒︎ string CachePath

The path to the directory with cached files.
## 🔒︎ int NumPluginPaths

The number of directory paths to plugins that were set using the [-plugin_path](../../../code/command_line.md#plugin_path) startup command-line option.
## 🔒︎ string SystemScript

The path to the system script.
## 🔒︎ string SystemCache

The path to the system script cache.
## 🔒︎ string EditorCache

The path to the editor script cache.
## 🔒︎ string VideoApp

The graphics API used for rendering.
## 🔒︎ string SoundApp

The sound API used.
## 🔒︎ string ExternDefine

The list of [external definitions](../../../code/command_line.md#extern_define) specified on the application start-up.
## 🔒︎ string Features

The list of features like Direct3D, Microprofile, Geodetic, etc.
## 🔒︎ string Version

The engine version info.
## Engine.BACKGROUND_UPDATE BackgroundUpdate

The value indicating whether the application window is updated when the window is hidden or out of focus (rendering frames in background). By default your UNIGINE application stops rendering frames and updating its main window, when it window goes out of focus (e.g. user switches to another window). Setting the background update mode enables constant rendering regardless of whether the application window is focused or in the background.
## 🔒︎ bool IsActive

The **active** state of the Engine.
## 🔒︎ bool IsFocus

The value showing if any of the Engine windows is in focus.
## 🔒︎ bool IsQuit

The **quitting** flag on engine quit.
## 🔒︎ float TotalTime

The total time (in milliseconds) that both rendering and calculating of the frame took (the duration of the [main loop](../../../code/fundamentals/execution_sequence/main_loop.md) in the application [execution sequence](../../../code/fundamentals/execution_sequence/index.md)). Includes *update, render, swap and wait GPU*.
## 🔒︎ float TotalCPUTime

The total CPU time (in milliseconds) taken to perform calculations for the frame (the duration of the [main loop](../../../code/fundamentals/execution_sequence/main_loop.md) in the application [execution sequence](../../../code/fundamentals/execution_sequence/index.md)). Includes *update, render and swap*.
## 🔒︎ float UpdateTime

The duration (in milliseconds) of the [update phase](../../../code/fundamentals/execution_sequence/main_loop.md#update), during which the objects are prepared for their collision response to be calculated.
## 🔒︎ float RenderTime

The time (in milliseconds) required to prepare all data to be rendered in the current frame and feed rendering commands from the CPU to the GPU. See the [Profiler](../../../tools/profiling/profiler/index.md#render_cpu) article for details.
## 🔒︎ float PresentTime

The total time (in milliseconds) spent on waiting for the GPU after all calculations on the CPU are completed. See the [Profiler](../../../tools/profiling/profiler/index.md#present) article for details.
## 🔒︎ float InterfaceTime

The total accumulative time (in milliseconds) spent on rendering GUI widgets.
## 🔒︎ Int64 Frame

The number of the current engine frame.
## 🔒︎ float Fps

The value of the Engine FPS counter.
## 🔒︎ float IFps

The inverse value of the Engine FPS counter (1/FPS).
## 🔒︎ float StatisticsFpsMin

The minimum FPS counter value for the last 600 frames.
## 🔒︎ float StatisticsFpsAvg

The average FPS counter value for the last 600 frames.
## 🔒︎ float StatisticsFpsMax

The maximum FPS counter value for the last 600 frames.
## 🔒︎ bool MainThread

The value indicating if the current thread is main.
## 🔒︎ Player MainPlayer

The main player.
## 🔒︎ bool Evaluation

The value indicating if the running version of the Engine is for evaluation only.
## 🔒︎ int NumEditorLogics

The number of [EditorLogic](../../../api/library/common/logic/class.editorlogic_cs.md) instances.
## 🔒︎ int NumWorldLogics

The number of [WorldLogic](../../../api/library/common/logic/class.worldlogic_cs.md) instances.
## 🔒︎ int NumSystemLogics

The number of [SystemLogic](../../../api/library/common/logic/class.systemlogic_cs.md) instances.
## 🔒︎ int NumArgs

The number of command line arguments.
## 🔒︎ int NumPlugins

The number of loaded plugins.
## 🔒︎ Engine.PRECISION Precision

The precision type.
## 🔒︎ Event EventBeginUpdate

The event triggered before the update stage is started. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginUpdate event handler
void beginupdate_event_handler()
{
	Log.Message("\Handling BeginUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventBeginUpdate.Connect(beginupdate_event_connections, beginupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventBeginUpdate.Connect(beginupdate_event_connections, () => {
		Log.Message("Handling BeginUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginUpdate event with a handler function
Engine.EventBeginUpdate.Connect(beginupdate_event_handler);

// remove subscription to the BeginUpdate event later by the handler function
Engine.EventBeginUpdate.Disconnect(beginupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginupdate_event_connection;

// subscribe to the BeginUpdate event with a lambda handler function and keeping the connection
beginupdate_event_connection = Engine.EventBeginUpdate.Connect(() => {
		Log.Message("Handling BeginUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventBeginUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventBeginUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginPropertiesUpdate

The event triggered before the properties update stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginPropertiesUpdate event handler
void beginpropertiesupdate_event_handler()
{
	Log.Message("\Handling BeginPropertiesUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginpropertiesupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventBeginPropertiesUpdate.Connect(beginpropertiesupdate_event_connections, beginpropertiesupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventBeginPropertiesUpdate.Connect(beginpropertiesupdate_event_connections, () => {
		Log.Message("Handling BeginPropertiesUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginpropertiesupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginPropertiesUpdate event with a handler function
Engine.EventBeginPropertiesUpdate.Connect(beginpropertiesupdate_event_handler);

// remove subscription to the BeginPropertiesUpdate event later by the handler function
Engine.EventBeginPropertiesUpdate.Disconnect(beginpropertiesupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginpropertiesupdate_event_connection;

// subscribe to the BeginPropertiesUpdate event with a lambda handler function and keeping the connection
beginpropertiesupdate_event_connection = Engine.EventBeginPropertiesUpdate.Connect(() => {
		Log.Message("Handling BeginPropertiesUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginpropertiesupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginpropertiesupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginpropertiesupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginPropertiesUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventBeginPropertiesUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventBeginPropertiesUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventEndPropertiesUpdate

The event triggered after the properties update stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndPropertiesUpdate event handler
void endpropertiesupdate_event_handler()
{
	Log.Message("\Handling EndPropertiesUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endpropertiesupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventEndPropertiesUpdate.Connect(endpropertiesupdate_event_connections, endpropertiesupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventEndPropertiesUpdate.Connect(endpropertiesupdate_event_connections, () => {
		Log.Message("Handling EndPropertiesUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endpropertiesupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndPropertiesUpdate event with a handler function
Engine.EventEndPropertiesUpdate.Connect(endpropertiesupdate_event_handler);

// remove subscription to the EndPropertiesUpdate event later by the handler function
Engine.EventEndPropertiesUpdate.Disconnect(endpropertiesupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endpropertiesupdate_event_connection;

// subscribe to the EndPropertiesUpdate event with a lambda handler function and keeping the connection
endpropertiesupdate_event_connection = Engine.EventEndPropertiesUpdate.Connect(() => {
		Log.Message("Handling EndPropertiesUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endpropertiesupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endpropertiesupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endpropertiesupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndPropertiesUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventEndPropertiesUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventEndPropertiesUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginInputUpdate

The event triggered before the input update stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginInputUpdate event handler
void begininputupdate_event_handler()
{
	Log.Message("\Handling BeginInputUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begininputupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventBeginInputUpdate.Connect(begininputupdate_event_connections, begininputupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventBeginInputUpdate.Connect(begininputupdate_event_connections, () => {
		Log.Message("Handling BeginInputUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
begininputupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginInputUpdate event with a handler function
Engine.EventBeginInputUpdate.Connect(begininputupdate_event_handler);

// remove subscription to the BeginInputUpdate event later by the handler function
Engine.EventBeginInputUpdate.Disconnect(begininputupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection begininputupdate_event_connection;

// subscribe to the BeginInputUpdate event with a lambda handler function and keeping the connection
begininputupdate_event_connection = Engine.EventBeginInputUpdate.Connect(() => {
		Log.Message("Handling BeginInputUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
begininputupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
begininputupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
begininputupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginInputUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventBeginInputUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventBeginInputUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventEndInputUpdate

The event triggered after the input update stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndInputUpdate event handler
void endinputupdate_event_handler()
{
	Log.Message("\Handling EndInputUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endinputupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventEndInputUpdate.Connect(endinputupdate_event_connections, endinputupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventEndInputUpdate.Connect(endinputupdate_event_connections, () => {
		Log.Message("Handling EndInputUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endinputupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndInputUpdate event with a handler function
Engine.EventEndInputUpdate.Connect(endinputupdate_event_handler);

// remove subscription to the EndInputUpdate event later by the handler function
Engine.EventEndInputUpdate.Disconnect(endinputupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endinputupdate_event_connection;

// subscribe to the EndInputUpdate event with a lambda handler function and keeping the connection
endinputupdate_event_connection = Engine.EventEndInputUpdate.Connect(() => {
		Log.Message("Handling EndInputUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endinputupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endinputupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endinputupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndInputUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventEndInputUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventEndInputUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginControlsUpdate

The event triggered before the controls update stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginControlsUpdate event handler
void begincontrolsupdate_event_handler()
{
	Log.Message("\Handling BeginControlsUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begincontrolsupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventBeginControlsUpdate.Connect(begincontrolsupdate_event_connections, begincontrolsupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventBeginControlsUpdate.Connect(begincontrolsupdate_event_connections, () => {
		Log.Message("Handling BeginControlsUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
begincontrolsupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginControlsUpdate event with a handler function
Engine.EventBeginControlsUpdate.Connect(begincontrolsupdate_event_handler);

// remove subscription to the BeginControlsUpdate event later by the handler function
Engine.EventBeginControlsUpdate.Disconnect(begincontrolsupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection begincontrolsupdate_event_connection;

// subscribe to the BeginControlsUpdate event with a lambda handler function and keeping the connection
begincontrolsupdate_event_connection = Engine.EventBeginControlsUpdate.Connect(() => {
		Log.Message("Handling BeginControlsUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
begincontrolsupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
begincontrolsupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
begincontrolsupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginControlsUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventBeginControlsUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventBeginControlsUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventEndControlsUpdate

The event triggered after the controls update stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndControlsUpdate event handler
void endcontrolsupdate_event_handler()
{
	Log.Message("\Handling EndControlsUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endcontrolsupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventEndControlsUpdate.Connect(endcontrolsupdate_event_connections, endcontrolsupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventEndControlsUpdate.Connect(endcontrolsupdate_event_connections, () => {
		Log.Message("Handling EndControlsUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endcontrolsupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndControlsUpdate event with a handler function
Engine.EventEndControlsUpdate.Connect(endcontrolsupdate_event_handler);

// remove subscription to the EndControlsUpdate event later by the handler function
Engine.EventEndControlsUpdate.Disconnect(endcontrolsupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endcontrolsupdate_event_connection;

// subscribe to the EndControlsUpdate event with a lambda handler function and keeping the connection
endcontrolsupdate_event_connection = Engine.EventEndControlsUpdate.Connect(() => {
		Log.Message("Handling EndControlsUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endcontrolsupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endcontrolsupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endcontrolsupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndControlsUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventEndControlsUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventEndControlsUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginWorldManagerUpdate

The event triggered before the world manager update stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginWorldManagerUpdate event handler
void beginworldmanagerupdate_event_handler()
{
	Log.Message("\Handling BeginWorldManagerUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginworldmanagerupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventBeginWorldManagerUpdate.Connect(beginworldmanagerupdate_event_connections, beginworldmanagerupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventBeginWorldManagerUpdate.Connect(beginworldmanagerupdate_event_connections, () => {
		Log.Message("Handling BeginWorldManagerUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginworldmanagerupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginWorldManagerUpdate event with a handler function
Engine.EventBeginWorldManagerUpdate.Connect(beginworldmanagerupdate_event_handler);

// remove subscription to the BeginWorldManagerUpdate event later by the handler function
Engine.EventBeginWorldManagerUpdate.Disconnect(beginworldmanagerupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginworldmanagerupdate_event_connection;

// subscribe to the BeginWorldManagerUpdate event with a lambda handler function and keeping the connection
beginworldmanagerupdate_event_connection = Engine.EventBeginWorldManagerUpdate.Connect(() => {
		Log.Message("Handling BeginWorldManagerUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginworldmanagerupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginworldmanagerupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginworldmanagerupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginWorldManagerUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventBeginWorldManagerUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventBeginWorldManagerUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventEndWorldManagerUpdate

The event triggered after the world manager update stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndWorldManagerUpdate event handler
void endworldmanagerupdate_event_handler()
{
	Log.Message("\Handling EndWorldManagerUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endworldmanagerupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventEndWorldManagerUpdate.Connect(endworldmanagerupdate_event_connections, endworldmanagerupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventEndWorldManagerUpdate.Connect(endworldmanagerupdate_event_connections, () => {
		Log.Message("Handling EndWorldManagerUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endworldmanagerupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndWorldManagerUpdate event with a handler function
Engine.EventEndWorldManagerUpdate.Connect(endworldmanagerupdate_event_handler);

// remove subscription to the EndWorldManagerUpdate event later by the handler function
Engine.EventEndWorldManagerUpdate.Disconnect(endworldmanagerupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endworldmanagerupdate_event_connection;

// subscribe to the EndWorldManagerUpdate event with a lambda handler function and keeping the connection
endworldmanagerupdate_event_connection = Engine.EventEndWorldManagerUpdate.Connect(() => {
		Log.Message("Handling EndWorldManagerUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endworldmanagerupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endworldmanagerupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endworldmanagerupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndWorldManagerUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventEndWorldManagerUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventEndWorldManagerUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginSoundManagerUpdate

The event triggered before the sound manager update stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginSoundManagerUpdate event handler
void beginsoundmanagerupdate_event_handler()
{
	Log.Message("\Handling BeginSoundManagerUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginsoundmanagerupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventBeginSoundManagerUpdate.Connect(beginsoundmanagerupdate_event_connections, beginsoundmanagerupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventBeginSoundManagerUpdate.Connect(beginsoundmanagerupdate_event_connections, () => {
		Log.Message("Handling BeginSoundManagerUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginsoundmanagerupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginSoundManagerUpdate event with a handler function
Engine.EventBeginSoundManagerUpdate.Connect(beginsoundmanagerupdate_event_handler);

// remove subscription to the BeginSoundManagerUpdate event later by the handler function
Engine.EventBeginSoundManagerUpdate.Disconnect(beginsoundmanagerupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginsoundmanagerupdate_event_connection;

// subscribe to the BeginSoundManagerUpdate event with a lambda handler function and keeping the connection
beginsoundmanagerupdate_event_connection = Engine.EventBeginSoundManagerUpdate.Connect(() => {
		Log.Message("Handling BeginSoundManagerUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginsoundmanagerupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginsoundmanagerupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginsoundmanagerupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginSoundManagerUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventBeginSoundManagerUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventBeginSoundManagerUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventEndSoundManagerUpdate

The event triggered after the sound manager update stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndSoundManagerUpdate event handler
void endsoundmanagerupdate_event_handler()
{
	Log.Message("\Handling EndSoundManagerUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endsoundmanagerupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventEndSoundManagerUpdate.Connect(endsoundmanagerupdate_event_connections, endsoundmanagerupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventEndSoundManagerUpdate.Connect(endsoundmanagerupdate_event_connections, () => {
		Log.Message("Handling EndSoundManagerUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endsoundmanagerupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndSoundManagerUpdate event with a handler function
Engine.EventEndSoundManagerUpdate.Connect(endsoundmanagerupdate_event_handler);

// remove subscription to the EndSoundManagerUpdate event later by the handler function
Engine.EventEndSoundManagerUpdate.Disconnect(endsoundmanagerupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endsoundmanagerupdate_event_connection;

// subscribe to the EndSoundManagerUpdate event with a lambda handler function and keeping the connection
endsoundmanagerupdate_event_connection = Engine.EventEndSoundManagerUpdate.Connect(() => {
		Log.Message("Handling EndSoundManagerUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endsoundmanagerupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endsoundmanagerupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endsoundmanagerupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndSoundManagerUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventEndSoundManagerUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventEndSoundManagerUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginGameUpdate

The event triggered before the game logic update stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginGameUpdate event handler
void begingameupdate_event_handler()
{
	Log.Message("\Handling BeginGameUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begingameupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventBeginGameUpdate.Connect(begingameupdate_event_connections, begingameupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventBeginGameUpdate.Connect(begingameupdate_event_connections, () => {
		Log.Message("Handling BeginGameUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
begingameupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginGameUpdate event with a handler function
Engine.EventBeginGameUpdate.Connect(begingameupdate_event_handler);

// remove subscription to the BeginGameUpdate event later by the handler function
Engine.EventBeginGameUpdate.Disconnect(begingameupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection begingameupdate_event_connection;

// subscribe to the BeginGameUpdate event with a lambda handler function and keeping the connection
begingameupdate_event_connection = Engine.EventBeginGameUpdate.Connect(() => {
		Log.Message("Handling BeginGameUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
begingameupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
begingameupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
begingameupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginGameUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventBeginGameUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventBeginGameUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventEndGameUpdate

The event triggered after the game logic update stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndGameUpdate event handler
void endgameupdate_event_handler()
{
	Log.Message("\Handling EndGameUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endgameupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventEndGameUpdate.Connect(endgameupdate_event_connections, endgameupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventEndGameUpdate.Connect(endgameupdate_event_connections, () => {
		Log.Message("Handling EndGameUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endgameupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndGameUpdate event with a handler function
Engine.EventEndGameUpdate.Connect(endgameupdate_event_handler);

// remove subscription to the EndGameUpdate event later by the handler function
Engine.EventEndGameUpdate.Disconnect(endgameupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endgameupdate_event_connection;

// subscribe to the EndGameUpdate event with a lambda handler function and keeping the connection
endgameupdate_event_connection = Engine.EventEndGameUpdate.Connect(() => {
		Log.Message("Handling EndGameUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endgameupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endgameupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endgameupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndGameUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventEndGameUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventEndGameUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginRenderUpdate

The event triggered before the render functions update stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginRenderUpdate event handler
void beginrenderupdate_event_handler()
{
	Log.Message("\Handling BeginRenderUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginrenderupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventBeginRenderUpdate.Connect(beginrenderupdate_event_connections, beginrenderupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventBeginRenderUpdate.Connect(beginrenderupdate_event_connections, () => {
		Log.Message("Handling BeginRenderUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginrenderupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginRenderUpdate event with a handler function
Engine.EventBeginRenderUpdate.Connect(beginrenderupdate_event_handler);

// remove subscription to the BeginRenderUpdate event later by the handler function
Engine.EventBeginRenderUpdate.Disconnect(beginrenderupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginrenderupdate_event_connection;

// subscribe to the BeginRenderUpdate event with a lambda handler function and keeping the connection
beginrenderupdate_event_connection = Engine.EventBeginRenderUpdate.Connect(() => {
		Log.Message("Handling BeginRenderUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginrenderupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginrenderupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginrenderupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginRenderUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventBeginRenderUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventBeginRenderUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventEndRenderUpdate

The event triggered after the render functions update stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndRenderUpdate event handler
void endrenderupdate_event_handler()
{
	Log.Message("\Handling EndRenderUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endrenderupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventEndRenderUpdate.Connect(endrenderupdate_event_connections, endrenderupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventEndRenderUpdate.Connect(endrenderupdate_event_connections, () => {
		Log.Message("Handling EndRenderUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endrenderupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndRenderUpdate event with a handler function
Engine.EventEndRenderUpdate.Connect(endrenderupdate_event_handler);

// remove subscription to the EndRenderUpdate event later by the handler function
Engine.EventEndRenderUpdate.Disconnect(endrenderupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endrenderupdate_event_connection;

// subscribe to the EndRenderUpdate event with a lambda handler function and keeping the connection
endrenderupdate_event_connection = Engine.EventEndRenderUpdate.Connect(() => {
		Log.Message("Handling EndRenderUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endrenderupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endrenderupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endrenderupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndRenderUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventEndRenderUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventEndRenderUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginExpressionUpdate

The event triggered before the expressions update stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginExpressionUpdate event handler
void beginexpressionupdate_event_handler()
{
	Log.Message("\Handling BeginExpressionUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginexpressionupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventBeginExpressionUpdate.Connect(beginexpressionupdate_event_connections, beginexpressionupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventBeginExpressionUpdate.Connect(beginexpressionupdate_event_connections, () => {
		Log.Message("Handling BeginExpressionUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginexpressionupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginExpressionUpdate event with a handler function
Engine.EventBeginExpressionUpdate.Connect(beginexpressionupdate_event_handler);

// remove subscription to the BeginExpressionUpdate event later by the handler function
Engine.EventBeginExpressionUpdate.Disconnect(beginexpressionupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginexpressionupdate_event_connection;

// subscribe to the BeginExpressionUpdate event with a lambda handler function and keeping the connection
beginexpressionupdate_event_connection = Engine.EventBeginExpressionUpdate.Connect(() => {
		Log.Message("Handling BeginExpressionUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginexpressionupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginexpressionupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginexpressionupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginExpressionUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventBeginExpressionUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventBeginExpressionUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventEndExpressionUpdate

The event triggered after the expressions update stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndExpressionUpdate event handler
void endexpressionupdate_event_handler()
{
	Log.Message("\Handling EndExpressionUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endexpressionupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventEndExpressionUpdate.Connect(endexpressionupdate_event_connections, endexpressionupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventEndExpressionUpdate.Connect(endexpressionupdate_event_connections, () => {
		Log.Message("Handling EndExpressionUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endexpressionupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndExpressionUpdate event with a handler function
Engine.EventEndExpressionUpdate.Connect(endexpressionupdate_event_handler);

// remove subscription to the EndExpressionUpdate event later by the handler function
Engine.EventEndExpressionUpdate.Disconnect(endexpressionupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endexpressionupdate_event_connection;

// subscribe to the EndExpressionUpdate event with a lambda handler function and keeping the connection
endexpressionupdate_event_connection = Engine.EventEndExpressionUpdate.Connect(() => {
		Log.Message("Handling EndExpressionUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endexpressionupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endexpressionupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endexpressionupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndExpressionUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventEndExpressionUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventEndExpressionUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginSoundsUpdate

The event triggered before the sounds update stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginSoundsUpdate event handler
void beginsoundsupdate_event_handler()
{
	Log.Message("\Handling BeginSoundsUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginsoundsupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventBeginSoundsUpdate.Connect(beginsoundsupdate_event_connections, beginsoundsupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventBeginSoundsUpdate.Connect(beginsoundsupdate_event_connections, () => {
		Log.Message("Handling BeginSoundsUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginsoundsupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginSoundsUpdate event with a handler function
Engine.EventBeginSoundsUpdate.Connect(beginsoundsupdate_event_handler);

// remove subscription to the BeginSoundsUpdate event later by the handler function
Engine.EventBeginSoundsUpdate.Disconnect(beginsoundsupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginsoundsupdate_event_connection;

// subscribe to the BeginSoundsUpdate event with a lambda handler function and keeping the connection
beginsoundsupdate_event_connection = Engine.EventBeginSoundsUpdate.Connect(() => {
		Log.Message("Handling BeginSoundsUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginsoundsupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginsoundsupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginsoundsupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginSoundsUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventBeginSoundsUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventBeginSoundsUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventEndSoundsUpdate

The event triggered after the sounds update stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndSoundsUpdate event handler
void endsoundsupdate_event_handler()
{
	Log.Message("\Handling EndSoundsUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endsoundsupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventEndSoundsUpdate.Connect(endsoundsupdate_event_connections, endsoundsupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventEndSoundsUpdate.Connect(endsoundsupdate_event_connections, () => {
		Log.Message("Handling EndSoundsUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endsoundsupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndSoundsUpdate event with a handler function
Engine.EventEndSoundsUpdate.Connect(endsoundsupdate_event_handler);

// remove subscription to the EndSoundsUpdate event later by the handler function
Engine.EventEndSoundsUpdate.Disconnect(endsoundsupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endsoundsupdate_event_connection;

// subscribe to the EndSoundsUpdate event with a lambda handler function and keeping the connection
endsoundsupdate_event_connection = Engine.EventEndSoundsUpdate.Connect(() => {
		Log.Message("Handling EndSoundsUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endsoundsupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endsoundsupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endsoundsupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndSoundsUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventEndSoundsUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventEndSoundsUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginPluginsUpdate

The event triggered before the plugins update stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginPluginsUpdate event handler
void beginpluginsupdate_event_handler()
{
	Log.Message("\Handling BeginPluginsUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginpluginsupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventBeginPluginsUpdate.Connect(beginpluginsupdate_event_connections, beginpluginsupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventBeginPluginsUpdate.Connect(beginpluginsupdate_event_connections, () => {
		Log.Message("Handling BeginPluginsUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginpluginsupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginPluginsUpdate event with a handler function
Engine.EventBeginPluginsUpdate.Connect(beginpluginsupdate_event_handler);

// remove subscription to the BeginPluginsUpdate event later by the handler function
Engine.EventBeginPluginsUpdate.Disconnect(beginpluginsupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginpluginsupdate_event_connection;

// subscribe to the BeginPluginsUpdate event with a lambda handler function and keeping the connection
beginpluginsupdate_event_connection = Engine.EventBeginPluginsUpdate.Connect(() => {
		Log.Message("Handling BeginPluginsUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginpluginsupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginpluginsupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginpluginsupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginPluginsUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventBeginPluginsUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventBeginPluginsUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventEndPluginsUpdate

The event triggered after the plugins update stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndPluginsUpdate event handler
void endpluginsupdate_event_handler()
{
	Log.Message("\Handling EndPluginsUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endpluginsupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventEndPluginsUpdate.Connect(endpluginsupdate_event_connections, endpluginsupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventEndPluginsUpdate.Connect(endpluginsupdate_event_connections, () => {
		Log.Message("Handling EndPluginsUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endpluginsupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndPluginsUpdate event with a handler function
Engine.EventEndPluginsUpdate.Connect(endpluginsupdate_event_handler);

// remove subscription to the EndPluginsUpdate event later by the handler function
Engine.EventEndPluginsUpdate.Disconnect(endpluginsupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endpluginsupdate_event_connection;

// subscribe to the EndPluginsUpdate event with a lambda handler function and keeping the connection
endpluginsupdate_event_connection = Engine.EventEndPluginsUpdate.Connect(() => {
		Log.Message("Handling EndPluginsUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endpluginsupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endpluginsupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endpluginsupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndPluginsUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventEndPluginsUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventEndPluginsUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginVRUpdate

The event triggered before the VR update stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginVRUpdate event handler
void beginvrupdate_event_handler()
{
	Log.Message("\Handling BeginVRUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginvrupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventBeginVRUpdate.Connect(beginvrupdate_event_connections, beginvrupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventBeginVRUpdate.Connect(beginvrupdate_event_connections, () => {
		Log.Message("Handling BeginVRUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginvrupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginVRUpdate event with a handler function
Engine.EventBeginVRUpdate.Connect(beginvrupdate_event_handler);

// remove subscription to the BeginVRUpdate event later by the handler function
Engine.EventBeginVRUpdate.Disconnect(beginvrupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginvrupdate_event_connection;

// subscribe to the BeginVRUpdate event with a lambda handler function and keeping the connection
beginvrupdate_event_connection = Engine.EventBeginVRUpdate.Connect(() => {
		Log.Message("Handling BeginVRUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginvrupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginvrupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginvrupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginVRUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventBeginVRUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventBeginVRUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventEndVRUpdate

The event triggered after the VR update stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndVRUpdate event handler
void endvrupdate_event_handler()
{
	Log.Message("\Handling EndVRUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endvrupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventEndVRUpdate.Connect(endvrupdate_event_connections, endvrupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventEndVRUpdate.Connect(endvrupdate_event_connections, () => {
		Log.Message("Handling EndVRUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endvrupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndVRUpdate event with a handler function
Engine.EventEndVRUpdate.Connect(endvrupdate_event_handler);

// remove subscription to the EndVRUpdate event later by the handler function
Engine.EventEndVRUpdate.Disconnect(endvrupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endvrupdate_event_connection;

// subscribe to the EndVRUpdate event with a lambda handler function and keeping the connection
endvrupdate_event_connection = Engine.EventEndVRUpdate.Connect(() => {
		Log.Message("Handling EndVRUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endvrupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endvrupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endvrupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndVRUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventEndVRUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventEndVRUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginEditorUpdate

The event triggered before the editor update stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginEditorUpdate event handler
void begineditorupdate_event_handler()
{
	Log.Message("\Handling BeginEditorUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begineditorupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventBeginEditorUpdate.Connect(begineditorupdate_event_connections, begineditorupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventBeginEditorUpdate.Connect(begineditorupdate_event_connections, () => {
		Log.Message("Handling BeginEditorUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
begineditorupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginEditorUpdate event with a handler function
Engine.EventBeginEditorUpdate.Connect(begineditorupdate_event_handler);

// remove subscription to the BeginEditorUpdate event later by the handler function
Engine.EventBeginEditorUpdate.Disconnect(begineditorupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection begineditorupdate_event_connection;

// subscribe to the BeginEditorUpdate event with a lambda handler function and keeping the connection
begineditorupdate_event_connection = Engine.EventBeginEditorUpdate.Connect(() => {
		Log.Message("Handling BeginEditorUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
begineditorupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
begineditorupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
begineditorupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginEditorUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventBeginEditorUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventBeginEditorUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventEndEditorUpdate

The event triggered after the editor update stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndEditorUpdate event handler
void endeditorupdate_event_handler()
{
	Log.Message("\Handling EndEditorUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endeditorupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventEndEditorUpdate.Connect(endeditorupdate_event_connections, endeditorupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventEndEditorUpdate.Connect(endeditorupdate_event_connections, () => {
		Log.Message("Handling EndEditorUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endeditorupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndEditorUpdate event with a handler function
Engine.EventEndEditorUpdate.Connect(endeditorupdate_event_handler);

// remove subscription to the EndEditorUpdate event later by the handler function
Engine.EventEndEditorUpdate.Disconnect(endeditorupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endeditorupdate_event_connection;

// subscribe to the EndEditorUpdate event with a lambda handler function and keeping the connection
endeditorupdate_event_connection = Engine.EventEndEditorUpdate.Connect(() => {
		Log.Message("Handling EndEditorUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endeditorupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endeditorupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endeditorupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndEditorUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventEndEditorUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventEndEditorUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginSystemScriptUpdate

The event triggered before the system script update stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginSystemScriptUpdate event handler
void beginsystemscriptupdate_event_handler()
{
	Log.Message("\Handling BeginSystemScriptUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginsystemscriptupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventBeginSystemScriptUpdate.Connect(beginsystemscriptupdate_event_connections, beginsystemscriptupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventBeginSystemScriptUpdate.Connect(beginsystemscriptupdate_event_connections, () => {
		Log.Message("Handling BeginSystemScriptUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginsystemscriptupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginSystemScriptUpdate event with a handler function
Engine.EventBeginSystemScriptUpdate.Connect(beginsystemscriptupdate_event_handler);

// remove subscription to the BeginSystemScriptUpdate event later by the handler function
Engine.EventBeginSystemScriptUpdate.Disconnect(beginsystemscriptupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginsystemscriptupdate_event_connection;

// subscribe to the BeginSystemScriptUpdate event with a lambda handler function and keeping the connection
beginsystemscriptupdate_event_connection = Engine.EventBeginSystemScriptUpdate.Connect(() => {
		Log.Message("Handling BeginSystemScriptUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginsystemscriptupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginsystemscriptupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginsystemscriptupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginSystemScriptUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventBeginSystemScriptUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventBeginSystemScriptUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventEndSystemScriptUpdate

The event triggered after the system script update stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndSystemScriptUpdate event handler
void endsystemscriptupdate_event_handler()
{
	Log.Message("\Handling EndSystemScriptUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endsystemscriptupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventEndSystemScriptUpdate.Connect(endsystemscriptupdate_event_connections, endsystemscriptupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventEndSystemScriptUpdate.Connect(endsystemscriptupdate_event_connections, () => {
		Log.Message("Handling EndSystemScriptUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endsystemscriptupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndSystemScriptUpdate event with a handler function
Engine.EventEndSystemScriptUpdate.Connect(endsystemscriptupdate_event_handler);

// remove subscription to the EndSystemScriptUpdate event later by the handler function
Engine.EventEndSystemScriptUpdate.Disconnect(endsystemscriptupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endsystemscriptupdate_event_connection;

// subscribe to the EndSystemScriptUpdate event with a lambda handler function and keeping the connection
endsystemscriptupdate_event_connection = Engine.EventEndSystemScriptUpdate.Connect(() => {
		Log.Message("Handling EndSystemScriptUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endsystemscriptupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endsystemscriptupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endsystemscriptupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndSystemScriptUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventEndSystemScriptUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventEndSystemScriptUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginSystemLogicUpdate

The event triggered before the system logic update stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginSystemLogicUpdate event handler
void beginsystemlogicupdate_event_handler()
{
	Log.Message("\Handling BeginSystemLogicUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginsystemlogicupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventBeginSystemLogicUpdate.Connect(beginsystemlogicupdate_event_connections, beginsystemlogicupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventBeginSystemLogicUpdate.Connect(beginsystemlogicupdate_event_connections, () => {
		Log.Message("Handling BeginSystemLogicUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginsystemlogicupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginSystemLogicUpdate event with a handler function
Engine.EventBeginSystemLogicUpdate.Connect(beginsystemlogicupdate_event_handler);

// remove subscription to the BeginSystemLogicUpdate event later by the handler function
Engine.EventBeginSystemLogicUpdate.Disconnect(beginsystemlogicupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginsystemlogicupdate_event_connection;

// subscribe to the BeginSystemLogicUpdate event with a lambda handler function and keeping the connection
beginsystemlogicupdate_event_connection = Engine.EventBeginSystemLogicUpdate.Connect(() => {
		Log.Message("Handling BeginSystemLogicUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginsystemlogicupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginsystemlogicupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginsystemlogicupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginSystemLogicUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventBeginSystemLogicUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventBeginSystemLogicUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventEndSystemLogicUpdate

The event triggered after the system logic update stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndSystemLogicUpdate event handler
void endsystemlogicupdate_event_handler()
{
	Log.Message("\Handling EndSystemLogicUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endsystemlogicupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventEndSystemLogicUpdate.Connect(endsystemlogicupdate_event_connections, endsystemlogicupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventEndSystemLogicUpdate.Connect(endsystemlogicupdate_event_connections, () => {
		Log.Message("Handling EndSystemLogicUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endsystemlogicupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndSystemLogicUpdate event with a handler function
Engine.EventEndSystemLogicUpdate.Connect(endsystemlogicupdate_event_handler);

// remove subscription to the EndSystemLogicUpdate event later by the handler function
Engine.EventEndSystemLogicUpdate.Disconnect(endsystemlogicupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endsystemlogicupdate_event_connection;

// subscribe to the EndSystemLogicUpdate event with a lambda handler function and keeping the connection
endsystemlogicupdate_event_connection = Engine.EventEndSystemLogicUpdate.Connect(() => {
		Log.Message("Handling EndSystemLogicUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endsystemlogicupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endsystemlogicupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endsystemlogicupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndSystemLogicUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventEndSystemLogicUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventEndSystemLogicUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginWorldUpdate

The event triggered before the world logic update stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginWorldUpdate event handler
void beginworldupdate_event_handler()
{
	Log.Message("\Handling BeginWorldUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginworldupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventBeginWorldUpdate.Connect(beginworldupdate_event_connections, beginworldupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventBeginWorldUpdate.Connect(beginworldupdate_event_connections, () => {
		Log.Message("Handling BeginWorldUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginworldupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginWorldUpdate event with a handler function
Engine.EventBeginWorldUpdate.Connect(beginworldupdate_event_handler);

// remove subscription to the BeginWorldUpdate event later by the handler function
Engine.EventBeginWorldUpdate.Disconnect(beginworldupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginworldupdate_event_connection;

// subscribe to the BeginWorldUpdate event with a lambda handler function and keeping the connection
beginworldupdate_event_connection = Engine.EventBeginWorldUpdate.Connect(() => {
		Log.Message("Handling BeginWorldUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginworldupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginworldupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginworldupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginWorldUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventBeginWorldUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventBeginWorldUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventEndWorldUpdate

The event triggered after the world logic update stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndWorldUpdate event handler
void endworldupdate_event_handler()
{
	Log.Message("\Handling EndWorldUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endworldupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventEndWorldUpdate.Connect(endworldupdate_event_connections, endworldupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventEndWorldUpdate.Connect(endworldupdate_event_connections, () => {
		Log.Message("Handling EndWorldUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endworldupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndWorldUpdate event with a handler function
Engine.EventEndWorldUpdate.Connect(endworldupdate_event_handler);

// remove subscription to the EndWorldUpdate event later by the handler function
Engine.EventEndWorldUpdate.Disconnect(endworldupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endworldupdate_event_connection;

// subscribe to the EndWorldUpdate event with a lambda handler function and keeping the connection
endworldupdate_event_connection = Engine.EventEndWorldUpdate.Connect(() => {
		Log.Message("Handling EndWorldUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endworldupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endworldupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endworldupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndWorldUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventEndWorldUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventEndWorldUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginAnimationManagerUpdate

The event triggered before the animation manager update stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginAnimationManagerUpdate event handler
void beginanimationmanagerupdate_event_handler()
{
	Log.Message("\Handling BeginAnimationManagerUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginanimationmanagerupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventBeginAnimationManagerUpdate.Connect(beginanimationmanagerupdate_event_connections, beginanimationmanagerupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventBeginAnimationManagerUpdate.Connect(beginanimationmanagerupdate_event_connections, () => {
		Log.Message("Handling BeginAnimationManagerUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginanimationmanagerupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginAnimationManagerUpdate event with a handler function
Engine.EventBeginAnimationManagerUpdate.Connect(beginanimationmanagerupdate_event_handler);

// remove subscription to the BeginAnimationManagerUpdate event later by the handler function
Engine.EventBeginAnimationManagerUpdate.Disconnect(beginanimationmanagerupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginanimationmanagerupdate_event_connection;

// subscribe to the BeginAnimationManagerUpdate event with a lambda handler function and keeping the connection
beginanimationmanagerupdate_event_connection = Engine.EventBeginAnimationManagerUpdate.Connect(() => {
		Log.Message("Handling BeginAnimationManagerUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginanimationmanagerupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginanimationmanagerupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginanimationmanagerupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginAnimationManagerUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventBeginAnimationManagerUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventBeginAnimationManagerUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventEndAnimationManagerUpdate

The event triggered after the animation manager update stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndAnimationManagerUpdate event handler
void endanimationmanagerupdate_event_handler()
{
	Log.Message("\Handling EndAnimationManagerUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endanimationmanagerupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventEndAnimationManagerUpdate.Connect(endanimationmanagerupdate_event_connections, endanimationmanagerupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventEndAnimationManagerUpdate.Connect(endanimationmanagerupdate_event_connections, () => {
		Log.Message("Handling EndAnimationManagerUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endanimationmanagerupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndAnimationManagerUpdate event with a handler function
Engine.EventEndAnimationManagerUpdate.Connect(endanimationmanagerupdate_event_handler);

// remove subscription to the EndAnimationManagerUpdate event later by the handler function
Engine.EventEndAnimationManagerUpdate.Disconnect(endanimationmanagerupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endanimationmanagerupdate_event_connection;

// subscribe to the EndAnimationManagerUpdate event with a lambda handler function and keeping the connection
endanimationmanagerupdate_event_connection = Engine.EventEndAnimationManagerUpdate.Connect(() => {
		Log.Message("Handling EndAnimationManagerUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endanimationmanagerupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endanimationmanagerupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endanimationmanagerupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndAnimationManagerUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventEndAnimationManagerUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventEndAnimationManagerUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginWorldPostUpdate

The event triggered before the world logic postupdate stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginWorldPostUpdate event handler
void beginworldpostupdate_event_handler()
{
	Log.Message("\Handling BeginWorldPostUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginworldpostupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventBeginWorldPostUpdate.Connect(beginworldpostupdate_event_connections, beginworldpostupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventBeginWorldPostUpdate.Connect(beginworldpostupdate_event_connections, () => {
		Log.Message("Handling BeginWorldPostUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginworldpostupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginWorldPostUpdate event with a handler function
Engine.EventBeginWorldPostUpdate.Connect(beginworldpostupdate_event_handler);

// remove subscription to the BeginWorldPostUpdate event later by the handler function
Engine.EventBeginWorldPostUpdate.Disconnect(beginworldpostupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginworldpostupdate_event_connection;

// subscribe to the BeginWorldPostUpdate event with a lambda handler function and keeping the connection
beginworldpostupdate_event_connection = Engine.EventBeginWorldPostUpdate.Connect(() => {
		Log.Message("Handling BeginWorldPostUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginworldpostupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginworldpostupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginworldpostupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginWorldPostUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventBeginWorldPostUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventBeginWorldPostUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventEndWorldPostUpdate

The event triggered after the world logic postupdate stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndWorldPostUpdate event handler
void endworldpostupdate_event_handler()
{
	Log.Message("\Handling EndWorldPostUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endworldpostupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventEndWorldPostUpdate.Connect(endworldpostupdate_event_connections, endworldpostupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventEndWorldPostUpdate.Connect(endworldpostupdate_event_connections, () => {
		Log.Message("Handling EndWorldPostUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endworldpostupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndWorldPostUpdate event with a handler function
Engine.EventEndWorldPostUpdate.Connect(endworldpostupdate_event_handler);

// remove subscription to the EndWorldPostUpdate event later by the handler function
Engine.EventEndWorldPostUpdate.Disconnect(endworldpostupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endworldpostupdate_event_connection;

// subscribe to the EndWorldPostUpdate event with a lambda handler function and keeping the connection
endworldpostupdate_event_connection = Engine.EventEndWorldPostUpdate.Connect(() => {
		Log.Message("Handling EndWorldPostUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endworldpostupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endworldpostupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endworldpostupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndWorldPostUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventEndWorldPostUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventEndWorldPostUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginSystemScriptPostUpdate

The event triggered before the system script postupdate stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginSystemScriptPostUpdate event handler
void beginsystemscriptpostupdate_event_handler()
{
	Log.Message("\Handling BeginSystemScriptPostUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginsystemscriptpostupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventBeginSystemScriptPostUpdate.Connect(beginsystemscriptpostupdate_event_connections, beginsystemscriptpostupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventBeginSystemScriptPostUpdate.Connect(beginsystemscriptpostupdate_event_connections, () => {
		Log.Message("Handling BeginSystemScriptPostUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginsystemscriptpostupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginSystemScriptPostUpdate event with a handler function
Engine.EventBeginSystemScriptPostUpdate.Connect(beginsystemscriptpostupdate_event_handler);

// remove subscription to the BeginSystemScriptPostUpdate event later by the handler function
Engine.EventBeginSystemScriptPostUpdate.Disconnect(beginsystemscriptpostupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginsystemscriptpostupdate_event_connection;

// subscribe to the BeginSystemScriptPostUpdate event with a lambda handler function and keeping the connection
beginsystemscriptpostupdate_event_connection = Engine.EventBeginSystemScriptPostUpdate.Connect(() => {
		Log.Message("Handling BeginSystemScriptPostUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginsystemscriptpostupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginsystemscriptpostupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginsystemscriptpostupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginSystemScriptPostUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventBeginSystemScriptPostUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventBeginSystemScriptPostUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventEndSystemScriptPostUpdate

The event triggered after the system script postupdate stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndSystemScriptPostUpdate event handler
void endsystemscriptpostupdate_event_handler()
{
	Log.Message("\Handling EndSystemScriptPostUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endsystemscriptpostupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventEndSystemScriptPostUpdate.Connect(endsystemscriptpostupdate_event_connections, endsystemscriptpostupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventEndSystemScriptPostUpdate.Connect(endsystemscriptpostupdate_event_connections, () => {
		Log.Message("Handling EndSystemScriptPostUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endsystemscriptpostupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndSystemScriptPostUpdate event with a handler function
Engine.EventEndSystemScriptPostUpdate.Connect(endsystemscriptpostupdate_event_handler);

// remove subscription to the EndSystemScriptPostUpdate event later by the handler function
Engine.EventEndSystemScriptPostUpdate.Disconnect(endsystemscriptpostupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endsystemscriptpostupdate_event_connection;

// subscribe to the EndSystemScriptPostUpdate event with a lambda handler function and keeping the connection
endsystemscriptpostupdate_event_connection = Engine.EventEndSystemScriptPostUpdate.Connect(() => {
		Log.Message("Handling EndSystemScriptPostUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endsystemscriptpostupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endsystemscriptpostupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endsystemscriptpostupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndSystemScriptPostUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventEndSystemScriptPostUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventEndSystemScriptPostUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginSystemLogicPostUpdate

The event triggered before the system logic postupdate stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginSystemLogicPostUpdate event handler
void beginsystemlogicpostupdate_event_handler()
{
	Log.Message("\Handling BeginSystemLogicPostUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginsystemlogicpostupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventBeginSystemLogicPostUpdate.Connect(beginsystemlogicpostupdate_event_connections, beginsystemlogicpostupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventBeginSystemLogicPostUpdate.Connect(beginsystemlogicpostupdate_event_connections, () => {
		Log.Message("Handling BeginSystemLogicPostUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginsystemlogicpostupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginSystemLogicPostUpdate event with a handler function
Engine.EventBeginSystemLogicPostUpdate.Connect(beginsystemlogicpostupdate_event_handler);

// remove subscription to the BeginSystemLogicPostUpdate event later by the handler function
Engine.EventBeginSystemLogicPostUpdate.Disconnect(beginsystemlogicpostupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginsystemlogicpostupdate_event_connection;

// subscribe to the BeginSystemLogicPostUpdate event with a lambda handler function and keeping the connection
beginsystemlogicpostupdate_event_connection = Engine.EventBeginSystemLogicPostUpdate.Connect(() => {
		Log.Message("Handling BeginSystemLogicPostUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginsystemlogicpostupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginsystemlogicpostupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginsystemlogicpostupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginSystemLogicPostUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventBeginSystemLogicPostUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventBeginSystemLogicPostUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventEndSystemLogicPostUpdate

The event triggered after the system logic postupdate stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndSystemLogicPostUpdate event handler
void endsystemlogicpostupdate_event_handler()
{
	Log.Message("\Handling EndSystemLogicPostUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endsystemlogicpostupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventEndSystemLogicPostUpdate.Connect(endsystemlogicpostupdate_event_connections, endsystemlogicpostupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventEndSystemLogicPostUpdate.Connect(endsystemlogicpostupdate_event_connections, () => {
		Log.Message("Handling EndSystemLogicPostUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endsystemlogicpostupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndSystemLogicPostUpdate event with a handler function
Engine.EventEndSystemLogicPostUpdate.Connect(endsystemlogicpostupdate_event_handler);

// remove subscription to the EndSystemLogicPostUpdate event later by the handler function
Engine.EventEndSystemLogicPostUpdate.Disconnect(endsystemlogicpostupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endsystemlogicpostupdate_event_connection;

// subscribe to the EndSystemLogicPostUpdate event with a lambda handler function and keeping the connection
endsystemlogicpostupdate_event_connection = Engine.EventEndSystemLogicPostUpdate.Connect(() => {
		Log.Message("Handling EndSystemLogicPostUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endsystemlogicpostupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endsystemlogicpostupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endsystemlogicpostupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndSystemLogicPostUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventEndSystemLogicPostUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventEndSystemLogicPostUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginEditorPostUpdate

The event triggered before the editor logic postupdate stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginEditorPostUpdate event handler
void begineditorpostupdate_event_handler()
{
	Log.Message("\Handling BeginEditorPostUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begineditorpostupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventBeginEditorPostUpdate.Connect(begineditorpostupdate_event_connections, begineditorpostupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventBeginEditorPostUpdate.Connect(begineditorpostupdate_event_connections, () => {
		Log.Message("Handling BeginEditorPostUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
begineditorpostupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginEditorPostUpdate event with a handler function
Engine.EventBeginEditorPostUpdate.Connect(begineditorpostupdate_event_handler);

// remove subscription to the BeginEditorPostUpdate event later by the handler function
Engine.EventBeginEditorPostUpdate.Disconnect(begineditorpostupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection begineditorpostupdate_event_connection;

// subscribe to the BeginEditorPostUpdate event with a lambda handler function and keeping the connection
begineditorpostupdate_event_connection = Engine.EventBeginEditorPostUpdate.Connect(() => {
		Log.Message("Handling BeginEditorPostUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
begineditorpostupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
begineditorpostupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
begineditorpostupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginEditorPostUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventBeginEditorPostUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventBeginEditorPostUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventEndEditorPostUpdate

The event triggered after the editor logic postupdate stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndEditorPostUpdate event handler
void endeditorpostupdate_event_handler()
{
	Log.Message("\Handling EndEditorPostUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endeditorpostupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventEndEditorPostUpdate.Connect(endeditorpostupdate_event_connections, endeditorpostupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventEndEditorPostUpdate.Connect(endeditorpostupdate_event_connections, () => {
		Log.Message("Handling EndEditorPostUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endeditorpostupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndEditorPostUpdate event with a handler function
Engine.EventEndEditorPostUpdate.Connect(endeditorpostupdate_event_handler);

// remove subscription to the EndEditorPostUpdate event later by the handler function
Engine.EventEndEditorPostUpdate.Disconnect(endeditorpostupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endeditorpostupdate_event_connection;

// subscribe to the EndEditorPostUpdate event with a lambda handler function and keeping the connection
endeditorpostupdate_event_connection = Engine.EventEndEditorPostUpdate.Connect(() => {
		Log.Message("Handling EndEditorPostUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endeditorpostupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endeditorpostupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endeditorpostupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndEditorPostUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventEndEditorPostUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventEndEditorPostUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginPluginsPostUpdate

The event triggered before the plugins postupdate stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginPluginsPostUpdate event handler
void beginpluginspostupdate_event_handler()
{
	Log.Message("\Handling BeginPluginsPostUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginpluginspostupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventBeginPluginsPostUpdate.Connect(beginpluginspostupdate_event_connections, beginpluginspostupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventBeginPluginsPostUpdate.Connect(beginpluginspostupdate_event_connections, () => {
		Log.Message("Handling BeginPluginsPostUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginpluginspostupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginPluginsPostUpdate event with a handler function
Engine.EventBeginPluginsPostUpdate.Connect(beginpluginspostupdate_event_handler);

// remove subscription to the BeginPluginsPostUpdate event later by the handler function
Engine.EventBeginPluginsPostUpdate.Disconnect(beginpluginspostupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginpluginspostupdate_event_connection;

// subscribe to the BeginPluginsPostUpdate event with a lambda handler function and keeping the connection
beginpluginspostupdate_event_connection = Engine.EventBeginPluginsPostUpdate.Connect(() => {
		Log.Message("Handling BeginPluginsPostUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginpluginspostupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginpluginspostupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginpluginspostupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginPluginsPostUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventBeginPluginsPostUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventBeginPluginsPostUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventEndPluginsPostUpdate

The event triggered after the plugins postupdate stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndPluginsPostUpdate event handler
void endpluginspostupdate_event_handler()
{
	Log.Message("\Handling EndPluginsPostUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endpluginspostupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventEndPluginsPostUpdate.Connect(endpluginspostupdate_event_connections, endpluginspostupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventEndPluginsPostUpdate.Connect(endpluginspostupdate_event_connections, () => {
		Log.Message("Handling EndPluginsPostUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endpluginspostupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndPluginsPostUpdate event with a handler function
Engine.EventEndPluginsPostUpdate.Connect(endpluginspostupdate_event_handler);

// remove subscription to the EndPluginsPostUpdate event later by the handler function
Engine.EventEndPluginsPostUpdate.Disconnect(endpluginspostupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endpluginspostupdate_event_connection;

// subscribe to the EndPluginsPostUpdate event with a lambda handler function and keeping the connection
endpluginspostupdate_event_connection = Engine.EventEndPluginsPostUpdate.Connect(() => {
		Log.Message("Handling EndPluginsPostUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endpluginspostupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endpluginspostupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endpluginspostupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndPluginsPostUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventEndPluginsPostUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventEndPluginsPostUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginSpatialUpdate

The event triggered before the spatial tree update stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginSpatialUpdate event handler
void beginspatialupdate_event_handler()
{
	Log.Message("\Handling BeginSpatialUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginspatialupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventBeginSpatialUpdate.Connect(beginspatialupdate_event_connections, beginspatialupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventBeginSpatialUpdate.Connect(beginspatialupdate_event_connections, () => {
		Log.Message("Handling BeginSpatialUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginspatialupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginSpatialUpdate event with a handler function
Engine.EventBeginSpatialUpdate.Connect(beginspatialupdate_event_handler);

// remove subscription to the BeginSpatialUpdate event later by the handler function
Engine.EventBeginSpatialUpdate.Disconnect(beginspatialupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginspatialupdate_event_connection;

// subscribe to the BeginSpatialUpdate event with a lambda handler function and keeping the connection
beginspatialupdate_event_connection = Engine.EventBeginSpatialUpdate.Connect(() => {
		Log.Message("Handling BeginSpatialUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginspatialupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginspatialupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginspatialupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginSpatialUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventBeginSpatialUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventBeginSpatialUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventEndSpatialUpdate

The event triggered after the spatial tree update stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndSpatialUpdate event handler
void endspatialupdate_event_handler()
{
	Log.Message("\Handling EndSpatialUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endspatialupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventEndSpatialUpdate.Connect(endspatialupdate_event_connections, endspatialupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventEndSpatialUpdate.Connect(endspatialupdate_event_connections, () => {
		Log.Message("Handling EndSpatialUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endspatialupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndSpatialUpdate event with a handler function
Engine.EventEndSpatialUpdate.Connect(endspatialupdate_event_handler);

// remove subscription to the EndSpatialUpdate event later by the handler function
Engine.EventEndSpatialUpdate.Disconnect(endspatialupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endspatialupdate_event_connection;

// subscribe to the EndSpatialUpdate event with a lambda handler function and keeping the connection
endspatialupdate_event_connection = Engine.EventEndSpatialUpdate.Connect(() => {
		Log.Message("Handling EndSpatialUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endspatialupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endspatialupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endspatialupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndSpatialUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventEndSpatialUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventEndSpatialUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginFilesystemUpdate

The event triggered before the filesystem update stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginFilesystemUpdate event handler
void beginfilesystemupdate_event_handler()
{
	Log.Message("\Handling BeginFilesystemUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginfilesystemupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventBeginFilesystemUpdate.Connect(beginfilesystemupdate_event_connections, beginfilesystemupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventBeginFilesystemUpdate.Connect(beginfilesystemupdate_event_connections, () => {
		Log.Message("Handling BeginFilesystemUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginfilesystemupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginFilesystemUpdate event with a handler function
Engine.EventBeginFilesystemUpdate.Connect(beginfilesystemupdate_event_handler);

// remove subscription to the BeginFilesystemUpdate event later by the handler function
Engine.EventBeginFilesystemUpdate.Disconnect(beginfilesystemupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginfilesystemupdate_event_connection;

// subscribe to the BeginFilesystemUpdate event with a lambda handler function and keeping the connection
beginfilesystemupdate_event_connection = Engine.EventBeginFilesystemUpdate.Connect(() => {
		Log.Message("Handling BeginFilesystemUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginfilesystemupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginfilesystemupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginfilesystemupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginFilesystemUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventBeginFilesystemUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventBeginFilesystemUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventEndFilesystemUpdate

The event triggered after the filesystem update stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndFilesystemUpdate event handler
void endfilesystemupdate_event_handler()
{
	Log.Message("\Handling EndFilesystemUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endfilesystemupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventEndFilesystemUpdate.Connect(endfilesystemupdate_event_connections, endfilesystemupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventEndFilesystemUpdate.Connect(endfilesystemupdate_event_connections, () => {
		Log.Message("Handling EndFilesystemUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endfilesystemupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndFilesystemUpdate event with a handler function
Engine.EventEndFilesystemUpdate.Connect(endfilesystemupdate_event_handler);

// remove subscription to the EndFilesystemUpdate event later by the handler function
Engine.EventEndFilesystemUpdate.Disconnect(endfilesystemupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endfilesystemupdate_event_connection;

// subscribe to the EndFilesystemUpdate event with a lambda handler function and keeping the connection
endfilesystemupdate_event_connection = Engine.EventEndFilesystemUpdate.Connect(() => {
		Log.Message("Handling EndFilesystemUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endfilesystemupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endfilesystemupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endfilesystemupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndFilesystemUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventEndFilesystemUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventEndFilesystemUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginPathfinding

The event triggered before the pathfinding module is updated. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginPathfinding event handler
void beginpathfinding_event_handler()
{
	Log.Message("\Handling BeginPathfinding event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginpathfinding_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventBeginPathfinding.Connect(beginpathfinding_event_connections, beginpathfinding_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventBeginPathfinding.Connect(beginpathfinding_event_connections, () => {
		Log.Message("Handling BeginPathfinding event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginpathfinding_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginPathfinding event with a handler function
Engine.EventBeginPathfinding.Connect(beginpathfinding_event_handler);

// remove subscription to the BeginPathfinding event later by the handler function
Engine.EventBeginPathfinding.Disconnect(beginpathfinding_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginpathfinding_event_connection;

// subscribe to the BeginPathfinding event with a lambda handler function and keeping the connection
beginpathfinding_event_connection = Engine.EventBeginPathfinding.Connect(() => {
		Log.Message("Handling BeginPathfinding event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginpathfinding_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginpathfinding_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginpathfinding_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginPathfinding events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventBeginPathfinding.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventBeginPathfinding.Enabled = true;

```

</details>

## 🔒︎ Event EventEndUpdate

The event triggered after the update stage is finished. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndUpdate event handler
void endupdate_event_handler()
{
	Log.Message("\Handling EndUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventEndUpdate.Connect(endupdate_event_connections, endupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventEndUpdate.Connect(endupdate_event_connections, () => {
		Log.Message("Handling EndUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndUpdate event with a handler function
Engine.EventEndUpdate.Connect(endupdate_event_handler);

// remove subscription to the EndUpdate event later by the handler function
Engine.EventEndUpdate.Disconnect(endupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endupdate_event_connection;

// subscribe to the EndUpdate event with a lambda handler function and keeping the connection
endupdate_event_connection = Engine.EventEndUpdate.Connect(() => {
		Log.Message("Handling EndUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventEndUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventEndUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventSyncBeginFramePhysics

The event triggered before the physics frame in the main thread. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the SyncBeginFramePhysics event handler
void syncbeginframephysics_event_handler()
{
	Log.Message("\Handling SyncBeginFramePhysics event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections syncbeginframephysics_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventSyncBeginFramePhysics.Connect(syncbeginframephysics_event_connections, syncbeginframephysics_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventSyncBeginFramePhysics.Connect(syncbeginframephysics_event_connections, () => {
		Log.Message("Handling SyncBeginFramePhysics event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
syncbeginframephysics_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the SyncBeginFramePhysics event with a handler function
Engine.EventSyncBeginFramePhysics.Connect(syncbeginframephysics_event_handler);

// remove subscription to the SyncBeginFramePhysics event later by the handler function
Engine.EventSyncBeginFramePhysics.Disconnect(syncbeginframephysics_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection syncbeginframephysics_event_connection;

// subscribe to the SyncBeginFramePhysics event with a lambda handler function and keeping the connection
syncbeginframephysics_event_connection = Engine.EventSyncBeginFramePhysics.Connect(() => {
		Log.Message("Handling SyncBeginFramePhysics event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
syncbeginframephysics_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
syncbeginframephysics_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
syncbeginframephysics_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring SyncBeginFramePhysics events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventSyncBeginFramePhysics.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventSyncBeginFramePhysics.Enabled = true;

```

</details>

## 🔒︎ Event EventSyncEndFramePhysics

The event triggered after the physics frame in the main thread. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the SyncEndFramePhysics event handler
void syncendframephysics_event_handler()
{
	Log.Message("\Handling SyncEndFramePhysics event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections syncendframephysics_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventSyncEndFramePhysics.Connect(syncendframephysics_event_connections, syncendframephysics_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventSyncEndFramePhysics.Connect(syncendframephysics_event_connections, () => {
		Log.Message("Handling SyncEndFramePhysics event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
syncendframephysics_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the SyncEndFramePhysics event with a handler function
Engine.EventSyncEndFramePhysics.Connect(syncendframephysics_event_handler);

// remove subscription to the SyncEndFramePhysics event later by the handler function
Engine.EventSyncEndFramePhysics.Disconnect(syncendframephysics_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection syncendframephysics_event_connection;

// subscribe to the SyncEndFramePhysics event with a lambda handler function and keeping the connection
syncendframephysics_event_connection = Engine.EventSyncEndFramePhysics.Connect(() => {
		Log.Message("Handling SyncEndFramePhysics event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
syncendframephysics_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
syncendframephysics_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
syncendframephysics_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring SyncEndFramePhysics events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventSyncEndFramePhysics.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventSyncEndFramePhysics.Enabled = true;

```

</details>

## 🔒︎ Event EventAsyncBeginFramePhysics

The event triggered before the physics frame in the physics thread. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the AsyncBeginFramePhysics event handler
void asyncbeginframephysics_event_handler()
{
	Log.Message("\Handling AsyncBeginFramePhysics event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections asyncbeginframephysics_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventAsyncBeginFramePhysics.Connect(asyncbeginframephysics_event_connections, asyncbeginframephysics_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventAsyncBeginFramePhysics.Connect(asyncbeginframephysics_event_connections, () => {
		Log.Message("Handling AsyncBeginFramePhysics event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
asyncbeginframephysics_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the AsyncBeginFramePhysics event with a handler function
Engine.EventAsyncBeginFramePhysics.Connect(asyncbeginframephysics_event_handler);

// remove subscription to the AsyncBeginFramePhysics event later by the handler function
Engine.EventAsyncBeginFramePhysics.Disconnect(asyncbeginframephysics_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection asyncbeginframephysics_event_connection;

// subscribe to the AsyncBeginFramePhysics event with a lambda handler function and keeping the connection
asyncbeginframephysics_event_connection = Engine.EventAsyncBeginFramePhysics.Connect(() => {
		Log.Message("Handling AsyncBeginFramePhysics event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
asyncbeginframephysics_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
asyncbeginframephysics_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
asyncbeginframephysics_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring AsyncBeginFramePhysics events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventAsyncBeginFramePhysics.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventAsyncBeginFramePhysics.Enabled = true;

```

</details>

## 🔒︎ Event EventAsyncEndFramePhysics

The event triggered after the physics frame in the physics thread. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the AsyncEndFramePhysics event handler
void asyncendframephysics_event_handler()
{
	Log.Message("\Handling AsyncEndFramePhysics event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections asyncendframephysics_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventAsyncEndFramePhysics.Connect(asyncendframephysics_event_connections, asyncendframephysics_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventAsyncEndFramePhysics.Connect(asyncendframephysics_event_connections, () => {
		Log.Message("Handling AsyncEndFramePhysics event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
asyncendframephysics_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the AsyncEndFramePhysics event with a handler function
Engine.EventAsyncEndFramePhysics.Connect(asyncendframephysics_event_handler);

// remove subscription to the AsyncEndFramePhysics event later by the handler function
Engine.EventAsyncEndFramePhysics.Disconnect(asyncendframephysics_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection asyncendframephysics_event_connection;

// subscribe to the AsyncEndFramePhysics event with a lambda handler function and keeping the connection
asyncendframephysics_event_connection = Engine.EventAsyncEndFramePhysics.Connect(() => {
		Log.Message("Handling AsyncEndFramePhysics event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
asyncendframephysics_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
asyncendframephysics_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
asyncendframephysics_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring AsyncEndFramePhysics events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventAsyncEndFramePhysics.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventAsyncEndFramePhysics.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginVRRender

The event triggered before the VR rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginVRRender event handler
void beginvrrender_event_handler()
{
	Log.Message("\Handling BeginVRRender event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginvrrender_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventBeginVRRender.Connect(beginvrrender_event_connections, beginvrrender_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventBeginVRRender.Connect(beginvrrender_event_connections, () => {
		Log.Message("Handling BeginVRRender event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginvrrender_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginVRRender event with a handler function
Engine.EventBeginVRRender.Connect(beginvrrender_event_handler);

// remove subscription to the BeginVRRender event later by the handler function
Engine.EventBeginVRRender.Disconnect(beginvrrender_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginvrrender_event_connection;

// subscribe to the BeginVRRender event with a lambda handler function and keeping the connection
beginvrrender_event_connection = Engine.EventBeginVRRender.Connect(() => {
		Log.Message("Handling BeginVRRender event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginvrrender_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginvrrender_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginvrrender_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginVRRender events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventBeginVRRender.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventBeginVRRender.Enabled = true;

```

</details>

## 🔒︎ Event EventEndVRRender

The event triggered after the VR rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndVRRender event handler
void endvrrender_event_handler()
{
	Log.Message("\Handling EndVRRender event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endvrrender_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventEndVRRender.Connect(endvrrender_event_connections, endvrrender_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventEndVRRender.Connect(endvrrender_event_connections, () => {
		Log.Message("Handling EndVRRender event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endvrrender_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndVRRender event with a handler function
Engine.EventEndVRRender.Connect(endvrrender_event_handler);

// remove subscription to the EndVRRender event later by the handler function
Engine.EventEndVRRender.Disconnect(endvrrender_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endvrrender_event_connection;

// subscribe to the EndVRRender event with a lambda handler function and keeping the connection
endvrrender_event_connection = Engine.EventEndVRRender.Connect(() => {
		Log.Message("Handling EndVRRender event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endvrrender_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endvrrender_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endvrrender_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndVRRender events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventEndVRRender.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventEndVRRender.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginRender

The event triggered before the rendering stage is started. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginRender event handler
void beginrender_event_handler()
{
	Log.Message("\Handling BeginRender event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginrender_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventBeginRender.Connect(beginrender_event_connections, beginrender_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventBeginRender.Connect(beginrender_event_connections, () => {
		Log.Message("Handling BeginRender event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginrender_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginRender event with a handler function
Engine.EventBeginRender.Connect(beginrender_event_handler);

// remove subscription to the BeginRender event later by the handler function
Engine.EventBeginRender.Disconnect(beginrender_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginrender_event_connection;

// subscribe to the BeginRender event with a lambda handler function and keeping the connection
beginrender_event_connection = Engine.EventBeginRender.Connect(() => {
		Log.Message("Handling BeginRender event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginrender_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginrender_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginrender_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginRender events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventBeginRender.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventBeginRender.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginEditorRender

The event triggered before the editor rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginEditorRender event handler
void begineditorrender_event_handler()
{
	Log.Message("\Handling BeginEditorRender event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begineditorrender_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventBeginEditorRender.Connect(begineditorrender_event_connections, begineditorrender_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventBeginEditorRender.Connect(begineditorrender_event_connections, () => {
		Log.Message("Handling BeginEditorRender event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
begineditorrender_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginEditorRender event with a handler function
Engine.EventBeginEditorRender.Connect(begineditorrender_event_handler);

// remove subscription to the BeginEditorRender event later by the handler function
Engine.EventBeginEditorRender.Disconnect(begineditorrender_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection begineditorrender_event_connection;

// subscribe to the BeginEditorRender event with a lambda handler function and keeping the connection
begineditorrender_event_connection = Engine.EventBeginEditorRender.Connect(() => {
		Log.Message("Handling BeginEditorRender event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
begineditorrender_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
begineditorrender_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
begineditorrender_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginEditorRender events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventBeginEditorRender.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventBeginEditorRender.Enabled = true;

```

</details>

## 🔒︎ Event EventEndEditorRender

The event triggered after the editor rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndEditorRender event handler
void endeditorrender_event_handler()
{
	Log.Message("\Handling EndEditorRender event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endeditorrender_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventEndEditorRender.Connect(endeditorrender_event_connections, endeditorrender_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventEndEditorRender.Connect(endeditorrender_event_connections, () => {
		Log.Message("Handling EndEditorRender event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endeditorrender_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndEditorRender event with a handler function
Engine.EventEndEditorRender.Connect(endeditorrender_event_handler);

// remove subscription to the EndEditorRender event later by the handler function
Engine.EventEndEditorRender.Disconnect(endeditorrender_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endeditorrender_event_connection;

// subscribe to the EndEditorRender event with a lambda handler function and keeping the connection
endeditorrender_event_connection = Engine.EventEndEditorRender.Connect(() => {
		Log.Message("Handling EndEditorRender event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endeditorrender_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endeditorrender_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endeditorrender_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndEditorRender events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventEndEditorRender.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventEndEditorRender.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginPluginsRender

The event triggered before the plugins rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginPluginsRender event handler
void beginpluginsrender_event_handler()
{
	Log.Message("\Handling BeginPluginsRender event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginpluginsrender_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventBeginPluginsRender.Connect(beginpluginsrender_event_connections, beginpluginsrender_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventBeginPluginsRender.Connect(beginpluginsrender_event_connections, () => {
		Log.Message("Handling BeginPluginsRender event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginpluginsrender_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginPluginsRender event with a handler function
Engine.EventBeginPluginsRender.Connect(beginpluginsrender_event_handler);

// remove subscription to the BeginPluginsRender event later by the handler function
Engine.EventBeginPluginsRender.Disconnect(beginpluginsrender_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginpluginsrender_event_connection;

// subscribe to the BeginPluginsRender event with a lambda handler function and keeping the connection
beginpluginsrender_event_connection = Engine.EventBeginPluginsRender.Connect(() => {
		Log.Message("Handling BeginPluginsRender event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginpluginsrender_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginpluginsrender_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginpluginsrender_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginPluginsRender events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventBeginPluginsRender.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventBeginPluginsRender.Enabled = true;

```

</details>

## 🔒︎ Event EventEndPluginsRender

The event triggered after the plugins rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndPluginsRender event handler
void endpluginsrender_event_handler()
{
	Log.Message("\Handling EndPluginsRender event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endpluginsrender_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventEndPluginsRender.Connect(endpluginsrender_event_connections, endpluginsrender_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventEndPluginsRender.Connect(endpluginsrender_event_connections, () => {
		Log.Message("Handling EndPluginsRender event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endpluginsrender_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndPluginsRender event with a handler function
Engine.EventEndPluginsRender.Connect(endpluginsrender_event_handler);

// remove subscription to the EndPluginsRender event later by the handler function
Engine.EventEndPluginsRender.Disconnect(endpluginsrender_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endpluginsrender_event_connection;

// subscribe to the EndPluginsRender event with a lambda handler function and keeping the connection
endpluginsrender_event_connection = Engine.EventEndPluginsRender.Connect(() => {
		Log.Message("Handling EndPluginsRender event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endpluginsrender_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endpluginsrender_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endpluginsrender_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndPluginsRender events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventEndPluginsRender.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventEndPluginsRender.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginRenderWorld

The event triggered before the world rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginRenderWorld event handler
void beginrenderworld_event_handler()
{
	Log.Message("\Handling BeginRenderWorld event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginrenderworld_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventBeginRenderWorld.Connect(beginrenderworld_event_connections, beginrenderworld_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventBeginRenderWorld.Connect(beginrenderworld_event_connections, () => {
		Log.Message("Handling BeginRenderWorld event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginrenderworld_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginRenderWorld event with a handler function
Engine.EventBeginRenderWorld.Connect(beginrenderworld_event_handler);

// remove subscription to the BeginRenderWorld event later by the handler function
Engine.EventBeginRenderWorld.Disconnect(beginrenderworld_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginrenderworld_event_connection;

// subscribe to the BeginRenderWorld event with a lambda handler function and keeping the connection
beginrenderworld_event_connection = Engine.EventBeginRenderWorld.Connect(() => {
		Log.Message("Handling BeginRenderWorld event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginrenderworld_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginrenderworld_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginrenderworld_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginRenderWorld events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventBeginRenderWorld.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventBeginRenderWorld.Enabled = true;

```

</details>

## 🔒︎ Event EventEndRenderWorld

The event triggered after the world rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndRenderWorld event handler
void endrenderworld_event_handler()
{
	Log.Message("\Handling EndRenderWorld event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endrenderworld_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventEndRenderWorld.Connect(endrenderworld_event_connections, endrenderworld_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventEndRenderWorld.Connect(endrenderworld_event_connections, () => {
		Log.Message("Handling EndRenderWorld event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endrenderworld_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndRenderWorld event with a handler function
Engine.EventEndRenderWorld.Connect(endrenderworld_event_handler);

// remove subscription to the EndRenderWorld event later by the handler function
Engine.EventEndRenderWorld.Disconnect(endrenderworld_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endrenderworld_event_connection;

// subscribe to the EndRenderWorld event with a lambda handler function and keeping the connection
endrenderworld_event_connection = Engine.EventEndRenderWorld.Connect(() => {
		Log.Message("Handling EndRenderWorld event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endrenderworld_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endrenderworld_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endrenderworld_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndRenderWorld events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventEndRenderWorld.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventEndRenderWorld.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginPluginsGui

The event triggered before the gui() function of plugins is called. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginPluginsGui event handler
void beginpluginsgui_event_handler()
{
	Log.Message("\Handling BeginPluginsGui event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginpluginsgui_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventBeginPluginsGui.Connect(beginpluginsgui_event_connections, beginpluginsgui_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventBeginPluginsGui.Connect(beginpluginsgui_event_connections, () => {
		Log.Message("Handling BeginPluginsGui event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginpluginsgui_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginPluginsGui event with a handler function
Engine.EventBeginPluginsGui.Connect(beginpluginsgui_event_handler);

// remove subscription to the BeginPluginsGui event later by the handler function
Engine.EventBeginPluginsGui.Disconnect(beginpluginsgui_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginpluginsgui_event_connection;

// subscribe to the BeginPluginsGui event with a lambda handler function and keeping the connection
beginpluginsgui_event_connection = Engine.EventBeginPluginsGui.Connect(() => {
		Log.Message("Handling BeginPluginsGui event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginpluginsgui_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginpluginsgui_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginpluginsgui_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginPluginsGui events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventBeginPluginsGui.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventBeginPluginsGui.Enabled = true;

```

</details>

## 🔒︎ Event EventEndPluginsGui

The event triggered after the gui() function of plugins is called. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndPluginsGui event handler
void endpluginsgui_event_handler()
{
	Log.Message("\Handling EndPluginsGui event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endpluginsgui_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventEndPluginsGui.Connect(endpluginsgui_event_connections, endpluginsgui_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventEndPluginsGui.Connect(endpluginsgui_event_connections, () => {
		Log.Message("Handling EndPluginsGui event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endpluginsgui_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndPluginsGui event with a handler function
Engine.EventEndPluginsGui.Connect(endpluginsgui_event_handler);

// remove subscription to the EndPluginsGui event later by the handler function
Engine.EventEndPluginsGui.Disconnect(endpluginsgui_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endpluginsgui_event_connection;

// subscribe to the EndPluginsGui event with a lambda handler function and keeping the connection
endpluginsgui_event_connection = Engine.EventEndPluginsGui.Connect(() => {
		Log.Message("Handling EndPluginsGui event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endpluginsgui_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endpluginsgui_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endpluginsgui_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndPluginsGui events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventEndPluginsGui.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventEndPluginsGui.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginPostRender

The event triggered before the post-rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginPostRender event handler
void beginpostrender_event_handler()
{
	Log.Message("\Handling BeginPostRender event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginpostrender_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventBeginPostRender.Connect(beginpostrender_event_connections, beginpostrender_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventBeginPostRender.Connect(beginpostrender_event_connections, () => {
		Log.Message("Handling BeginPostRender event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginpostrender_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginPostRender event with a handler function
Engine.EventBeginPostRender.Connect(beginpostrender_event_handler);

// remove subscription to the BeginPostRender event later by the handler function
Engine.EventBeginPostRender.Disconnect(beginpostrender_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginpostrender_event_connection;

// subscribe to the BeginPostRender event with a lambda handler function and keeping the connection
beginpostrender_event_connection = Engine.EventBeginPostRender.Connect(() => {
		Log.Message("Handling BeginPostRender event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginpostrender_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginpostrender_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginpostrender_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginPostRender events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventBeginPostRender.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventBeginPostRender.Enabled = true;

```

</details>

## 🔒︎ Event EventEndPostRender

The event triggered after the post-rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndPostRender event handler
void endpostrender_event_handler()
{
	Log.Message("\Handling EndPostRender event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endpostrender_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventEndPostRender.Connect(endpostrender_event_connections, endpostrender_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventEndPostRender.Connect(endpostrender_event_connections, () => {
		Log.Message("Handling EndPostRender event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endpostrender_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndPostRender event with a handler function
Engine.EventEndPostRender.Connect(endpostrender_event_handler);

// remove subscription to the EndPostRender event later by the handler function
Engine.EventEndPostRender.Disconnect(endpostrender_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endpostrender_event_connection;

// subscribe to the EndPostRender event with a lambda handler function and keeping the connection
endpostrender_event_connection = Engine.EventEndPostRender.Connect(() => {
		Log.Message("Handling EndPostRender event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endpostrender_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endpostrender_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endpostrender_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndPostRender events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventEndPostRender.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventEndPostRender.Enabled = true;

```

</details>

## 🔒︎ Event EventEndRender

The event triggered after the rendering stage is finished. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndRender event handler
void endrender_event_handler()
{
	Log.Message("\Handling EndRender event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endrender_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventEndRender.Connect(endrender_event_connections, endrender_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventEndRender.Connect(endrender_event_connections, () => {
		Log.Message("Handling EndRender event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endrender_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndRender event with a handler function
Engine.EventEndRender.Connect(endrender_event_handler);

// remove subscription to the EndRender event later by the handler function
Engine.EventEndRender.Disconnect(endrender_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endrender_event_connection;

// subscribe to the EndRender event with a lambda handler function and keeping the connection
endrender_event_connection = Engine.EventEndRender.Connect(() => {
		Log.Message("Handling EndRender event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endrender_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endrender_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endrender_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndRender events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventEndRender.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventEndRender.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginSwap

The event triggered before the swap stage is started. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginSwap event handler
void beginswap_event_handler()
{
	Log.Message("\Handling BeginSwap event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginswap_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventBeginSwap.Connect(beginswap_event_connections, beginswap_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventBeginSwap.Connect(beginswap_event_connections, () => {
		Log.Message("Handling BeginSwap event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginswap_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginSwap event with a handler function
Engine.EventBeginSwap.Connect(beginswap_event_handler);

// remove subscription to the BeginSwap event later by the handler function
Engine.EventBeginSwap.Disconnect(beginswap_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginswap_event_connection;

// subscribe to the BeginSwap event with a lambda handler function and keeping the connection
beginswap_event_connection = Engine.EventBeginSwap.Connect(() => {
		Log.Message("Handling BeginSwap event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginswap_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginswap_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginswap_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginSwap events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventBeginSwap.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventBeginSwap.Enabled = true;

```

</details>

## 🔒︎ Event EventEndPathfinding

The event triggered after the pathfinding is updated. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndPathfinding event handler
void endpathfinding_event_handler()
{
	Log.Message("\Handling EndPathfinding event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endpathfinding_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventEndPathfinding.Connect(endpathfinding_event_connections, endpathfinding_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventEndPathfinding.Connect(endpathfinding_event_connections, () => {
		Log.Message("Handling EndPathfinding event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endpathfinding_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndPathfinding event with a handler function
Engine.EventEndPathfinding.Connect(endpathfinding_event_handler);

// remove subscription to the EndPathfinding event later by the handler function
Engine.EventEndPathfinding.Disconnect(endpathfinding_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endpathfinding_event_connection;

// subscribe to the EndPathfinding event with a lambda handler function and keeping the connection
endpathfinding_event_connection = Engine.EventEndPathfinding.Connect(() => {
		Log.Message("Handling EndPathfinding event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endpathfinding_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endpathfinding_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endpathfinding_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndPathfinding events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventEndPathfinding.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventEndPathfinding.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginWorldSwap

The event triggered before the world logic swap() function is executed. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginWorldSwap event handler
void beginworldswap_event_handler()
{
	Log.Message("\Handling BeginWorldSwap event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginworldswap_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventBeginWorldSwap.Connect(beginworldswap_event_connections, beginworldswap_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventBeginWorldSwap.Connect(beginworldswap_event_connections, () => {
		Log.Message("Handling BeginWorldSwap event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginworldswap_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginWorldSwap event with a handler function
Engine.EventBeginWorldSwap.Connect(beginworldswap_event_handler);

// remove subscription to the BeginWorldSwap event later by the handler function
Engine.EventBeginWorldSwap.Disconnect(beginworldswap_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginworldswap_event_connection;

// subscribe to the BeginWorldSwap event with a lambda handler function and keeping the connection
beginworldswap_event_connection = Engine.EventBeginWorldSwap.Connect(() => {
		Log.Message("Handling BeginWorldSwap event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginworldswap_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginworldswap_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginworldswap_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginWorldSwap events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventBeginWorldSwap.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventBeginWorldSwap.Enabled = true;

```

</details>

## 🔒︎ Event EventEndWorldSwap

The event triggered after the world logic swap() function is executed. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndWorldSwap event handler
void endworldswap_event_handler()
{
	Log.Message("\Handling EndWorldSwap event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endworldswap_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventEndWorldSwap.Connect(endworldswap_event_connections, endworldswap_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventEndWorldSwap.Connect(endworldswap_event_connections, () => {
		Log.Message("Handling EndWorldSwap event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endworldswap_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndWorldSwap event with a handler function
Engine.EventEndWorldSwap.Connect(endworldswap_event_handler);

// remove subscription to the EndWorldSwap event later by the handler function
Engine.EventEndWorldSwap.Disconnect(endworldswap_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endworldswap_event_connection;

// subscribe to the EndWorldSwap event with a lambda handler function and keeping the connection
endworldswap_event_connection = Engine.EventEndWorldSwap.Connect(() => {
		Log.Message("Handling EndWorldSwap event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endworldswap_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endworldswap_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endworldswap_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndWorldSwap events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventEndWorldSwap.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventEndWorldSwap.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginPluginsSwap

The event triggered before the plugin swap() function is called, if it exists. You can subscribe to events via *Connect()* ï¿½and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginPluginsSwap event handler
void beginpluginsswap_event_handler()
{
	Log.Message("\Handling BeginPluginsSwap event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginpluginsswap_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventBeginPluginsSwap.Connect(beginpluginsswap_event_connections, beginpluginsswap_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventBeginPluginsSwap.Connect(beginpluginsswap_event_connections, () => {
		Log.Message("Handling BeginPluginsSwap event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginpluginsswap_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginPluginsSwap event with a handler function
Engine.EventBeginPluginsSwap.Connect(beginpluginsswap_event_handler);

// remove subscription to the BeginPluginsSwap event later by the handler function
Engine.EventBeginPluginsSwap.Disconnect(beginpluginsswap_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginpluginsswap_event_connection;

// subscribe to the BeginPluginsSwap event with a lambda handler function and keeping the connection
beginpluginsswap_event_connection = Engine.EventBeginPluginsSwap.Connect(() => {
		Log.Message("Handling BeginPluginsSwap event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginpluginsswap_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginpluginsswap_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginpluginsswap_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginPluginsSwap events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventBeginPluginsSwap.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventBeginPluginsSwap.Enabled = true;

```

</details>

## 🔒︎ Event EventEndPluginsSwap

The event triggered after the plugin swap() function is called, if it exists. You can subscribe to events via *Connect()* ï¿½and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndPluginsSwap event handler
void endpluginsswap_event_handler()
{
	Log.Message("\Handling EndPluginsSwap event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endpluginsswap_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventEndPluginsSwap.Connect(endpluginsswap_event_connections, endpluginsswap_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventEndPluginsSwap.Connect(endpluginsswap_event_connections, () => {
		Log.Message("Handling EndPluginsSwap event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endpluginsswap_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndPluginsSwap event with a handler function
Engine.EventEndPluginsSwap.Connect(endpluginsswap_event_handler);

// remove subscription to the EndPluginsSwap event later by the handler function
Engine.EventEndPluginsSwap.Disconnect(endpluginsswap_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endpluginsswap_event_connection;

// subscribe to the EndPluginsSwap event with a lambda handler function and keeping the connection
endpluginsswap_event_connection = Engine.EventEndPluginsSwap.Connect(() => {
		Log.Message("Handling EndPluginsSwap event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endpluginsswap_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endpluginsswap_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endpluginsswap_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndPluginsSwap events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventEndPluginsSwap.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventEndPluginsSwap.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginDeleteObjects

The event triggered before the objects are deleted. You can subscribe to events via *Connect()* ï¿½and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginDeleteObjects event handler
void begindeleteobjects_event_handler()
{
	Log.Message("\Handling BeginDeleteObjects event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begindeleteobjects_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventBeginDeleteObjects.Connect(begindeleteobjects_event_connections, begindeleteobjects_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventBeginDeleteObjects.Connect(begindeleteobjects_event_connections, () => {
		Log.Message("Handling BeginDeleteObjects event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
begindeleteobjects_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginDeleteObjects event with a handler function
Engine.EventBeginDeleteObjects.Connect(begindeleteobjects_event_handler);

// remove subscription to the BeginDeleteObjects event later by the handler function
Engine.EventBeginDeleteObjects.Disconnect(begindeleteobjects_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection begindeleteobjects_event_connection;

// subscribe to the BeginDeleteObjects event with a lambda handler function and keeping the connection
begindeleteobjects_event_connection = Engine.EventBeginDeleteObjects.Connect(() => {
		Log.Message("Handling BeginDeleteObjects event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
begindeleteobjects_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
begindeleteobjects_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
begindeleteobjects_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginDeleteObjects events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventBeginDeleteObjects.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventBeginDeleteObjects.Enabled = true;

```

</details>

## 🔒︎ Event EventEndDeleteObjects

The event triggered after the objects are deleted. You can subscribe to events via *Connect()* ï¿½and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndDeleteObjects event handler
void enddeleteobjects_event_handler()
{
	Log.Message("\Handling EndDeleteObjects event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections enddeleteobjects_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventEndDeleteObjects.Connect(enddeleteobjects_event_connections, enddeleteobjects_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventEndDeleteObjects.Connect(enddeleteobjects_event_connections, () => {
		Log.Message("Handling EndDeleteObjects event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
enddeleteobjects_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndDeleteObjects event with a handler function
Engine.EventEndDeleteObjects.Connect(enddeleteobjects_event_handler);

// remove subscription to the EndDeleteObjects event later by the handler function
Engine.EventEndDeleteObjects.Disconnect(enddeleteobjects_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection enddeleteobjects_event_connection;

// subscribe to the EndDeleteObjects event with a lambda handler function and keeping the connection
enddeleteobjects_event_connection = Engine.EventEndDeleteObjects.Connect(() => {
		Log.Message("Handling EndDeleteObjects event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
enddeleteobjects_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
enddeleteobjects_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
enddeleteobjects_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndDeleteObjects events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventEndDeleteObjects.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventEndDeleteObjects.Enabled = true;

```

</details>

## 🔒︎ Event EventEndSwap

The event triggered after the swap stage is finished. You can subscribe to events via *Connect()* ï¿½and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndSwap event handler
void endswap_event_handler()
{
	Log.Message("\Handling EndSwap event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endswap_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventEndSwap.Connect(endswap_event_connections, endswap_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventEndSwap.Connect(endswap_event_connections, () => {
		Log.Message("Handling EndSwap event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endswap_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndSwap event with a handler function
Engine.EventEndSwap.Connect(endswap_event_handler);

// remove subscription to the EndSwap event later by the handler function
Engine.EventEndSwap.Disconnect(endswap_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endswap_event_connection;

// subscribe to the EndSwap event with a lambda handler function and keeping the connection
endswap_event_connection = Engine.EventEndSwap.Connect(() => {
		Log.Message("Handling EndSwap event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endswap_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endswap_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endswap_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndSwap events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventEndSwap.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventEndSwap.Enabled = true;

```

</details>

## 🔒︎ Event EventFocusGained

The event triggered when any of the engine windows gained the focus. You can subscribe to events via *Connect()* ï¿½and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the FocusGained event handler
void focusgained_event_handler()
{
	Log.Message("\Handling FocusGained event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections focusgained_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventFocusGained.Connect(focusgained_event_connections, focusgained_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventFocusGained.Connect(focusgained_event_connections, () => {
		Log.Message("Handling FocusGained event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
focusgained_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the FocusGained event with a handler function
Engine.EventFocusGained.Connect(focusgained_event_handler);

// remove subscription to the FocusGained event later by the handler function
Engine.EventFocusGained.Disconnect(focusgained_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection focusgained_event_connection;

// subscribe to the FocusGained event with a lambda handler function and keeping the connection
focusgained_event_connection = Engine.EventFocusGained.Connect(() => {
		Log.Message("Handling FocusGained event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
focusgained_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
focusgained_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
focusgained_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring FocusGained events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventFocusGained.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventFocusGained.Enabled = true;

```

</details>

## 🔒︎ Event EventFocusLost

The event triggered when all engine windows lost the focus. You can subscribe to events via *Connect()* ï¿½and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the FocusLost event handler
void focuslost_event_handler()
{
	Log.Message("\Handling FocusLost event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections focuslost_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventFocusLost.Connect(focuslost_event_connections, focuslost_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventFocusLost.Connect(focuslost_event_connections, () => {
		Log.Message("Handling FocusLost event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
focuslost_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the FocusLost event with a handler function
Engine.EventFocusLost.Connect(focuslost_event_handler);

// remove subscription to the FocusLost event later by the handler function
Engine.EventFocusLost.Disconnect(focuslost_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection focuslost_event_connection;

// subscribe to the FocusLost event with a lambda handler function and keeping the connection
focuslost_event_connection = Engine.EventFocusLost.Connect(() => {
		Log.Message("Handling FocusLost event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
focuslost_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
focuslost_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
focuslost_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring FocusLost events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventFocusLost.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventFocusLost.Enabled = true;

```

</details>

## 🔒︎ Event<string> EventPluginAdded

The event triggered on loading a plugin. You can subscribe to events via *Connect()*ï¿½ and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)*ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)*ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(string **plugin_name**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the PluginAdded event handler
void pluginadded_event_handler(string plugin_name)
{
	Log.Message("\Handling PluginAdded event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections pluginadded_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventPluginAdded.Connect(pluginadded_event_connections, pluginadded_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventPluginAdded.Connect(pluginadded_event_connections, (string plugin_name) => {
		Log.Message("Handling PluginAdded event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
pluginadded_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the PluginAdded event with a handler function
Engine.EventPluginAdded.Connect(pluginadded_event_handler);

// remove subscription to the PluginAdded event later by the handler function
Engine.EventPluginAdded.Disconnect(pluginadded_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection pluginadded_event_connection;

// subscribe to the PluginAdded event with a lambda handler function and keeping the connection
pluginadded_event_connection = Engine.EventPluginAdded.Connect((string plugin_name) => {
		Log.Message("Handling PluginAdded event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
pluginadded_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
pluginadded_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
pluginadded_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring PluginAdded events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventPluginAdded.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventPluginAdded.Enabled = true;

```

</details>

## 🔒︎ Event<string> EventPluginRemoved

The event triggered on removing a plugin. You can subscribe to events via *Connect()*ï¿½ and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)*ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)*ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(string **plugin_name**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the PluginRemoved event handler
void pluginremoved_event_handler(string plugin_name)
{
	Log.Message("\Handling PluginRemoved event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections pluginremoved_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine.EventPluginRemoved.Connect(pluginremoved_event_connections, pluginremoved_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine.EventPluginRemoved.Connect(pluginremoved_event_connections, (string plugin_name) => {
		Log.Message("Handling PluginRemoved event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
pluginremoved_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the PluginRemoved event with a handler function
Engine.EventPluginRemoved.Connect(pluginremoved_event_handler);

// remove subscription to the PluginRemoved event later by the handler function
Engine.EventPluginRemoved.Disconnect(pluginremoved_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection pluginremoved_event_connection;

// subscribe to the PluginRemoved event with a lambda handler function and keeping the connection
pluginremoved_event_connection = Engine.EventPluginRemoved.Connect((string plugin_name) => {
		Log.Message("Handling PluginRemoved event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
pluginremoved_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
pluginremoved_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
pluginremoved_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring PluginRemoved events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine.EventPluginRemoved.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Engine.EventPluginRemoved.Enabled = true;

```

</details>

### Members

---

## virtual string GetArg ( int num )

Returns a [command line](../../../code/command_line.md) argument by its index.
### Arguments

- *int* **num** - Index of the command line argument.

### Return value

Command line argument.
## virtual float GetArgf ( int num ) =0

Returns a [command line](../../../code/command_line.md) argument by its index converted to a floating point value.
### Arguments

- *int* **num** - Index of the command line argument.

### Return value

Command line argument.
## virtual int GetArgi ( int num ) =0

Returns a [command line](../../../code/command_line.md) argument by its index converted to an integer value.
### Arguments

- *int* **num** - Index of the command line argument.

### Return value

Command line argument.
## static Engine.BUILD_CONFIG BuildConfiguration ( )

Returns the current Engine build configuration.
### Return value

Current build configuration. One of the [BUILD_CONFIG_](#BUILD_CONFIG) values.
## static string getLibraryModulePath ( )

Returns a path to the Engine's dynamic library file.
### Return value

Path to the Engine's dynamic library file.
## virtual int GetEditorFunction ( string name , int num_args )

Returns the editor function identifier.
### Arguments

- *string* **name** - Name of the editor script function.
- *int* **num_args** - Number of editor script function arguments.

### Return value

The editor script function identifier.
## virtual bool IsEditorFunction ( string name , int num_args )

Returns a value indicating if the editor script function exists.
### Arguments

- *string* **name** - Name of the editor script function.
- *int* **num_args** - Number of editor script function arguments.

### Return value

true if the editor script function exists; otherwise, false.
## virtual IntPtr GetEditorInterpreter ( ) =0

Returns a pointer to the editor interpreter.
### Return value

Pointer to the editor interpreter.
## virtual bool IsEditorInterpreter ( ) =0

Returns a value indicating if the function is called from the editor script.
### Return value

true if the function is called from the editor script; otherwise, false.
## virtual bool IsEditorLoaded ( ) =0

Returns a value indicating if the editor script is loaded.
### Return value

true if the editor script is loaded; otherwise, false.
## virtual EditorLogic GetEditorLogic ( int num ) =0

Returns the registered [EditorLogic](../../../api/library/common/logic/class.editorlogic_cs.md) instance by its number.
### Arguments

- *int* **num** - Number of the EditorLogic instance.

### Return value

[EditorLogic](../../../api/library/common/logic/class.editorlogic_cs.md) instance.
## virtual void SetEditorVariable ( string name , Variable v ) =0

Sets the editor script variable by its name.
### Arguments

- *string* **name** - Name of the editor script variable.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **v** - Value of the editor script variable.

## virtual Variable GetEditorVariable ( string name ) =0

Returns the editor script variable by its name.
### Arguments

- *string* **name** - Name of the world script variable.

### Return value

Value of the editor script variable.
## virtual bool IsEditorVariable ( string name ) =0

Returns a value indicating if the editor script variable exists.
### Arguments

- *string* **name** - Name of the editor script variable.

### Return value

true if the editor script variable exists; otherwise, false.
## virtual string GetArg ( int num ) =0

Returns the command-line argument by its index.
### Arguments

- *int* **num** - Index of the argument.

### Return value

Command-line argument
## string GetPluginName ( int num )

Returns the name of the specified loaded plugin by calling its *[GetName()](../../../api/library/common/class.plugin_cs.md#get_name_const_char_ptr)* method.
### Arguments

- *int* **num** - Index of the loaded plugin.

### Return value

Loaded plugin name.
## int GetPluginOrder ( int num )

Returns the execution order of the specified loaded plugin by calling its *[GetOrder()](../../../api/library/common/class.plugin_cs.md#get_order_int)* method.
### Arguments

- *int* **num** - Index of the loaded plugin.

### Return value

Loaded plugin execution order.
## string GetPluginPath ( int num )

Returns a path to a plugin directory specified via [-plugin_path](../../../code/command_line.md#plugin_path).
### Arguments

- *int* **num** - Plugin path number in the row of the specified plugin paths.

### Return value

Path to a plugin directory.
## string GetPluginAbsolutePath ( int num )

Returns an absolute path to a plugin directory.
### Arguments

- *int* **num** - Plugin path number in the row of the specified plugin paths.

### Return value

Absolute path to a plugin directory.
## int GetSystemFunction ( string name , int num_args )

Returns the system function identifier.
### Arguments

- *string* **name** - Name of the system script function.
- *int* **num_args** - Number of system script function arguments.

### Return value

System script function identifier.
## IsSystemFunction ( string name , int num_args )

Checks whether the system script function exists.
### Arguments

- *string* **name** - Name of the system script function.
- *int* **num_args** - Number of system script function arguments.

### Return value

true if the system script function exists; otherwise, false.
## virtual IntPtr GetSystemInterpreter ( ) =0

Returns a pointer to the system interpreter.
### Return value

Pointer to the system interpreter.
## virtual bool IsSystemInterpreter ( ) =0

Checks if the function is called from the system script.
### Return value

true when the function is called from the system script; otherwise, false.
## virtual System GetSystemLogic ( int num ) =0

Returns the registered [SystemLogic](../../../api/library/common/logic/class.systemlogic_cs.md) instance by the given number.
### Arguments

- *int* **num** - Number of the SystemLogic instance.

### Return value

[SystemLogic](../../../api/library/common/logic/class.systemlogic_cs.md) instance.
## void SetSystemVariable ( string name , Variable v )

Sets a system script variable by a name.
### Arguments

- *string* **name** - Name of the system script variable.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **v** - Value of the system script variable.

## Variable GetSystemVariable ( string name )

Returns the system script variable by its name.
### Arguments

- *string* **name** - Name of the system script variable.

### Return value

System script variable.
## bool IsSystemVariable ( string name )

Checks whether a system script variable exists.
### Arguments

- *string* **name** - Name of the system script variable.

### Return value

true if the system script variable exists; otherwise, false.
## int GetWorldFunction ( string name , int num_args )

Returns the world script function identifier.
### Arguments

- *string* **name** - Name of the world script function.
- *int* **num_args** - Number of world script function arguments.

### Return value

World script function identifier.
## bool IsWorldFunction ( string name , int num_args )

Returns value indicating if the world script function exists.
### Arguments

- *string* **name** - Name of the world script function.
- *int* **num_args** - Number of world script function arguments.

### Return value

true if the world script function exists; otherwise, false.
## virtual IntPtr GetWorldInterpreter ( ) =0

Returns a pointer to the world interpreter.
### Return value

Pointer to the world interpreter.
## virtual bool IsWorldInterpreter ( ) =0

Returns a value indicating if the function is called from the world script.
### Return value

true if the function is called from the world script; otherwise, false.
## virtual bool IsWorldLoaded ( ) =0

Returns a value indicating if the world script is loaded.
### Return value

true if the world script is loaded; otherwise, false.
## virtual WorldLogic GetWorldLogic ( int num ) =0

Returns the registered [WorldLogic](../../../api/library/common/logic/class.worldlogic_cs.md) instance by its number.
### Arguments

- *int* **num** - Number of the WorldLogic instance.

### Return value

[WorldLogic](../../../api/library/common/logic/class.worldlogic_cs.md) instance.
## void SetWorldVariable ( string name , Variable v )

Sets a world script variable by its name.
### Arguments

- *string* **name** - Name of the world script variable.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **v** - Value of the world script variable.

## Variable GetWorldVariable ( string name )

Returns a world script variable by its name.
### Arguments

- *string* **name** - Name of the world script variable.

### Return value

World script variable.
## bool IsWorldVariable ( string name )

Returns a value indicating if the world script variable exists.
### Arguments

- *string* **name** - Name of the world script variable.

### Return value

true if the world script variable exists; otherwise, false.
## bool AddEditorLogic ( EditorLogic logic )

Adds an [EditorLogic](../../../api/library/common/logic/class.editorlogic_cs.md) instance to the engine runtime.
### Arguments

- *[EditorLogic](../../../api/library/common/logic/class.editorlogic_cs.md)* **logic** - [EditorLogic](../../../api/library/common/logic/class.editorlogic_cs.md) instance.

### Return value

true if the EditorLogic instance has been added successfully; otherwise, false.
## virtual bool AddPlugin ( Plugin plugin ) =0

Adds a plugin to engine runtime by using a pointer to this plugin.
### Arguments

- *[Plugin](../../../api/library/common/class.plugin_cs.md)* **plugin** - Plugin.

### Return value

true if the plugin ha been added successfully; otherwise, false.
## bool AddPlugin ( string name )

Adds a plugin to engine runtime by its name.
### Arguments

- *string* **name** - Plugin name.

### Return value

true if the plugin has been added successfully; otherwise, false.
## bool AddSystemLogic ( System logic )

Adds a [SystemLogic](../../../api/library/common/logic/class.systemlogic_cs.md) instance to Engine runtime.
### Arguments

- *System* **logic** - [SystemLogic](../../../api/library/common/logic/class.systemlogic_cs.md) instance.

### Return value

true if the SystemLogic instance has been added successfully; otherwise, false.
## bool AddWorldLogic ( WorldLogic logic )


Adds a [WorldLogic](../../../api/library/common/logic/class.worldlogic_cs.md) instance to the engine runtime.


> **Notice:** Instances of the *WorldLogic* class **should not be added while the world is loaded** and the world script is being executed (as you can't change a world script while the world is loaded). In such a case the ***init()*** method shall not be called if the WorldLogic is added before opening the world.


### Arguments

- *[WorldLogic](../../../api/library/common/logic/class.worldlogic_cs.md)* **logic** - [WorldLogic](../../../api/library/common/logic/class.worldlogic_cs.md) instance.

### Return value

true if the WorldLogic instance has been added successfully; otherwise, false.
## int FindPlugin ( string name )

Searches the index of the loaded plugin by its name.
### Arguments

- *string* **name** - Name of the plugin.

### Return value

Index of the plugin if it is found, or -1 otherwise.
## void Main ( SystemLogic system , WorldLogic world , EditorLogic editor )

Engine main loop. Replaces the following commands:
```cpp
while (!Engine::get()->isQuit()) {
	Engine::get()->update();
	Engine::get()->render();
	Engine::get()->swap();
}

```


```csharp
while (!Engine.IsQuit) {
	Engine.Update();
	Engine.Render();
	Engine.Swap();
}

```


### Arguments

- *[SystemLogic](../../../api/library/common/logic/class.systemlogic_cs.md)* **system** - A [SystemLogic](../../../api/library/common/logic/class.systemlogic_cs.md) instance.
- *[WorldLogic](../../../api/library/common/logic/class.worldlogic_cs.md)* **world** - A [WorldLogic](../../../api/library/common/logic/class.worldlogic_cs.md) instance.
- *[EditorLogic](../../../api/library/common/logic/class.editorlogic_cs.md)* **editor** - An [EditorLogic](../../../api/library/common/logic/class.editorlogic_cs.md) instance.

## bool RemoveEditorLogic ( EditorLogic logic )

Removes an [EditorLogic](../../../api/library/common/logic/class.editorlogic_cs.md) instance from engine runtime.
### Arguments

- *[EditorLogic](../../../api/library/common/logic/class.editorlogic_cs.md)* **logic** - An [EditorLogic](../../../api/library/common/logic/class.editorlogic_cs.md) instance.

### Return value

true if the instance has been removed successfully; otherwise, false.
## virtual bool DestroyPlugin ( Plugin plugin ) =0

Removes the specified plugin.
### Arguments

- *[Plugin](../../../api/library/common/class.plugin_cs.md)* **plugin** - Plugin instance to remove.

### Return value

true if the plugin has been removed successfully; otherwise, false.
## bool RemoveSystemLogic ( System logic )

Removes a [SystemLogic](../../../api/library/common/logic/class.systemlogic_cs.md) instance from engine runtime.
### Arguments

- *System* **logic** - A [SystemLogic](../../../api/library/common/logic/class.systemlogic_cs.md) instance.

### Return value

true if the instance has been removed successfully; otherwise, false.
## bool RemoveWorldLogic ( WorldLogic logic )


Removes a [WorldLogic](../../../api/library/common/logic/class.worldlogic_cs.md) instance from engine runtime.


> **Notice:** Instances of the *WorldLogic* class **should not be removed while the world is loaded** and the world script is being executed (as you can't change a world script while the world is loaded). In such a case the ***shutdown()*** method shall not be called if the WorldLogic is removed before closing the world.


### Arguments

- *[WorldLogic](../../../api/library/common/logic/class.worldlogic_cs.md)* **logic** - A [WorldLogic](../../../api/library/common/logic/class.worldlogic_cs.md) instance.

### Return value

true if the instance has been removed successfully; otherwise, false.
## virtual Variable RunEditorFunction ( Variable name ) =0

Runs the editor script function by its name. The target function can receive up to 8 arguments.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **name** - Name of the editor script function.

### Return value

Editor script function return value.
## Variable RunEditorFunction ( Variable name , Variable a0 )

Runs the editor script function by its name. The target function must receive 1 argument.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **name** - Name of the editor script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.

### Return value

Editor script function return value.
## Variable RunEditorFunction ( Variable name , Variable a0 , Variable a1 )

Runs the editor script function by its name. The target function must receive 2 arguments.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **name** - Name of the editor script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a1** - Second argument.

### Return value

Editor script function return value.
## Variable RunEditorFunction ( Variable name , Variable a0 , Variable a1 , Variable a2 )

Runs the editor script function by its name. The target function must receive 3 arguments.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **name** - Name of the editor script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a1** - Second argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a2** - Third argument.

### Return value

Editor script function return value.
## Variable RunEditorFunction ( Variable name , Variable a0 , Variable a1 , Variable a2 , Variable a3 )

Runs the editor script function by its name. The target function must receive 4 arguments.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **name** - Name of the editor script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a1** - Second argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a2** - Third argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a3** - Fourth argument.

### Return value

Editor script function return value.
## Variable RunEditorFunction ( Variable name , Variable a0 , Variable a1 , Variable a2 , Variable a3 , Variable a4 )

Runs the editor script function by its name. The target function must receive 5 arguments.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **name** - Name of the editor script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a1** - Second argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a2** - Third argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a3** - Fourth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a4** - Fifth argument.

### Return value

Editor script function return value.
## Variable RunEditorFunction ( Variable name , Variable a0 , Variable a1 , Variable a2 , Variable a3 , Variable a4 , Variable a5 )

Runs the editor script function by its name. The target function must receive 6 arguments.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **name** - Name of the editor script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a1** - Second argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a2** - Third argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a3** - Fourth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a4** - Fifth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a5** - Sixth argument.

### Return value

Editor script function return value.
## Variable RunEditorFunction ( Variable name , Variable a0 , Variable a1 , Variable a2 , Variable a3 , Variable a4 , Variable a5 , Variable a6 )

Runs the editor script function by its name. The target function must receive 7 arguments.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **name** - Name of the editor script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a1** - Second argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a2** - Third argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a3** - Fourth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a4** - Fifth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a5** - Sixth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a6** - Seventh argument.

### Return value

Editor script function return value.
## Variable RunEditorFunction ( Variable name , Variable a0 , Variable a1 , Variable a2 , Variable a3 , Variable a4 , Variable a5 , Variable a6 , Variable a7 )

Runs the editor script function by its name. The target function must receive 8 arguments.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **name** - Name of the editor script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a1** - Second argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a2** - Third argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a3** - Fourth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a4** - Fifth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a5** - Sixth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a6** - Seventh argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a7** - Eighth argument.

### Return value

Editor script function return value.
## Variable RunEditorFunction ( int id )

Runs the editor script function by its id. The target function can receive up to 8 arguments.
### Arguments

- *int* **id** - ID of the editor script function.

### Return value

Editor script function return value.
## Variable RunEditorFunction ( int id , Variable a0 )

Runs the editor script function by its name. The target function must receive 1 argument.
### Arguments

- *int* **id** - ID of the editor script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.

### Return value

Editor script function return value.
## Variable RunEditorFunction ( int id , Variable a0 , Variable a1 )

Runs the editor script function by its name. The target function must receive 2 arguments.
### Arguments

- *int* **id** - ID of the editor script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a1** - Second argument.

### Return value

Editor script function return value.
## Variable RunEditorFunction ( int id , Variable a0 , Variable a1 , Variable a2 )

Runs the editor script function by its name. The target function must receive 3 arguments.
### Arguments

- *int* **id** - ID of the editor script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a1** - Second argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a2** - Third argument.

### Return value

Editor script function return value.
## Variable RunEditorFunction ( int id , Variable a0 , Variable a1 , Variable a2 , Variable a3 )

Runs the editor script function by its name. The target function must receive 4 arguments.
### Arguments

- *int* **id** - ID of the editor script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a1** - Second argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a2** - Third argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a3** - Fourth argument.

### Return value

Editor script function return value.
## Variable RunEditorFunction ( int id , Variable a0 , Variable a1 , Variable a2 , Variable a3 , Variable a4 )

Runs the editor script function by its name. The target function must receive 5 arguments.
### Arguments

- *int* **id** - ID of the editor script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a1** - Second argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a2** - Third argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a3** - Fourth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a4** - Fifth argument.

### Return value

Editor script function return value.
## Variable RunEditorFunction ( int id , Variable a0 , Variable a1 , Variable a2 , Variable a3 , Variable a4 , Variable a5 )

Runs the editor script function by its name. The target function must receive 6 arguments.
### Arguments

- *int* **id** - ID of the editor script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a1** - Second argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a2** - Third argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a3** - Fourth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a4** - Fifth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a5** - Sixth argument.

### Return value

Editor script function return value.
## Variable RunEditorFunction ( int id , Variable a0 , Variable a1 , Variable a2 , Variable a3 , Variable a4 , Variable a5 , Variable a6 )

Runs the editor script function by its name. The target function must receive 7 arguments.
### Arguments

- *int* **id** - ID of the editor script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a1** - Second argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a2** - Third argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a3** - Fourth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a4** - Fifth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a5** - Sixth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a6** - Seventh argument.

### Return value

Editor script function return value.
## Variable RunEditorFunction ( int id , Variable a0 , Variable a1 , Variable a2 , Variable a3 , Variable a4 , Variable a5 , Variable a6 , Variable a7 )

Runs the editor script function by its name. The target function must receive 8 arguments.
### Arguments

- *int* **id** - ID of the editor script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a1** - Second argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a2** - Third argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a3** - Fourth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a4** - Fifth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a5** - Sixth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a6** - Seventh argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a7** - Eighth argument.

### Return value

Editor script function return value.
## virtual Variable RunSystemFunction ( Variable name ) =0

Runs the system script function by its name. The target function can receive up to 8 arguments.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **name** - Name of the system script function.

### Return value

System script function return value.
## Variable RunSystemFunction ( Variable name , Variable a0 )

Runs the system script function by its name. The target function must receive 1 argument.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **name** - Name of the system script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.

### Return value

System script function return value.
## Variable RunSystemFunction ( Variable name , Variable a0 , Variable a1 )

Runs the system script function by its name. The target function must receive 2 arguments.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **name** - Name of the system script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a1** - Second argument.

### Return value

System script function return value.
## Variable RunSystemFunction ( Variable name , Variable a0 , Variable a1 , Variable a2 )

Runs the system script function by its name. The target function must receive 3 arguments.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **name** - Name of the system script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a1** - Second argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a2** - Third argument.

### Return value

System script function return value.
## Variable RunSystemFunction ( Variable name , Variable a0 , Variable a1 , Variable a2 , Variable a3 )

Runs the system script function by its name. The target function must receive 4 arguments.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **name** - Name of the system script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a1** - Second argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a2** - Third argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a3** - Fourth argument.

### Return value

System script function return value.
## Variable RunSystemFunction ( Variable name , Variable a0 , Variable a1 , Variable a2 , Variable a3 , Variable a4 )

Runs the system script function by its name. The target function must receive 4 arguments.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **name** - Name of the system script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a1** - Second argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a2** - Third argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a3** - Fourth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a4** - Fifth argument.

### Return value

System script function return value.
## Variable RunSystemFunction ( Variable name , Variable a0 , Variable a1 , Variable a2 , Variable a3 , Variable a4 , Variable a5 )

Runs the system script function by its name. The target function must receive 6 arguments.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **name** - Name of the system script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a1** - Second argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a2** - Third argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a3** - Fourth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a4** - Fifth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a5** - Sixth argument.

### Return value

System script function return value.
## Variable RunSystemFunction ( Variable name , Variable a0 , Variable a1 , Variable a2 , Variable a3 , Variable a4 , Variable a5 , Variable a6 )

Runs the system script function by its name. The target function must receive 7 arguments.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **name** - Name of the system script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a1** - Second argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a2** - Third argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a3** - Fourth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a4** - Fifth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a5** - Sixth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a6** - Seventh argument.

### Return value

System script function return value.
## Variable RunSystemFunction ( Variable name , Variable a0 , Variable a1 , Variable a2 , Variable a3 , Variable a4 , Variable a5 , Variable a6 , Variable a7 )

Runs the system script function by its name. The target function must receive 8 arguments.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **name** - Name of the system script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a1** - Second argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a2** - Third argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a3** - Fourth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a4** - Fifth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a5** - Sixth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a6** - Seventh argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a7** - Eighth argument.

### Return value

System script function return value.
## Variable RunSystemFunction ( int id )

Runs the system script function by its id. The target function can receive up to 8 arguments.
### Arguments

- *int* **id** - ID of the system script function.

### Return value

System script function return value.
## Variable RunSystemFunction ( int id , Variable a0 )

Runs the system script function by its id. The target function must receive 1 argument.
### Arguments

- *int* **id** - ID of the system script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.

### Return value

System script function return value.
## Variable RunSystemFunction ( int id , Variable a0 , Variable a1 )

Runs the system script function by its id. The target function must receive 2 arguments.
### Arguments

- *int* **id** - ID of the system script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a1** - Second argument.

### Return value

System script function return value.
## Variable RunSystemFunction ( int id , Variable a0 , Variable a1 , Variable a2 )

Runs the system script function by its id. The target function must receive 3 arguments.
### Arguments

- *int* **id** - ID of the system script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a1** - Second argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a2** - Third argument.

### Return value

System script function return value.
## Variable RunSystemFunction ( int id , Variable a0 , Variable a1 , Variable a2 , Variable a3 )

Runs the system script function by its id. The target function must receive 4 arguments.
### Arguments

- *int* **id** - ID of the system script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a1** - Second argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a2** - Third argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a3** - Fourth argument.

### Return value

System script function return value.
## Variable RunSystemFunction ( int id , Variable a0 , Variable a1 , Variable a2 , Variable a3 , Variable a4 )

Runs the system script function by its id. The target function must receive 5 arguments.
### Arguments

- *int* **id** - ID of the system script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a1** - Second argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a2** - Third argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a3** - Fourth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a4** - Fifth argument.

### Return value

System script function return value.
## Variable RunSystemFunction ( int id , Variable a0 , Variable a1 , Variable a2 , Variable a3 , Variable a4 , Variable a5 )

Runs the system script function by its id. The target function must receive 6 arguments.
### Arguments

- *int* **id** - ID of the system script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a1** - Second argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a2** - Third argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a3** - Fourth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a4** - Fifth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a5** - Sixth argument.

### Return value

System script function return value.
## Variable RunSystemFunction ( int id , Variable a0 , Variable a1 , Variable a2 , Variable a3 , Variable a4 , Variable a5 , Variable a6 )

Runs the system script function by its id. The target function must receive 7 arguments.
### Arguments

- *int* **id** - ID of the system script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a1** - Second argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a2** - Third argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a3** - Fourth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a4** - Fifth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a5** - Sixth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a6** - Seventh argument.

### Return value

System script function return value.
## Variable RunSystemFunction ( int id , Variable a0 , Variable a1 , Variable a2 , Variable a3 , Variable a4 , Variable a5 , Variable a6 , Variable a7 )

Runs the system script function by its id. The target function must receive 8 arguments.
### Arguments

- *int* **id** - ID of the system script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a1** - Second argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a2** - Third argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a3** - Fourth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a4** - Fifth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a5** - Sixth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a6** - Seventh argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a7** - Eighth argument.

### Return value

System script function return value.
## virtual Variable RunWorldFunction ( Variable name ) =0

Runs the world script function by its name. The target function can receive up to 8 arguments.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **name** - Name of the world script function.

### Return value

World script function return value.
## Variable RunWorldFunction ( Variable name , Variable a0 )

Runs the world script function by its name. The target function must receive 1 argument.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **name** - Name of the world script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.

### Return value

World script function return value.
## Variable RunWorldFunction ( int id , Variable a0 )

Runs the world script function by its identifier. The target function must receive one argument.
### Arguments

- *int* **id** - Identifier of the world script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - Argument

### Return value

World script function return value.
## Variable RunWorldFunction ( Variable name , Variable a0 , Variable a1 )

Runs the world script function by its name. The target function must receive 2 arguments.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **name** - Name of the world script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a1** - Second argument.

### Return value

World script function return value.
## Variable RunWorldFunction ( Variable name , Variable a0 , Variable a1 , Variable a2 )

Runs the world script function by its name. The target function must receive 3 arguments.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **name** - Name of the world script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a1** - Second argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a2** - Third argument.

### Return value

World script function return value.
## Variable RunWorldFunction ( Variable name , Variable a0 , Variable a1 , Variable a2 , Variable a3 )

Runs the world script function by its name. The target function must receive 4 arguments.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **name** - Name of the world script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a1** - Second argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a2** - Third argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a3** - Fourth argument.

### Return value

World script function return value.
## Variable RunWorldFunction ( Variable name , Variable a0 , Variable a1 , Variable a2 , Variable a3 , Variable a4 )

Runs the world script function by its name. The target function must receive 5 arguments.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **name** - Name of the world script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a1** - Second argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a2** - Third argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a3** - Fourth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a4** - Fifth argument.

### Return value

World script function return value.
## Variable RunWorldFunction ( Variable name , Variable a0 , Variable a1 , Variable a2 , Variable a3 , Variable a4 , Variable a5 )

Runs the world script function by its name. The target function must receive 6 arguments.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **name** - Name of the world script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a1** - Second argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a2** - Third argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a3** - Fourth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a4** - Fifth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a5** - Sixth argument.

### Return value

World script function return value.
## Variable RunWorldFunction ( Variable name , Variable a0 , Variable a1 , Variable a2 , Variable a3 , Variable a4 , Variable a5 , Variable a6 )

Runs the world script function by its name. The target function must receive 8 arguments.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **name** - Name of the world script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a1** - Second argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a2** - Third argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a3** - Fourth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a4** - Fifth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a5** - Sixth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a6** - Seventh argument.

### Return value

World script function return value.
## Variable RunWorldFunction ( Variable name , Variable a0 , Variable a1 , Variable a2 , Variable a3 , Variable a4 , Variable a5 , Variable a6 , Variable a7 )

Runs the world script function by its name. The target function must receive 8 arguments.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **name** - Name of the world script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a1** - Second argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a2** - Third argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a3** - Fourth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a4** - Fifth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a5** - Sixth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a6** - Seventh argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a7** - Eighth argument.

### Return value

World script function return value.
## Variable RunWorldFunction ( int id )

Runs the world script function by its id.
### Arguments

- *int* **id** - ID of the world script function.

### Return value

World script function return value.
## Variable RunWorldFunction ( int id , Variable a0 , Variable a1 )

Runs the world script function by its id. The target function must receive 2 arguments.
### Arguments

- *int* **id** - ID of the world script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a1** - Second argument.

### Return value

World script function return value.
## Variable RunWorldFunction ( int id , Variable a0 , Variable a1 , Variable a2 )

Runs the world script function by its id. The target function must receive 3 arguments.
### Arguments

- *int* **id** - ID of the world script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a1** - Second argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a2** - Third argument.

### Return value

World script function return value.
## Variable RunWorldFunction ( int id , Variable a0 , Variable a1 , Variable a2 , Variable a3 )

### Arguments

- *int* **id** - ID of the world script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a1** - Second argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a2** - Third argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a3** - Fourth argument.

### Return value

World script function return value.Runs the world script function by its id. The target function must receive 4 arguments.
## Variable RunWorldFunction ( int id , Variable a0 , Variable a1 , Variable a2 , Variable a3 , Variable a4 )

Runs the world script function by its id. The target function must receive 5 arguments.
### Arguments

- *int* **id** - ID of the world script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a1** - Second argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a2** - Third argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a3** - Fourth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a4** - Fifth argument.

### Return value

World script function return value.
## Variable RunWorldFunction ( int id , Variable a0 , Variable a1 , Variable a2 , Variable a3 , Variable a4 , Variable a5 )

Runs the world script function by its id. The target function must receive 6 arguments.
### Arguments

- *int* **id** - ID of the world script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a1** - Second argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a2** - Third argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a3** - Fourth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a4** - Fifth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a5** - Sixth argument.

### Return value

World script function return value.
## Variable RunWorldFunction ( int id , Variable a0 , Variable a1 , Variable a2 , Variable a3 , Variable a4 , Variable a5 , Variable a6 )

Runs the world script function by its id. The target function must receive 7 arguments.
### Arguments

- *int* **id** - ID of the world script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a1** - Second argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a2** - Third argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a3** - Fourth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a4** - Fifth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a5** - Sixth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a6** - Seventh argument.

### Return value

World script function return value.
## Variable RunWorldFunction ( int id , Variable a0 , Variable a1 , Variable a2 , Variable a3 , Variable a4 , Variable a5 , Variable a6 , Variable a7 )

Runs the world script function by its id. The target function must receive 8 arguments.
### Arguments

- *int* **id** - ID of the world script function.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a0** - First argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a1** - Second argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a2** - Third argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a3** - Fourth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a4** - Fifth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a5** - Sixth argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a6** - Seventh argument.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **a7** - Eighth argument.

### Return value

World script function return value.
## void Shutdown ( )

Deletes the pointer to the existing engine instance.
## virtual void Iterate ( ) =0

Engine iterate function (update, render, swap). This function must be called every frame.
## void BeginOutsideLoopRender ( )

Starts a block of code where you can call *[Render](../../../api/library/rendering/class.render_cs.md)* class methods from outside the Engine's Loop. The end of this block should be marked with a call to the **[EndOutsideLoopRender()](../../...md#endOutsideLoopRender_void)** method.
## void EndOutsideLoopRender ( )

Closes a block of code where you can call *[Render](../../../api/library/rendering/class.render_cs.md)* class methods from outside the Engine's Loop started with a call to the **[BeginOutsideLoopRender()](../../...md#beginOutsideLoopRender_void)** method.
## void StartFps ( )

Starts the FPS counter if it was stopped. All function calls are placed into a stack, so the number of calls to this function should correspond to the number of calls to the *[stopFps()](#stopFps_void)* function.
## void StopFps ( )

Stops the FPS counter. This function should be called if application window is hidden or some heavy non-rendering tasks are processing. All function calls are placed into a stack, so the number of calls to this function should correspond to the number of calls to the *[startFps()](#startFps_void)* function.
## int GetVideoContextFlags ( )

Returns the current video context flags.
### Return value

A set of current video context flags as an integer value.
## static void Init ( string[] args )

Initializes a new engine instance to be used with an external graphics application.
### Arguments

- *string[]* **args** - Array of [command line arguments](../../../code/command_line.md).

## static void Init ( InitParameters init_parameters , string[] args )

Initializes a new engine instance to be used with an external graphics application.
### Arguments

- *InitParameters* **init_parameters** - Structure of [initializing parameters](#init_parameters).
- *string[]* **args** - Array of [command line arguments](../../../code/command_line.md).

## void Quit ( )

The Engine requests to exit the application.
