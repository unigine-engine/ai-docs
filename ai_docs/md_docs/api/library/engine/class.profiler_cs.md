# Unigine::Profiler Class (CS)

> **Notice:** This class is a singleton.


The Profiler class is used to create counters for the engine [Performance Profiler](../../../tools/profiling/profiler/index.md). Allows using counters in your code in the following manner:


```csharp
Profiler.Begin("my_counter");
// ...code to profile...
Profiler.End();

```


> **Notice:** Counters can be nested.


### Usage Example


The following example contains different approaches to creating counters:


- Two counters are added via the *setValue()* function: one shows the number of dynamic mesh vertices, the other shows the update time. This approach should be used when you need to show, for example, a value of a setting, the number of objects, and so on.
- Another two counters are added by using the *begin()/end()* construction. They show the time spent for mesh grid modifying and the time spent for mesh normal vectors, tangent vectors and a mesh bounding box calculation. This approach should be used when you need to show time spent for executing a part of the code.


A dynamic mesh is created in *Init* and then modified on the engine update. All counters are created in *Update()*, too.


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

#region Math Variables
#if UNIGINE_DOUBLE
using Scalar = System.Double;
using Vec3 = Unigine.dvec3;
#else
using Scalar = System.Single;
using Vec3 = Unigine.vec3;
#endif
#endregion

public partial class ProfilerClass : Component
{
	// declare variables
	int size = 128;
	ObjectMeshDynamic mesh;

	private void Init()
	{
		// create a dynamic mesh
		mesh = new ObjectMeshDynamic(ObjectMeshDynamic.USAGE_DYNAMIC_VERTEX | ObjectMeshDynamic.USAGE_IMMUTABLE_INDICES);
		// set the mesh settings
		mesh.WorldTransform = MathLib.Translate(new Vec3(0.0f,0.0f,2.0f));

		// create dynamic mesh vertices
		for(int y = 0; y < size; y++) {
			for (int x = 0; x < size; x++)
			{
				mesh.AddVertex(new vec3(0));
				mesh.AddTexCoord(new vec4((float)x / size,(float)y / size,0.0f,0.0f));
			}
		}

		// create dynamic mesh indices
		for(int y = 0; y < size - 1; y++) {
			int offset = size * y;
			for(int x = 0; x < size - 1; x++) {
				mesh.AddIndex(offset);
				mesh.AddIndex(offset + 1);
				mesh.AddIndex(offset + size);
				mesh.AddIndex(offset + size);
				mesh.AddIndex(offset + 1);
				mesh.AddIndex(offset + size + 1);
				offset++;
			}
		}
	}

	private void Update()
	{
		// initialize the graph color
		float[] color = new float [4] {1.0f,1.0f,1.0f,1.0f};

		// add a counter that shows time spent between the previous frame update and the current one
		Profiler.SetValue("Frame update time", "s", Game.Time, 1.0f, color);

		float time = Game.Time;
		float isize = 30.0f / size;
		// start the counter that shows the time spent for dymanic mesh grid modifying
		Profiler.Begin("Grid", new vec4(1.0f));
		for(int y = 0; y < size; y++)
		{
			for (int i = 0; i < size; i++)
			{
				float Y = y * isize - 15.0f;
				float Z = MathLib.Cos(Y + time);
				for (int x = 0; x < size; x++)
				{
					float X = x * isize - 15.0f;
					mesh.SetVertex(i++, new vec3(X, Y, Z * MathLib.Sin(X + time)));
				}
			}
		}
		// stop the counter
		Profiler.End();
		// start the counter that shows the time spent for
		// dynamic mesh normal vectors, tangent vectors and a mesh bounding box calculation
		Profiler.Begin("Mesh");
		mesh.UpdateBounds();
		mesh.UpdateTangents();
		mesh.FlushVertex();
		// stop the counter
		Profiler.End();

		// add the counter that shows the number of dynamic mesh vertices
		Profiler.SetValue("Num vertices", "", mesh.NumVertex, 20000, null);

	}
}

```


> **Notice:** To create **[nested counters](../../../tools/profiling/microprofile/index_cs.md#nested_cs)**, you need to use the *[beginMicro()](#beginMicro_cstr_int_int)* and *[endMicro()](#endMicro_int_void)* functions.


#### See Also


- Example of [profiling the application logic](../../../tools/profiling/microprofile/index_cs.md#app_logic_cs).


## Profiler Class

### Enums

## COUNTER_VR_FLAG

Flags defining whether a custom counter appears in the VR (HMD) profiler overlay in addition to the regular screen profiler.
| Name | Description |
|---|---|
| **DISABLED** = 0 | The counter is displayed only in the regular screen profiler and never in the VR profiler overlay (default). |
| **PERFORMANCE_ADVANCED** = 1 << 1 | The counter is included in the advanced performance panel of the VR profiler shown inside the HMD (requires the VR profiler enabled in the advanced mode). |

### Properties

## Gui Gui

The [GUI](../../../api/library/gui/class.gui_cs.md) of the engine [Performance Profiler](../../../tools/profiling/profiler/index.md).
## bool Enabled

The value indicating if the profiler is enabled.
## 🔒︎ string MicroprofileUrl

The microprofile web server url.
## 🔒︎ int NumCounters

The total number of the profiler counters.
## 🔒︎ Event EventProfileDumpStart

The Event triggered when profiler dump recording starts. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the ProfileDumpStart event handler
void profiledumpstart_event_handler()
{
	Log.Message("\Handling ProfileDumpStart event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections profiledumpstart_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Profiler.EventProfileDumpStart.Connect(profiledumpstart_event_connections, profiledumpstart_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Profiler.EventProfileDumpStart.Connect(profiledumpstart_event_connections, () => {
		Log.Message("Handling ProfileDumpStart event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
profiledumpstart_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the ProfileDumpStart event with a handler function
Profiler.EventProfileDumpStart.Connect(profiledumpstart_event_handler);

// remove subscription to the ProfileDumpStart event later by the handler function
Profiler.EventProfileDumpStart.Disconnect(profiledumpstart_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection profiledumpstart_event_connection;

// subscribe to the ProfileDumpStart event with a lambda handler function and keeping the connection
profiledumpstart_event_connection = Profiler.EventProfileDumpStart.Connect(() => {
		Log.Message("Handling ProfileDumpStart event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
profiledumpstart_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
profiledumpstart_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
profiledumpstart_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring ProfileDumpStart events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Profiler.EventProfileDumpStart.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Profiler.EventProfileDumpStart.Enabled = true;

```

</details>

## 🔒︎ Event EventProfileDumpEnd

The Event triggered when profiler dump recording ends. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the ProfileDumpEnd event handler
void profiledumpend_event_handler()
{
	Log.Message("\Handling ProfileDumpEnd event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections profiledumpend_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Profiler.EventProfileDumpEnd.Connect(profiledumpend_event_connections, profiledumpend_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Profiler.EventProfileDumpEnd.Connect(profiledumpend_event_connections, () => {
		Log.Message("Handling ProfileDumpEnd event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
profiledumpend_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the ProfileDumpEnd event with a handler function
Profiler.EventProfileDumpEnd.Connect(profiledumpend_event_handler);

// remove subscription to the ProfileDumpEnd event later by the handler function
Profiler.EventProfileDumpEnd.Disconnect(profiledumpend_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection profiledumpend_event_connection;

// subscribe to the ProfileDumpEnd event with a lambda handler function and keeping the connection
profiledumpend_event_connection = Profiler.EventProfileDumpEnd.Connect(() => {
		Log.Message("Handling ProfileDumpEnd event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
profiledumpend_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
profiledumpend_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
profiledumpend_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring ProfileDumpEnd events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Profiler.EventProfileDumpEnd.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Profiler.EventProfileDumpEnd.Enabled = true;

```

</details>

### Members

---

## void SetValue ( string name , string units , int value , int max_value , float[] OUT_arg5 , Profiler.COUNTER_VR_FLAG vr_flags = Enum.Profiler.COUNTER_VR_FLAG.DISABLED , bool show_chart = true )

Sets the value of a custom integer counter displayed in the engine profiler and, depending on the flags, in the VR profiler overlay. The counter is updated only while the profiler (or the VR profiler) is enabled.
```csharp
// initialize the graph color
float[] color = new float [4] {1.0f,1.0f,1.0f,1.0f};

// add a counter without a graph
Profiler.SetValue("Random value 1", "", new System.Random().Next(0,5), 4, null, COUNTER_VR_FLAG.DISABLED);
// add a counter with a colored graph
Profiler.SetValue("Random value 2", "", new System.Random().Next(0,10), 9, color, COUNTER_VR_FLAG.DISABLED);

```


### Arguments

- *string* **name** - Name of the counter, also used as its label.
- *string* **units** - Unit suffix appended after the printed value (for example, ms); can be omitted.
- *int* **value** - Value of the counter for the current frame.
- *int* **max_value** - Reference maximum used to scale the counter's colored bar in the profiler chart.
- *float[]* **OUT_arg5** - Color of the counter's chart bar (RGBA); if omitted, no chart bar is created. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *[Profiler.COUNTER_VR_FLAG](../../../api/library/engine/class.profiler_cs.md#COUNTER_VR_FLAG)* **vr_flags** - Flags controlling the counter's visibility in the VR profiler, a combination of the *COUNTER_VR_FLAG_** values.
- *bool* **show_chart** - Flag defining whether the counter draws its chart curve in the profiler.

## void SetValue ( string name , string units , float value , float max_value , float[] OUT_arg5 , Profiler.COUNTER_VR_FLAG vr_flags = Enum.Profiler.COUNTER_VR_FLAG.DISABLED , bool show_chart = true )

Sets the value of a custom float counter displayed in the engine profiler and, depending on the flags, in the VR profiler overlay. The counter is updated only while the profiler (or the VR profiler) is enabled.
```csharp
// initialize the graph color
float[] color = new float [4] {1.0f,1.0f,1.0f,1.0f};

float rvalue = (float)new System.Random().NextDouble() * 1;
// add a counter without a graph
Profiler.SetValue("Random value 1", "", rvalue, 1.0f, null, COUNTER_VR_FLAG.DISABLED);
// add a counter with a colored graph
Profiler.SetValue("Random value 2", "", 1 + rvalue, 10.0f, color, COUNTER_VR_FLAG.DISABLED);

```


### Arguments

- *string* **name** - Name of the counter, also used as its label.
- *string* **units** - Unit suffix appended after the printed value (for example, ms); can be omitted.
- *float* **value** - Value of the counter for the current frame.
- *float* **max_value** - Reference maximum used to scale the counter's colored bar in the profiler chart.
- *float[]* **OUT_arg5** - Color of the counter's chart bar (RGBA); if omitted, no chart bar is created. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *[Profiler.COUNTER_VR_FLAG](../../../api/library/engine/class.profiler_cs.md#COUNTER_VR_FLAG)* **vr_flags** - Flags controlling the counter's visibility in the VR profiler, a combination of the *COUNTER_VR_FLAG_** values.
- *bool* **show_chart** - Flag defining whether the counter draws its chart curve in the profiler.

## float GetValue ( string name )

Returns a value of the specified counter.
### Arguments

- *string* **name** - The name of the counter.

### Return value

Value of the counter in milliseconds.
## void Begin ( string name , vec4 color )


Starts a counter with a given name and shows a colored graph (if the `show_profiler 1` console variable is set). The counter shows user how many millisecods have been spent for the operation that is performed between the *begin()* and the *[end()](#end_float)* functions.


```csharp
int size = 128;

ObjectMeshDynamic mesh;

	float time = Game.Time;
	float isize = 30.0f / size;
	// start the counter that shows the time spent for dymanic mesh grid modifying
	Profiler.Begin("Grid", new vec4(1.0f));
	for(int y = 0; y < size; y++)
	{
		for (int i = 0; i < size; i++)
		{
			float Y = y * isize - 15.0f;
			float Z = MathLib.Cos(Y + time);
			for (int x = 0; x < size; x++)
			{
				float X = x * isize - 15.0f;
				mesh.SetVertex(i++, new vec3(X, Y, Z * MathLib.Sin(X + time)));
			}
		}
	}
	// stop the counter
	Profiler.End();

```


### Arguments

- *string* **name** - Name of the counter.
- *vec4* **color** - Color of the graph.

## void Begin ( string name )


Starts a counter with a given name. The counter shows user how many millisecods have been spent for the operation that is performed between the *begin()* and the *[end()](#end_float)* functions.


```csharp
ObjectMeshDynamic mesh;

	// start the counter that shows the time spent for
	// dynamic mesh normal vectors, tangent vectors and a mesh bounding box calculation
	Profiler.Begin("Mesh");
	mesh.UpdateBounds();
	mesh.UpdateTangents();
	mesh.FlushVertex();
	// stop the counter
	Profiler.End();

```


### Arguments

- *string* **name** - Name of the counter.

## float End ( )

Stops the last [activated](#begin_cstr_vec4_void) counter and returns its value.
### Return value

Value of the counter in milliseconds.
## int BeginMicro ( string name , bool gpu = 0 )


Starts a counter with a given name in the [Microprofile](../../../tools/profiling/microprofile/index_cs.md) only, without overloading the [Performance Profiler](../../../tools/profiling/profiler/index.md) layout. The counter shows user how many millisecods have been spent for the operation that is performed between the *beginMicro()* and the *[endMicro()](#endMicro_int_void)* functions.


> **Notice:** Each counter has an ID. Thus, several nested *beginMicro() / endMicro()* blocks can be created, which can't be done in the [Performance Profiler](../../../tools/profiling/profiler/index.md).


```csharp
ObjectMeshDynamic mesh;

	// start the counter that shows the time spent for dynamic mesh normal vectors,
	// tangent vectors and a mesh bounding box calculation, with a nested counter for tangent vectors only
	int c_id = Profiler.BeginMicro("mesh");
	mesh.UpdateBounds();
	int c_nested_id = Profiler.BeginMicro("mesh_tangents");
	mesh.UpdateTangents();
	Profiler.EndMicro(c_nested_id);
	mesh.FlushVertex();
	// stop the counter
	Profiler.EndMicro(c_id);

```


### Arguments

- *string* **name** - Name of the counter.
- *bool* **gpu** - true for the GPU counter; false � for the CPU counter. The default value is false.

### Return value

ID of the added counter.
## void EndMicro ( int id )

Stops a previously [activated](#beginMicro_cstr_int_int) Microprofile counter with the specified ID.
### Arguments

- *int* **id** - Microprofile counter ID.

## void InitThread ( string name , int priority = 0 )


Initiates the custom thread for Microprofile calculations to avoid spikes, which otherwise are registered by Microprofile on registering a new thread. This method shall be called at the beginning of the thread and before [*BeginMicro()*](#beginMicro_cstr_int_int) and followed by [*ShutdownThread()*](#shutdownThread_void) when the thread is not required anymore.


```csharp
void thread_function()
{
	// initiate thread for profiling
	Profiler.InitThread("thread1");

	while (true) //thread loop
	{
		// start the counter
		int c_id = Profiler.BeginMicro("mesh");

		//...code to be profiled.../

		// stop the counter
		Profiler.EndMicro(c_id);
	}

	// shutdown thread for profiling
	Profiler.ShutdownThread();
}

```


### Arguments

- *string* **name** - Name of the thread displayed in Microprofile.
- *int* **priority** - Order (ordinal number) of the thread displayed in Microprofile.

## void ShutdownThread ( )

Stops a previously [activated](#initThread_cstr_int_void) Microprofile thread counter. This method shall be called after [*EndMicro()*](#endMicro_int_void) and before the thread ends.
## int FindCounter ( string name )

Returns the counter number by its name.
### Arguments

- *string* **name** - Name of the counter.

### Return value

Counter number in range from 0 to the [total number of counters](#NumCounters).
## string GetCounterName ( int num )

Returns the counter name by its number.
### Arguments

- *int* **num** - Counter number in range from 0 to the [total number of counters](#NumCounters).

### Return value

Name of the counter.
## string GetCounterText ( int num )

Returns the text of the specified counter.
### Arguments

- *int* **num** - Counter number in range from 0 to the [total number of counters](#NumCounters).

### Return value

Text of the counter.
## vec4 GetCounterColor ( int num )

Returns the color of the specified counter.
### Arguments

- *int* **num** - Counter number in range from 0 to the [total number of counters](#NumCounters).

### Return value

Color of the counter.
## float GetCounterValue ( int num )

Returns the value of the specified counter.
### Arguments

- *int* **num** - Counter number in range from 0 to the [total number of counters](#NumCounters).

### Return value

Value of the counter.
## long GetCounterFrame ( int num )

Returns the frame of the specified counter.
### Arguments

- *int* **num** - Counter number in range from 0 to the [total number of counters](#NumCounters).

### Return value

Frame of the counter.
## bool IsCounterActive ( int num )

Returns the value indicating if the specified counter is active.
### Arguments

- *int* **num** - Counter number in range from 0 to the [total number of counters](#NumCounters).

### Return value

true if the counter is active; otherwise false.
## bool IsCounterSeparator ( int num )

Returns the value indicating if a separator is placed after the specified counter.
### Arguments

- *int* **num** - Counter number in range from 0 to the [total number of counters](#NumCounters).

### Return value

true if the separator is placed; otherwise false.
## static void StartProfilerDump ( string path = nullptr )

***Console*:**`profiling_start`Starts collecting a profiler dump to the specified file path. The profiler dump contains per-frame runtime performance data that can be later analyzed using the *[ProfilerDump](../../../api/library/engine/class.profilerdump_cs.md) class*. Recording continues until either the *[*StopProfilerDump()*](../../../api/library/engine/class.profiler_cs.md#stopProfilerDump_void)* method or the [profiling_stop](../../../code/console/index.md#profiling_stop) command is called.
### Arguments

- *string* **path** - The file path where the profiler dump will be written. You can specify an absolute path or a path relative to *[profiling_dump_dir](../../../code/console/index.md#profiling_dump_dir)*. If the path isn't specified, the profiler dump will be saved to: `profiling_dump_dir/profiling_dump_{currentdatetime}`

## static void StartProfilerDump ( int frames , string path = nullptr )

***Console*:**`profiling_start_frames`Starts collecting a profiler dump for a specified number of frames and writes it to the given file path. The profiler dump contains per-frame runtime performance data that can be later analyzed using the *[ProfilerDump](../../../api/library/engine/class.profilerdump_cs.md) class*. Recording automatically stops after the specified number of frames, or earlier if the *[*StopProfilerDump()*](../../../api/library/engine/class.profiler_cs.md#stopProfilerDump_void)* method or the [profiling_stop](../../../code/console/index.md#profiling_stop) command is called.
### Arguments

- *int* **frames** - The number of frames to record the data. The profiler will automatically stop recording after this period.
- *string* **path** - The file path where the profiler dump will be written. You can specify an absolute path or a path relative to *[profiling_dump_dir](../../../code/console/index.md#profiling_dump_dir)*. If the path isn't specified, the profiler dump will be saved to: `profiling_dump_dir/profiling_dump_{currentdatetime}`

## static void StartProfilerDump ( float seconds , string path = nullptr )

***Console*:**`profiling_start_seconds`Starts collecting a profiler dump for a specified duration (in seconds) and writes it to the given file path. The profiler dump contains per-frame runtime performance data that can be later analyzed using the *[ProfilerDump](../../../api/library/engine/class.profilerdump_cs.md) class*. Recording automatically stops after the specified number of seconds, or earlier if the *[*StopProfilerDump()*](../../../api/library/engine/class.profiler_cs.md#stopProfilerDump_void)* method or the [profiling_stop](../../../code/console/index.md#profiling_stop) command is called.
### Arguments

- *float* **seconds** - The duration, in seconds, for which the profiler should collect data. The profiler will automatically stop recording after this period.
- *string* **path** - The file path where the profiler dump will be written. You can specify an absolute path or a path relative to *[profiling_dump_dir](../../../code/console/index.md#profiling_dump_dir)*. If the path isn't specified, the profiler dump will be saved to: `profiling_dump_dir/profiling_dump_{currentdatetime}`

## static bool IsProfilerDumpEnabled ( )

Checks whether the profiler dump recording is currently active.
### Return value

true if a profiler dump is currently being recorded; otherwise false.
## static void StopProfilerDump ( )

***Console*:**`profiling_stop`Stops the currently active profiler dump recording. If a profiler dump is in progress, calling this method finalizes the dump and closes the output file.
