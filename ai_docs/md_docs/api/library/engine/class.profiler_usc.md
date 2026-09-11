# Unigine::Profiler Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


The Profiler class is used to create counters for the engine [Performance Profiler](../../../tools/profiling/profiler/index.md). Allows using counters in your code in the following manner:


```cpp
engine.profiler.begin("my_counter");
// ...code to profile...
engine.profiler.end();

```


> **Notice:** Counters can be nested.


### Usage Example


The following example contains different approaches to creating counters:


- Two counters are added via the *setValue()* function: one shows the number of dynamic mesh vertices, the other shows the update time. This approach should be used when you need to show, for example, a value of a setting, the number of objects, and so on.
- Another two counters are added by using the *begin()/end()* construction. They show the time spent for mesh grid modifying and the time spent for mesh normal vectors, tangent vectors and a mesh bounding box calculation. This approach should be used when you need to show time spent for executing a part of the code.


In the code below, a dynamic mesh is created and then modified on the engine update. All counters are created in *update()* too.


```cpp
#include <core/unigine.h>

// declare variables
int size = 128;
ObjectMeshDynamic mesh;

int init() {

	// create a dynamic mesh and remove script ownership
	mesh = new ObjectMeshDynamic(OBJECT_DYNAMIC_VERTEX | OBJECT_IMMUTABLE_INDICES);

	// set the mesh settings
	mesh.setWorldTransform(translate(Vec3(0.0f,0.0f,2.0f)));

	// create dynamic mesh vertices
	for(int y = 0; y < size; y++) {
		for(int x = 0; x < size; x++) {
			mesh.addVertex(vec3_zero);
			mesh.addTexCoord(vec4(float(x) / size,float(y) / size,0.0f,0.0f));
		}
	}

	// create dynamic mesh indices
	for(int y = 0; y < size - 1; y++) {
		int offset = size * y;
		for(int x = 0; x < size - 1; x++) {
			mesh.addIndex(offset);
			mesh.addIndex(offset + 1);
			mesh.addIndex(offset + size);
			mesh.addIndex(offset + size);
			mesh.addIndex(offset + 1);
			mesh.addIndex(offset + size + 1);
			offset++;
		}
	}

	return 1;
}

int update() {

	// add a counter that shows the number of dynamic mesh vertices
	engine.profiler.setValue("Num Vertices", "", mesh.getNumVertex());
	// add a counter that shows engine update phase duration
	engine.profiler.setValue("Update time", "ms", engine.getUpdateTime(),1.0f,vec4(1.0f));

	float time = engine.game.getTime();
	float isize = 30.0f / size;
	// start the counter that shows the time spent for dymanic mesh grid modifying
	engine.profiler.begin("grid",vec4(1.0f));
	forloop(int y = 0, i = 0; size) {
		float Y = y * isize - 15.0f;
		float Z = cos(Y + time);
		forloop(int x = 0; size) {
			float X = x * isize - 15.0f;
			mesh.setVertex(i++,vec3(X,Y,Z * sin(X + time)));
		}
	}
	// stop the counter
	engine.profiler.end();

	// start the counter that shows the time spent for
	// dynamic mesh normal vectors, tangent vectors and a mesh bounding box calculation
	engine.profiler.begin("mesh");
	mesh.updateBounds();
	mesh.updateTangents();
	mesh.flushVertex();
	// stop the counter
	engine.profiler.end();

	return 1;
}

```


#### See Also


## Profiler Class

### Members

## void setGui ( Gui gui )

Sets a new [GUI](../../../api/library/gui/class.gui_usc.md) of the engine [Performance Profiler](../../../tools/profiling/profiler/index.md).
### Arguments

- *[Gui](../../../api/library/gui/class.gui_usc.md)* **gui** - The GUI.

## Gui getGui () const

Returns the current [GUI](../../../api/library/gui/class.gui_usc.md) of the engine [Performance Profiler](../../../tools/profiling/profiler/index.md).
### Return value

Current GUI.
## void setEnabled ( int enabled )

Sets a new value indicating if the profiler is enabled.
### Arguments

- *int* **enabled** - The the profiler

## int isEnabled () const

Returns the current value indicating if the profiler is enabled.
### Return value

Current the profiler
## const char * getMicroprofileUrl () const

Returns the current microprofile web server url.
### Return value

Current microprofile web server url represented in the following way:
http://localhost:p/, where p is the local port.


## int getNumCounters () const

Returns the current total number of the profiler counters.
### Return value

Current total number of the profiler counters
## static getEventProfileDumpStart () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventProfileDumpEnd () const

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

## float engine.profiler. getValue ( string name )

Returns a value of the specified counter.
### Arguments

- *string* **name** - The name of the counter.

### Return value

Value of the counter in milliseconds.
## void engine.profiler. begin ( )


Starts a counter with a given name and shows a colored graph (if the `show_profiler 1` console variable is set). The counter shows user how many millisecods have been spent for the operation that is performed between the *engine.profiler.begin()* and the *[engine.profiler.end()](#end_float)* functions.


```cpp
int size = 128;
ObjectMeshDynamic mesh;
// ...
float time = engine.game.getTime();
// start the counter that shows the time spent for dymanic mesh grid calculation
engine.profiler.begin("grid",vec4(1.0f));
// modify a mesh grid
forloop(int y = 0, i = 0; size) {
	float Y = y * isize - 15.0f;
	float Z = cos(Y + time);
	forloop(int x = 0; size) {
		float X = x * isize - 15.0f;
		mesh.setVertex(i++,vec3(X,Y,Z * sin(X + time)));
	}
}
// stop the counter
engine.profiler.end();

```


### Arguments

## void engine.profiler. begin ( )


Starts a counter with a given name. The counter shows user how many millisecods have been spent for the operation that is performed between the *engine.profiler.begin()* and the *[engine.profiler.end()](#end_float)* functions.


```cpp
ObjectMeshDynamic mesh;
// ...
// start the counter that shows the time spent for
// dynamic mesh normal vectors, tangent vectors and a mesh bounding box calculation
engine.profiler.begin("mesh");
mesh.updateBounds();
mesh.updateTangents();
mesh.flushVertex();
// stop the counter
engine.profiler.end();

```


### Arguments

## float engine.profiler. end ( )

Stops the last [activated](#begin_cstr_vec4_void) counter and returns its value.
### Return value

Value of the counter in milliseconds.
## int engine.profiler. beginMicro ( string name , int gpu = 0 )


Starts a counter with a given name in the [Microprofile](../../../tools/profiling/microprofile/index.md) only, without overloading the [Performance Profiler](../../../tools/profiling/profiler/index.md) layout. The counter shows user how many millisecods have been spent for the operation that is performed between the *engine.profiler.beginMicro()* and the *[engine.profiler.endMicro()](#endMicro_int_void)* functions.


> **Notice:** Each counter has an ID. Thus, several nested *beginMicro() / endMicro()* blocks can be created, which can't be done in the [Performance Profiler](../../../tools/profiling/profiler/index.md).


```cpp
ObjectMeshDynamic mesh;
// ...
// start the counter that shows the time spent for
// dynamic mesh normal vectors, tangent vectors and a mesh bounding box calculation, with a nested counter for tangent vectors only
int c_id = engine.profiler.beginMicro("mesh");
mesh.updateBounds();
int c_nested_id = engine.profiler.beginMicro("mesh_tangents");
mesh.updateTangents();
engine.profiler.endMicro(c_nested_id);
mesh.flushVertex();
// stop the counter
engine.profiler.endMicro(c_id);

```


### Arguments

- *string* **name** - Name of the counter.
- *int* **gpu** - **1** for the GPU counter; **0** � for the CPU counter. The default value is **0**.

### Return value

ID of the added counter.
## void engine.profiler. endMicro ( int id )

Stops a previously [activated](#beginMicro_cstr_int_int) Microprofile counter with the specified ID.
### Arguments

- *int* **id** - Microprofile counter ID.

## void engine.profiler. initThread ( string name , int priority = 0 )


Initiates the custom thread for Microprofile calculations to avoid spikes, which otherwise are registered by Microprofile on registering a new thread. This method shall be called at the beginning of the thread and before  and followed by  when the thread is not required anymore.


### Arguments

- *string* **name** - Name of the thread displayed in Microprofile.
- *int* **priority** - Order (ordinal number) of the thread displayed in Microprofile.

## void engine.profiler. shutdownThread ( )

Stops a previously [activated](#initThread_cstr_int_void) Microprofile thread counter. This method shall be called after  and before the thread ends.
## int engine.profiler. findCounter ( string name )

Returns the counter number by its name.
### Arguments

- *string* **name** - Name of the counter.

### Return value

Counter number in range from 0 to the [total number of counters](#NumCounters).
## string engine.profiler. getCounterName ( int num )

Returns the counter name by its number.
### Arguments

- *int* **num** - Counter number in range from 0 to the [total number of counters](#NumCounters).

### Return value

Name of the counter.
## string engine.profiler. getCounterText ( int num )

Returns the text of the specified counter.
### Arguments

- *int* **num** - Counter number in range from 0 to the [total number of counters](#NumCounters).

### Return value

Text of the counter.
## vec4 engine.profiler. getCounterColor ( int num )

Returns the color of the specified counter.
### Arguments

- *int* **num** - Counter number in range from 0 to the [total number of counters](#NumCounters).

### Return value

Color of the counter.
## float engine.profiler. getCounterValue ( int num )

Returns the value of the specified counter.
### Arguments

- *int* **num** - Counter number in range from 0 to the [total number of counters](#NumCounters).

### Return value

Value of the counter.
## long engine.profiler. getCounterFrame ( int num )

Returns the frame of the specified counter.
### Arguments

- *int* **num** - Counter number in range from 0 to the [total number of counters](#NumCounters).

### Return value

Frame of the counter.
## int engine.profiler. isCounterActive ( int num )

Returns the value indicating if the specified counter is active.
### Arguments

- *int* **num** - Counter number in range from 0 to the [total number of counters](#NumCounters).

### Return value

**1** if the counter is active; otherwise **0**.
## int engine.profiler. isCounterSeparator ( int num )

Returns the value indicating if a separator is placed after the specified counter.
### Arguments

- *int* **num** - Counter number in range from 0 to the [total number of counters](#NumCounters).

### Return value

**1** if the separator is placed; otherwise **0**.
## static int engine.profiler. isProfilerDumpEnabled ( )

Checks whether the profiler dump recording is currently active.
### Return value

**1** if a profiler dump is currently being recorded; otherwise **0**.
## static void engine.profiler. stopProfilerDump ( )

***Console*:**`profiling_stop`Stops the currently active profiler dump recording. If a profiler dump is in progress, calling this method finalizes the dump and closes the output file.
