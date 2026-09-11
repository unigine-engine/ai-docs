# Unigine::Profiler Class (CPP)

**Header:** #include <UnigineProfiler.h>

> **Notice:** This class is a singleton.


The Profiler class is used to create counters for the engine [Performance Profiler](../../../tools/profiling/profiler/index.md). Allows using counters in your code in the following manner:


```cpp
Profiler::begin("my_counter");
// ...code to profile...
Profiler::end();

```


> **Notice:** Counters can be nested.


### Usage Example


The following example contains different approaches to creating counters:


- Two counters are added via the *setValue()* function: one shows the number of dynamic mesh vertices, the other shows the update time. This approach should be used when you need to show, for example, a value of a setting, the number of objects, and so on.
- Another two counters are added by using the *begin()/end()* construction. They show the time spent for mesh grid modifying and the time spent for mesh normal vectors, tangent vectors and a mesh bounding box calculation. This approach should be used when you need to show time spent for executing a part of the code.


`AppWorldLogic.h` contains declaration of the required variables.


```cpp
#include <UnigineLogic.h>
#include <UnigineStreams.h>
#include <UnigineObjects.h>

class AppWorldLogic: public Unigine::WorldLogic
{

public:
	AppWorldLogic();
	virtual ~AppWorldLogic();

	int init() override;

	int update() override;
	int postUpdate() override;
	int updatePhysics() override;

	int shutdown() override;

	int save(const Unigine::StreamPtr &stream) override;
	int restore(const Unigine::StreamPtr &stream) override;

private:
	// declare variables
	int size = 128;
	Unigine::ObjectMeshDynamicPtr mesh;
};

```


In `AppWorldLogic.cpp`, a dynamic mesh is created and then modified on the engine update. All counters are created in *update()* too.


```cpp
#include "AppWorldLogic.h"
#include <UnigineProfiler.h>
#include <UnigineEditor.h>
#include <UnigineGame.h>

using namespace Unigine;

int AppWorldLogic::init()
{
	// create a dynamic mesh
	mesh = ObjectMeshDynamic::create(ObjectMeshDynamic::USAGE_DYNAMIC_VERTEX | ObjectMeshDynamic::USAGE_IMMUTABLE_INDICES);
	// set the mesh settings
	mesh->setWorldTransform(Math::translate(Math::Vec3(0.0f, 0.0f, 2.0f)));

	// create dynamic mesh vertices
	for (int y = 0; y < size; y++) {
		for (int x = 0; x < size; x++)
		{
			mesh->addVertex(Math::vec3(0.0f));
			mesh->addTexCoord(Math::vec4((float)x / size, (float)y / size, 0.0f, 0.0f));
		}
	}

	// create dynamic mesh indices
	for (int y = 0; y < size - 1; y++) {
		int offset = size * y;
		for (int x = 0; x < size - 1; x++) {
			mesh->addIndex(offset);
			mesh->addIndex(offset + 1);
			mesh->addIndex(offset + size);
			mesh->addIndex(offset + size);
			mesh->addIndex(offset + 1);
			mesh->addIndex(offset + size + 1);
			offset++;
		}
	}

	return 1;
}

int AppWorldLogic::update()
{
	// add a counter that shows engine update phase duration
	Profiler::setValue("Update time", "ms", Engine::get()->getUpdateTime(), 50.0f, Math::vec4(0.0f, 0.0f, 0.0f, 1.0f));
	float time = Game::getTime();
	float isize = 30.0f / size;
	// start the counter that shows the time spent for dymanic mesh grid modifying
	Profiler::begin("Grid", Math::vec4(1.0f));
	for (int y = 0; y < size; y++)
	{
		for (int i = 0; i < size; i++)
		{
			float Y = y * isize - 15.0f;
			float Z = Math::cos(Y + time);
			for (int x = 0; x < size; x++)
			{
				float X = x * isize - 15.0f;
				mesh->setVertex(i++, Math::vec3(X, Y, Z * Math::sin(X + time)));
			}
		}
	}
	// stop the counter
	Profiler::end();
	// start the counter that shows the time spent for
	// dynamic mesh normal vectors, tangent vectors and a mesh bounding box calculation
	Profiler::begin("mesh");
	mesh->updateBounds();
	mesh->updateTangents();
	mesh->flushVertex();
	// stop the counter
	Profiler::end();

	// add the counter that shows the number of dynamic mesh vertices
	Profiler::setValue("Num vertices", "", mesh->getNumVertex(), 32768, NULL);

	return 1;
}


```


> **Notice:** To create **[nested counters](../../../tools/profiling/microprofile/index_cpp.md#nested_cpp)**, you need to use the *[beginMicro()](#beginMicro_cstr_int_int)* and *[endMicro()](#endMicro_int_void)* functions.


#### See Also


- Example of [profiling the application logic](../../../tools/profiling/microprofile/index_cpp.md#app_logic_cpp).


## Profiler Class

### Enums

## COUNTER_VR_FLAG

Flags defining whether a custom counter appears in the VR (HMD) profiler overlay in addition to the regular screen profiler.
| Name | Description |
|---|---|
| **COUNTER_VR_FLAG_DISABLED** = 0 | The counter is displayed only in the regular screen profiler and never in the VR profiler overlay (default). |
| **COUNTER_VR_FLAG_PERFORMANCE_ADVANCED** = 1 << 1 | The counter is included in the advanced performance panel of the VR profiler shown inside the HMD (requires the VR profiler enabled in the advanced mode). |

### Members

## void setGui ( const Ptr < Gui >& gui )

Sets a new [GUI](../../../api/library/gui/class.gui_cpp.md) of the engine [Performance Profiler](../../../tools/profiling/profiler/index.md).
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../api/library/gui/class.gui_cpp.md)>&* **gui** - The pointer to the GUI.

## Ptr < Gui > getGui () const

Returns the current [GUI](../../../api/library/gui/class.gui_cpp.md) of the engine [Performance Profiler](../../../tools/profiling/profiler/index.md).
### Return value

Current pointer to the GUI.
## void setEnabled ( bool enabled )

Sets a new value indicating if the profiler is enabled.
### Arguments

- *bool* **enabled** - Set **true** to enable the profiler; **false** - to disable it.

## bool isEnabled () const

Returns the current value indicating if the profiler is enabled.
### Return value

**true** if the profiler is enabled ; otherwise **false**.
## const char * getMicroprofileUrl () const

Returns the current microprofile web server url.
### Return value

Current microprofile web server url represented in the following way:
http://localhost:p/, where p is the local port.


## int getNumCounters () const

Returns the current total number of the profiler counters.
### Return value

Current total number of the profiler counters
## static Event<> getEventProfileDumpStart () const

Event triggered when profiler dump recording starts. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the ProfileDumpStart event handler
void profiledumpstart_event_handler()
{
	Log::message("\Handling ProfileDumpStart event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections profiledumpstart_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Profiler::getEventProfileDumpStart().connect(profiledumpstart_event_connections, profiledumpstart_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Profiler::getEventProfileDumpStart().connect(profiledumpstart_event_connections, []() {
		Log::message("\Handling ProfileDumpStart event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
profiledumpstart_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection profiledumpstart_event_connection;

// subscribe to the ProfileDumpStart event with a handler function keeping the connection
Profiler::getEventProfileDumpStart().connect(profiledumpstart_event_connection, profiledumpstart_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
profiledumpstart_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
profiledumpstart_event_connection.setEnabled(true);

// ...

// remove subscription to the ProfileDumpStart event via the connection
profiledumpstart_event_connection.disconnect();

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

	// A ProfileDumpStart event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling ProfileDumpStart event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Profiler::getEventProfileDumpStart().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId profiledumpstart_handler_id;

// subscribe to the ProfileDumpStart event with a lambda handler function and keeping connection ID
profiledumpstart_handler_id = Profiler::getEventProfileDumpStart().connect(e_connections, []() {
		Log::message("\Handling ProfileDumpStart event (lambda).\n");
	}
);

// remove the subscription later using the ID
Profiler::getEventProfileDumpStart().disconnect(profiledumpstart_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all ProfileDumpStart events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Profiler::getEventProfileDumpStart().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Profiler::getEventProfileDumpStart().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<> getEventProfileDumpEnd () const

Event triggered when profiler dump recording ends. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the ProfileDumpEnd event handler
void profiledumpend_event_handler()
{
	Log::message("\Handling ProfileDumpEnd event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections profiledumpend_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Profiler::getEventProfileDumpEnd().connect(profiledumpend_event_connections, profiledumpend_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Profiler::getEventProfileDumpEnd().connect(profiledumpend_event_connections, []() {
		Log::message("\Handling ProfileDumpEnd event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
profiledumpend_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection profiledumpend_event_connection;

// subscribe to the ProfileDumpEnd event with a handler function keeping the connection
Profiler::getEventProfileDumpEnd().connect(profiledumpend_event_connection, profiledumpend_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
profiledumpend_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
profiledumpend_event_connection.setEnabled(true);

// ...

// remove subscription to the ProfileDumpEnd event via the connection
profiledumpend_event_connection.disconnect();

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

	// A ProfileDumpEnd event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling ProfileDumpEnd event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Profiler::getEventProfileDumpEnd().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId profiledumpend_handler_id;

// subscribe to the ProfileDumpEnd event with a lambda handler function and keeping connection ID
profiledumpend_handler_id = Profiler::getEventProfileDumpEnd().connect(e_connections, []() {
		Log::message("\Handling ProfileDumpEnd event (lambda).\n");
	}
);

// remove the subscription later using the ID
Profiler::getEventProfileDumpEnd().disconnect(profiledumpend_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all ProfileDumpEnd events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Profiler::getEventProfileDumpEnd().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Profiler::getEventProfileDumpEnd().setEnabled(true);

```

</details>

### Return value

Event instance.
---

## void setValue ( const char * name , const char * units , int value , int max_value , float * OUT_arg5 , Profiler::COUNTER_VR_FLAG vr_flags = Enum.Profiler.COUNTER_VR_FLAG.DISABLED , bool show_chart = true )

Sets the value of a custom integer counter displayed in the engine profiler and, depending on the flags, in the VR profiler overlay. The counter is updated only while the profiler (or the VR profiler) is enabled.
```cpp
// add a counter without a graph
Profiler::setValue("Random value 1", "", rand() % 5, 4, NULL, COUNTER_VR_FLAG_DISABLED);
// add a counter with a colored graph
Profiler::setValue("Random value 2", "", rand() % 10, 9, Math::vec4(1.0f), COUNTER_VR_FLAG_DISABLED);

```


### Arguments

- *const char ** **name** - Name of the counter, also used as its label.
- *const char ** **units** - Unit suffix appended after the printed value (for example, ms); can be omitted.
- *int* **value** - Value of the counter for the current frame.
- *int* **max_value** - Reference maximum used to scale the counter's colored bar in the profiler chart.
- *float ** **OUT_arg5** - Color of the counter's chart bar (RGBA); if omitted, no chart bar is created. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *[Profiler::COUNTER_VR_FLAG](../../../api/library/engine/class.profiler_cpp.md#COUNTER_VR_FLAG)* **vr_flags** - Flags controlling the counter's visibility in the VR profiler, a combination of the *COUNTER_VR_FLAG_** values.
- *bool* **show_chart** - Flag defining whether the counter draws its chart curve in the profiler.

## void setValue ( const char * name , const char * units , float value , float max_value , float * OUT_arg5 , Profiler::COUNTER_VR_FLAG vr_flags = Enum.Profiler.COUNTER_VR_FLAG.DISABLED , bool show_chart = true )

Sets the value of a custom float counter displayed in the engine profiler and, depending on the flags, in the VR profiler overlay. The counter is updated only while the profiler (or the VR profiler) is enabled.
```cpp
float rvalue1 = static_cast<float>(rand()) / static_cast<float>(RAND_MAX);
float rvalue2 = static_cast<float>(rand()) / static_cast<float>(RAND_MAX);
// add a counter without a graph
Profiler::setValue("Random value 1", "", rvalue1, 1.0f, NULL, COUNTER_VR_FLAG_DISABLED);
// add a counter with a colored graph
Profiler::setValue("Random value 2", "", 1 + rvalue2, 10.0f, Math::vec4(1.0f), COUNTER_VR_FLAG_DISABLED);

```


### Arguments

- *const char ** **name** - Name of the counter, also used as its label.
- *const char ** **units** - Unit suffix appended after the printed value (for example, ms); can be omitted.
- *float* **value** - Value of the counter for the current frame.
- *float* **max_value** - Reference maximum used to scale the counter's colored bar in the profiler chart.
- *float ** **OUT_arg5** - Color of the counter's chart bar (RGBA); if omitted, no chart bar is created. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *[Profiler::COUNTER_VR_FLAG](../../../api/library/engine/class.profiler_cpp.md#COUNTER_VR_FLAG)* **vr_flags** - Flags controlling the counter's visibility in the VR profiler, a combination of the *COUNTER_VR_FLAG_** values.
- *bool* **show_chart** - Flag defining whether the counter draws its chart curve in the profiler.

## float getValue ( const char * name ) const

Returns a value of the specified counter.
### Arguments

- *const char ** **name** - The name of the counter.

### Return value

Value of the counter in milliseconds.
## void begin ( const char * name , const Math:: vec4 & color ) const


Starts a counter with a given name and shows a colored graph (if the `show_profiler 1` console variable is set). The counter shows user how many millisecods have been spent for the operation that is performed between the *begin()* and the *[end()](#end_float)* functions.


```cpp
int size = 128;

Unigine::ObjectMeshDynamicPtr mesh;

	float time = Game::getTime();
	float isize = 30.0f / size;
	// start the counter that shows the time spent for dymanic mesh grid modifying
	Profiler::begin("Grid", Math::vec4(1.0f));
	for (int y = 0; y < size; y++)
	{
		for (int i = 0; i < size; i++)
		{
			float Y = y * isize - 15.0f;
			float Z = Math::cos(Y + time);
			for (int x = 0; x < size; x++)
			{
				float X = x * isize - 15.0f;
				mesh->setVertex(i++, Math::vec3(X, Y, Z * Math::sin(X + time)));
			}
		}
	}
	// stop the counter
	Profiler::end();

```


### Arguments

- *const char ** **name** - Name of the counter.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color of the graph.

## void begin ( const char * name ) const


Starts a counter with a given name. The counter shows user how many millisecods have been spent for the operation that is performed between the *begin()* and the *[end()](#end_float)* functions.


```cpp
Unigine::ObjectMeshDynamicPtr mesh;

	// start the counter that shows the time spent for
	// dynamic mesh normal vectors, tangent vectors and a mesh bounding box calculation
	Profiler::begin("mesh");
	mesh->updateBounds();
	mesh->updateTangents();
	mesh->flushVertex();
	// stop the counter
	Profiler::end();

```


### Arguments

- *const char ** **name** - Name of the counter.

## float end ( ) const

Stops the last [activated](#begin_cstr_vec4_void) counter and returns its value.
### Return value

Value of the counter in milliseconds.
## int beginMicro ( const char * name , bool gpu = 0 ) const


Starts a counter with a given name in the [Microprofile](../../../tools/profiling/microprofile/index_cpp.md) only, without overloading the [Performance Profiler](../../../tools/profiling/profiler/index.md) layout. The counter shows user how many millisecods have been spent for the operation that is performed between the *beginMicro()* and the *[endMicro()](#endMicro_int_void)* functions.


> **Notice:** Each counter has an ID. Thus, several nested *beginMicro() / endMicro()* blocks can be created, which can't be done in the [Performance Profiler](../../../tools/profiling/profiler/index.md).


```cpp
Unigine::ObjectMeshDynamicPtr mesh;

	// start the counter that shows the time spent for dynamic mesh normal vectors,
	// tangent vectors and a mesh bounding box calculation, with a nested counter for tangent vectors only
	int c_id = Profiler::beginMicro("mesh");
	mesh->updateBounds();
	int c_nested_id = Profiler::beginMicro("mesh_tangents");
	mesh->updateTangents();
	Profiler::endMicro(c_nested_id);
	mesh->flushVertex();
	// stop the counter
	Profiler::endMicro(c_id);

```


### Arguments

- *const char ** **name** - Name of the counter.
- *bool* **gpu** - true for the GPU counter; false � for the CPU counter. The default value is false.

### Return value

ID of the added counter.
## void endMicro ( int id ) const

Stops a previously [activated](#beginMicro_cstr_int_int) Microprofile counter with the specified ID.
### Arguments

- *int* **id** - Microprofile counter ID.

## void initThread ( const char * name , int priority = 0 )


Initiates the custom thread for Microprofile calculations to avoid spikes, which otherwise are registered by Microprofile on registering a new thread. This method shall be called at the beginning of the thread and before [*beginMicro()*](#beginMicro_cstr_int_int) and followed by [*shutdownThread()*](#shutdownThread_void) when the thread is not required anymore.


```cpp
void thread_function()
{
	// initiate thread for profiling
	Profiler::initThread("thread1");

	while (true) //thread loop
	{
		// start the counter
		int c_id = Profiler::beginMicro("mesh");

		//...code to be profiled.../

		// stop the counter
		Profiler::endMicro(c_id);
	}

	// shutdown thread for profiling
	Profiler::shutdownThread();
}

```


### Arguments

- *const char ** **name** - Name of the thread displayed in Microprofile.
- *int* **priority** - Order (ordinal number) of the thread displayed in Microprofile.

## void shutdownThread ( )

Stops a previously [activated](#initThread_cstr_int_void) Microprofile thread counter. This method shall be called after [*endMicro()*](#endMicro_int_void) and before the thread ends.
## int findCounter ( const char * name ) const

Returns the counter number by its name.
### Arguments

- *const char ** **name** - Name of the counter.

### Return value

Counter number in range from 0 to the [total number of counters](#NumCounters).
## const char * getCounterName ( int num ) const

Returns the counter name by its number.
### Arguments

- *int* **num** - Counter number in range from 0 to the [total number of counters](#NumCounters).

### Return value

Name of the counter.
## const char * getCounterText ( int num ) const

Returns the text of the specified counter.
### Arguments

- *int* **num** - Counter number in range from 0 to the [total number of counters](#NumCounters).

### Return value

Text of the counter.
## Math:: vec4 getCounterColor ( int num ) const

Returns the color of the specified counter.
### Arguments

- *int* **num** - Counter number in range from 0 to the [total number of counters](#NumCounters).

### Return value

Color of the counter.
## float getCounterValue ( int num ) const

Returns the value of the specified counter.
### Arguments

- *int* **num** - Counter number in range from 0 to the [total number of counters](#NumCounters).

### Return value

Value of the counter.
## long long getCounterFrame ( int num ) const

Returns the frame of the specified counter.
### Arguments

- *int* **num** - Counter number in range from 0 to the [total number of counters](#NumCounters).

### Return value

Frame of the counter.
## bool isCounterActive ( int num ) const

Returns the value indicating if the specified counter is active.
### Arguments

- *int* **num** - Counter number in range from 0 to the [total number of counters](#NumCounters).

### Return value

true if the counter is active; otherwise false.
## bool isCounterSeparator ( int num ) const

Returns the value indicating if a separator is placed after the specified counter.
### Arguments

- *int* **num** - Counter number in range from 0 to the [total number of counters](#NumCounters).

### Return value

true if the separator is placed; otherwise false.
## static void startProfilerDump ( const char * path = nullptr )

***Console*:**`profiling_start`Starts collecting a profiler dump to the specified file path. The profiler dump contains per-frame runtime performance data that can be later analyzed using the *[ProfilerDump](../../../api/library/engine/class.profilerdump_cpp.md) class*. Recording continues until either the *[*stopProfilerDump()*](../../../api/library/engine/class.profiler_cpp.md#stopProfilerDump_void)* method or the [profiling_stop](../../../code/console/index.md#profiling_stop) command is called.
### Arguments

- *const char ** **path** - The file path where the profiler dump will be written. You can specify an absolute path or a path relative to *[profiling_dump_dir](../../../code/console/index.md#profiling_dump_dir)*. If the path isn't specified, the profiler dump will be saved to: `profiling_dump_dir/profiling_dump_{currentdatetime}`

## static void startProfilerDump ( int frames , const char * path = nullptr )

***Console*:**`profiling_start_frames`Starts collecting a profiler dump for a specified number of frames and writes it to the given file path. The profiler dump contains per-frame runtime performance data that can be later analyzed using the *[ProfilerDump](../../../api/library/engine/class.profilerdump_cpp.md) class*. Recording automatically stops after the specified number of frames, or earlier if the *[*stopProfilerDump()*](../../../api/library/engine/class.profiler_cpp.md#stopProfilerDump_void)* method or the [profiling_stop](../../../code/console/index.md#profiling_stop) command is called.
### Arguments

- *int* **frames** - The number of frames to record the data. The profiler will automatically stop recording after this period.
- *const char ** **path** - The file path where the profiler dump will be written. You can specify an absolute path or a path relative to *[profiling_dump_dir](../../../code/console/index.md#profiling_dump_dir)*. If the path isn't specified, the profiler dump will be saved to: `profiling_dump_dir/profiling_dump_{currentdatetime}`

## static void startProfilerDump ( float seconds , const char * path = nullptr )

***Console*:**`profiling_start_seconds`Starts collecting a profiler dump for a specified duration (in seconds) and writes it to the given file path. The profiler dump contains per-frame runtime performance data that can be later analyzed using the *[ProfilerDump](../../../api/library/engine/class.profilerdump_cpp.md) class*. Recording automatically stops after the specified number of seconds, or earlier if the *[*stopProfilerDump()*](../../../api/library/engine/class.profiler_cpp.md#stopProfilerDump_void)* method or the [profiling_stop](../../../code/console/index.md#profiling_stop) command is called.
### Arguments

- *float* **seconds** - The duration, in seconds, for which the profiler should collect data. The profiler will automatically stop recording after this period.
- *const char ** **path** - The file path where the profiler dump will be written. You can specify an absolute path or a path relative to *[profiling_dump_dir](../../../code/console/index.md#profiling_dump_dir)*. If the path isn't specified, the profiler dump will be saved to: `profiling_dump_dir/profiling_dump_{currentdatetime}`

## static bool isProfilerDumpEnabled ( )

Checks whether the profiler dump recording is currently active.
### Return value

true if a profiler dump is currently being recorded; otherwise false.
## static void stopProfilerDump ( )

***Console*:**`profiling_stop`Stops the currently active profiler dump recording. If a profiler dump is in progress, calling this method finalizes the dump and closes the output file.
