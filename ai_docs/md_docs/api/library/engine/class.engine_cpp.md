# Unigine::Engine Class (CPP)

**Header:** #include <UnigineEngine.h>


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
| **system_proxy** | Instance of the [CustomSystemProxy](../../../api/library/engine/class.customsystemproxy_cpp.md) class. |


## Engine Class

### Enums

## BUILD_CONFIG

Engine build configuration.
| Name | Description |
|---|---|
| **BUILD_CONFIG_DEBUG** = 0 | Debug build configuration. |
| **BUILD_CONFIG_DEVELOPMENT** = 1 | Development build configuration. |
| **BUILD_CONFIG_RELEASE** = 2 | Release build configuration. |

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
| **PRECISION_PRECISION_FLOAT** = 0 | Float precision type. |
| **PRECISION_PRECISION_DOUBLE** = 1 | Double precision type. |

### Members

## static bool isInitialized () const

Returns the current value indicating whether the engine is initialized.
### Return value

**true** if the Engine is initialized; otherwise **false**.
## static const char * getAppPath () const

Returns the current path to a directory where binary executable file is stored.
### Return value

Current path to a directory where binary executable file is stored.
## static const char * getDataPath () const

Returns the current path to the data directory.
### Return value

Current path to the data directory.
## static const char * getHomePath () const

Returns the current path to the user's home directory.
### Return value

Current path to the user's home directory.
## static const char * getSavePath () const

Returns the current path to a directory with the default configuration file, saved files, etc.
### Return value

Current path to a directory with the default configuration file, saved files, etc.
## static const char * getCachePath () const

Returns the current path to the directory with cached files.
### Return value

Current path to the directory with cached files.
## static int getNumPluginPaths () const

Returns the current number of directory paths to plugins that were set using the [-plugin_path](../../../code/command_line.md#plugin_path) startup command-line option.
### Return value

Current number of directory paths to plugins that were set using the [-plugin_path](../../../code/command_line.md#plugin_path) startup command-line option.
## static const char * getSystemScript () const

Returns the current path to the system script.
### Return value

Current path to the system script.
## static const char * getSystemCache () const

Returns the current path to the system script cache.
### Return value

Current path to the system script cache.
## static const char * getEditorCache () const

Returns the current path to the editor script cache.
### Return value

Current path to the editor script cache.
## static const char * getVideoApp () const

Returns the current graphics API used for rendering.
### Return value

Current graphics API used for rendering.
## static const char * getSoundApp () const

Returns the current sound API used.
### Return value

Current sound API used.
## static const char * getExternDefine () const

Returns the current list of [external definitions](../../../code/command_line.md#extern_define) specified on the application start-up.
### Return value

Current list of external definitions.
## static const char * getFeatures () const

Returns the current list of features like Direct3D, Microprofile, Geodetic, etc.
### Return value

Current list of features like Direct3D, Microprofile, Geodetic, etc.
## static const char * getVersion () const

Returns the current engine version info.
### Return value

Current engine version info.
## static void setBackgroundUpdate ( Engine.BACKGROUND_UPDATE update )

Sets a new value indicating whether the application window is updated when the window is hidden or out of focus (rendering frames in background). By default your UNIGINE application stops rendering frames and updating its main window, when it window goes out of focus (e.g. user switches to another window). Setting the background update mode enables constant rendering regardless of whether the application window is focused or in the background.
### Arguments

- *[Engine.BACKGROUND_UPDATE](../../../api/library/engine/class.engine_cpp.md#BACKGROUND_UPDATE)* **update** - The value indicating whether the application window is updated when the window is hidden or out of focus (rendering frames in background).

## static Engine.BACKGROUND_UPDATE getBackgroundUpdate () const

Returns the current value indicating whether the application window is updated when the window is hidden or out of focus (rendering frames in background). By default your UNIGINE application stops rendering frames and updating its main window, when it window goes out of focus (e.g. user switches to another window). Setting the background update mode enables constant rendering regardless of whether the application window is focused or in the background.
### Return value

Current value indicating whether the application window is updated when the window is hidden or out of focus (rendering frames in background).
## static bool isActive () const

Returns the current **active** state of the Engine.
### Return value

**true** if the engine is active; otherwise **false**.
## static bool isFocus () const

Returns the current value showing if any of the Engine windows is in focus.
### Return value

**true** if the Engine window is focused; otherwise **false**.
## static bool isQuit () const

Returns the current **quitting** flag on engine quit.
### Return value

**true** if the engine is quitting; otherwise **false**.
## static float getTotalTime () const

Returns the current total time (in milliseconds) that both rendering and calculating of the frame took (the duration of the [main loop](../../../code/fundamentals/execution_sequence/main_loop.md) in the application [execution sequence](../../../code/fundamentals/execution_sequence/index.md)). Includes *update, render, swap and wait GPU*.
### Return value

Current total time value, in milliseconds.
## static float getTotalCPUTime () const

Returns the current total CPU time (in milliseconds) taken to perform calculations for the frame (the duration of the [main loop](../../../code/fundamentals/execution_sequence/main_loop.md) in the application [execution sequence](../../../code/fundamentals/execution_sequence/index.md)). Includes *update, render and swap*.
### Return value

Current total CPU time value, in milliseconds.
## static float getUpdateTime () const

Returns the current duration (in milliseconds) of the [update phase](../../../code/fundamentals/execution_sequence/main_loop.md#update), during which the objects are prepared for their collision response to be calculated.
### Return value

Current update phase duration value, in milliseconds.
## static float getRenderTime () const

Returns the current time (in milliseconds) required to prepare all data to be rendered in the current frame and feed rendering commands from the CPU to the GPU. See the [Profiler](../../../tools/profiling/profiler/index.md#render_cpu) article for details.
### Return value

Current rendering time value, in milliseconds.
## static float getPresentTime () const

Returns the current total time (in milliseconds) spent on waiting for the GPU after all calculations on the CPU are completed. See the [Profiler](../../../tools/profiling/profiler/index.md#present) article for details.
### Return value

Current time value, in milliseconds.
## static float getInterfaceTime () const

Returns the current total accumulative time (in milliseconds) spent on rendering GUI widgets.
### Return value

Current time value, in milliseconds.
## static int64_t getFrame () const

Returns the current number of the current engine frame.
### Return value

Current engine frame number.
## static float getFps () const

Returns the current value of the Engine FPS counter.
### Return value

Current value of the Engine FPS counter.
## static float getIFps () const

Returns the current inverse value of the Engine FPS counter (1/FPS).
### Return value

Current inverse value of the Engine FPS counter (1/FPS).
## static float getStatisticsFpsMin () const

Returns the current minimum FPS counter value for the last 600 frames.
### Return value

Current minimum FPS counter value for the last 600 frames.
## static float getStatisticsFpsAvg () const

Returns the current average FPS counter value for the last 600 frames.
### Return value

Current average FPS counter value for the last 600 frames.
## static float getStatisticsFpsMax () const

Returns the current maximum FPS counter value for the last 600 frames.
### Return value

Current maximum FPS counter value for the last 600 frames.
## static bool isMainThread () const

Returns the current value indicating if the current thread is main.
### Return value

**true** if the current thread is main; otherwise **false**.
## static Ptr < Player > getMainPlayer () const

Returns the current main player.
### Return value

Current main player.
## static bool isEvaluation () const

Returns the current value indicating if the running version of the Engine is for evaluation only.
### Return value

**true** if the evaluation version of the Engine is used; otherwise **false**.
## static int getNumEditorLogics () const

Returns the current number of [EditorLogic](../../../api/library/common/logic/class.editorlogic_cpp.md) instances.
### Return value

Current number of [EditorLogic](../../../api/library/common/logic/class.editorlogic_cpp.md) instances.
## static int getNumWorldLogics () const

Returns the current number of [WorldLogic](../../../api/library/common/logic/class.worldlogic_cpp.md) instances.
### Return value

Current number of [WorldLogic](../../../api/library/common/logic/class.worldlogic_cpp.md) instances.
## static int getNumSystemLogics () const

Returns the current number of [SystemLogic](../../../api/library/common/logic/class.systemlogic_cpp.md) instances.
### Return value

Current number of [SystemLogic](../../../api/library/common/logic/class.systemlogic_cpp.md) instances.
## static int getNumArgs () const

Returns the current number of command line arguments.
### Return value

Current number of command line arguments.
## static int getNumPlugins () const

Returns the current number of loaded plugins.
### Return value

Current number of loaded plugins.
## static Engine::PRECISION getPrecision () const

Returns the current precision type.
### Return value

Current precision type.
## static Event getEventBeginUpdate () const

event triggered before the update stage is started. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginUpdate event handler
void beginupdate_event_handler()
{
	Log::message("\Handling BeginUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventBeginUpdate().connect(beginupdate_event_connections, beginupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventBeginUpdate().connect(beginupdate_event_connections, []() {
		Log::message("\Handling BeginUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginupdate_event_connection;

// subscribe to the BeginUpdate event with a handler function keeping the connection
Engine::getEventBeginUpdate().connect(beginupdate_event_connection, beginupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginUpdate event via the connection
beginupdate_event_connection.disconnect();

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

	// A BeginUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventBeginUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginupdate_handler_id;

// subscribe to the BeginUpdate event with a lambda handler function and keeping connection ID
beginupdate_handler_id = Engine::getEventBeginUpdate().connect(e_connections, []() {
		Log::message("\Handling BeginUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventBeginUpdate().disconnect(beginupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventBeginUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventBeginUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventBeginPropertiesUpdate () const

event triggered before the properties update stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginPropertiesUpdate event handler
void beginpropertiesupdate_event_handler()
{
	Log::message("\Handling BeginPropertiesUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginpropertiesupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventBeginPropertiesUpdate().connect(beginpropertiesupdate_event_connections, beginpropertiesupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventBeginPropertiesUpdate().connect(beginpropertiesupdate_event_connections, []() {
		Log::message("\Handling BeginPropertiesUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginpropertiesupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginpropertiesupdate_event_connection;

// subscribe to the BeginPropertiesUpdate event with a handler function keeping the connection
Engine::getEventBeginPropertiesUpdate().connect(beginpropertiesupdate_event_connection, beginpropertiesupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginpropertiesupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginpropertiesupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginPropertiesUpdate event via the connection
beginpropertiesupdate_event_connection.disconnect();

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

	// A BeginPropertiesUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginPropertiesUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventBeginPropertiesUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginpropertiesupdate_handler_id;

// subscribe to the BeginPropertiesUpdate event with a lambda handler function and keeping connection ID
beginpropertiesupdate_handler_id = Engine::getEventBeginPropertiesUpdate().connect(e_connections, []() {
		Log::message("\Handling BeginPropertiesUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventBeginPropertiesUpdate().disconnect(beginpropertiesupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginPropertiesUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventBeginPropertiesUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventBeginPropertiesUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventEndPropertiesUpdate () const

event triggered after the properties update stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndPropertiesUpdate event handler
void endpropertiesupdate_event_handler()
{
	Log::message("\Handling EndPropertiesUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endpropertiesupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventEndPropertiesUpdate().connect(endpropertiesupdate_event_connections, endpropertiesupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventEndPropertiesUpdate().connect(endpropertiesupdate_event_connections, []() {
		Log::message("\Handling EndPropertiesUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endpropertiesupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endpropertiesupdate_event_connection;

// subscribe to the EndPropertiesUpdate event with a handler function keeping the connection
Engine::getEventEndPropertiesUpdate().connect(endpropertiesupdate_event_connection, endpropertiesupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endpropertiesupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endpropertiesupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the EndPropertiesUpdate event via the connection
endpropertiesupdate_event_connection.disconnect();

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

	// A EndPropertiesUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndPropertiesUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventEndPropertiesUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endpropertiesupdate_handler_id;

// subscribe to the EndPropertiesUpdate event with a lambda handler function and keeping connection ID
endpropertiesupdate_handler_id = Engine::getEventEndPropertiesUpdate().connect(e_connections, []() {
		Log::message("\Handling EndPropertiesUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventEndPropertiesUpdate().disconnect(endpropertiesupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndPropertiesUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventEndPropertiesUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventEndPropertiesUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventBeginInputUpdate () const

event triggered before the input update stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginInputUpdate event handler
void begininputupdate_event_handler()
{
	Log::message("\Handling BeginInputUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begininputupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventBeginInputUpdate().connect(begininputupdate_event_connections, begininputupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventBeginInputUpdate().connect(begininputupdate_event_connections, []() {
		Log::message("\Handling BeginInputUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
begininputupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection begininputupdate_event_connection;

// subscribe to the BeginInputUpdate event with a handler function keeping the connection
Engine::getEventBeginInputUpdate().connect(begininputupdate_event_connection, begininputupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
begininputupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
begininputupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginInputUpdate event via the connection
begininputupdate_event_connection.disconnect();

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

	// A BeginInputUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginInputUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventBeginInputUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId begininputupdate_handler_id;

// subscribe to the BeginInputUpdate event with a lambda handler function and keeping connection ID
begininputupdate_handler_id = Engine::getEventBeginInputUpdate().connect(e_connections, []() {
		Log::message("\Handling BeginInputUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventBeginInputUpdate().disconnect(begininputupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginInputUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventBeginInputUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventBeginInputUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventEndInputUpdate () const

event triggered after the input update stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndInputUpdate event handler
void endinputupdate_event_handler()
{
	Log::message("\Handling EndInputUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endinputupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventEndInputUpdate().connect(endinputupdate_event_connections, endinputupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventEndInputUpdate().connect(endinputupdate_event_connections, []() {
		Log::message("\Handling EndInputUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endinputupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endinputupdate_event_connection;

// subscribe to the EndInputUpdate event with a handler function keeping the connection
Engine::getEventEndInputUpdate().connect(endinputupdate_event_connection, endinputupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endinputupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endinputupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the EndInputUpdate event via the connection
endinputupdate_event_connection.disconnect();

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

	// A EndInputUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndInputUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventEndInputUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endinputupdate_handler_id;

// subscribe to the EndInputUpdate event with a lambda handler function and keeping connection ID
endinputupdate_handler_id = Engine::getEventEndInputUpdate().connect(e_connections, []() {
		Log::message("\Handling EndInputUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventEndInputUpdate().disconnect(endinputupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndInputUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventEndInputUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventEndInputUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventBeginControlsUpdate () const

event triggered before the controls update stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginControlsUpdate event handler
void begincontrolsupdate_event_handler()
{
	Log::message("\Handling BeginControlsUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begincontrolsupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventBeginControlsUpdate().connect(begincontrolsupdate_event_connections, begincontrolsupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventBeginControlsUpdate().connect(begincontrolsupdate_event_connections, []() {
		Log::message("\Handling BeginControlsUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
begincontrolsupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection begincontrolsupdate_event_connection;

// subscribe to the BeginControlsUpdate event with a handler function keeping the connection
Engine::getEventBeginControlsUpdate().connect(begincontrolsupdate_event_connection, begincontrolsupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
begincontrolsupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
begincontrolsupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginControlsUpdate event via the connection
begincontrolsupdate_event_connection.disconnect();

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

	// A BeginControlsUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginControlsUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventBeginControlsUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId begincontrolsupdate_handler_id;

// subscribe to the BeginControlsUpdate event with a lambda handler function and keeping connection ID
begincontrolsupdate_handler_id = Engine::getEventBeginControlsUpdate().connect(e_connections, []() {
		Log::message("\Handling BeginControlsUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventBeginControlsUpdate().disconnect(begincontrolsupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginControlsUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventBeginControlsUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventBeginControlsUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventEndControlsUpdate () const

event triggered after the controls update stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndControlsUpdate event handler
void endcontrolsupdate_event_handler()
{
	Log::message("\Handling EndControlsUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endcontrolsupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventEndControlsUpdate().connect(endcontrolsupdate_event_connections, endcontrolsupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventEndControlsUpdate().connect(endcontrolsupdate_event_connections, []() {
		Log::message("\Handling EndControlsUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endcontrolsupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endcontrolsupdate_event_connection;

// subscribe to the EndControlsUpdate event with a handler function keeping the connection
Engine::getEventEndControlsUpdate().connect(endcontrolsupdate_event_connection, endcontrolsupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endcontrolsupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endcontrolsupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the EndControlsUpdate event via the connection
endcontrolsupdate_event_connection.disconnect();

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

	// A EndControlsUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndControlsUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventEndControlsUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endcontrolsupdate_handler_id;

// subscribe to the EndControlsUpdate event with a lambda handler function and keeping connection ID
endcontrolsupdate_handler_id = Engine::getEventEndControlsUpdate().connect(e_connections, []() {
		Log::message("\Handling EndControlsUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventEndControlsUpdate().disconnect(endcontrolsupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndControlsUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventEndControlsUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventEndControlsUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventBeginWorldManagerUpdate () const

event triggered before the world manager update stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginWorldManagerUpdate event handler
void beginworldmanagerupdate_event_handler()
{
	Log::message("\Handling BeginWorldManagerUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginworldmanagerupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventBeginWorldManagerUpdate().connect(beginworldmanagerupdate_event_connections, beginworldmanagerupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventBeginWorldManagerUpdate().connect(beginworldmanagerupdate_event_connections, []() {
		Log::message("\Handling BeginWorldManagerUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginworldmanagerupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginworldmanagerupdate_event_connection;

// subscribe to the BeginWorldManagerUpdate event with a handler function keeping the connection
Engine::getEventBeginWorldManagerUpdate().connect(beginworldmanagerupdate_event_connection, beginworldmanagerupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginworldmanagerupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginworldmanagerupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginWorldManagerUpdate event via the connection
beginworldmanagerupdate_event_connection.disconnect();

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

	// A BeginWorldManagerUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginWorldManagerUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventBeginWorldManagerUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginworldmanagerupdate_handler_id;

// subscribe to the BeginWorldManagerUpdate event with a lambda handler function and keeping connection ID
beginworldmanagerupdate_handler_id = Engine::getEventBeginWorldManagerUpdate().connect(e_connections, []() {
		Log::message("\Handling BeginWorldManagerUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventBeginWorldManagerUpdate().disconnect(beginworldmanagerupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginWorldManagerUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventBeginWorldManagerUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventBeginWorldManagerUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventEndWorldManagerUpdate () const

event triggered after the world manager update stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndWorldManagerUpdate event handler
void endworldmanagerupdate_event_handler()
{
	Log::message("\Handling EndWorldManagerUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endworldmanagerupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventEndWorldManagerUpdate().connect(endworldmanagerupdate_event_connections, endworldmanagerupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventEndWorldManagerUpdate().connect(endworldmanagerupdate_event_connections, []() {
		Log::message("\Handling EndWorldManagerUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endworldmanagerupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endworldmanagerupdate_event_connection;

// subscribe to the EndWorldManagerUpdate event with a handler function keeping the connection
Engine::getEventEndWorldManagerUpdate().connect(endworldmanagerupdate_event_connection, endworldmanagerupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endworldmanagerupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endworldmanagerupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the EndWorldManagerUpdate event via the connection
endworldmanagerupdate_event_connection.disconnect();

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

	// A EndWorldManagerUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndWorldManagerUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventEndWorldManagerUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endworldmanagerupdate_handler_id;

// subscribe to the EndWorldManagerUpdate event with a lambda handler function and keeping connection ID
endworldmanagerupdate_handler_id = Engine::getEventEndWorldManagerUpdate().connect(e_connections, []() {
		Log::message("\Handling EndWorldManagerUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventEndWorldManagerUpdate().disconnect(endworldmanagerupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndWorldManagerUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventEndWorldManagerUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventEndWorldManagerUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventBeginSoundManagerUpdate () const

event triggered before the sound manager update stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginSoundManagerUpdate event handler
void beginsoundmanagerupdate_event_handler()
{
	Log::message("\Handling BeginSoundManagerUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginsoundmanagerupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventBeginSoundManagerUpdate().connect(beginsoundmanagerupdate_event_connections, beginsoundmanagerupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventBeginSoundManagerUpdate().connect(beginsoundmanagerupdate_event_connections, []() {
		Log::message("\Handling BeginSoundManagerUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginsoundmanagerupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginsoundmanagerupdate_event_connection;

// subscribe to the BeginSoundManagerUpdate event with a handler function keeping the connection
Engine::getEventBeginSoundManagerUpdate().connect(beginsoundmanagerupdate_event_connection, beginsoundmanagerupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginsoundmanagerupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginsoundmanagerupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginSoundManagerUpdate event via the connection
beginsoundmanagerupdate_event_connection.disconnect();

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

	// A BeginSoundManagerUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginSoundManagerUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventBeginSoundManagerUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginsoundmanagerupdate_handler_id;

// subscribe to the BeginSoundManagerUpdate event with a lambda handler function and keeping connection ID
beginsoundmanagerupdate_handler_id = Engine::getEventBeginSoundManagerUpdate().connect(e_connections, []() {
		Log::message("\Handling BeginSoundManagerUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventBeginSoundManagerUpdate().disconnect(beginsoundmanagerupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginSoundManagerUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventBeginSoundManagerUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventBeginSoundManagerUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventEndSoundManagerUpdate () const

event triggered after the sound manager update stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndSoundManagerUpdate event handler
void endsoundmanagerupdate_event_handler()
{
	Log::message("\Handling EndSoundManagerUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endsoundmanagerupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventEndSoundManagerUpdate().connect(endsoundmanagerupdate_event_connections, endsoundmanagerupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventEndSoundManagerUpdate().connect(endsoundmanagerupdate_event_connections, []() {
		Log::message("\Handling EndSoundManagerUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endsoundmanagerupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endsoundmanagerupdate_event_connection;

// subscribe to the EndSoundManagerUpdate event with a handler function keeping the connection
Engine::getEventEndSoundManagerUpdate().connect(endsoundmanagerupdate_event_connection, endsoundmanagerupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endsoundmanagerupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endsoundmanagerupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the EndSoundManagerUpdate event via the connection
endsoundmanagerupdate_event_connection.disconnect();

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

	// A EndSoundManagerUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndSoundManagerUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventEndSoundManagerUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endsoundmanagerupdate_handler_id;

// subscribe to the EndSoundManagerUpdate event with a lambda handler function and keeping connection ID
endsoundmanagerupdate_handler_id = Engine::getEventEndSoundManagerUpdate().connect(e_connections, []() {
		Log::message("\Handling EndSoundManagerUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventEndSoundManagerUpdate().disconnect(endsoundmanagerupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndSoundManagerUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventEndSoundManagerUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventEndSoundManagerUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventBeginGameUpdate () const

event triggered before the game logic update stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginGameUpdate event handler
void begingameupdate_event_handler()
{
	Log::message("\Handling BeginGameUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begingameupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventBeginGameUpdate().connect(begingameupdate_event_connections, begingameupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventBeginGameUpdate().connect(begingameupdate_event_connections, []() {
		Log::message("\Handling BeginGameUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
begingameupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection begingameupdate_event_connection;

// subscribe to the BeginGameUpdate event with a handler function keeping the connection
Engine::getEventBeginGameUpdate().connect(begingameupdate_event_connection, begingameupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
begingameupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
begingameupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginGameUpdate event via the connection
begingameupdate_event_connection.disconnect();

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

	// A BeginGameUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginGameUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventBeginGameUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId begingameupdate_handler_id;

// subscribe to the BeginGameUpdate event with a lambda handler function and keeping connection ID
begingameupdate_handler_id = Engine::getEventBeginGameUpdate().connect(e_connections, []() {
		Log::message("\Handling BeginGameUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventBeginGameUpdate().disconnect(begingameupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginGameUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventBeginGameUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventBeginGameUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventEndGameUpdate () const

event triggered after the game logic update stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndGameUpdate event handler
void endgameupdate_event_handler()
{
	Log::message("\Handling EndGameUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endgameupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventEndGameUpdate().connect(endgameupdate_event_connections, endgameupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventEndGameUpdate().connect(endgameupdate_event_connections, []() {
		Log::message("\Handling EndGameUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endgameupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endgameupdate_event_connection;

// subscribe to the EndGameUpdate event with a handler function keeping the connection
Engine::getEventEndGameUpdate().connect(endgameupdate_event_connection, endgameupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endgameupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endgameupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the EndGameUpdate event via the connection
endgameupdate_event_connection.disconnect();

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

	// A EndGameUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndGameUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventEndGameUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endgameupdate_handler_id;

// subscribe to the EndGameUpdate event with a lambda handler function and keeping connection ID
endgameupdate_handler_id = Engine::getEventEndGameUpdate().connect(e_connections, []() {
		Log::message("\Handling EndGameUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventEndGameUpdate().disconnect(endgameupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndGameUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventEndGameUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventEndGameUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventBeginRenderUpdate () const

event triggered before the render functions update stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginRenderUpdate event handler
void beginrenderupdate_event_handler()
{
	Log::message("\Handling BeginRenderUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginrenderupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventBeginRenderUpdate().connect(beginrenderupdate_event_connections, beginrenderupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventBeginRenderUpdate().connect(beginrenderupdate_event_connections, []() {
		Log::message("\Handling BeginRenderUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginrenderupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginrenderupdate_event_connection;

// subscribe to the BeginRenderUpdate event with a handler function keeping the connection
Engine::getEventBeginRenderUpdate().connect(beginrenderupdate_event_connection, beginrenderupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginrenderupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginrenderupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginRenderUpdate event via the connection
beginrenderupdate_event_connection.disconnect();

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

	// A BeginRenderUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginRenderUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventBeginRenderUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginrenderupdate_handler_id;

// subscribe to the BeginRenderUpdate event with a lambda handler function and keeping connection ID
beginrenderupdate_handler_id = Engine::getEventBeginRenderUpdate().connect(e_connections, []() {
		Log::message("\Handling BeginRenderUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventBeginRenderUpdate().disconnect(beginrenderupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginRenderUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventBeginRenderUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventBeginRenderUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventEndRenderUpdate () const

event triggered after the render functions update stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndRenderUpdate event handler
void endrenderupdate_event_handler()
{
	Log::message("\Handling EndRenderUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endrenderupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventEndRenderUpdate().connect(endrenderupdate_event_connections, endrenderupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventEndRenderUpdate().connect(endrenderupdate_event_connections, []() {
		Log::message("\Handling EndRenderUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endrenderupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endrenderupdate_event_connection;

// subscribe to the EndRenderUpdate event with a handler function keeping the connection
Engine::getEventEndRenderUpdate().connect(endrenderupdate_event_connection, endrenderupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endrenderupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endrenderupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the EndRenderUpdate event via the connection
endrenderupdate_event_connection.disconnect();

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

	// A EndRenderUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndRenderUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventEndRenderUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endrenderupdate_handler_id;

// subscribe to the EndRenderUpdate event with a lambda handler function and keeping connection ID
endrenderupdate_handler_id = Engine::getEventEndRenderUpdate().connect(e_connections, []() {
		Log::message("\Handling EndRenderUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventEndRenderUpdate().disconnect(endrenderupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndRenderUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventEndRenderUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventEndRenderUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventBeginExpressionUpdate () const

event triggered before the expressions update stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginExpressionUpdate event handler
void beginexpressionupdate_event_handler()
{
	Log::message("\Handling BeginExpressionUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginexpressionupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventBeginExpressionUpdate().connect(beginexpressionupdate_event_connections, beginexpressionupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventBeginExpressionUpdate().connect(beginexpressionupdate_event_connections, []() {
		Log::message("\Handling BeginExpressionUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginexpressionupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginexpressionupdate_event_connection;

// subscribe to the BeginExpressionUpdate event with a handler function keeping the connection
Engine::getEventBeginExpressionUpdate().connect(beginexpressionupdate_event_connection, beginexpressionupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginexpressionupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginexpressionupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginExpressionUpdate event via the connection
beginexpressionupdate_event_connection.disconnect();

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

	// A BeginExpressionUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginExpressionUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventBeginExpressionUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginexpressionupdate_handler_id;

// subscribe to the BeginExpressionUpdate event with a lambda handler function and keeping connection ID
beginexpressionupdate_handler_id = Engine::getEventBeginExpressionUpdate().connect(e_connections, []() {
		Log::message("\Handling BeginExpressionUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventBeginExpressionUpdate().disconnect(beginexpressionupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginExpressionUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventBeginExpressionUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventBeginExpressionUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventEndExpressionUpdate () const

event triggered after the expressions update stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndExpressionUpdate event handler
void endexpressionupdate_event_handler()
{
	Log::message("\Handling EndExpressionUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endexpressionupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventEndExpressionUpdate().connect(endexpressionupdate_event_connections, endexpressionupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventEndExpressionUpdate().connect(endexpressionupdate_event_connections, []() {
		Log::message("\Handling EndExpressionUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endexpressionupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endexpressionupdate_event_connection;

// subscribe to the EndExpressionUpdate event with a handler function keeping the connection
Engine::getEventEndExpressionUpdate().connect(endexpressionupdate_event_connection, endexpressionupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endexpressionupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endexpressionupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the EndExpressionUpdate event via the connection
endexpressionupdate_event_connection.disconnect();

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

	// A EndExpressionUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndExpressionUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventEndExpressionUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endexpressionupdate_handler_id;

// subscribe to the EndExpressionUpdate event with a lambda handler function and keeping connection ID
endexpressionupdate_handler_id = Engine::getEventEndExpressionUpdate().connect(e_connections, []() {
		Log::message("\Handling EndExpressionUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventEndExpressionUpdate().disconnect(endexpressionupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndExpressionUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventEndExpressionUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventEndExpressionUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventBeginSoundsUpdate () const

event triggered before the sounds update stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginSoundsUpdate event handler
void beginsoundsupdate_event_handler()
{
	Log::message("\Handling BeginSoundsUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginsoundsupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventBeginSoundsUpdate().connect(beginsoundsupdate_event_connections, beginsoundsupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventBeginSoundsUpdate().connect(beginsoundsupdate_event_connections, []() {
		Log::message("\Handling BeginSoundsUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginsoundsupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginsoundsupdate_event_connection;

// subscribe to the BeginSoundsUpdate event with a handler function keeping the connection
Engine::getEventBeginSoundsUpdate().connect(beginsoundsupdate_event_connection, beginsoundsupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginsoundsupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginsoundsupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginSoundsUpdate event via the connection
beginsoundsupdate_event_connection.disconnect();

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

	// A BeginSoundsUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginSoundsUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventBeginSoundsUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginsoundsupdate_handler_id;

// subscribe to the BeginSoundsUpdate event with a lambda handler function and keeping connection ID
beginsoundsupdate_handler_id = Engine::getEventBeginSoundsUpdate().connect(e_connections, []() {
		Log::message("\Handling BeginSoundsUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventBeginSoundsUpdate().disconnect(beginsoundsupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginSoundsUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventBeginSoundsUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventBeginSoundsUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventEndSoundsUpdate () const

event triggered after the sounds update stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndSoundsUpdate event handler
void endsoundsupdate_event_handler()
{
	Log::message("\Handling EndSoundsUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endsoundsupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventEndSoundsUpdate().connect(endsoundsupdate_event_connections, endsoundsupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventEndSoundsUpdate().connect(endsoundsupdate_event_connections, []() {
		Log::message("\Handling EndSoundsUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endsoundsupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endsoundsupdate_event_connection;

// subscribe to the EndSoundsUpdate event with a handler function keeping the connection
Engine::getEventEndSoundsUpdate().connect(endsoundsupdate_event_connection, endsoundsupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endsoundsupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endsoundsupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the EndSoundsUpdate event via the connection
endsoundsupdate_event_connection.disconnect();

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

	// A EndSoundsUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndSoundsUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventEndSoundsUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endsoundsupdate_handler_id;

// subscribe to the EndSoundsUpdate event with a lambda handler function and keeping connection ID
endsoundsupdate_handler_id = Engine::getEventEndSoundsUpdate().connect(e_connections, []() {
		Log::message("\Handling EndSoundsUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventEndSoundsUpdate().disconnect(endsoundsupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndSoundsUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventEndSoundsUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventEndSoundsUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventBeginPluginsUpdate () const

event triggered before the plugins update stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginPluginsUpdate event handler
void beginpluginsupdate_event_handler()
{
	Log::message("\Handling BeginPluginsUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginpluginsupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventBeginPluginsUpdate().connect(beginpluginsupdate_event_connections, beginpluginsupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventBeginPluginsUpdate().connect(beginpluginsupdate_event_connections, []() {
		Log::message("\Handling BeginPluginsUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginpluginsupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginpluginsupdate_event_connection;

// subscribe to the BeginPluginsUpdate event with a handler function keeping the connection
Engine::getEventBeginPluginsUpdate().connect(beginpluginsupdate_event_connection, beginpluginsupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginpluginsupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginpluginsupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginPluginsUpdate event via the connection
beginpluginsupdate_event_connection.disconnect();

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

	// A BeginPluginsUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginPluginsUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventBeginPluginsUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginpluginsupdate_handler_id;

// subscribe to the BeginPluginsUpdate event with a lambda handler function and keeping connection ID
beginpluginsupdate_handler_id = Engine::getEventBeginPluginsUpdate().connect(e_connections, []() {
		Log::message("\Handling BeginPluginsUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventBeginPluginsUpdate().disconnect(beginpluginsupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginPluginsUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventBeginPluginsUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventBeginPluginsUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventEndPluginsUpdate () const

event triggered after the plugins update stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndPluginsUpdate event handler
void endpluginsupdate_event_handler()
{
	Log::message("\Handling EndPluginsUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endpluginsupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventEndPluginsUpdate().connect(endpluginsupdate_event_connections, endpluginsupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventEndPluginsUpdate().connect(endpluginsupdate_event_connections, []() {
		Log::message("\Handling EndPluginsUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endpluginsupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endpluginsupdate_event_connection;

// subscribe to the EndPluginsUpdate event with a handler function keeping the connection
Engine::getEventEndPluginsUpdate().connect(endpluginsupdate_event_connection, endpluginsupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endpluginsupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endpluginsupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the EndPluginsUpdate event via the connection
endpluginsupdate_event_connection.disconnect();

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

	// A EndPluginsUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndPluginsUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventEndPluginsUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endpluginsupdate_handler_id;

// subscribe to the EndPluginsUpdate event with a lambda handler function and keeping connection ID
endpluginsupdate_handler_id = Engine::getEventEndPluginsUpdate().connect(e_connections, []() {
		Log::message("\Handling EndPluginsUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventEndPluginsUpdate().disconnect(endpluginsupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndPluginsUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventEndPluginsUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventEndPluginsUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventBeginVRUpdate () const

event triggered before the VR update stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginVRUpdate event handler
void beginvrupdate_event_handler()
{
	Log::message("\Handling BeginVRUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginvrupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventBeginVRUpdate().connect(beginvrupdate_event_connections, beginvrupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventBeginVRUpdate().connect(beginvrupdate_event_connections, []() {
		Log::message("\Handling BeginVRUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginvrupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginvrupdate_event_connection;

// subscribe to the BeginVRUpdate event with a handler function keeping the connection
Engine::getEventBeginVRUpdate().connect(beginvrupdate_event_connection, beginvrupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginvrupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginvrupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginVRUpdate event via the connection
beginvrupdate_event_connection.disconnect();

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

	// A BeginVRUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginVRUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventBeginVRUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginvrupdate_handler_id;

// subscribe to the BeginVRUpdate event with a lambda handler function and keeping connection ID
beginvrupdate_handler_id = Engine::getEventBeginVRUpdate().connect(e_connections, []() {
		Log::message("\Handling BeginVRUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventBeginVRUpdate().disconnect(beginvrupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginVRUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventBeginVRUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventBeginVRUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventEndVRUpdate () const

event triggered after the VR update stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndVRUpdate event handler
void endvrupdate_event_handler()
{
	Log::message("\Handling EndVRUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endvrupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventEndVRUpdate().connect(endvrupdate_event_connections, endvrupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventEndVRUpdate().connect(endvrupdate_event_connections, []() {
		Log::message("\Handling EndVRUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endvrupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endvrupdate_event_connection;

// subscribe to the EndVRUpdate event with a handler function keeping the connection
Engine::getEventEndVRUpdate().connect(endvrupdate_event_connection, endvrupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endvrupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endvrupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the EndVRUpdate event via the connection
endvrupdate_event_connection.disconnect();

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

	// A EndVRUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndVRUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventEndVRUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endvrupdate_handler_id;

// subscribe to the EndVRUpdate event with a lambda handler function and keeping connection ID
endvrupdate_handler_id = Engine::getEventEndVRUpdate().connect(e_connections, []() {
		Log::message("\Handling EndVRUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventEndVRUpdate().disconnect(endvrupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndVRUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventEndVRUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventEndVRUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventBeginEditorUpdate () const

event triggered before the editor update stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginEditorUpdate event handler
void begineditorupdate_event_handler()
{
	Log::message("\Handling BeginEditorUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begineditorupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventBeginEditorUpdate().connect(begineditorupdate_event_connections, begineditorupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventBeginEditorUpdate().connect(begineditorupdate_event_connections, []() {
		Log::message("\Handling BeginEditorUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
begineditorupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection begineditorupdate_event_connection;

// subscribe to the BeginEditorUpdate event with a handler function keeping the connection
Engine::getEventBeginEditorUpdate().connect(begineditorupdate_event_connection, begineditorupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
begineditorupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
begineditorupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginEditorUpdate event via the connection
begineditorupdate_event_connection.disconnect();

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

	// A BeginEditorUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginEditorUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventBeginEditorUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId begineditorupdate_handler_id;

// subscribe to the BeginEditorUpdate event with a lambda handler function and keeping connection ID
begineditorupdate_handler_id = Engine::getEventBeginEditorUpdate().connect(e_connections, []() {
		Log::message("\Handling BeginEditorUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventBeginEditorUpdate().disconnect(begineditorupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginEditorUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventBeginEditorUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventBeginEditorUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventEndEditorUpdate () const

event triggered after the editor update stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndEditorUpdate event handler
void endeditorupdate_event_handler()
{
	Log::message("\Handling EndEditorUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endeditorupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventEndEditorUpdate().connect(endeditorupdate_event_connections, endeditorupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventEndEditorUpdate().connect(endeditorupdate_event_connections, []() {
		Log::message("\Handling EndEditorUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endeditorupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endeditorupdate_event_connection;

// subscribe to the EndEditorUpdate event with a handler function keeping the connection
Engine::getEventEndEditorUpdate().connect(endeditorupdate_event_connection, endeditorupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endeditorupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endeditorupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the EndEditorUpdate event via the connection
endeditorupdate_event_connection.disconnect();

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

	// A EndEditorUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndEditorUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventEndEditorUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endeditorupdate_handler_id;

// subscribe to the EndEditorUpdate event with a lambda handler function and keeping connection ID
endeditorupdate_handler_id = Engine::getEventEndEditorUpdate().connect(e_connections, []() {
		Log::message("\Handling EndEditorUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventEndEditorUpdate().disconnect(endeditorupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndEditorUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventEndEditorUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventEndEditorUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventBeginSystemScriptUpdate () const

event triggered before the system script update stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginSystemScriptUpdate event handler
void beginsystemscriptupdate_event_handler()
{
	Log::message("\Handling BeginSystemScriptUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginsystemscriptupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventBeginSystemScriptUpdate().connect(beginsystemscriptupdate_event_connections, beginsystemscriptupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventBeginSystemScriptUpdate().connect(beginsystemscriptupdate_event_connections, []() {
		Log::message("\Handling BeginSystemScriptUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginsystemscriptupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginsystemscriptupdate_event_connection;

// subscribe to the BeginSystemScriptUpdate event with a handler function keeping the connection
Engine::getEventBeginSystemScriptUpdate().connect(beginsystemscriptupdate_event_connection, beginsystemscriptupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginsystemscriptupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginsystemscriptupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginSystemScriptUpdate event via the connection
beginsystemscriptupdate_event_connection.disconnect();

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

	// A BeginSystemScriptUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginSystemScriptUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventBeginSystemScriptUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginsystemscriptupdate_handler_id;

// subscribe to the BeginSystemScriptUpdate event with a lambda handler function and keeping connection ID
beginsystemscriptupdate_handler_id = Engine::getEventBeginSystemScriptUpdate().connect(e_connections, []() {
		Log::message("\Handling BeginSystemScriptUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventBeginSystemScriptUpdate().disconnect(beginsystemscriptupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginSystemScriptUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventBeginSystemScriptUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventBeginSystemScriptUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventEndSystemScriptUpdate () const

event triggered after the system script update stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndSystemScriptUpdate event handler
void endsystemscriptupdate_event_handler()
{
	Log::message("\Handling EndSystemScriptUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endsystemscriptupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventEndSystemScriptUpdate().connect(endsystemscriptupdate_event_connections, endsystemscriptupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventEndSystemScriptUpdate().connect(endsystemscriptupdate_event_connections, []() {
		Log::message("\Handling EndSystemScriptUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endsystemscriptupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endsystemscriptupdate_event_connection;

// subscribe to the EndSystemScriptUpdate event with a handler function keeping the connection
Engine::getEventEndSystemScriptUpdate().connect(endsystemscriptupdate_event_connection, endsystemscriptupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endsystemscriptupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endsystemscriptupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the EndSystemScriptUpdate event via the connection
endsystemscriptupdate_event_connection.disconnect();

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

	// A EndSystemScriptUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndSystemScriptUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventEndSystemScriptUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endsystemscriptupdate_handler_id;

// subscribe to the EndSystemScriptUpdate event with a lambda handler function and keeping connection ID
endsystemscriptupdate_handler_id = Engine::getEventEndSystemScriptUpdate().connect(e_connections, []() {
		Log::message("\Handling EndSystemScriptUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventEndSystemScriptUpdate().disconnect(endsystemscriptupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndSystemScriptUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventEndSystemScriptUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventEndSystemScriptUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventBeginSystemLogicUpdate () const

event triggered before the system logic update stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginSystemLogicUpdate event handler
void beginsystemlogicupdate_event_handler()
{
	Log::message("\Handling BeginSystemLogicUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginsystemlogicupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventBeginSystemLogicUpdate().connect(beginsystemlogicupdate_event_connections, beginsystemlogicupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventBeginSystemLogicUpdate().connect(beginsystemlogicupdate_event_connections, []() {
		Log::message("\Handling BeginSystemLogicUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginsystemlogicupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginsystemlogicupdate_event_connection;

// subscribe to the BeginSystemLogicUpdate event with a handler function keeping the connection
Engine::getEventBeginSystemLogicUpdate().connect(beginsystemlogicupdate_event_connection, beginsystemlogicupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginsystemlogicupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginsystemlogicupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginSystemLogicUpdate event via the connection
beginsystemlogicupdate_event_connection.disconnect();

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

	// A BeginSystemLogicUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginSystemLogicUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventBeginSystemLogicUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginsystemlogicupdate_handler_id;

// subscribe to the BeginSystemLogicUpdate event with a lambda handler function and keeping connection ID
beginsystemlogicupdate_handler_id = Engine::getEventBeginSystemLogicUpdate().connect(e_connections, []() {
		Log::message("\Handling BeginSystemLogicUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventBeginSystemLogicUpdate().disconnect(beginsystemlogicupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginSystemLogicUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventBeginSystemLogicUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventBeginSystemLogicUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventEndSystemLogicUpdate () const

event triggered after the system logic update stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndSystemLogicUpdate event handler
void endsystemlogicupdate_event_handler()
{
	Log::message("\Handling EndSystemLogicUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endsystemlogicupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventEndSystemLogicUpdate().connect(endsystemlogicupdate_event_connections, endsystemlogicupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventEndSystemLogicUpdate().connect(endsystemlogicupdate_event_connections, []() {
		Log::message("\Handling EndSystemLogicUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endsystemlogicupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endsystemlogicupdate_event_connection;

// subscribe to the EndSystemLogicUpdate event with a handler function keeping the connection
Engine::getEventEndSystemLogicUpdate().connect(endsystemlogicupdate_event_connection, endsystemlogicupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endsystemlogicupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endsystemlogicupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the EndSystemLogicUpdate event via the connection
endsystemlogicupdate_event_connection.disconnect();

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

	// A EndSystemLogicUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndSystemLogicUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventEndSystemLogicUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endsystemlogicupdate_handler_id;

// subscribe to the EndSystemLogicUpdate event with a lambda handler function and keeping connection ID
endsystemlogicupdate_handler_id = Engine::getEventEndSystemLogicUpdate().connect(e_connections, []() {
		Log::message("\Handling EndSystemLogicUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventEndSystemLogicUpdate().disconnect(endsystemlogicupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndSystemLogicUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventEndSystemLogicUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventEndSystemLogicUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventBeginWorldUpdate () const

event triggered before the world logic update stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginWorldUpdate event handler
void beginworldupdate_event_handler()
{
	Log::message("\Handling BeginWorldUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginworldupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventBeginWorldUpdate().connect(beginworldupdate_event_connections, beginworldupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventBeginWorldUpdate().connect(beginworldupdate_event_connections, []() {
		Log::message("\Handling BeginWorldUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginworldupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginworldupdate_event_connection;

// subscribe to the BeginWorldUpdate event with a handler function keeping the connection
Engine::getEventBeginWorldUpdate().connect(beginworldupdate_event_connection, beginworldupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginworldupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginworldupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginWorldUpdate event via the connection
beginworldupdate_event_connection.disconnect();

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

	// A BeginWorldUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginWorldUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventBeginWorldUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginworldupdate_handler_id;

// subscribe to the BeginWorldUpdate event with a lambda handler function and keeping connection ID
beginworldupdate_handler_id = Engine::getEventBeginWorldUpdate().connect(e_connections, []() {
		Log::message("\Handling BeginWorldUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventBeginWorldUpdate().disconnect(beginworldupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginWorldUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventBeginWorldUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventBeginWorldUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventEndWorldUpdate () const

event triggered after the world logic update stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndWorldUpdate event handler
void endworldupdate_event_handler()
{
	Log::message("\Handling EndWorldUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endworldupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventEndWorldUpdate().connect(endworldupdate_event_connections, endworldupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventEndWorldUpdate().connect(endworldupdate_event_connections, []() {
		Log::message("\Handling EndWorldUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endworldupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endworldupdate_event_connection;

// subscribe to the EndWorldUpdate event with a handler function keeping the connection
Engine::getEventEndWorldUpdate().connect(endworldupdate_event_connection, endworldupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endworldupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endworldupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the EndWorldUpdate event via the connection
endworldupdate_event_connection.disconnect();

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

	// A EndWorldUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndWorldUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventEndWorldUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endworldupdate_handler_id;

// subscribe to the EndWorldUpdate event with a lambda handler function and keeping connection ID
endworldupdate_handler_id = Engine::getEventEndWorldUpdate().connect(e_connections, []() {
		Log::message("\Handling EndWorldUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventEndWorldUpdate().disconnect(endworldupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndWorldUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventEndWorldUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventEndWorldUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventBeginAnimationManagerUpdate () const

event triggered before the animation manager update stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginAnimationManagerUpdate event handler
void beginanimationmanagerupdate_event_handler()
{
	Log::message("\Handling BeginAnimationManagerUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginanimationmanagerupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventBeginAnimationManagerUpdate().connect(beginanimationmanagerupdate_event_connections, beginanimationmanagerupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventBeginAnimationManagerUpdate().connect(beginanimationmanagerupdate_event_connections, []() {
		Log::message("\Handling BeginAnimationManagerUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginanimationmanagerupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginanimationmanagerupdate_event_connection;

// subscribe to the BeginAnimationManagerUpdate event with a handler function keeping the connection
Engine::getEventBeginAnimationManagerUpdate().connect(beginanimationmanagerupdate_event_connection, beginanimationmanagerupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginanimationmanagerupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginanimationmanagerupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginAnimationManagerUpdate event via the connection
beginanimationmanagerupdate_event_connection.disconnect();

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

	// A BeginAnimationManagerUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginAnimationManagerUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventBeginAnimationManagerUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginanimationmanagerupdate_handler_id;

// subscribe to the BeginAnimationManagerUpdate event with a lambda handler function and keeping connection ID
beginanimationmanagerupdate_handler_id = Engine::getEventBeginAnimationManagerUpdate().connect(e_connections, []() {
		Log::message("\Handling BeginAnimationManagerUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventBeginAnimationManagerUpdate().disconnect(beginanimationmanagerupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginAnimationManagerUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventBeginAnimationManagerUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventBeginAnimationManagerUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventEndAnimationManagerUpdate () const

event triggered after the animation manager update stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndAnimationManagerUpdate event handler
void endanimationmanagerupdate_event_handler()
{
	Log::message("\Handling EndAnimationManagerUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endanimationmanagerupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventEndAnimationManagerUpdate().connect(endanimationmanagerupdate_event_connections, endanimationmanagerupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventEndAnimationManagerUpdate().connect(endanimationmanagerupdate_event_connections, []() {
		Log::message("\Handling EndAnimationManagerUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endanimationmanagerupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endanimationmanagerupdate_event_connection;

// subscribe to the EndAnimationManagerUpdate event with a handler function keeping the connection
Engine::getEventEndAnimationManagerUpdate().connect(endanimationmanagerupdate_event_connection, endanimationmanagerupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endanimationmanagerupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endanimationmanagerupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the EndAnimationManagerUpdate event via the connection
endanimationmanagerupdate_event_connection.disconnect();

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

	// A EndAnimationManagerUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndAnimationManagerUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventEndAnimationManagerUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endanimationmanagerupdate_handler_id;

// subscribe to the EndAnimationManagerUpdate event with a lambda handler function and keeping connection ID
endanimationmanagerupdate_handler_id = Engine::getEventEndAnimationManagerUpdate().connect(e_connections, []() {
		Log::message("\Handling EndAnimationManagerUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventEndAnimationManagerUpdate().disconnect(endanimationmanagerupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndAnimationManagerUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventEndAnimationManagerUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventEndAnimationManagerUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventBeginWorldPostUpdate () const

event triggered before the world logic postupdate stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginWorldPostUpdate event handler
void beginworldpostupdate_event_handler()
{
	Log::message("\Handling BeginWorldPostUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginworldpostupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventBeginWorldPostUpdate().connect(beginworldpostupdate_event_connections, beginworldpostupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventBeginWorldPostUpdate().connect(beginworldpostupdate_event_connections, []() {
		Log::message("\Handling BeginWorldPostUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginworldpostupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginworldpostupdate_event_connection;

// subscribe to the BeginWorldPostUpdate event with a handler function keeping the connection
Engine::getEventBeginWorldPostUpdate().connect(beginworldpostupdate_event_connection, beginworldpostupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginworldpostupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginworldpostupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginWorldPostUpdate event via the connection
beginworldpostupdate_event_connection.disconnect();

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

	// A BeginWorldPostUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginWorldPostUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventBeginWorldPostUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginworldpostupdate_handler_id;

// subscribe to the BeginWorldPostUpdate event with a lambda handler function and keeping connection ID
beginworldpostupdate_handler_id = Engine::getEventBeginWorldPostUpdate().connect(e_connections, []() {
		Log::message("\Handling BeginWorldPostUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventBeginWorldPostUpdate().disconnect(beginworldpostupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginWorldPostUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventBeginWorldPostUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventBeginWorldPostUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventEndWorldPostUpdate () const

event triggered after the world logic postupdate stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndWorldPostUpdate event handler
void endworldpostupdate_event_handler()
{
	Log::message("\Handling EndWorldPostUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endworldpostupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventEndWorldPostUpdate().connect(endworldpostupdate_event_connections, endworldpostupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventEndWorldPostUpdate().connect(endworldpostupdate_event_connections, []() {
		Log::message("\Handling EndWorldPostUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endworldpostupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endworldpostupdate_event_connection;

// subscribe to the EndWorldPostUpdate event with a handler function keeping the connection
Engine::getEventEndWorldPostUpdate().connect(endworldpostupdate_event_connection, endworldpostupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endworldpostupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endworldpostupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the EndWorldPostUpdate event via the connection
endworldpostupdate_event_connection.disconnect();

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

	// A EndWorldPostUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndWorldPostUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventEndWorldPostUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endworldpostupdate_handler_id;

// subscribe to the EndWorldPostUpdate event with a lambda handler function and keeping connection ID
endworldpostupdate_handler_id = Engine::getEventEndWorldPostUpdate().connect(e_connections, []() {
		Log::message("\Handling EndWorldPostUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventEndWorldPostUpdate().disconnect(endworldpostupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndWorldPostUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventEndWorldPostUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventEndWorldPostUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventBeginSystemScriptPostUpdate () const

event triggered before the system script postupdate stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginSystemScriptPostUpdate event handler
void beginsystemscriptpostupdate_event_handler()
{
	Log::message("\Handling BeginSystemScriptPostUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginsystemscriptpostupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventBeginSystemScriptPostUpdate().connect(beginsystemscriptpostupdate_event_connections, beginsystemscriptpostupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventBeginSystemScriptPostUpdate().connect(beginsystemscriptpostupdate_event_connections, []() {
		Log::message("\Handling BeginSystemScriptPostUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginsystemscriptpostupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginsystemscriptpostupdate_event_connection;

// subscribe to the BeginSystemScriptPostUpdate event with a handler function keeping the connection
Engine::getEventBeginSystemScriptPostUpdate().connect(beginsystemscriptpostupdate_event_connection, beginsystemscriptpostupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginsystemscriptpostupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginsystemscriptpostupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginSystemScriptPostUpdate event via the connection
beginsystemscriptpostupdate_event_connection.disconnect();

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

	// A BeginSystemScriptPostUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginSystemScriptPostUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventBeginSystemScriptPostUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginsystemscriptpostupdate_handler_id;

// subscribe to the BeginSystemScriptPostUpdate event with a lambda handler function and keeping connection ID
beginsystemscriptpostupdate_handler_id = Engine::getEventBeginSystemScriptPostUpdate().connect(e_connections, []() {
		Log::message("\Handling BeginSystemScriptPostUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventBeginSystemScriptPostUpdate().disconnect(beginsystemscriptpostupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginSystemScriptPostUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventBeginSystemScriptPostUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventBeginSystemScriptPostUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventEndSystemScriptPostUpdate () const

event triggered after the system script postupdate stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndSystemScriptPostUpdate event handler
void endsystemscriptpostupdate_event_handler()
{
	Log::message("\Handling EndSystemScriptPostUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endsystemscriptpostupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventEndSystemScriptPostUpdate().connect(endsystemscriptpostupdate_event_connections, endsystemscriptpostupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventEndSystemScriptPostUpdate().connect(endsystemscriptpostupdate_event_connections, []() {
		Log::message("\Handling EndSystemScriptPostUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endsystemscriptpostupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endsystemscriptpostupdate_event_connection;

// subscribe to the EndSystemScriptPostUpdate event with a handler function keeping the connection
Engine::getEventEndSystemScriptPostUpdate().connect(endsystemscriptpostupdate_event_connection, endsystemscriptpostupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endsystemscriptpostupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endsystemscriptpostupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the EndSystemScriptPostUpdate event via the connection
endsystemscriptpostupdate_event_connection.disconnect();

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

	// A EndSystemScriptPostUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndSystemScriptPostUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventEndSystemScriptPostUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endsystemscriptpostupdate_handler_id;

// subscribe to the EndSystemScriptPostUpdate event with a lambda handler function and keeping connection ID
endsystemscriptpostupdate_handler_id = Engine::getEventEndSystemScriptPostUpdate().connect(e_connections, []() {
		Log::message("\Handling EndSystemScriptPostUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventEndSystemScriptPostUpdate().disconnect(endsystemscriptpostupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndSystemScriptPostUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventEndSystemScriptPostUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventEndSystemScriptPostUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventBeginSystemLogicPostUpdate () const

event triggered before the system logic postupdate stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginSystemLogicPostUpdate event handler
void beginsystemlogicpostupdate_event_handler()
{
	Log::message("\Handling BeginSystemLogicPostUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginsystemlogicpostupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventBeginSystemLogicPostUpdate().connect(beginsystemlogicpostupdate_event_connections, beginsystemlogicpostupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventBeginSystemLogicPostUpdate().connect(beginsystemlogicpostupdate_event_connections, []() {
		Log::message("\Handling BeginSystemLogicPostUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginsystemlogicpostupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginsystemlogicpostupdate_event_connection;

// subscribe to the BeginSystemLogicPostUpdate event with a handler function keeping the connection
Engine::getEventBeginSystemLogicPostUpdate().connect(beginsystemlogicpostupdate_event_connection, beginsystemlogicpostupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginsystemlogicpostupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginsystemlogicpostupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginSystemLogicPostUpdate event via the connection
beginsystemlogicpostupdate_event_connection.disconnect();

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

	// A BeginSystemLogicPostUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginSystemLogicPostUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventBeginSystemLogicPostUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginsystemlogicpostupdate_handler_id;

// subscribe to the BeginSystemLogicPostUpdate event with a lambda handler function and keeping connection ID
beginsystemlogicpostupdate_handler_id = Engine::getEventBeginSystemLogicPostUpdate().connect(e_connections, []() {
		Log::message("\Handling BeginSystemLogicPostUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventBeginSystemLogicPostUpdate().disconnect(beginsystemlogicpostupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginSystemLogicPostUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventBeginSystemLogicPostUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventBeginSystemLogicPostUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventEndSystemLogicPostUpdate () const

event triggered after the system logic postupdate stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndSystemLogicPostUpdate event handler
void endsystemlogicpostupdate_event_handler()
{
	Log::message("\Handling EndSystemLogicPostUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endsystemlogicpostupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventEndSystemLogicPostUpdate().connect(endsystemlogicpostupdate_event_connections, endsystemlogicpostupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventEndSystemLogicPostUpdate().connect(endsystemlogicpostupdate_event_connections, []() {
		Log::message("\Handling EndSystemLogicPostUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endsystemlogicpostupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endsystemlogicpostupdate_event_connection;

// subscribe to the EndSystemLogicPostUpdate event with a handler function keeping the connection
Engine::getEventEndSystemLogicPostUpdate().connect(endsystemlogicpostupdate_event_connection, endsystemlogicpostupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endsystemlogicpostupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endsystemlogicpostupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the EndSystemLogicPostUpdate event via the connection
endsystemlogicpostupdate_event_connection.disconnect();

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

	// A EndSystemLogicPostUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndSystemLogicPostUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventEndSystemLogicPostUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endsystemlogicpostupdate_handler_id;

// subscribe to the EndSystemLogicPostUpdate event with a lambda handler function and keeping connection ID
endsystemlogicpostupdate_handler_id = Engine::getEventEndSystemLogicPostUpdate().connect(e_connections, []() {
		Log::message("\Handling EndSystemLogicPostUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventEndSystemLogicPostUpdate().disconnect(endsystemlogicpostupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndSystemLogicPostUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventEndSystemLogicPostUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventEndSystemLogicPostUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventBeginEditorPostUpdate () const

event triggered before the editor logic postupdate stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginEditorPostUpdate event handler
void begineditorpostupdate_event_handler()
{
	Log::message("\Handling BeginEditorPostUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begineditorpostupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventBeginEditorPostUpdate().connect(begineditorpostupdate_event_connections, begineditorpostupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventBeginEditorPostUpdate().connect(begineditorpostupdate_event_connections, []() {
		Log::message("\Handling BeginEditorPostUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
begineditorpostupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection begineditorpostupdate_event_connection;

// subscribe to the BeginEditorPostUpdate event with a handler function keeping the connection
Engine::getEventBeginEditorPostUpdate().connect(begineditorpostupdate_event_connection, begineditorpostupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
begineditorpostupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
begineditorpostupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginEditorPostUpdate event via the connection
begineditorpostupdate_event_connection.disconnect();

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

	// A BeginEditorPostUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginEditorPostUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventBeginEditorPostUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId begineditorpostupdate_handler_id;

// subscribe to the BeginEditorPostUpdate event with a lambda handler function and keeping connection ID
begineditorpostupdate_handler_id = Engine::getEventBeginEditorPostUpdate().connect(e_connections, []() {
		Log::message("\Handling BeginEditorPostUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventBeginEditorPostUpdate().disconnect(begineditorpostupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginEditorPostUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventBeginEditorPostUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventBeginEditorPostUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventEndEditorPostUpdate () const

event triggered after the editor logic postupdate stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndEditorPostUpdate event handler
void endeditorpostupdate_event_handler()
{
	Log::message("\Handling EndEditorPostUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endeditorpostupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventEndEditorPostUpdate().connect(endeditorpostupdate_event_connections, endeditorpostupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventEndEditorPostUpdate().connect(endeditorpostupdate_event_connections, []() {
		Log::message("\Handling EndEditorPostUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endeditorpostupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endeditorpostupdate_event_connection;

// subscribe to the EndEditorPostUpdate event with a handler function keeping the connection
Engine::getEventEndEditorPostUpdate().connect(endeditorpostupdate_event_connection, endeditorpostupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endeditorpostupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endeditorpostupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the EndEditorPostUpdate event via the connection
endeditorpostupdate_event_connection.disconnect();

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

	// A EndEditorPostUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndEditorPostUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventEndEditorPostUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endeditorpostupdate_handler_id;

// subscribe to the EndEditorPostUpdate event with a lambda handler function and keeping connection ID
endeditorpostupdate_handler_id = Engine::getEventEndEditorPostUpdate().connect(e_connections, []() {
		Log::message("\Handling EndEditorPostUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventEndEditorPostUpdate().disconnect(endeditorpostupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndEditorPostUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventEndEditorPostUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventEndEditorPostUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventBeginPluginsPostUpdate () const

event triggered before the plugins postupdate stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginPluginsPostUpdate event handler
void beginpluginspostupdate_event_handler()
{
	Log::message("\Handling BeginPluginsPostUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginpluginspostupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventBeginPluginsPostUpdate().connect(beginpluginspostupdate_event_connections, beginpluginspostupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventBeginPluginsPostUpdate().connect(beginpluginspostupdate_event_connections, []() {
		Log::message("\Handling BeginPluginsPostUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginpluginspostupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginpluginspostupdate_event_connection;

// subscribe to the BeginPluginsPostUpdate event with a handler function keeping the connection
Engine::getEventBeginPluginsPostUpdate().connect(beginpluginspostupdate_event_connection, beginpluginspostupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginpluginspostupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginpluginspostupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginPluginsPostUpdate event via the connection
beginpluginspostupdate_event_connection.disconnect();

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

	// A BeginPluginsPostUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginPluginsPostUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventBeginPluginsPostUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginpluginspostupdate_handler_id;

// subscribe to the BeginPluginsPostUpdate event with a lambda handler function and keeping connection ID
beginpluginspostupdate_handler_id = Engine::getEventBeginPluginsPostUpdate().connect(e_connections, []() {
		Log::message("\Handling BeginPluginsPostUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventBeginPluginsPostUpdate().disconnect(beginpluginspostupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginPluginsPostUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventBeginPluginsPostUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventBeginPluginsPostUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventEndPluginsPostUpdate () const

event triggered after the plugins postupdate stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndPluginsPostUpdate event handler
void endpluginspostupdate_event_handler()
{
	Log::message("\Handling EndPluginsPostUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endpluginspostupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventEndPluginsPostUpdate().connect(endpluginspostupdate_event_connections, endpluginspostupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventEndPluginsPostUpdate().connect(endpluginspostupdate_event_connections, []() {
		Log::message("\Handling EndPluginsPostUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endpluginspostupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endpluginspostupdate_event_connection;

// subscribe to the EndPluginsPostUpdate event with a handler function keeping the connection
Engine::getEventEndPluginsPostUpdate().connect(endpluginspostupdate_event_connection, endpluginspostupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endpluginspostupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endpluginspostupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the EndPluginsPostUpdate event via the connection
endpluginspostupdate_event_connection.disconnect();

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

	// A EndPluginsPostUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndPluginsPostUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventEndPluginsPostUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endpluginspostupdate_handler_id;

// subscribe to the EndPluginsPostUpdate event with a lambda handler function and keeping connection ID
endpluginspostupdate_handler_id = Engine::getEventEndPluginsPostUpdate().connect(e_connections, []() {
		Log::message("\Handling EndPluginsPostUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventEndPluginsPostUpdate().disconnect(endpluginspostupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndPluginsPostUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventEndPluginsPostUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventEndPluginsPostUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventBeginSpatialUpdate () const

event triggered before the spatial tree update stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginSpatialUpdate event handler
void beginspatialupdate_event_handler()
{
	Log::message("\Handling BeginSpatialUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginspatialupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventBeginSpatialUpdate().connect(beginspatialupdate_event_connections, beginspatialupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventBeginSpatialUpdate().connect(beginspatialupdate_event_connections, []() {
		Log::message("\Handling BeginSpatialUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginspatialupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginspatialupdate_event_connection;

// subscribe to the BeginSpatialUpdate event with a handler function keeping the connection
Engine::getEventBeginSpatialUpdate().connect(beginspatialupdate_event_connection, beginspatialupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginspatialupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginspatialupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginSpatialUpdate event via the connection
beginspatialupdate_event_connection.disconnect();

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

	// A BeginSpatialUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginSpatialUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventBeginSpatialUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginspatialupdate_handler_id;

// subscribe to the BeginSpatialUpdate event with a lambda handler function and keeping connection ID
beginspatialupdate_handler_id = Engine::getEventBeginSpatialUpdate().connect(e_connections, []() {
		Log::message("\Handling BeginSpatialUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventBeginSpatialUpdate().disconnect(beginspatialupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginSpatialUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventBeginSpatialUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventBeginSpatialUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventEndSpatialUpdate () const

event triggered after the spatial tree update stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndSpatialUpdate event handler
void endspatialupdate_event_handler()
{
	Log::message("\Handling EndSpatialUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endspatialupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventEndSpatialUpdate().connect(endspatialupdate_event_connections, endspatialupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventEndSpatialUpdate().connect(endspatialupdate_event_connections, []() {
		Log::message("\Handling EndSpatialUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endspatialupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endspatialupdate_event_connection;

// subscribe to the EndSpatialUpdate event with a handler function keeping the connection
Engine::getEventEndSpatialUpdate().connect(endspatialupdate_event_connection, endspatialupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endspatialupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endspatialupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the EndSpatialUpdate event via the connection
endspatialupdate_event_connection.disconnect();

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

	// A EndSpatialUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndSpatialUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventEndSpatialUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endspatialupdate_handler_id;

// subscribe to the EndSpatialUpdate event with a lambda handler function and keeping connection ID
endspatialupdate_handler_id = Engine::getEventEndSpatialUpdate().connect(e_connections, []() {
		Log::message("\Handling EndSpatialUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventEndSpatialUpdate().disconnect(endspatialupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndSpatialUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventEndSpatialUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventEndSpatialUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventBeginFilesystemUpdate () const

event triggered before the filesystem update stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginFilesystemUpdate event handler
void beginfilesystemupdate_event_handler()
{
	Log::message("\Handling BeginFilesystemUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginfilesystemupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventBeginFilesystemUpdate().connect(beginfilesystemupdate_event_connections, beginfilesystemupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventBeginFilesystemUpdate().connect(beginfilesystemupdate_event_connections, []() {
		Log::message("\Handling BeginFilesystemUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginfilesystemupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginfilesystemupdate_event_connection;

// subscribe to the BeginFilesystemUpdate event with a handler function keeping the connection
Engine::getEventBeginFilesystemUpdate().connect(beginfilesystemupdate_event_connection, beginfilesystemupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginfilesystemupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginfilesystemupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginFilesystemUpdate event via the connection
beginfilesystemupdate_event_connection.disconnect();

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

	// A BeginFilesystemUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginFilesystemUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventBeginFilesystemUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginfilesystemupdate_handler_id;

// subscribe to the BeginFilesystemUpdate event with a lambda handler function and keeping connection ID
beginfilesystemupdate_handler_id = Engine::getEventBeginFilesystemUpdate().connect(e_connections, []() {
		Log::message("\Handling BeginFilesystemUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventBeginFilesystemUpdate().disconnect(beginfilesystemupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginFilesystemUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventBeginFilesystemUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventBeginFilesystemUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventEndFilesystemUpdate () const

event triggered after the filesystem update stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndFilesystemUpdate event handler
void endfilesystemupdate_event_handler()
{
	Log::message("\Handling EndFilesystemUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endfilesystemupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventEndFilesystemUpdate().connect(endfilesystemupdate_event_connections, endfilesystemupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventEndFilesystemUpdate().connect(endfilesystemupdate_event_connections, []() {
		Log::message("\Handling EndFilesystemUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endfilesystemupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endfilesystemupdate_event_connection;

// subscribe to the EndFilesystemUpdate event with a handler function keeping the connection
Engine::getEventEndFilesystemUpdate().connect(endfilesystemupdate_event_connection, endfilesystemupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endfilesystemupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endfilesystemupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the EndFilesystemUpdate event via the connection
endfilesystemupdate_event_connection.disconnect();

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

	// A EndFilesystemUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndFilesystemUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventEndFilesystemUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endfilesystemupdate_handler_id;

// subscribe to the EndFilesystemUpdate event with a lambda handler function and keeping connection ID
endfilesystemupdate_handler_id = Engine::getEventEndFilesystemUpdate().connect(e_connections, []() {
		Log::message("\Handling EndFilesystemUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventEndFilesystemUpdate().disconnect(endfilesystemupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndFilesystemUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventEndFilesystemUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventEndFilesystemUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventBeginPathfinding () const

event triggered before the pathfinding module is updated. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginPathfinding event handler
void beginpathfinding_event_handler()
{
	Log::message("\Handling BeginPathfinding event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginpathfinding_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventBeginPathfinding().connect(beginpathfinding_event_connections, beginpathfinding_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventBeginPathfinding().connect(beginpathfinding_event_connections, []() {
		Log::message("\Handling BeginPathfinding event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginpathfinding_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginpathfinding_event_connection;

// subscribe to the BeginPathfinding event with a handler function keeping the connection
Engine::getEventBeginPathfinding().connect(beginpathfinding_event_connection, beginpathfinding_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginpathfinding_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginpathfinding_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginPathfinding event via the connection
beginpathfinding_event_connection.disconnect();

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

	// A BeginPathfinding event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginPathfinding event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventBeginPathfinding().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginpathfinding_handler_id;

// subscribe to the BeginPathfinding event with a lambda handler function and keeping connection ID
beginpathfinding_handler_id = Engine::getEventBeginPathfinding().connect(e_connections, []() {
		Log::message("\Handling BeginPathfinding event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventBeginPathfinding().disconnect(beginpathfinding_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginPathfinding events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventBeginPathfinding().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventBeginPathfinding().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventEndUpdate () const

event triggered after the update stage is finished. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndUpdate event handler
void endupdate_event_handler()
{
	Log::message("\Handling EndUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventEndUpdate().connect(endupdate_event_connections, endupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventEndUpdate().connect(endupdate_event_connections, []() {
		Log::message("\Handling EndUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endupdate_event_connection;

// subscribe to the EndUpdate event with a handler function keeping the connection
Engine::getEventEndUpdate().connect(endupdate_event_connection, endupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the EndUpdate event via the connection
endupdate_event_connection.disconnect();

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

	// A EndUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventEndUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endupdate_handler_id;

// subscribe to the EndUpdate event with a lambda handler function and keeping connection ID
endupdate_handler_id = Engine::getEventEndUpdate().connect(e_connections, []() {
		Log::message("\Handling EndUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventEndUpdate().disconnect(endupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventEndUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventEndUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventSyncBeginFramePhysics () const

event triggered before the physics frame in the main thread. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the SyncBeginFramePhysics event handler
void syncbeginframephysics_event_handler()
{
	Log::message("\Handling SyncBeginFramePhysics event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections syncbeginframephysics_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventSyncBeginFramePhysics().connect(syncbeginframephysics_event_connections, syncbeginframephysics_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventSyncBeginFramePhysics().connect(syncbeginframephysics_event_connections, []() {
		Log::message("\Handling SyncBeginFramePhysics event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
syncbeginframephysics_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection syncbeginframephysics_event_connection;

// subscribe to the SyncBeginFramePhysics event with a handler function keeping the connection
Engine::getEventSyncBeginFramePhysics().connect(syncbeginframephysics_event_connection, syncbeginframephysics_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
syncbeginframephysics_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
syncbeginframephysics_event_connection.setEnabled(true);

// ...

// remove subscription to the SyncBeginFramePhysics event via the connection
syncbeginframephysics_event_connection.disconnect();

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

	// A SyncBeginFramePhysics event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling SyncBeginFramePhysics event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventSyncBeginFramePhysics().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId syncbeginframephysics_handler_id;

// subscribe to the SyncBeginFramePhysics event with a lambda handler function and keeping connection ID
syncbeginframephysics_handler_id = Engine::getEventSyncBeginFramePhysics().connect(e_connections, []() {
		Log::message("\Handling SyncBeginFramePhysics event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventSyncBeginFramePhysics().disconnect(syncbeginframephysics_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all SyncBeginFramePhysics events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventSyncBeginFramePhysics().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventSyncBeginFramePhysics().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventSyncEndFramePhysics () const

event triggered after the physics frame in the main thread. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the SyncEndFramePhysics event handler
void syncendframephysics_event_handler()
{
	Log::message("\Handling SyncEndFramePhysics event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections syncendframephysics_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventSyncEndFramePhysics().connect(syncendframephysics_event_connections, syncendframephysics_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventSyncEndFramePhysics().connect(syncendframephysics_event_connections, []() {
		Log::message("\Handling SyncEndFramePhysics event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
syncendframephysics_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection syncendframephysics_event_connection;

// subscribe to the SyncEndFramePhysics event with a handler function keeping the connection
Engine::getEventSyncEndFramePhysics().connect(syncendframephysics_event_connection, syncendframephysics_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
syncendframephysics_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
syncendframephysics_event_connection.setEnabled(true);

// ...

// remove subscription to the SyncEndFramePhysics event via the connection
syncendframephysics_event_connection.disconnect();

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

	// A SyncEndFramePhysics event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling SyncEndFramePhysics event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventSyncEndFramePhysics().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId syncendframephysics_handler_id;

// subscribe to the SyncEndFramePhysics event with a lambda handler function and keeping connection ID
syncendframephysics_handler_id = Engine::getEventSyncEndFramePhysics().connect(e_connections, []() {
		Log::message("\Handling SyncEndFramePhysics event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventSyncEndFramePhysics().disconnect(syncendframephysics_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all SyncEndFramePhysics events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventSyncEndFramePhysics().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventSyncEndFramePhysics().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventAsyncBeginFramePhysics () const

event triggered before the physics frame in the physics thread. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the AsyncBeginFramePhysics event handler
void asyncbeginframephysics_event_handler()
{
	Log::message("\Handling AsyncBeginFramePhysics event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections asyncbeginframephysics_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventAsyncBeginFramePhysics().connect(asyncbeginframephysics_event_connections, asyncbeginframephysics_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventAsyncBeginFramePhysics().connect(asyncbeginframephysics_event_connections, []() {
		Log::message("\Handling AsyncBeginFramePhysics event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
asyncbeginframephysics_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection asyncbeginframephysics_event_connection;

// subscribe to the AsyncBeginFramePhysics event with a handler function keeping the connection
Engine::getEventAsyncBeginFramePhysics().connect(asyncbeginframephysics_event_connection, asyncbeginframephysics_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
asyncbeginframephysics_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
asyncbeginframephysics_event_connection.setEnabled(true);

// ...

// remove subscription to the AsyncBeginFramePhysics event via the connection
asyncbeginframephysics_event_connection.disconnect();

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

	// A AsyncBeginFramePhysics event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling AsyncBeginFramePhysics event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventAsyncBeginFramePhysics().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId asyncbeginframephysics_handler_id;

// subscribe to the AsyncBeginFramePhysics event with a lambda handler function and keeping connection ID
asyncbeginframephysics_handler_id = Engine::getEventAsyncBeginFramePhysics().connect(e_connections, []() {
		Log::message("\Handling AsyncBeginFramePhysics event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventAsyncBeginFramePhysics().disconnect(asyncbeginframephysics_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all AsyncBeginFramePhysics events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventAsyncBeginFramePhysics().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventAsyncBeginFramePhysics().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventAsyncEndFramePhysics () const

event triggered after the physics frame in the physics thread. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the AsyncEndFramePhysics event handler
void asyncendframephysics_event_handler()
{
	Log::message("\Handling AsyncEndFramePhysics event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections asyncendframephysics_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventAsyncEndFramePhysics().connect(asyncendframephysics_event_connections, asyncendframephysics_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventAsyncEndFramePhysics().connect(asyncendframephysics_event_connections, []() {
		Log::message("\Handling AsyncEndFramePhysics event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
asyncendframephysics_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection asyncendframephysics_event_connection;

// subscribe to the AsyncEndFramePhysics event with a handler function keeping the connection
Engine::getEventAsyncEndFramePhysics().connect(asyncendframephysics_event_connection, asyncendframephysics_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
asyncendframephysics_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
asyncendframephysics_event_connection.setEnabled(true);

// ...

// remove subscription to the AsyncEndFramePhysics event via the connection
asyncendframephysics_event_connection.disconnect();

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

	// A AsyncEndFramePhysics event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling AsyncEndFramePhysics event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventAsyncEndFramePhysics().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId asyncendframephysics_handler_id;

// subscribe to the AsyncEndFramePhysics event with a lambda handler function and keeping connection ID
asyncendframephysics_handler_id = Engine::getEventAsyncEndFramePhysics().connect(e_connections, []() {
		Log::message("\Handling AsyncEndFramePhysics event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventAsyncEndFramePhysics().disconnect(asyncendframephysics_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all AsyncEndFramePhysics events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventAsyncEndFramePhysics().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventAsyncEndFramePhysics().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventBeginVRRender () const

event triggered before the VR rendering stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginVRRender event handler
void beginvrrender_event_handler()
{
	Log::message("\Handling BeginVRRender event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginvrrender_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventBeginVRRender().connect(beginvrrender_event_connections, beginvrrender_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventBeginVRRender().connect(beginvrrender_event_connections, []() {
		Log::message("\Handling BeginVRRender event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginvrrender_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginvrrender_event_connection;

// subscribe to the BeginVRRender event with a handler function keeping the connection
Engine::getEventBeginVRRender().connect(beginvrrender_event_connection, beginvrrender_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginvrrender_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginvrrender_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginVRRender event via the connection
beginvrrender_event_connection.disconnect();

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

	// A BeginVRRender event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginVRRender event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventBeginVRRender().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginvrrender_handler_id;

// subscribe to the BeginVRRender event with a lambda handler function and keeping connection ID
beginvrrender_handler_id = Engine::getEventBeginVRRender().connect(e_connections, []() {
		Log::message("\Handling BeginVRRender event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventBeginVRRender().disconnect(beginvrrender_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginVRRender events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventBeginVRRender().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventBeginVRRender().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventEndVRRender () const

event triggered after the VR rendering stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndVRRender event handler
void endvrrender_event_handler()
{
	Log::message("\Handling EndVRRender event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endvrrender_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventEndVRRender().connect(endvrrender_event_connections, endvrrender_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventEndVRRender().connect(endvrrender_event_connections, []() {
		Log::message("\Handling EndVRRender event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endvrrender_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endvrrender_event_connection;

// subscribe to the EndVRRender event with a handler function keeping the connection
Engine::getEventEndVRRender().connect(endvrrender_event_connection, endvrrender_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endvrrender_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endvrrender_event_connection.setEnabled(true);

// ...

// remove subscription to the EndVRRender event via the connection
endvrrender_event_connection.disconnect();

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

	// A EndVRRender event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndVRRender event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventEndVRRender().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endvrrender_handler_id;

// subscribe to the EndVRRender event with a lambda handler function and keeping connection ID
endvrrender_handler_id = Engine::getEventEndVRRender().connect(e_connections, []() {
		Log::message("\Handling EndVRRender event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventEndVRRender().disconnect(endvrrender_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndVRRender events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventEndVRRender().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventEndVRRender().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventBeginRender () const

event triggered before the rendering stage is started. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginRender event handler
void beginrender_event_handler()
{
	Log::message("\Handling BeginRender event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginrender_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventBeginRender().connect(beginrender_event_connections, beginrender_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventBeginRender().connect(beginrender_event_connections, []() {
		Log::message("\Handling BeginRender event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginrender_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginrender_event_connection;

// subscribe to the BeginRender event with a handler function keeping the connection
Engine::getEventBeginRender().connect(beginrender_event_connection, beginrender_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginrender_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginrender_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginRender event via the connection
beginrender_event_connection.disconnect();

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

	// A BeginRender event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginRender event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventBeginRender().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginrender_handler_id;

// subscribe to the BeginRender event with a lambda handler function and keeping connection ID
beginrender_handler_id = Engine::getEventBeginRender().connect(e_connections, []() {
		Log::message("\Handling BeginRender event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventBeginRender().disconnect(beginrender_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginRender events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventBeginRender().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventBeginRender().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventBeginEditorRender () const

event triggered before the editor rendering stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginEditorRender event handler
void begineditorrender_event_handler()
{
	Log::message("\Handling BeginEditorRender event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begineditorrender_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventBeginEditorRender().connect(begineditorrender_event_connections, begineditorrender_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventBeginEditorRender().connect(begineditorrender_event_connections, []() {
		Log::message("\Handling BeginEditorRender event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
begineditorrender_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection begineditorrender_event_connection;

// subscribe to the BeginEditorRender event with a handler function keeping the connection
Engine::getEventBeginEditorRender().connect(begineditorrender_event_connection, begineditorrender_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
begineditorrender_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
begineditorrender_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginEditorRender event via the connection
begineditorrender_event_connection.disconnect();

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

	// A BeginEditorRender event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginEditorRender event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventBeginEditorRender().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId begineditorrender_handler_id;

// subscribe to the BeginEditorRender event with a lambda handler function and keeping connection ID
begineditorrender_handler_id = Engine::getEventBeginEditorRender().connect(e_connections, []() {
		Log::message("\Handling BeginEditorRender event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventBeginEditorRender().disconnect(begineditorrender_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginEditorRender events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventBeginEditorRender().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventBeginEditorRender().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventEndEditorRender () const

event triggered after the editor rendering stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndEditorRender event handler
void endeditorrender_event_handler()
{
	Log::message("\Handling EndEditorRender event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endeditorrender_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventEndEditorRender().connect(endeditorrender_event_connections, endeditorrender_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventEndEditorRender().connect(endeditorrender_event_connections, []() {
		Log::message("\Handling EndEditorRender event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endeditorrender_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endeditorrender_event_connection;

// subscribe to the EndEditorRender event with a handler function keeping the connection
Engine::getEventEndEditorRender().connect(endeditorrender_event_connection, endeditorrender_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endeditorrender_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endeditorrender_event_connection.setEnabled(true);

// ...

// remove subscription to the EndEditorRender event via the connection
endeditorrender_event_connection.disconnect();

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

	// A EndEditorRender event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndEditorRender event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventEndEditorRender().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endeditorrender_handler_id;

// subscribe to the EndEditorRender event with a lambda handler function and keeping connection ID
endeditorrender_handler_id = Engine::getEventEndEditorRender().connect(e_connections, []() {
		Log::message("\Handling EndEditorRender event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventEndEditorRender().disconnect(endeditorrender_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndEditorRender events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventEndEditorRender().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventEndEditorRender().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventBeginPluginsRender () const

event triggered before the plugins rendering stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginPluginsRender event handler
void beginpluginsrender_event_handler()
{
	Log::message("\Handling BeginPluginsRender event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginpluginsrender_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventBeginPluginsRender().connect(beginpluginsrender_event_connections, beginpluginsrender_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventBeginPluginsRender().connect(beginpluginsrender_event_connections, []() {
		Log::message("\Handling BeginPluginsRender event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginpluginsrender_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginpluginsrender_event_connection;

// subscribe to the BeginPluginsRender event with a handler function keeping the connection
Engine::getEventBeginPluginsRender().connect(beginpluginsrender_event_connection, beginpluginsrender_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginpluginsrender_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginpluginsrender_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginPluginsRender event via the connection
beginpluginsrender_event_connection.disconnect();

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

	// A BeginPluginsRender event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginPluginsRender event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventBeginPluginsRender().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginpluginsrender_handler_id;

// subscribe to the BeginPluginsRender event with a lambda handler function and keeping connection ID
beginpluginsrender_handler_id = Engine::getEventBeginPluginsRender().connect(e_connections, []() {
		Log::message("\Handling BeginPluginsRender event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventBeginPluginsRender().disconnect(beginpluginsrender_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginPluginsRender events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventBeginPluginsRender().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventBeginPluginsRender().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventEndPluginsRender () const

event triggered after the plugins rendering stage. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndPluginsRender event handler
void endpluginsrender_event_handler()
{
	Log::message("\Handling EndPluginsRender event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endpluginsrender_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventEndPluginsRender().connect(endpluginsrender_event_connections, endpluginsrender_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventEndPluginsRender().connect(endpluginsrender_event_connections, []() {
		Log::message("\Handling EndPluginsRender event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endpluginsrender_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endpluginsrender_event_connection;

// subscribe to the EndPluginsRender event with a handler function keeping the connection
Engine::getEventEndPluginsRender().connect(endpluginsrender_event_connection, endpluginsrender_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endpluginsrender_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endpluginsrender_event_connection.setEnabled(true);

// ...

// remove subscription to the EndPluginsRender event via the connection
endpluginsrender_event_connection.disconnect();

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

	// A EndPluginsRender event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndPluginsRender event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventEndPluginsRender().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endpluginsrender_handler_id;

// subscribe to the EndPluginsRender event with a lambda handler function and keeping connection ID
endpluginsrender_handler_id = Engine::getEventEndPluginsRender().connect(e_connections, []() {
		Log::message("\Handling EndPluginsRender event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventEndPluginsRender().disconnect(endpluginsrender_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndPluginsRender events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventEndPluginsRender().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventEndPluginsRender().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventBeginRenderWorld () const

event triggered before the world rendering stage. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginRenderWorld event handler
void beginrenderworld_event_handler()
{
	Log::message("\Handling BeginRenderWorld event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginrenderworld_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventBeginRenderWorld().connect(beginrenderworld_event_connections, beginrenderworld_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventBeginRenderWorld().connect(beginrenderworld_event_connections, []() {
		Log::message("\Handling BeginRenderWorld event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginrenderworld_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginrenderworld_event_connection;

// subscribe to the BeginRenderWorld event with a handler function keeping the connection
Engine::getEventBeginRenderWorld().connect(beginrenderworld_event_connection, beginrenderworld_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginrenderworld_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginrenderworld_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginRenderWorld event via the connection
beginrenderworld_event_connection.disconnect();

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

	// A BeginRenderWorld event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginRenderWorld event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventBeginRenderWorld().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginrenderworld_handler_id;

// subscribe to the BeginRenderWorld event with a lambda handler function and keeping connection ID
beginrenderworld_handler_id = Engine::getEventBeginRenderWorld().connect(e_connections, []() {
		Log::message("\Handling BeginRenderWorld event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventBeginRenderWorld().disconnect(beginrenderworld_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginRenderWorld events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventBeginRenderWorld().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventBeginRenderWorld().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventEndRenderWorld () const

event triggered after the world rendering stage. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndRenderWorld event handler
void endrenderworld_event_handler()
{
	Log::message("\Handling EndRenderWorld event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endrenderworld_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventEndRenderWorld().connect(endrenderworld_event_connections, endrenderworld_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventEndRenderWorld().connect(endrenderworld_event_connections, []() {
		Log::message("\Handling EndRenderWorld event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endrenderworld_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endrenderworld_event_connection;

// subscribe to the EndRenderWorld event with a handler function keeping the connection
Engine::getEventEndRenderWorld().connect(endrenderworld_event_connection, endrenderworld_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endrenderworld_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endrenderworld_event_connection.setEnabled(true);

// ...

// remove subscription to the EndRenderWorld event via the connection
endrenderworld_event_connection.disconnect();

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

	// A EndRenderWorld event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndRenderWorld event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventEndRenderWorld().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endrenderworld_handler_id;

// subscribe to the EndRenderWorld event with a lambda handler function and keeping connection ID
endrenderworld_handler_id = Engine::getEventEndRenderWorld().connect(e_connections, []() {
		Log::message("\Handling EndRenderWorld event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventEndRenderWorld().disconnect(endrenderworld_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndRenderWorld events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventEndRenderWorld().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventEndRenderWorld().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventBeginPluginsGui () const

event triggered before the gui() function of plugins is called. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginPluginsGui event handler
void beginpluginsgui_event_handler()
{
	Log::message("\Handling BeginPluginsGui event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginpluginsgui_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventBeginPluginsGui().connect(beginpluginsgui_event_connections, beginpluginsgui_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventBeginPluginsGui().connect(beginpluginsgui_event_connections, []() {
		Log::message("\Handling BeginPluginsGui event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginpluginsgui_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginpluginsgui_event_connection;

// subscribe to the BeginPluginsGui event with a handler function keeping the connection
Engine::getEventBeginPluginsGui().connect(beginpluginsgui_event_connection, beginpluginsgui_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginpluginsgui_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginpluginsgui_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginPluginsGui event via the connection
beginpluginsgui_event_connection.disconnect();

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

	// A BeginPluginsGui event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginPluginsGui event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventBeginPluginsGui().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginpluginsgui_handler_id;

// subscribe to the BeginPluginsGui event with a lambda handler function and keeping connection ID
beginpluginsgui_handler_id = Engine::getEventBeginPluginsGui().connect(e_connections, []() {
		Log::message("\Handling BeginPluginsGui event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventBeginPluginsGui().disconnect(beginpluginsgui_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginPluginsGui events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventBeginPluginsGui().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventBeginPluginsGui().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventEndPluginsGui () const

event triggered after the gui() function of plugins is called. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndPluginsGui event handler
void endpluginsgui_event_handler()
{
	Log::message("\Handling EndPluginsGui event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endpluginsgui_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventEndPluginsGui().connect(endpluginsgui_event_connections, endpluginsgui_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventEndPluginsGui().connect(endpluginsgui_event_connections, []() {
		Log::message("\Handling EndPluginsGui event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endpluginsgui_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endpluginsgui_event_connection;

// subscribe to the EndPluginsGui event with a handler function keeping the connection
Engine::getEventEndPluginsGui().connect(endpluginsgui_event_connection, endpluginsgui_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endpluginsgui_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endpluginsgui_event_connection.setEnabled(true);

// ...

// remove subscription to the EndPluginsGui event via the connection
endpluginsgui_event_connection.disconnect();

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

	// A EndPluginsGui event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndPluginsGui event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventEndPluginsGui().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endpluginsgui_handler_id;

// subscribe to the EndPluginsGui event with a lambda handler function and keeping connection ID
endpluginsgui_handler_id = Engine::getEventEndPluginsGui().connect(e_connections, []() {
		Log::message("\Handling EndPluginsGui event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventEndPluginsGui().disconnect(endpluginsgui_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndPluginsGui events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventEndPluginsGui().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventEndPluginsGui().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventBeginPostRender () const

event triggered before the post-rendering stage. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginPostRender event handler
void beginpostrender_event_handler()
{
	Log::message("\Handling BeginPostRender event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginpostrender_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventBeginPostRender().connect(beginpostrender_event_connections, beginpostrender_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventBeginPostRender().connect(beginpostrender_event_connections, []() {
		Log::message("\Handling BeginPostRender event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginpostrender_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginpostrender_event_connection;

// subscribe to the BeginPostRender event with a handler function keeping the connection
Engine::getEventBeginPostRender().connect(beginpostrender_event_connection, beginpostrender_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginpostrender_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginpostrender_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginPostRender event via the connection
beginpostrender_event_connection.disconnect();

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

	// A BeginPostRender event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginPostRender event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventBeginPostRender().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginpostrender_handler_id;

// subscribe to the BeginPostRender event with a lambda handler function and keeping connection ID
beginpostrender_handler_id = Engine::getEventBeginPostRender().connect(e_connections, []() {
		Log::message("\Handling BeginPostRender event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventBeginPostRender().disconnect(beginpostrender_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginPostRender events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventBeginPostRender().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventBeginPostRender().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventEndPostRender () const

event triggered after the post-rendering stage. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndPostRender event handler
void endpostrender_event_handler()
{
	Log::message("\Handling EndPostRender event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endpostrender_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventEndPostRender().connect(endpostrender_event_connections, endpostrender_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventEndPostRender().connect(endpostrender_event_connections, []() {
		Log::message("\Handling EndPostRender event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endpostrender_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endpostrender_event_connection;

// subscribe to the EndPostRender event with a handler function keeping the connection
Engine::getEventEndPostRender().connect(endpostrender_event_connection, endpostrender_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endpostrender_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endpostrender_event_connection.setEnabled(true);

// ...

// remove subscription to the EndPostRender event via the connection
endpostrender_event_connection.disconnect();

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

	// A EndPostRender event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndPostRender event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventEndPostRender().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endpostrender_handler_id;

// subscribe to the EndPostRender event with a lambda handler function and keeping connection ID
endpostrender_handler_id = Engine::getEventEndPostRender().connect(e_connections, []() {
		Log::message("\Handling EndPostRender event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventEndPostRender().disconnect(endpostrender_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndPostRender events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventEndPostRender().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventEndPostRender().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventEndRender () const

event triggered after the rendering stage is finished. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndRender event handler
void endrender_event_handler()
{
	Log::message("\Handling EndRender event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endrender_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventEndRender().connect(endrender_event_connections, endrender_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventEndRender().connect(endrender_event_connections, []() {
		Log::message("\Handling EndRender event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endrender_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endrender_event_connection;

// subscribe to the EndRender event with a handler function keeping the connection
Engine::getEventEndRender().connect(endrender_event_connection, endrender_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endrender_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endrender_event_connection.setEnabled(true);

// ...

// remove subscription to the EndRender event via the connection
endrender_event_connection.disconnect();

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

	// A EndRender event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndRender event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventEndRender().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endrender_handler_id;

// subscribe to the EndRender event with a lambda handler function and keeping connection ID
endrender_handler_id = Engine::getEventEndRender().connect(e_connections, []() {
		Log::message("\Handling EndRender event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventEndRender().disconnect(endrender_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndRender events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventEndRender().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventEndRender().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventBeginSwap () const

event triggered before the swap stage is started. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginSwap event handler
void beginswap_event_handler()
{
	Log::message("\Handling BeginSwap event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginswap_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventBeginSwap().connect(beginswap_event_connections, beginswap_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventBeginSwap().connect(beginswap_event_connections, []() {
		Log::message("\Handling BeginSwap event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginswap_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginswap_event_connection;

// subscribe to the BeginSwap event with a handler function keeping the connection
Engine::getEventBeginSwap().connect(beginswap_event_connection, beginswap_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginswap_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginswap_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginSwap event via the connection
beginswap_event_connection.disconnect();

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

	// A BeginSwap event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginSwap event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventBeginSwap().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginswap_handler_id;

// subscribe to the BeginSwap event with a lambda handler function and keeping connection ID
beginswap_handler_id = Engine::getEventBeginSwap().connect(e_connections, []() {
		Log::message("\Handling BeginSwap event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventBeginSwap().disconnect(beginswap_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginSwap events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventBeginSwap().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventBeginSwap().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventEndPathfinding () const

event triggered after the pathfinding is updated. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndPathfinding event handler
void endpathfinding_event_handler()
{
	Log::message("\Handling EndPathfinding event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endpathfinding_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventEndPathfinding().connect(endpathfinding_event_connections, endpathfinding_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventEndPathfinding().connect(endpathfinding_event_connections, []() {
		Log::message("\Handling EndPathfinding event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endpathfinding_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endpathfinding_event_connection;

// subscribe to the EndPathfinding event with a handler function keeping the connection
Engine::getEventEndPathfinding().connect(endpathfinding_event_connection, endpathfinding_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endpathfinding_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endpathfinding_event_connection.setEnabled(true);

// ...

// remove subscription to the EndPathfinding event via the connection
endpathfinding_event_connection.disconnect();

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

	// A EndPathfinding event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndPathfinding event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventEndPathfinding().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endpathfinding_handler_id;

// subscribe to the EndPathfinding event with a lambda handler function and keeping connection ID
endpathfinding_handler_id = Engine::getEventEndPathfinding().connect(e_connections, []() {
		Log::message("\Handling EndPathfinding event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventEndPathfinding().disconnect(endpathfinding_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndPathfinding events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventEndPathfinding().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventEndPathfinding().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventBeginWorldSwap () const

event triggered before the world logic swap() function is executed. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginWorldSwap event handler
void beginworldswap_event_handler()
{
	Log::message("\Handling BeginWorldSwap event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginworldswap_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventBeginWorldSwap().connect(beginworldswap_event_connections, beginworldswap_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventBeginWorldSwap().connect(beginworldswap_event_connections, []() {
		Log::message("\Handling BeginWorldSwap event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginworldswap_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginworldswap_event_connection;

// subscribe to the BeginWorldSwap event with a handler function keeping the connection
Engine::getEventBeginWorldSwap().connect(beginworldswap_event_connection, beginworldswap_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginworldswap_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginworldswap_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginWorldSwap event via the connection
beginworldswap_event_connection.disconnect();

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

	// A BeginWorldSwap event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginWorldSwap event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventBeginWorldSwap().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginworldswap_handler_id;

// subscribe to the BeginWorldSwap event with a lambda handler function and keeping connection ID
beginworldswap_handler_id = Engine::getEventBeginWorldSwap().connect(e_connections, []() {
		Log::message("\Handling BeginWorldSwap event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventBeginWorldSwap().disconnect(beginworldswap_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginWorldSwap events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventBeginWorldSwap().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventBeginWorldSwap().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventEndWorldSwap () const

event triggered after the world logic swap() function is executed. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndWorldSwap event handler
void endworldswap_event_handler()
{
	Log::message("\Handling EndWorldSwap event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endworldswap_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventEndWorldSwap().connect(endworldswap_event_connections, endworldswap_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventEndWorldSwap().connect(endworldswap_event_connections, []() {
		Log::message("\Handling EndWorldSwap event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endworldswap_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endworldswap_event_connection;

// subscribe to the EndWorldSwap event with a handler function keeping the connection
Engine::getEventEndWorldSwap().connect(endworldswap_event_connection, endworldswap_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endworldswap_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endworldswap_event_connection.setEnabled(true);

// ...

// remove subscription to the EndWorldSwap event via the connection
endworldswap_event_connection.disconnect();

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

	// A EndWorldSwap event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndWorldSwap event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventEndWorldSwap().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endworldswap_handler_id;

// subscribe to the EndWorldSwap event with a lambda handler function and keeping connection ID
endworldswap_handler_id = Engine::getEventEndWorldSwap().connect(e_connections, []() {
		Log::message("\Handling EndWorldSwap event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventEndWorldSwap().disconnect(endworldswap_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndWorldSwap events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventEndWorldSwap().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventEndWorldSwap().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventBeginPluginsSwap () const

event triggered before the plugin swap() function is called, if it exists. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginPluginsSwap event handler
void beginpluginsswap_event_handler()
{
	Log::message("\Handling BeginPluginsSwap event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginpluginsswap_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventBeginPluginsSwap().connect(beginpluginsswap_event_connections, beginpluginsswap_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventBeginPluginsSwap().connect(beginpluginsswap_event_connections, []() {
		Log::message("\Handling BeginPluginsSwap event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginpluginsswap_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginpluginsswap_event_connection;

// subscribe to the BeginPluginsSwap event with a handler function keeping the connection
Engine::getEventBeginPluginsSwap().connect(beginpluginsswap_event_connection, beginpluginsswap_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginpluginsswap_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginpluginsswap_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginPluginsSwap event via the connection
beginpluginsswap_event_connection.disconnect();

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

	// A BeginPluginsSwap event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginPluginsSwap event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventBeginPluginsSwap().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginpluginsswap_handler_id;

// subscribe to the BeginPluginsSwap event with a lambda handler function and keeping connection ID
beginpluginsswap_handler_id = Engine::getEventBeginPluginsSwap().connect(e_connections, []() {
		Log::message("\Handling BeginPluginsSwap event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventBeginPluginsSwap().disconnect(beginpluginsswap_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginPluginsSwap events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventBeginPluginsSwap().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventBeginPluginsSwap().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventEndPluginsSwap () const

event triggered after the plugin swap() function is called, if it exists. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndPluginsSwap event handler
void endpluginsswap_event_handler()
{
	Log::message("\Handling EndPluginsSwap event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endpluginsswap_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventEndPluginsSwap().connect(endpluginsswap_event_connections, endpluginsswap_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventEndPluginsSwap().connect(endpluginsswap_event_connections, []() {
		Log::message("\Handling EndPluginsSwap event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endpluginsswap_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endpluginsswap_event_connection;

// subscribe to the EndPluginsSwap event with a handler function keeping the connection
Engine::getEventEndPluginsSwap().connect(endpluginsswap_event_connection, endpluginsswap_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endpluginsswap_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endpluginsswap_event_connection.setEnabled(true);

// ...

// remove subscription to the EndPluginsSwap event via the connection
endpluginsswap_event_connection.disconnect();

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

	// A EndPluginsSwap event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndPluginsSwap event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventEndPluginsSwap().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endpluginsswap_handler_id;

// subscribe to the EndPluginsSwap event with a lambda handler function and keeping connection ID
endpluginsswap_handler_id = Engine::getEventEndPluginsSwap().connect(e_connections, []() {
		Log::message("\Handling EndPluginsSwap event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventEndPluginsSwap().disconnect(endpluginsswap_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndPluginsSwap events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventEndPluginsSwap().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventEndPluginsSwap().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventBeginDeleteObjects () const

event triggered before the objects are deleted. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginDeleteObjects event handler
void begindeleteobjects_event_handler()
{
	Log::message("\Handling BeginDeleteObjects event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begindeleteobjects_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventBeginDeleteObjects().connect(begindeleteobjects_event_connections, begindeleteobjects_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventBeginDeleteObjects().connect(begindeleteobjects_event_connections, []() {
		Log::message("\Handling BeginDeleteObjects event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
begindeleteobjects_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection begindeleteobjects_event_connection;

// subscribe to the BeginDeleteObjects event with a handler function keeping the connection
Engine::getEventBeginDeleteObjects().connect(begindeleteobjects_event_connection, begindeleteobjects_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
begindeleteobjects_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
begindeleteobjects_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginDeleteObjects event via the connection
begindeleteobjects_event_connection.disconnect();

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

	// A BeginDeleteObjects event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginDeleteObjects event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventBeginDeleteObjects().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId begindeleteobjects_handler_id;

// subscribe to the BeginDeleteObjects event with a lambda handler function and keeping connection ID
begindeleteobjects_handler_id = Engine::getEventBeginDeleteObjects().connect(e_connections, []() {
		Log::message("\Handling BeginDeleteObjects event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventBeginDeleteObjects().disconnect(begindeleteobjects_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginDeleteObjects events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventBeginDeleteObjects().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventBeginDeleteObjects().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventEndDeleteObjects () const

event triggered after the objects are deleted. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndDeleteObjects event handler
void enddeleteobjects_event_handler()
{
	Log::message("\Handling EndDeleteObjects event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections enddeleteobjects_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventEndDeleteObjects().connect(enddeleteobjects_event_connections, enddeleteobjects_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventEndDeleteObjects().connect(enddeleteobjects_event_connections, []() {
		Log::message("\Handling EndDeleteObjects event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
enddeleteobjects_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection enddeleteobjects_event_connection;

// subscribe to the EndDeleteObjects event with a handler function keeping the connection
Engine::getEventEndDeleteObjects().connect(enddeleteobjects_event_connection, enddeleteobjects_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
enddeleteobjects_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
enddeleteobjects_event_connection.setEnabled(true);

// ...

// remove subscription to the EndDeleteObjects event via the connection
enddeleteobjects_event_connection.disconnect();

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

	// A EndDeleteObjects event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndDeleteObjects event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventEndDeleteObjects().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId enddeleteobjects_handler_id;

// subscribe to the EndDeleteObjects event with a lambda handler function and keeping connection ID
enddeleteobjects_handler_id = Engine::getEventEndDeleteObjects().connect(e_connections, []() {
		Log::message("\Handling EndDeleteObjects event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventEndDeleteObjects().disconnect(enddeleteobjects_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndDeleteObjects events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventEndDeleteObjects().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventEndDeleteObjects().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventEndSwap () const

event triggered after the swap stage is finished. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndSwap event handler
void endswap_event_handler()
{
	Log::message("\Handling EndSwap event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endswap_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventEndSwap().connect(endswap_event_connections, endswap_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventEndSwap().connect(endswap_event_connections, []() {
		Log::message("\Handling EndSwap event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endswap_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endswap_event_connection;

// subscribe to the EndSwap event with a handler function keeping the connection
Engine::getEventEndSwap().connect(endswap_event_connection, endswap_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endswap_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endswap_event_connection.setEnabled(true);

// ...

// remove subscription to the EndSwap event via the connection
endswap_event_connection.disconnect();

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

	// A EndSwap event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndSwap event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventEndSwap().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endswap_handler_id;

// subscribe to the EndSwap event with a lambda handler function and keeping connection ID
endswap_handler_id = Engine::getEventEndSwap().connect(e_connections, []() {
		Log::message("\Handling EndSwap event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventEndSwap().disconnect(endswap_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndSwap events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventEndSwap().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventEndSwap().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventFocusGained () const

event triggered when any of the engine windows gained the focus. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the FocusGained event handler
void focusgained_event_handler()
{
	Log::message("\Handling FocusGained event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections focusgained_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventFocusGained().connect(focusgained_event_connections, focusgained_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventFocusGained().connect(focusgained_event_connections, []() {
		Log::message("\Handling FocusGained event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
focusgained_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection focusgained_event_connection;

// subscribe to the FocusGained event with a handler function keeping the connection
Engine::getEventFocusGained().connect(focusgained_event_connection, focusgained_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
focusgained_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
focusgained_event_connection.setEnabled(true);

// ...

// remove subscription to the FocusGained event via the connection
focusgained_event_connection.disconnect();

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

	// A FocusGained event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling FocusGained event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventFocusGained().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId focusgained_handler_id;

// subscribe to the FocusGained event with a lambda handler function and keeping connection ID
focusgained_handler_id = Engine::getEventFocusGained().connect(e_connections, []() {
		Log::message("\Handling FocusGained event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventFocusGained().disconnect(focusgained_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all FocusGained events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventFocusGained().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventFocusGained().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event getEventFocusLost () const

event triggered when all engine windows lost the focus. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the FocusLost event handler
void focuslost_event_handler()
{
	Log::message("\Handling FocusLost event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections focuslost_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventFocusLost().connect(focuslost_event_connections, focuslost_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventFocusLost().connect(focuslost_event_connections, []() {
		Log::message("\Handling FocusLost event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
focuslost_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection focuslost_event_connection;

// subscribe to the FocusLost event with a handler function keeping the connection
Engine::getEventFocusLost().connect(focuslost_event_connection, focuslost_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
focuslost_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
focuslost_event_connection.setEnabled(true);

// ...

// remove subscription to the FocusLost event via the connection
focuslost_event_connection.disconnect();

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

	// A FocusLost event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling FocusLost event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventFocusLost().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId focuslost_handler_id;

// subscribe to the FocusLost event with a lambda handler function and keeping connection ID
focuslost_handler_id = Engine::getEventFocusLost().connect(e_connections, []() {
		Log::message("\Handling FocusLost event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventFocusLost().disconnect(focuslost_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all FocusLost events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventFocusLost().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventFocusLost().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const char*> getEventPluginAdded () const

event triggered before the update stage is started. You can subscribe to events via *connect()*ï¿½ and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)*ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const char ***plugin_name**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the PluginAdded event handler
void pluginadded_event_handler(const char *plugin_name)
{
	Log::message("\Handling PluginAdded event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections pluginadded_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventPluginAdded().connect(pluginadded_event_connections, pluginadded_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventPluginAdded().connect(pluginadded_event_connections, [](const char *plugin_name) {
		Log::message("\Handling PluginAdded event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
pluginadded_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection pluginadded_event_connection;

// subscribe to the PluginAdded event with a handler function keeping the connection
Engine::getEventPluginAdded().connect(pluginadded_event_connection, pluginadded_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
pluginadded_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
pluginadded_event_connection.setEnabled(true);

// ...

// remove subscription to the PluginAdded event via the connection
pluginadded_event_connection.disconnect();

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

	// A PluginAdded event handler implemented as a class member
	void event_handler(const char *plugin_name)
	{
		Log::message("\Handling PluginAdded event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventPluginAdded().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId pluginadded_handler_id;

// subscribe to the PluginAdded event with a lambda handler function and keeping connection ID
pluginadded_handler_id = Engine::getEventPluginAdded().connect(e_connections, [](const char *plugin_name) {
		Log::message("\Handling PluginAdded event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventPluginAdded().disconnect(pluginadded_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all PluginAdded events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventPluginAdded().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventPluginAdded().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const char*> getEventPluginRemoved () const

event triggered before the update stage is started. You can subscribe to events via *connect()*ï¿½ and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)*ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const char ***plugin_name**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the PluginRemoved event handler
void pluginremoved_event_handler(const char *plugin_name)
{
	Log::message("\Handling PluginRemoved event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections pluginremoved_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Engine::getEventPluginRemoved().connect(pluginremoved_event_connections, pluginremoved_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Engine::getEventPluginRemoved().connect(pluginremoved_event_connections, [](const char *plugin_name) {
		Log::message("\Handling PluginRemoved event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
pluginremoved_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection pluginremoved_event_connection;

// subscribe to the PluginRemoved event with a handler function keeping the connection
Engine::getEventPluginRemoved().connect(pluginremoved_event_connection, pluginremoved_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
pluginremoved_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
pluginremoved_event_connection.setEnabled(true);

// ...

// remove subscription to the PluginRemoved event via the connection
pluginremoved_event_connection.disconnect();

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

	// A PluginRemoved event handler implemented as a class member
	void event_handler(const char *plugin_name)
	{
		Log::message("\Handling PluginRemoved event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Engine::getEventPluginRemoved().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId pluginremoved_handler_id;

// subscribe to the PluginRemoved event with a lambda handler function and keeping connection ID
pluginremoved_handler_id = Engine::getEventPluginRemoved().connect(e_connections, [](const char *plugin_name) {
		Log::message("\Handling PluginRemoved event (lambda).\n");
	}
);

// remove the subscription later using the ID
Engine::getEventPluginRemoved().disconnect(pluginremoved_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all PluginRemoved events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Engine::getEventPluginRemoved().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Engine::getEventPluginRemoved().setEnabled(true);

```

</details>

### Return value

Event instance.
---

## static Engine * get ( )

Returns a pointer to the existing engine instance.
### Return value

Pointer to the existing engine.
## virtual const char * getArg ( int num ) const

Returns a [command line](../../../code/command_line.md) argument by its index.
### Arguments

- *int* **num** - Index of the command line argument.

### Return value

Command line argument.
## virtual float getArgf ( int num ) const =0

Returns a [command line](../../../code/command_line.md) argument by its index converted to a floating point value.
### Arguments

- *int* **num** - Index of the command line argument.

### Return value

Command line argument.
## virtual int getArgi ( int num ) const =0

Returns a [command line](../../../code/command_line.md) argument by its index converted to an integer value.
### Arguments

- *int* **num** - Index of the command line argument.

### Return value

Command line argument.
## static Engine::BUILD_CONFIG getBuildConfiguration ( )

Returns the current Engine build configuration.
### Return value

Current build configuration. One of the [BUILD_CONFIG_](#BUILD_CONFIG) values.
## static const char * getLibraryModulePath ( )

Returns a path to the Engine's dynamic library file.
### Return value

Path to the Engine's dynamic library file.
## virtual int getEditorFunction ( const char * name , int num_args ) const

Returns the editor function identifier.
### Arguments

- *const char ** **name** - Name of the editor script function.
- *int* **num_args** - Number of editor script function arguments.

### Return value

The editor script function identifier.
## virtual bool isEditorFunction ( const char * name , int num_args ) const

Returns a value indicating if the editor script function exists.
### Arguments

- *const char ** **name** - Name of the editor script function.
- *int* **num_args** - Number of editor script function arguments.

### Return value

true if the editor script function exists; otherwise, false.
## virtual void * getEditorInterpreter ( ) const =0

Returns a pointer to the editor interpreter.
### Return value

Pointer to the editor interpreter.
## virtual bool isEditorInterpreter ( ) const =0

Returns a value indicating if the function is called from the editor script.
### Return value

true if the function is called from the editor script; otherwise, false.
## virtual bool isEditorLoaded ( ) const =0

Returns a value indicating if the editor script is loaded.
### Return value

true if the editor script is loaded; otherwise, false.
## virtual EditorLogic * getEditorLogic ( int num ) const =0

Returns the registered [EditorLogic](../../../api/library/common/logic/class.editorlogic_cpp.md) instance by its number.
### Arguments

- *int* **num** - Number of the EditorLogic instance.

### Return value

[EditorLogic](../../../api/library/common/logic/class.editorlogic_cpp.md) instance.
## virtual void setEditorVariable ( const char * name , const Variable & v ) =0

Sets the editor script variable by its name.
### Arguments

- *const char ** **name** - Name of the editor script variable.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **v** - Value of the editor script variable.

## virtual const Variable & getEditorVariable ( const char * name ) const =0

Returns the editor script variable by its name.
### Arguments

- *const char ** **name** - Name of the world script variable.

### Return value

Value of the editor script variable.
## virtual bool isEditorVariable ( const char * name ) const =0

Returns a value indicating if the editor script variable exists.
### Arguments

- *const char ** **name** - Name of the editor script variable.

### Return value

true if the editor script variable exists; otherwise, false.
## virtual const char * getArg ( int num ) =0

Returns the command-line argument by its index.
### Arguments

- *int* **num** - Index of the argument.

### Return value

Command-line argument
## template < SingletonClass class >

## SingletonClass * getPlugin ( const char * name )

Returns the loaded plugin interface.
### Arguments

- *const char ** **name** - Name of the loaded plugin.

### Return value

Interface of the loaded plugin, if it exists; otherwise, **nullptr**.
## virtual void * getPluginData ( int num ) const =0

Returns the data of the specified loaded plugin by calling its [get_data()](../../../api/library/common/class.plugin_cpp.md#get_data_void_ptr) method.
### Arguments

- *int* **num** - Index of the loaded plugin.

### Return value

Data of the loaded plugin, if it exists; otherwise, **0**.
## virtual Plugin * getPluginInterface ( int num ) const =0

Returns the loaded plugin interface.
### Arguments

- *int* **num** - Index of the loaded plugin.

### Return value

Interface of the loaded plugin, if it exists; otherwise, **0**.
## const char * getPluginName ( int num ) const

Returns the name of the specified loaded plugin by calling its *[get_name()](../../../api/library/common/class.plugin_cpp.md#get_name_const_char_ptr)* method.
### Arguments

- *int* **num** - Index of the loaded plugin.

### Return value

Loaded plugin name.
## int getPluginOrder ( int num ) const

Returns the execution order of the specified loaded plugin by calling its *[get_order()](../../../api/library/common/class.plugin_cpp.md#get_order_int)* method.
### Arguments

- *int* **num** - Index of the loaded plugin.

### Return value

Loaded plugin execution order.
## const char * getPluginPath ( int num ) const

Returns a path to a plugin directory specified via [-plugin_path](../../../code/command_line.md#plugin_path).
### Arguments

- *int* **num** - Plugin path number in the row of the specified plugin paths.

### Return value

Path to a plugin directory.
## const char * getPluginAbsolutePath ( int num ) const

Returns an absolute path to a plugin directory.
### Arguments

- *int* **num** - Plugin path number in the row of the specified plugin paths.

### Return value

Absolute path to a plugin directory.
## int getSystemFunction ( const char * name , int num_args ) const

Returns the system function identifier.
### Arguments

- *const char ** **name** - Name of the system script function.
- *int* **num_args** - Number of system script function arguments.

### Return value

System script function identifier.
## bool isSystemFunction ( const char * name , int num_args ) const

Checks whether the system script function exists.
### Arguments

- *const char ** **name** - Name of the system script function.
- *int* **num_args** - Number of system script function arguments.

### Return value

true if the system script function exists; otherwise, false.
## virtual void * getSystemInterpreter ( ) const =0

Returns a pointer to the system interpreter.
### Return value

Pointer to the system interpreter.
## virtual bool isSystemInterpreter ( ) const =0

Checks if the function is called from the system script.
### Return value

true when the function is called from the system script; otherwise, false.
## virtual SystemLogic * getSystemLogic ( int num ) const =0

Returns the registered [SystemLogic](../../../api/library/common/logic/class.systemlogic_cpp.md) instance by the given number.
### Arguments

- *int* **num** - Number of the SystemLogic instance.

### Return value

[SystemLogic](../../../api/library/common/logic/class.systemlogic_cpp.md) instance.
## void setSystemVariable ( const char * name , const Variable & v )

Sets a system script variable by a name.
### Arguments

- *const char ** **name** - Name of the system script variable.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **v** - Value of the system script variable.

## const Variable & getSystemVariable ( const char * name ) const

Returns the system script variable by its name.
### Arguments

- *const char ** **name** - Name of the system script variable.

### Return value

System script variable.
## bool isSystemVariable ( const char * name ) const

Checks whether a system script variable exists.
### Arguments

- *const char ** **name** - Name of the system script variable.

### Return value

true if the system script variable exists; otherwise, false.
## int getWorldFunction ( const char * name , int num_args ) const

Returns the world script function identifier.
### Arguments

- *const char ** **name** - Name of the world script function.
- *int* **num_args** - Number of world script function arguments.

### Return value

World script function identifier.
## bool isWorldFunction ( const char * name , int num_args ) const

Returns value indicating if the world script function exists.
### Arguments

- *const char ** **name** - Name of the world script function.
- *int* **num_args** - Number of world script function arguments.

### Return value

true if the world script function exists; otherwise, false.
## virtual void * getWorldInterpreter ( ) const =0

Returns a pointer to the world interpreter.
### Return value

Pointer to the world interpreter.
## virtual bool isWorldInterpreter ( ) const =0

Returns a value indicating if the function is called from the world script.
### Return value

true if the function is called from the world script; otherwise, false.
## virtual bool isWorldLoaded ( ) const =0

Returns a value indicating if the world script is loaded.
### Return value

true if the world script is loaded; otherwise, false.
## virtual WorldLogic * getWorldLogic ( int num ) const =0

Returns the registered [WorldLogic](../../../api/library/common/logic/class.worldlogic_cpp.md) instance by its number.
### Arguments

- *int* **num** - Number of the WorldLogic instance.

### Return value

[WorldLogic](../../../api/library/common/logic/class.worldlogic_cpp.md) instance.
## void setWorldVariable ( const char * name , const Variable & v )

Sets a world script variable by its name.
### Arguments

- *const char ** **name** - Name of the world script variable.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **v** - Value of the world script variable.

## const Variable & getWorldVariable ( const char * name ) const

Returns a world script variable by its name.
### Arguments

- *const char ** **name** - Name of the world script variable.

### Return value

World script variable.
## bool isWorldVariable ( const char * name ) const

Returns a value indicating if the world script variable exists.
### Arguments

- *const char ** **name** - Name of the world script variable.

### Return value

true if the world script variable exists; otherwise, false.
## bool addEditorLogic ( EditorLogic * logic )

Adds an [EditorLogic](../../../api/library/common/logic/class.editorlogic_cpp.md) instance to the engine runtime.
### Arguments

- *[EditorLogic](../../../api/library/common/logic/class.editorlogic_cpp.md) ** **logic** - [EditorLogic](../../../api/library/common/logic/class.editorlogic_cpp.md) instance.

### Return value

true if the EditorLogic instance has been added successfully; otherwise, false.
## virtual bool addPlugin ( Plugin * plugin ) =0

Adds a plugin to engine runtime by using a pointer to this plugin.
### Arguments

- *[Plugin](../../../api/library/common/class.plugin_cpp.md) ** **plugin** - Plugin pointer.

### Return value

true if the plugin ha been added successfully; otherwise, false.
## bool addPlugin ( const char * name )

Adds a plugin to engine runtime by its name.
### Arguments

- *const char ** **name** - Plugin name.

### Return value

true if the plugin has been added successfully; otherwise, false.
## bool addSystemLogic ( SystemLogic * logic )

Adds a [SystemLogic](../../../api/library/common/logic/class.systemlogic_cpp.md) instance to Engine runtime.
### Arguments

- *[SystemLogic](../../../api/library/common/logic/class.systemlogic_cpp.md) ** **logic** - [SystemLogic](../../../api/library/common/logic/class.systemlogic_cpp.md) instance.

### Return value

true if the SystemLogic instance has been added successfully; otherwise, false.
## bool addWorldLogic ( WorldLogic * logic )


Adds a [WorldLogic](../../../api/library/common/logic/class.worldlogic_cpp.md) instance to the engine runtime.


> **Notice:** Instances of the *WorldLogic* class **should not be added while the world is loaded** and the world script is being executed (as you can't change a world script while the world is loaded). In such a case the ***init()*** method shall not be called if the WorldLogic is added before opening the world.


### Arguments

- *[WorldLogic](../../../api/library/common/logic/class.worldlogic_cpp.md) ** **logic** - [WorldLogic](../../../api/library/common/logic/class.worldlogic_cpp.md) instance.

### Return value

true if the WorldLogic instance has been added successfully; otherwise, false.
## int findPlugin ( const char * name ) const

Searches the index of the loaded plugin by its name.
### Arguments

- *const char ** **name** - Name of the plugin.

### Return value

Index of the plugin if it is found, or -1 otherwise.
## void main ( SystemLogic * system , WorldLogic * world , EditorLogic * editor )

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

- *[SystemLogic](../../../api/library/common/logic/class.systemlogic_cpp.md) ** **system** - A [SystemLogic](../../../api/library/common/logic/class.systemlogic_cpp.md) instance.
- *[WorldLogic](../../../api/library/common/logic/class.worldlogic_cpp.md) ** **world** - A [WorldLogic](../../../api/library/common/logic/class.worldlogic_cpp.md) instance.
- *[EditorLogic](../../../api/library/common/logic/class.editorlogic_cpp.md) ** **editor** - An [EditorLogic](../../../api/library/common/logic/class.editorlogic_cpp.md) instance.

## bool removeEditorLogic ( EditorLogic * logic )

Removes an [EditorLogic](../../../api/library/common/logic/class.editorlogic_cpp.md) instance from engine runtime.
### Arguments

- *[EditorLogic](../../../api/library/common/logic/class.editorlogic_cpp.md) ** **logic** - An [EditorLogic](../../../api/library/common/logic/class.editorlogic_cpp.md) instance.

### Return value

true if the instance has been removed successfully; otherwise, false.
## virtual bool destroyPlugin ( Plugin * plugin ) =0

Removes the specified plugin.
### Arguments

- *[Plugin](../../../api/library/common/class.plugin_cpp.md) ** **plugin** - Plugin pointer to remove.

### Return value

true if the plugin has been removed successfully; otherwise, false.
## bool removeSystemLogic ( SystemLogic * logic )

Removes a [SystemLogic](../../../api/library/common/logic/class.systemlogic_cpp.md) instance from engine runtime.
### Arguments

- *[SystemLogic](../../../api/library/common/logic/class.systemlogic_cpp.md) ** **logic** - A [SystemLogic](../../../api/library/common/logic/class.systemlogic_cpp.md) instance.

### Return value

true if the instance has been removed successfully; otherwise, false.
## bool removeWorldLogic ( WorldLogic * logic )


Removes a [WorldLogic](../../../api/library/common/logic/class.worldlogic_cpp.md) instance from engine runtime.


> **Notice:** Instances of the *WorldLogic* class **should not be removed while the world is loaded** and the world script is being executed (as you can't change a world script while the world is loaded). In such a case the ***shutdown()*** method shall not be called if the WorldLogic is removed before closing the world.


### Arguments

- *[WorldLogic](../../../api/library/common/logic/class.worldlogic_cpp.md) ** **logic** - A [WorldLogic](../../../api/library/common/logic/class.worldlogic_cpp.md) instance.

### Return value

true if the instance has been removed successfully; otherwise, false.
## virtual const Variable & runEditorFunction ( const Variable & name ) =0

Runs the editor script function by its name. The target function can receive up to 8 arguments.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **name** - Name of the editor script function.

### Return value

Editor script function return value.
## const Variable & runEditorFunction ( const Variable & name , const Variable & a0 )

Runs the editor script function by its name. The target function must receive 1 argument.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **name** - Name of the editor script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.

### Return value

Editor script function return value.
## const Variable & runEditorFunction ( const Variable & name , const Variable & a0 , const Variable & a1 )

Runs the editor script function by its name. The target function must receive 2 arguments.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **name** - Name of the editor script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a1** - Second argument.

### Return value

Editor script function return value.
## const Variable & runEditorFunction ( const Variable & name , const Variable & a0 , const Variable & a1 , const Variable & a2 )

Runs the editor script function by its name. The target function must receive 3 arguments.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **name** - Name of the editor script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a1** - Second argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a2** - Third argument.

### Return value

Editor script function return value.
## const Variable & runEditorFunction ( const Variable & name , const Variable & a0 , const Variable & a1 , const Variable & a2 , const Variable & a3 )

Runs the editor script function by its name. The target function must receive 4 arguments.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **name** - Name of the editor script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a1** - Second argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a2** - Third argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a3** - Fourth argument.

### Return value

Editor script function return value.
## const Variable & runEditorFunction ( const Variable & name , const Variable & a0 , const Variable & a1 , const Variable & a2 , const Variable & a3 , const Variable & a4 )

Runs the editor script function by its name. The target function must receive 5 arguments.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **name** - Name of the editor script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a1** - Second argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a2** - Third argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a3** - Fourth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a4** - Fifth argument.

### Return value

Editor script function return value.
## const Variable & runEditorFunction ( const Variable & name , const Variable & a0 , const Variable & a1 , const Variable & a2 , const Variable & a3 , const Variable & a4 , const Variable & a5 )

Runs the editor script function by its name. The target function must receive 6 arguments.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **name** - Name of the editor script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a1** - Second argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a2** - Third argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a3** - Fourth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a4** - Fifth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a5** - Sixth argument.

### Return value

Editor script function return value.
## const Variable & runEditorFunction ( const Variable & name , const Variable & a0 , const Variable & a1 , const Variable & a2 , const Variable & a3 , const Variable & a4 , const Variable & a5 , const Variable & a6 )

Runs the editor script function by its name. The target function must receive 7 arguments.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **name** - Name of the editor script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a1** - Second argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a2** - Third argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a3** - Fourth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a4** - Fifth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a5** - Sixth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a6** - Seventh argument.

### Return value

Editor script function return value.
## const Variable & runEditorFunction ( const Variable & name , const Variable & a0 , const Variable & a1 , const Variable & a2 , const Variable & a3 , const Variable & a4 , const Variable & a5 , const Variable & a6 , const Variable & a7 )

Runs the editor script function by its name. The target function must receive 8 arguments.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **name** - Name of the editor script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a1** - Second argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a2** - Third argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a3** - Fourth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a4** - Fifth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a5** - Sixth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a6** - Seventh argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a7** - Eighth argument.

### Return value

Editor script function return value.
## virtual const Variable & runEditorFunction ( const Variable & name , const Variable * args , int num_args ) =0

Runs the editor script function by its name.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **name** - Name of the editor script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) ** **args** - Pointer to editor script function arguments.
- *int* **num_args** - Number of editor script function arguments.

### Return value

Editor script function return value.
## const Variable & runEditorFunction ( int id )

Runs the editor script function by its id. The target function can receive up to 8 arguments.
### Arguments

- *int* **id** - ID of the editor script function.

### Return value

Editor script function return value.
## const Variable & runEditorFunction ( int id , const Variable * args , int num_args )

Runs the editor script function by its id.
### Arguments

- *int* **id** - ID of the editor script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) ** **args** - Pointer to editor script function arguments.
- *int* **num_args** - Number of editor script function arguments.

### Return value

Editor script function return value.
## const Variable & runEditorFunction ( int id , const Variable & a0 )

Runs the editor script function by its name. The target function must receive 1 argument.
### Arguments

- *int* **id** - ID of the editor script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.

### Return value

Editor script function return value.
## const Variable & runEditorFunction ( int id , const Variable & a0 , const Variable & a1 )

Runs the editor script function by its name. The target function must receive 2 arguments.
### Arguments

- *int* **id** - ID of the editor script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a1** - Second argument.

### Return value

Editor script function return value.
## const Variable & runEditorFunction ( int id , const Variable & a0 , const Variable & a1 , const Variable & a2 )

Runs the editor script function by its name. The target function must receive 3 arguments.
### Arguments

- *int* **id** - ID of the editor script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a1** - Second argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a2** - Third argument.

### Return value

Editor script function return value.
## const Variable & runEditorFunction ( int id , const Variable & a0 , const Variable & a1 , const Variable & a2 , const Variable & a3 )

Runs the editor script function by its name. The target function must receive 4 arguments.
### Arguments

- *int* **id** - ID of the editor script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a1** - Second argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a2** - Third argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a3** - Fourth argument.

### Return value

Editor script function return value.
## const Variable & runEditorFunction ( int id , const Variable & a0 , const Variable & a1 , const Variable & a2 , const Variable & a3 , const Variable & a4 )

Runs the editor script function by its name. The target function must receive 5 arguments.
### Arguments

- *int* **id** - ID of the editor script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a1** - Second argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a2** - Third argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a3** - Fourth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a4** - Fifth argument.

### Return value

Editor script function return value.
## const Variable & runEditorFunction ( int id , const Variable & a0 , const Variable & a1 , const Variable & a2 , const Variable & a3 , const Variable & a4 , const Variable & a5 )

Runs the editor script function by its name. The target function must receive 6 arguments.
### Arguments

- *int* **id** - ID of the editor script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a1** - Second argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a2** - Third argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a3** - Fourth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a4** - Fifth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a5** - Sixth argument.

### Return value

Editor script function return value.
## const Variable & runEditorFunction ( int id , const Variable & a0 , const Variable & a1 , const Variable & a2 , const Variable & a3 , const Variable & a4 , const Variable & a5 , const Variable & a6 )

Runs the editor script function by its name. The target function must receive 7 arguments.
### Arguments

- *int* **id** - ID of the editor script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a1** - Second argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a2** - Third argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a3** - Fourth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a4** - Fifth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a5** - Sixth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a6** - Seventh argument.

### Return value

Editor script function return value.
## const Variable & runEditorFunction ( int id , const Variable & a0 , const Variable & a1 , const Variable & a2 , const Variable & a3 , const Variable & a4 , const Variable & a5 , const Variable & a6 , const Variable & a7 )

Runs the editor script function by its name. The target function must receive 8 arguments.
### Arguments

- *int* **id** - ID of the editor script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a1** - Second argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a2** - Third argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a3** - Fourth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a4** - Fifth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a5** - Sixth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a6** - Seventh argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a7** - Eighth argument.

### Return value

Editor script function return value.
## virtual const Variable & runSystemFunction ( const Variable & name ) =0

Runs the system script function by its name. The target function can receive up to 8 arguments.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **name** - Name of the system script function.

### Return value

System script function return value.
## const Variable & runSystemFunction ( const Variable & name , const Variable & a0 )

Runs the system script function by its name. The target function must receive 1 argument.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **name** - Name of the system script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.

### Return value

System script function return value.
## const Variable & runSystemFunction ( const Variable & name , const Variable & a0 , const Variable & a1 )

Runs the system script function by its name. The target function must receive 2 arguments.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **name** - Name of the system script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a1** - Second argument.

### Return value

System script function return value.
## const Variable & runSystemFunction ( const Variable & name , const Variable & a0 , const Variable & a1 , const Variable & a2 )

Runs the system script function by its name. The target function must receive 3 arguments.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **name** - Name of the system script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a1** - Second argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a2** - Third argument.

### Return value

System script function return value.
## const Variable & runSystemFunction ( const Variable & name , const Variable & a0 , const Variable & a1 , const Variable & a2 , const Variable & a3 )

Runs the system script function by its name. The target function must receive 4 arguments.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **name** - Name of the system script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a1** - Second argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a2** - Third argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a3** - Fourth argument.

### Return value

System script function return value.
## const Variable & runSystemFunction ( const Variable & name , const Variable & a0 , const Variable & a1 , const Variable & a2 , const Variable & a3 , const Variable & a4 )

Runs the system script function by its name. The target function must receive 4 arguments.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **name** - Name of the system script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a1** - Second argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a2** - Third argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a3** - Fourth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a4** - Fifth argument.

### Return value

System script function return value.
## const Variable & runSystemFunction ( const Variable & name , const Variable & a0 , const Variable & a1 , const Variable & a2 , const Variable & a3 , const Variable & a4 , const Variable & a5 )

Runs the system script function by its name. The target function must receive 6 arguments.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **name** - Name of the system script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a1** - Second argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a2** - Third argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a3** - Fourth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a4** - Fifth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a5** - Sixth argument.

### Return value

System script function return value.
## const Variable & runSystemFunction ( const Variable & name , const Variable & a0 , const Variable & a1 , const Variable & a2 , const Variable & a3 , const Variable & a4 , const Variable & a5 , const Variable & a6 )

Runs the system script function by its name. The target function must receive 7 arguments.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **name** - Name of the system script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a1** - Second argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a2** - Third argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a3** - Fourth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a4** - Fifth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a5** - Sixth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a6** - Seventh argument.

### Return value

System script function return value.
## const Variable & runSystemFunction ( const Variable & name , const Variable & a0 , const Variable & a1 , const Variable & a2 , const Variable & a3 , const Variable & a4 , const Variable & a5 , const Variable & a6 , const Variable & a7 )

Runs the system script function by its name. The target function must receive 8 arguments.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **name** - Name of the system script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a1** - Second argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a2** - Third argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a3** - Fourth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a4** - Fifth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a5** - Sixth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a6** - Seventh argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a7** - Eighth argument.

### Return value

System script function return value.
## virtual const Variable & runSystemFunction ( const Variable & name , const Variable * args , int num_args ) =0

Runs system script function by its name.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **name** - Name of the system script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) ** **args** - Pointer to system script function arguments.
- *int* **num_args** - Number of system script function arguments.

### Return value

System script function return value.
## const Variable & runSystemFunction ( int id )

Runs the system script function by its id. The target function can receive up to 8 arguments.
### Arguments

- *int* **id** - ID of the system script function.

### Return value

System script function return value.
## const Variable & runSystemFunction ( int id , const Variable * args , int num_args )

Runs system script function by its id.
### Arguments

- *int* **id** - ID of the system script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) ** **args** - Pointer to system script function arguments.
- *int* **num_args** - Number of system script function arguments.

## const Variable & runSystemFunction ( int id , const Variable & a0 )

Runs the system script function by its id. The target function must receive 1 argument.
### Arguments

- *int* **id** - ID of the system script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.

### Return value

System script function return value.
## const Variable & runSystemFunction ( int id , const Variable & a0 , const Variable & a1 )

Runs the system script function by its id. The target function must receive 2 arguments.
### Arguments

- *int* **id** - ID of the system script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a1** - Second argument.

### Return value

System script function return value.
## const Variable & runSystemFunction ( int id , const Variable & a0 , const Variable & a1 , const Variable & a2 )

Runs the system script function by its id. The target function must receive 3 arguments.
### Arguments

- *int* **id** - ID of the system script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a1** - Second argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a2** - Third argument.

### Return value

System script function return value.
## const Variable & runSystemFunction ( int id , const Variable & a0 , const Variable & a1 , const Variable & a2 , const Variable & a3 )

Runs the system script function by its id. The target function must receive 4 arguments.
### Arguments

- *int* **id** - ID of the system script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a1** - Second argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a2** - Third argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a3** - Fourth argument.

### Return value

System script function return value.
## const Variable & runSystemFunction ( int id , const Variable & a0 , const Variable & a1 , const Variable & a2 , const Variable & a3 , const Variable & a4 )

Runs the system script function by its id. The target function must receive 5 arguments.
### Arguments

- *int* **id** - ID of the system script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a1** - Second argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a2** - Third argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a3** - Fourth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a4** - Fifth argument.

### Return value

System script function return value.
## const Variable & runSystemFunction ( int id , const Variable & a0 , const Variable & a1 , const Variable & a2 , const Variable & a3 , const Variable & a4 , const Variable & a5 )

Runs the system script function by its id. The target function must receive 6 arguments.
### Arguments

- *int* **id** - ID of the system script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a1** - Second argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a2** - Third argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a3** - Fourth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a4** - Fifth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a5** - Sixth argument.

### Return value

System script function return value.
## const Variable & runSystemFunction ( int id , const Variable & a0 , const Variable & a1 , const Variable & a2 , const Variable & a3 , const Variable & a4 , const Variable & a5 , const Variable & a6 )

Runs the system script function by its id. The target function must receive 7 arguments.
### Arguments

- *int* **id** - ID of the system script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a1** - Second argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a2** - Third argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a3** - Fourth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a4** - Fifth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a5** - Sixth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a6** - Seventh argument.

### Return value

System script function return value.
## const Variable & runSystemFunction ( int id , const Variable & a0 , const Variable & a1 , const Variable & a2 , const Variable & a3 , const Variable & a4 , const Variable & a5 , const Variable & a6 , const Variable & a7 )

Runs the system script function by its id. The target function must receive 8 arguments.
### Arguments

- *int* **id** - ID of the system script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a1** - Second argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a2** - Third argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a3** - Fourth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a4** - Fifth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a5** - Sixth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a6** - Seventh argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a7** - Eighth argument.

### Return value

System script function return value.
## virtual const Variable & runWorldFunction ( const Variable & name ) =0

Runs the world script function by its name. The target function can receive up to 8 arguments.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **name** - Name of the world script function.

### Return value

World script function return value.
## const Variable & runWorldFunction ( const Variable & name , const Variable & a0 )

Runs the world script function by its name. The target function must receive 1 argument.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **name** - Name of the world script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.

### Return value

World script function return value.
## const Variable & runWorldFunction ( int id , const Variable & a0 )

Runs the world script function by its identifier. The target function must receive one argument.
### Arguments

- *int* **id** - Identifier of the world script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - Argument

### Return value

World script function return value.
## const Variable & runWorldFunction ( const Variable & name , const Variable & a0 , const Variable & a1 )

Runs the world script function by its name. The target function must receive 2 arguments.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **name** - Name of the world script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a1** - Second argument.

### Return value

World script function return value.
## const Variable & runWorldFunction ( const Variable & name , const Variable & a0 , const Variable & a1 , const Variable & a2 )

Runs the world script function by its name. The target function must receive 3 arguments.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **name** - Name of the world script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a1** - Second argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a2** - Third argument.

### Return value

World script function return value.
## const Variable & runWorldFunction ( const Variable & name , const Variable & a0 , const Variable & a1 , const Variable & a2 , const Variable & a3 )

Runs the world script function by its name. The target function must receive 4 arguments.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **name** - Name of the world script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a1** - Second argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a2** - Third argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a3** - Fourth argument.

### Return value

World script function return value.
## const Variable & runWorldFunction ( const Variable & name , const Variable & a0 , const Variable & a1 , const Variable & a2 , const Variable & a3 , const Variable & a4 )

Runs the world script function by its name. The target function must receive 5 arguments.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **name** - Name of the world script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a1** - Second argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a2** - Third argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a3** - Fourth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a4** - Fifth argument.

### Return value

World script function return value.
## const Variable & runWorldFunction ( const Variable & name , const Variable & a0 , const Variable & a1 , const Variable & a2 , const Variable & a3 , const Variable & a4 , const Variable & a5 )

Runs the world script function by its name. The target function must receive 6 arguments.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **name** - Name of the world script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a1** - Second argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a2** - Third argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a3** - Fourth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a4** - Fifth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a5** - Sixth argument.

### Return value

World script function return value.
## const Variable & runWorldFunction ( const Variable & name , const Variable & a0 , const Variable & a1 , const Variable & a2 , const Variable & a3 , const Variable & a4 , const Variable & a5 , const Variable & a6 )

Runs the world script function by its name. The target function must receive 8 arguments.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **name** - Name of the world script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a1** - Second argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a2** - Third argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a3** - Fourth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a4** - Fifth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a5** - Sixth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a6** - Seventh argument.

### Return value

World script function return value.
## const Variable & runWorldFunction ( const Variable & name , const Variable & a0 , const Variable & a1 , const Variable & a2 , const Variable & a3 , const Variable & a4 , const Variable & a5 , const Variable & a6 , const Variable & a7 )

Runs the world script function by its name. The target function must receive 8 arguments.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **name** - Name of the world script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a1** - Second argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a2** - Third argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a3** - Fourth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a4** - Fifth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a5** - Sixth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a6** - Seventh argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a7** - Eighth argument.

### Return value

World script function return value.
## virtual const Variable & runWorldFunction ( const Variable & name , const Variable * args , int num_args ) =0

Runs the world script function by its name.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **name** - Name of the world script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) ** **args** - Pointer to world script function arguments.
- *int* **num_args** - Number of world script function arguments.

### Return value

World script function return value.
## const Variable & runWorldFunction ( int id )

Runs the world script function by its id.
### Arguments

- *int* **id** - ID of the world script function.

### Return value

World script function return value.
## const Variable & runWorldFunction ( int id , const Variable * args , int num_args )

Runs the world script function by its id.
### Arguments

- *int* **id** - ID of the world script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) ** **args** - Pointer to world script function arguments.
- *int* **num_args** - Number of world script function arguments.

### Return value

World script function return value.
## const Variable & runWorldFunction ( int id , const Variable & a0 , const Variable & a1 )

Runs the world script function by its id. The target function must receive 2 arguments.
### Arguments

- *int* **id** - ID of the world script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a1** - Second argument.

### Return value

World script function return value.
## const Variable & runWorldFunction ( int id , const Variable & a0 , const Variable & a1 , const Variable & a2 )

Runs the world script function by its id. The target function must receive 3 arguments.
### Arguments

- *int* **id** - ID of the world script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a1** - Second argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a2** - Third argument.

### Return value

World script function return value.
## const Variable & runWorldFunction ( int id , const Variable & a0 , const Variable & a1 , const Variable & a2 , const Variable & a3 )

### Arguments

- *int* **id** - ID of the world script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a1** - Second argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a2** - Third argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a3** - Fourth argument.

### Return value

World script function return value.Runs the world script function by its id. The target function must receive 4 arguments.
## const Variable & runWorldFunction ( int id , const Variable & a0 , const Variable & a1 , const Variable & a2 , const Variable & a3 , const Variable & a4 )

Runs the world script function by its id. The target function must receive 5 arguments.
### Arguments

- *int* **id** - ID of the world script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a1** - Second argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a2** - Third argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a3** - Fourth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a4** - Fifth argument.

### Return value

World script function return value.
## const Variable & runWorldFunction ( int id , const Variable & a0 , const Variable & a1 , const Variable & a2 , const Variable & a3 , const Variable & a4 , const Variable & a5 )

Runs the world script function by its id. The target function must receive 6 arguments.
### Arguments

- *int* **id** - ID of the world script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a1** - Second argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a2** - Third argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a3** - Fourth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a4** - Fifth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a5** - Sixth argument.

### Return value

World script function return value.
## const Variable & runWorldFunction ( int id , const Variable & a0 , const Variable & a1 , const Variable & a2 , const Variable & a3 , const Variable & a4 , const Variable & a5 , const Variable & a6 )

Runs the world script function by its id. The target function must receive 7 arguments.
### Arguments

- *int* **id** - ID of the world script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a1** - Second argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a2** - Third argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a3** - Fourth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a4** - Fifth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a5** - Sixth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a6** - Seventh argument.

### Return value

World script function return value.
## const Variable & runWorldFunction ( int id , const Variable & a0 , const Variable & a1 , const Variable & a2 , const Variable & a3 , const Variable & a4 , const Variable & a5 , const Variable & a6 , const Variable & a7 )

Runs the world script function by its id. The target function must receive 8 arguments.
### Arguments

- *int* **id** - ID of the world script function.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a0** - First argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a1** - Second argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a2** - Third argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a3** - Fourth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a4** - Fifth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a5** - Sixth argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a6** - Seventh argument.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **a7** - Eighth argument.

### Return value

World script function return value.
## void shutdown ( )

Deletes the pointer to the existing engine instance.
## virtual void iterate ( ) =0

Engine iterate function (update, render, swap). This function must be called every frame.
## void beginOutsideLoopRender ( )

Starts a block of code where you can call *[Render](../../../api/library/rendering/class.render_cpp.md)* class methods from outside the Engine's Loop. The end of this block should be marked with a call to the **[endOutsideLoopRender()](../../...md#endOutsideLoopRender_void)** method.
## void endOutsideLoopRender ( )

Closes a block of code where you can call *[Render](../../../api/library/rendering/class.render_cpp.md)* class methods from outside the Engine's Loop started with a call to the **[beginOutsideLoopRender()](../../...md#beginOutsideLoopRender_void)** method.
## void startFps ( )

Starts the FPS counter if it was stopped. All function calls are placed into a stack, so the number of calls to this function should correspond to the number of calls to the *[stopFps()](#stopFps_void)* function.
## void stopFps ( )

Stops the FPS counter. This function should be called if application window is hidden or some heavy non-rendering tasks are processing. All function calls are placed into a stack, so the number of calls to this function should correspond to the number of calls to the *[startFps()](#startFps_void)* function.
## int getVideoContextFlags ( )

Returns the current video context flags.
### Return value

A set of current video context flags as an integer value.
## static Engine * init ( int argc , char** argv )

Initializes a new engine instance to be used with an external graphics application.
### Arguments

- *int* **argc** - Number of [command line arguments](../../../code/command_line.md).
- *char*** **argv** - Array of [command line arguments](../../../code/command_line.md) values.

### Return value

Pointer to the new engine instance.
## static Engine * init ( int argc , wchar_t** argv )

Initializes a new engine instance to be used with an external graphics application.
### Arguments

- *int* **argc** - Number of [command line arguments](../../../code/command_line.md).
- *wchar_t*** **argv** - Array of [command line arguments](../../../code/command_line.md) values.

### Return value

Pointer to the new engine instance.
## static Engine * init ( const InitParameters& init_parameters , int argc , char** argv )

Initializes a new engine instance to be used with an external graphics application.
### Arguments

- *const InitParameters&* **init_parameters** - Structure of [initializing parameters](#init_parameters).
- *int* **argc** - Number of [command line arguments](../../../code/command_line.md).
- *char*** **argv** - Array of [command line arguments](../../../code/command_line.md) values.

### Return value

Pointer to the new engine instance.
## static Engine * init ( const InitParameters& init_parameters , int argc , wchar_t** argv )

Initializes a new engine instance to be used with an external graphics application.
### Arguments

- *const InitParameters&* **init_parameters** - Structure of [initializing parameters](#init_parameters).
- *int* **argc** - Number of [command line arguments](../../../code/command_line.md).
- *wchar_t*** **argv** - Array of [command line arguments](../../../code/command_line.md) values.

### Return value

Pointer to the new engine instance.
## void quit ( )

The Engine requests to exit the application.
