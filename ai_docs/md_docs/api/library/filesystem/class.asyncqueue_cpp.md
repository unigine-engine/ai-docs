# Unigine::AsyncQueue Class (CPP)

**Header:** #include <UnigineAsyncQueue.h>

> **Notice:** This class is a singleton.


Loading of files/meshes/images/nodes on demand is performed in a separate system thread, in addition to asynchronous content streaming. This class is used to control asynchronous data loading. It is possible to control loading queue by organizing files in groups and setting individual weights inside these groups.


To load files on demand, call the functions in the following order:


1. First *[loadFile()](../../...md#loadFile_cstr_int_float_int)* function is called to place the file in the queue for loading and obtain an ***ID***, that will be used to identify a resource in subsequent operations.
2. After that, different operations can be performed:

  - *[forceFile()](../../...md#forceFile_int_int)* to load the file immediately.
  - *[removeFile()](../../...md#removeFile_int_int)* to remove the file from the queue in case there is no need to load it any more of to remove a file from the list of loaded files if it was loaded but no longer needed.
  - *[checkFile()](../../...md#checkFile_int_int)* to check if the given file was requested to be loaded via *loadFile()* or if it has already been loaded.


The same algorithm is true for:


- **Meshes** - see methods *[loadMesh()](../../...md#loadMesh_cstr_int_float_int)*, *[forceMesh()](../../...md#forceMesh_int_int)*, *[getMesh()](../../...md#getMesh_int_Mesh)*, *[takeMesh()](../../...md#takeMesh_int_Mesh)*, *[checkMesh()](../../...md#checkMesh_int_int)*, and *[removeMesh()](../../...md#removeMesh_int_int)*.
- **Images** - see methods *[loadImage()](../../...md#loadImage_cstr_int_float_int)*, *[forceImage()](../../...md#forceImage_int_int)*, *[getImage()](../../...md#getImage_int_Image)*, *[takeImage()](../../...md#takeImage_int_Image)*, *[checkImage()](../../...md#checkImage_int_int)*, and *[removeImage()](../../...md#removeImage_int_int)*.
- **Nodes** - see methods *[loadNode()](../../...md#loadNode_cstr_int_float_int)*, *[forceNode()](../../...md#forceNode_int_int)*, *[getNode()](../../...md#getNode_int_Node)*, *[takeNode()](../../...md#takeNode_int_Node)*, *[checkNode()](../../...md#checkNode_int_int)*, and *[removeNode()](../../...md#removeNode_int_int)*.


To get a loaded resource (image, mesh, or node) the following 2 groups of methods can be used:


- **Get-methods** - these methods return the loaded resource:

  - *[getImage()](../../...md#getImage_int_Image)*
  - *[getMesh()](../../...md#getMesh_int_Mesh)*
  - *[getNode()](../../...md#getNode_int_Node)*
- **Take-methods** - these methods return the loaded resource and remove it from the list of loaded ones:

  - *[takeImage()](../../...md#takeImage_int_Image)*
  - *[takeMesh()](../../...md#takeMesh_int_Mesh)*
  - *[takeNode()](../../...md#takeNode_int_Node)*


For example:


```cpp
// specify relative paths to resources to be loaded to a queue
static const char *meshes[] = {
	"meshes/box.mesh",
	"meshes/capsule.mesh",
	"meshes/cbox.mesh",
};

#define ARRAY_LENGTH(array) static_cast<int>(sizeof(array) / sizeof(array[0]))

struct AsyncLoadRequest
{
	String name;
	int id;
};

Vector<AsyncLoadRequest> mesh_load_requests;

void AsyncSample::init()
{

	// enqueue meshes to load
	for (int i = 0; i < ARRAY_LENGTH(meshes); ++i)
	{
		const char *name = meshes[i];
		AsyncLoadRequest request;
		request.name = name;
		request.id = AsyncQueue::loadMesh(name);
		mesh_load_requests.append(request);
	}

}

void AsyncSample::update()
{
	// check mesh load requests
	for (int i = 0; i < mesh_load_requests.size(); ++i)
	{
		const auto &r = mesh_load_requests[i];

		if (!AsyncQueue::checkMesh(r.id))
			continue;

		// remove the mesh from the list of the loaded meshes and print a message
		AsyncQueue::removeMesh(r.id);
		Log::message("Loaded mesh \"%s\"\n", r.name.get());

		mesh_load_requests.remove(i--);
	}
}


```


### Handling Events


You can add "resource loaded" event handlers for files, images, meshes or nodes and perform certain actions as a resource is loaded. The example below shows how to add a "loaded" event handler for image resource, that reports the name and id of the loaded image.

> **Notice:** Do not call [***take-methods***](#take_methods) inside a handler function unless you are absolutely sure, that the resource is yours, otherwise internal engine managers will be forced to load it again and again every time. In such cases it is recommended to use [***get-methods***](#take_methods).


```cpp
// specify relative paths to resources to be loaded to a queue
static const char *textures[] = {
	"textures/black_d.texture",
	"textures/blue_d.texture",
	"textures/green_d.texture",
	"textures/orange_d.texture",
	"textures/red_d.texture",
	"textures/white_d.texture",
	"textures/yellow_d.texture",
};

#define ARRAY_LENGTH(array) static_cast<int>(sizeof(array) / sizeof(array[0]))

void AsyncSample::init()
{

	// enqueue textures to load
	for (int i = 0; i < ARRAY_LENGTH(textures); ++i)
		AsyncQueue::loadImage(textures[i]);
	// subscribing for the ImageLoaded event
	AsyncQueue::getEventImageLoaded().connect(this, &AsyncSample::image_loaded);

}

// image loaded event handler function
void AsyncSample::image_loaded(const char *name, int id)
{
	AsyncQueue::removeImage(id);
	Log::message("Image \"%s\" loaded, ID: %d\n", name, id);
}


```


### Async and Multithreaded Execution


In addition to managing background file loading and on-demand streaming, the ***AsyncQueue*** class provides general-purpose asynchronous and multithreaded execution functionality. It enables scheduling user-defined tasks in dedicated threads, including parallel execution across multiple CPU cores.


This class supports both asynchronous and synchronous multithreaded workflows, with optional frame synchronization. It allows offloading expensive operations, such as procedural generation or complex data processing, without blocking the main thread.


To provide fine control over task placement, the ***AsyncQueue*** provides several dedicated thread types via the ***[ASYNC_THREAD](#ASYNC_THREAD)*** enumeration:


- **MAIN** - the Engine's main thread.
- **SYNC** - Sync pool thread for frame-synchronized tasks.
- **ASYNC** - general-purpose async Engine thread.
- **COMMON** - Common pool thread with flexible cross-pool load balancing.
- **CRITICAL** - critical thread for high-priority tasks.
- **BACKGROUND** - background thread for long-running tasks.
- **FILE_STREAM** - a thread for disk I/O operations.
- **GPU_STREAM** - a thread to work with GPU resources.
- **NEW** - isolated thread taken from a thread pool.


***AsyncQueue*** also provides control over task scheduling priority via the ***[ASYNC_PRIORITY](#ASYNC_PRIORITY)*** enumeration (8 levels from *CRITICAL* to *IDLE*). The default priority for *runAsync()* is *BACKGROUND*.


![](thread_sequence.png)

*Microprofiletool: Task pipeline using all thread types.*


By combining these thread types and priorities, you can design flexible execution chains that distribute workload efficiently across engine subsystems.


The multi-thread methods create *[CPUShader](../../../api/library/common/mt/class.cpushader_cpp.md)* instances, while single-thread methods create *[CPUTask](../../../api/library/common/mt/class.cputask_cpp.md)* instances. These classes are available directly only in C++, while *AsyncQueue* provides a unified interface for C++, C#, and UnigineScript. For more details on thread pools, task priority, and frame synchronization, see the **[UNIGINE Thread System](../../../code/fundamentals/thread_system/index.md)** article.


### See Also


- C++ samples:

  -
  -
  -
- C# samples:

  -
  -
  -
- UnigineScript samples:

  -
  -


## AsyncQueue Class

### Enums

## ASYNC_THREAD

| Name | Description |
|---|---|
| **ASYNC_THREAD_MAIN** = 0 | Main thread of the Engine. Required for any operation that interacts with scene objects or Engine state directly. Use this thread when executing callbacks that must safely modify or access scene elements. Typically used for dispatching final-stage results from background tasks. |
| **ASYNC_THREAD_SYNC** = 1 | Sync pool thread. Tasks on this pool are frame-synchronized and the main thread contributes as a worker during synchronous operations. |
| **ASYNC_THREAD_ASYNC** = 2 | General-purpose async thread used by the Engine for tasks like prefetching, landscape updates, data streaming, and other background operations. Overusing this thread may delay core Engine systems. |
| **ASYNC_THREAD_COMMON** = 3 | Common pool thread. Workers in this pool can pick up tasks from multiple other pools (Sync, Async, Common), providing flexible load balancing across the thread system. |
| **ASYNC_THREAD_CRITICAL** = 4 | Critical thread for high-priority tasks that must be processed as soon as possible. |
| **ASYNC_THREAD_BACKGROUND** = 5 | Background thread with the lowest priority. Rarely used by the Engine itself, primarily intended for user-driven procedural operations such as geometry modification. Safe for long-running background tasks, as it does not interfere with streaming or other critical Engine systems. |
| **ASYNC_THREAD_FILE_STREAM** = 6 | Dedicated thread for file I/O operations. Similar in priority to ASYNC, but separated to reduce contention between CPU work and disk access. Suitable for loading/saving geometry, streaming data from disk, or handling heavy I/O without affecting core async systems. Overloading this thread may impact streaming performance. |
| **ASYNC_THREAD_GPU_STREAM** = 7 | Specialized thread with a dedicated command queue for transferring data from RAM to VRAM. Used to asynchronously create GPU resources (e.g., *[Texture](../../../api/library/rendering/class.texture_cpp.md)*, *[MeshRender](../../../api/library/rendering/class.meshrender_cpp.md)*) from corresponding RAM objects ( *[Image](../../../api/library/common/class.image_cpp.md)*, *[Mesh](../../../api/library/rendering/class.mesh_cpp.md)*). Ideal for implementing custom data streaming system or dynamic GPU data updates. |
| **ASYNC_THREAD_NEW** = 8 | Creates a new isolated thread from the internal thread pool. Meant for custom user operations that must not block or interfere with existing Engine threads. Ideal for long-running or experimental tasks. This thread runs independently and does not impact Engine systems. |
| **NUM_ASYNC_THREADS** = 9 | Number of predefined async thread types. Used to validate or iterate over thread type constants. |

## ASYNC_PRIORITY

| Name | Description |
|---|---|
| **ASYNC_PRIORITY_CRITICAL** = 0 | Highest priority. Tasks with this level are scheduled for execution before all others. |
| **ASYNC_PRIORITY_HIGHEST** = 1 | Second highest priority level. |
| **ASYNC_PRIORITY_ABOVENORMAL** = 2 | Above normal priority level. |
| **ASYNC_PRIORITY_NORMAL** = 3 | Default priority level for general-purpose tasks. |
| **ASYNC_PRIORITY_BELOWNORMAL** = 4 | Below normal priority level. |
| **ASYNC_PRIORITY_LOWEST** = 5 | Second lowest priority level. |
| **ASYNC_PRIORITY_BACKGROUND** = 6 | Background priority level for non-urgent tasks. |
| **ASYNC_PRIORITY_IDLE** = 7 | Lowest priority. Tasks are only scheduled when no higher-priority tasks are pending. |

### Members

## int getNumLoadedResources () const

Returns the current total number of currently loaded resources.
### Return value

Current total number of currently loaded resources � the sum of currently loaded data, files, images and meshes.
## int getNumLoadedNodes () const

Returns the current total number of loaded nodes.
### Return value

Current total number of loaded nodes including currently processed ones.
## int getNumLoadedMeshes () const

Returns the current total number of loaded meshes.
### Return value

Current total number of loaded meshes.
## int getNumLoadedImages () const

Returns the current total number of loaded images.
### Return value

Current total number of loaded images.
## int getNumLoadedFiles () const

Returns the current total number of loaded files.
### Return value

Current total number of loaded files.
## int getNumLoadedData () const

Returns the current total number of loaded data segments.
### Return value

Current total number of loaded data segments.
## int getNumQueuedResources () const

Returns the current total number of queued resources waiting for background loading.
### Return value

Current total number of queued resources waiting for background loading � the sum of queued and currently processed data, files, images and meshes.
## int getNumQueuedNodes () const

Returns the current total number of queued nodes waiting for the background loading.
### Return value

Current total number of queued nodes waiting for the background loading including currently processed ones.
## int getNumQueuedMeshes () const

Returns the current total number of queued meshes waiting for the background loading.
### Return value

Current total number of queued meshes waiting for the background loading including currently processed ones.
## int getNumQueuedImages () const

Returns the current total number of queued images waiting for the background loading.
### Return value

Current total number of queued images waiting for the background loading including currently processed ones.
## int getNumQueuedFiles () const

Returns the current total number of queued files waiting for the background loading.
### Return value

Current total number of queued files waiting for the background loading including currently processed ones.
## int getNumQueuedData () const

Returns the current total number of queued data segments waiting for the background loading.
### Return value

Current total number of queued data segments waiting for the background loading including currently processed ones.
## float getTotalTime () const

Returns the current total time it took to process the loading queue.
### Return value

Current total time it took to process the loading queue.
## static Event<const char *, int> getEventNodeLoaded () const

event triggered when the node is loaded. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const char * **name**, int **id**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the NodeLoaded event handler
void nodeloaded_event_handler(const char * name,  int id)
{
	Log::message("\Handling NodeLoaded event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections nodeloaded_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
AsyncQueue::getEventNodeLoaded().connect(nodeloaded_event_connections, nodeloaded_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
AsyncQueue::getEventNodeLoaded().connect(nodeloaded_event_connections, [](const char * name,  int id) {
		Log::message("\Handling NodeLoaded event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
nodeloaded_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection nodeloaded_event_connection;

// subscribe to the NodeLoaded event with a handler function keeping the connection
AsyncQueue::getEventNodeLoaded().connect(nodeloaded_event_connection, nodeloaded_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
nodeloaded_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
nodeloaded_event_connection.setEnabled(true);

// ...

// remove subscription to the NodeLoaded event via the connection
nodeloaded_event_connection.disconnect();

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

	// A NodeLoaded event handler implemented as a class member
	void event_handler(const char * name,  int id)
	{
		Log::message("\Handling NodeLoaded event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
AsyncQueue::getEventNodeLoaded().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId nodeloaded_handler_id;

// subscribe to the NodeLoaded event with a lambda handler function and keeping connection ID
nodeloaded_handler_id = AsyncQueue::getEventNodeLoaded().connect(e_connections, [](const char * name,  int id) {
		Log::message("\Handling NodeLoaded event (lambda).\n");
	}
);

// remove the subscription later using the ID
AsyncQueue::getEventNodeLoaded().disconnect(nodeloaded_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all NodeLoaded events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
AsyncQueue::getEventNodeLoaded().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
AsyncQueue::getEventNodeLoaded().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const char *, int> getEventMeshLoaded () const

event triggered when the mesh is loaded. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const char * **name**, int **id**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the MeshLoaded event handler
void meshloaded_event_handler(const char * name,  int id)
{
	Log::message("\Handling MeshLoaded event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections meshloaded_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
AsyncQueue::getEventMeshLoaded().connect(meshloaded_event_connections, meshloaded_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
AsyncQueue::getEventMeshLoaded().connect(meshloaded_event_connections, [](const char * name,  int id) {
		Log::message("\Handling MeshLoaded event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
meshloaded_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection meshloaded_event_connection;

// subscribe to the MeshLoaded event with a handler function keeping the connection
AsyncQueue::getEventMeshLoaded().connect(meshloaded_event_connection, meshloaded_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
meshloaded_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
meshloaded_event_connection.setEnabled(true);

// ...

// remove subscription to the MeshLoaded event via the connection
meshloaded_event_connection.disconnect();

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

	// A MeshLoaded event handler implemented as a class member
	void event_handler(const char * name,  int id)
	{
		Log::message("\Handling MeshLoaded event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
AsyncQueue::getEventMeshLoaded().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId meshloaded_handler_id;

// subscribe to the MeshLoaded event with a lambda handler function and keeping connection ID
meshloaded_handler_id = AsyncQueue::getEventMeshLoaded().connect(e_connections, [](const char * name,  int id) {
		Log::message("\Handling MeshLoaded event (lambda).\n");
	}
);

// remove the subscription later using the ID
AsyncQueue::getEventMeshLoaded().disconnect(meshloaded_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all MeshLoaded events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
AsyncQueue::getEventMeshLoaded().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
AsyncQueue::getEventMeshLoaded().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const char *, int> getEventImageLoaded () const

event triggered when the image is loaded. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const char * **name**, int **id**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the ImageLoaded event handler
void imageloaded_event_handler(const char * name,  int id)
{
	Log::message("\Handling ImageLoaded event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections imageloaded_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
AsyncQueue::getEventImageLoaded().connect(imageloaded_event_connections, imageloaded_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
AsyncQueue::getEventImageLoaded().connect(imageloaded_event_connections, [](const char * name,  int id) {
		Log::message("\Handling ImageLoaded event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
imageloaded_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection imageloaded_event_connection;

// subscribe to the ImageLoaded event with a handler function keeping the connection
AsyncQueue::getEventImageLoaded().connect(imageloaded_event_connection, imageloaded_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
imageloaded_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
imageloaded_event_connection.setEnabled(true);

// ...

// remove subscription to the ImageLoaded event via the connection
imageloaded_event_connection.disconnect();

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

	// A ImageLoaded event handler implemented as a class member
	void event_handler(const char * name,  int id)
	{
		Log::message("\Handling ImageLoaded event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
AsyncQueue::getEventImageLoaded().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId imageloaded_handler_id;

// subscribe to the ImageLoaded event with a lambda handler function and keeping connection ID
imageloaded_handler_id = AsyncQueue::getEventImageLoaded().connect(e_connections, [](const char * name,  int id) {
		Log::message("\Handling ImageLoaded event (lambda).\n");
	}
);

// remove the subscription later using the ID
AsyncQueue::getEventImageLoaded().disconnect(imageloaded_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all ImageLoaded events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
AsyncQueue::getEventImageLoaded().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
AsyncQueue::getEventImageLoaded().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const char *, int> getEventFileLoaded () const

event triggered when the file is loaded. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const char * **name**, int **id**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the FileLoaded event handler
void fileloaded_event_handler(const char * name,  int id)
{
	Log::message("\Handling FileLoaded event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections fileloaded_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
AsyncQueue::getEventFileLoaded().connect(fileloaded_event_connections, fileloaded_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
AsyncQueue::getEventFileLoaded().connect(fileloaded_event_connections, [](const char * name,  int id) {
		Log::message("\Handling FileLoaded event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
fileloaded_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection fileloaded_event_connection;

// subscribe to the FileLoaded event with a handler function keeping the connection
AsyncQueue::getEventFileLoaded().connect(fileloaded_event_connection, fileloaded_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
fileloaded_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
fileloaded_event_connection.setEnabled(true);

// ...

// remove subscription to the FileLoaded event via the connection
fileloaded_event_connection.disconnect();

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

	// A FileLoaded event handler implemented as a class member
	void event_handler(const char * name,  int id)
	{
		Log::message("\Handling FileLoaded event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
AsyncQueue::getEventFileLoaded().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId fileloaded_handler_id;

// subscribe to the FileLoaded event with a lambda handler function and keeping connection ID
fileloaded_handler_id = AsyncQueue::getEventFileLoaded().connect(e_connections, [](const char * name,  int id) {
		Log::message("\Handling FileLoaded event (lambda).\n");
	}
);

// remove the subscription later using the ID
AsyncQueue::getEventFileLoaded().disconnect(fileloaded_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all FileLoaded events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
AsyncQueue::getEventFileLoaded().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
AsyncQueue::getEventFileLoaded().setEnabled(true);

```

</details>

### Return value

Event instance.
---

## Ptr < Image > getImage ( int id )

Returns the image loaded by the specified operation.
> **Notice:** This method does not remove the image from the list of loaded ones. If you want the image to be removed from this list right after retrieving it, use the *[takeImage()](../../...md#takeImage_int_Image)* method.


### Arguments

- *int* **id** - Loading operation identifier (see the *[loadImage()](../../...md#loadImage_cstr_int_float_int)* method).

### Return value

Image smart pointer.
## Ptr < Mesh > getMesh ( int id )

Returns the mesh loaded by the specified operation.
> **Notice:** This method does not remove the mesh from the list of loaded ones. If you want the mesh to be removed from this list right after retrieving it, use the *[takeMesh()](../../...md#takeMesh_int_Mesh)* method.


### Arguments

- *int* **id** - Loading operation identifier (see the *[loadMesh()](../../...md#loadMesh_cstr_int_float_int)* method).

### Return value

Mesh smart pointer.
## Ptr < Node > getNode ( int id )

Returns the node loaded by the specified operation. If the node loaded by the specified operation consists of multiple objects, a new [dummy object](../../../api/library/objects/class.objectdummy_cpp.md) to combine them is created and its smart pointer is returned.
> **Notice:** This method does not remove the node from the list of loaded ones. If you want the node to be removed from this list right after retrieving it, use the *[takeNode()](../../...md#takeNode_int_Node)* method.


### Arguments

- *int* **id** - Loading operation identifier (see the *[loadNode()](../../...md#loadNode_cstr_int_float_int)* method).

### Return value

Node smart pointer.
## int getNodes ( int id , Vector < Ptr < Node >> & OUT_nodes ) const

Puts the nodes loaded by the specified operation to the specified array. If the node loaded by the specified operation consists of multiple objects, they are put into the array.
> **Notice:** This method does not remove the nodes from the list of loaded ones. If you want the nodes to be removed from this list right after retrieving them, use the *[takeNodes()](../../...md#takeNodes_int_VECNode_int)* method.


### Arguments

- *int* **id** - Loading operation identifier.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>> &* **OUT_nodes** - Array of loaded nodes' smart pointers. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

1 if the operation is successful; otherwise, 0.
## int checkFile ( int id )

Returns a value indicating if the file is in the loading queue or already loaded.
### Arguments

- *int* **id** - Loading operation identifier (see the *[loadFile()](../../...md#loadFile_cstr_int_float_int)* method).

### Return value

1 if the file is in the loading queue or already loaded; otherwise, 0.
## int checkImage ( int id )

Returns a value indicating if the image is in the loading queue or already loaded.
### Arguments

- *int* **id** - Loading operation identifier (see the *[loadImage()](../../...md#loadImage_cstr_int_float_int)* method).

### Return value

1 if the image is in the loading queue or already loaded; otherwise, 0.
## int checkMesh ( int id )

Returns a value indicating if the mesh is in the loading queue or already loaded.
### Arguments

- *int* **id** - Loading operation identifier (see the *[loadMesh()](../../...md#loadMesh_cstr_int_float_int)* method).

### Return value

1 if the mesh is in the loading queue or already loaded; otherwise, 0.
## int checkNode ( int id )

Returns a value indicating if the node is in the loading queue or already loaded.
### Arguments

- *int* **id** - Loading operation identifier (see the *[loadNode()](../../...md#loadNode_cstr_int_float_int)* method).

### Return value

1 if the node is in the loading queue or already loaded; otherwise, 0.
## int forceFile ( int id )

Forces loading of the file. The specified file will be loaded right after the currently loading file (if any) is processed. All other file system operations are suspended until the forced file is loaded.
> **Notice:** The file won't be loaded immediately after calling the method as it can be large.


### Arguments

- *int* **id** - Loading operation identifier (see the *[loadFile()](../../...md#loadFile_cstr_int_float_int)* method).

### Return value

1 if the file is loaded successfully; otherwise, 0.
## int forceImage ( int id )

Forces loading of the image. The specified image will be loaded right after the currently loading image (if any) is processed. All other file system operations are suspended until the forced image is loaded.
> **Notice:** The image won't be loaded immediately after calling the method as it can be large.


### Arguments

- *int* **id** - Loading operation identifier (see the *[loadImage()](../../...md#loadImage_cstr_int_float_int)* method).

### Return value

1 if the image is loaded successfully; otherwise, 0.
## int forceMesh ( int id )

Forces loading of the mesh. The specified mesh will be loaded right after the currently loading mesh (if any) is processed. All other file system operations are suspended until the forced mesh is loaded.
> **Notice:** The mesh won't be loaded immediately after calling the method as it can be large.


### Arguments

- *int* **id** - Loading operation identifier (see the *[loadMesh()](../../...md#loadMesh_cstr_int_float_int)* method).

### Return value

1 if the mesh is loaded successfully; otherwise, 0.
## int forceNode ( int id )

Forces loading of the node. The specified node will be loaded right after the currently loading node (if any) is processed. All other file system operations are suspended until the forced node is loaded.
> **Notice:** The node won't be loaded immediately after calling the method as it can be large.


### Arguments

- *int* **id** - Loading operation identifier (see the *[loadNode()](../../...md#loadNode_cstr_int_float_int)* method).

### Return value

1 if the node is loaded successfully; otherwise, 0.
## int loadFile ( const char * name , int group = 0 , float weight = 0.0f )

Loads a given file with the specified group and priority to the thread.
### Arguments

- *const char ** **name** - Absolute or relative path to the file (including its name).
- *int* **group** - Priority group. Greater priority means faster loading. The default value is 0.
- *float* **weight** - Weight of the priority inside the group. Greater weight means faster loading inside the same priority group. The default value is 0.0f.

### Return value

Loading operation identifier.
## int loadImage ( const char * name , int group = 0 , float weight = 0.0f )

Loads a given image file with the specified group and priority to the thread.
### Arguments

- *const char ** **name** - Absolute or relative path to the image file (including its name).
- *int* **group** - Priority group. Greater priority means faster loading. The default value is 0.
- *float* **weight** - Weight of the priority inside the group. Greater weight means faster loading inside the same priority group. The default value is 0.0f.

### Return value

Loading operation identifier.
## int loadMesh ( const char * name , int group = 0 , float weight = 0.0f )

Loads a given `mesh`-file with the specified group and priority to the thread.
### Arguments

- *const char ** **name** - Absolute or relative path to the **.mesh* file (including its name).
- *int* **group** - Priority group. Greater priority means faster loading. The default value is 0.
- *float* **weight** - Weight of the priority inside the group. Greater weight means faster loading inside the same priority group. The default value is 0.0f.

### Return value

Loading operation identifier.
## int loadNode ( const char * name , int group = 0 , float weight = 0.0f )

Loads a given `node`-file with the specified group and priority to the thread.
> **Notice:** In order to display such asynchronously loaded node, the [*updateEnabled()*](../../../api/library/nodes/class.node_cpp.md#updateEnabled_void) method should be called for it **from the main thread**.


### Arguments

- *const char ** **name** - Absolute or relative path to the **.node* file (including its name).
- *int* **group** - Priority group. Greater priority means faster loading. The default value is 0.
- *float* **weight** - Weight of the priority inside the group. Greater weight means faster loading inside the same priority group. The default value is 0.0f.

### Return value

Loading operation identifier.
## int removeFile ( int id )

Removes the given file from the loading queue or from the list of loaded files, if it was already loaded.
> **Notice:** If the specified file is currently loading, it will be removed after the loading operation is completed.


### Arguments

- *int* **id** - Loading operation identifier (see the *[loadFile()](../../...md#loadFile_cstr_int_float_int)* method).

### Return value

**1** if the file is successfully removed; otherwise, **0**.
## int removeImage ( int id )

Removes the given image from the loading queue or from the list of loaded images, if it was already loaded.
> **Notice:** If the specified image is currently loading, it will be removed after the loading operation is completed.


### Arguments

- *int* **id** - Loading operation identifier (see the *[loadImage()](../../...md#loadImage_cstr_int_float_int)* method).

### Return value

**1** if the image is successfully removed; otherwise, **0**.
## int removeMesh ( int id )

Removes the given mesh from the loading queue or from the list of loaded meshes, if it was already loaded.
> **Notice:** If the specified mesh is currently loading, it will be removed after the loading operation is completed.


### Arguments

- *int* **id** - Loading operation identifier (see the *[loadMesh()](../../...md#loadMesh_cstr_int_float_int)* method).

### Return value

**1** if the mesh is successfully removed; otherwise, **0**.
## int removeNode ( int id )

Removes the given node from the loading queue or from the list of loaded nodes, if it was already loaded.
> **Notice:** If the specified node is currently loading, it will be removed after the loading operation is completed. Nodes are removed with all their hierarchy.


### Arguments

- *int* **id** - Loading operation identifier (see the *[loadNode()](../../...md#loadNode_cstr_int_float_int)* method).

### Return value

1 if the node is removed successfully; otherwise, 0.
## Ptr < Image > takeImage ( int id )

Returns the image loaded by the specified operation and removes it from the list of loaded images.
### Arguments

- *int* **id** - Loading operation identifier (see the *[loadImage()](../../...md#loadImage_cstr_int_float_int)* method).

### Return value

Image smart pointer.
## Ptr < Mesh > takeMesh ( int id )

Returns the mesh loaded by the specified operation and removes it from the list of loaded meshes.
### Arguments

- *int* **id** - Loading operation identifier (see the *[loadMesh()](../../...md#loadMesh_cstr_int_float_int)* method).

### Return value

Mesh smart pointer.
## Ptr < Node > takeNode ( int id )

Returns the node loaded by the specified operation and removes it from the list of loaded nodes.
> **Notice:** Nodes are removed with all their hierarchy.


### Arguments

- *int* **id** - Loading operation identifier (see the *[loadNode()](../../...md#loadNode_cstr_int_float_int)* method).

### Return value

Node smart pointer.
## int takeNodes ( int id , Vector < Ptr < Node >> & OUT_nodes ) const

Puts the nodes loaded by the specified operation to the specified array and removes them from the list of loaded nodes. If the node loaded by the specified operation consists of multiple objects, they are put into the array.
> **Notice:** Nodes are removed with all their hierarchy.


### Arguments

- *int* **id** - Loading operation identifier.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>> &* **OUT_nodes** - Array of loaded nodes' smart pointers. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

1 if the operation is successful; otherwise, 0.
## int loadImageInfo ( const char * name , int group = 0 , float weight = 0.0f )

Loads file info (size format, etc.) for the specified image, group and priority to the thread.
### Arguments

- *const char ** **name** - Absolute or relative path to the image file (including its name).
- *int* **group** - Priority group. Greater priority means faster loading. The default value is 0.
- *float* **weight** - Weight of the priority inside the group. Greater weight means faster loading inside the same priority group. The default value is 0.0f.

### Return value

Loading operation identifier.
## void runAsync ( AsyncQueue::ASYNC_THREAD thread_type , CallbackBase * callback , AsyncQueue::ASYNC_PRIORITY priority = Enum.AsyncQueue.ASYNC_PRIORITY.BACKGROUND )


Creates a [CPUTask](../../../api/library/common/mt/class.cputask_cpp.md) that executes the specified callback on the given thread with [FrameSyncMode::Disabled](../../../api/library/common/mt/class.threadspool_cpp.md#FrameSyncMode) (independent of the frame).


Use this method to offload operations such as geometry generation, file parsing, or image processing to a dedicated Engine-managed thread.


### Arguments

- *[AsyncQueue::ASYNC_THREAD](../../../api/library/filesystem/class.asyncqueue_cpp.md#ASYNC_THREAD)* **thread_type** - [Type of thread](#ASYNC_THREAD) to run the task on.
- *[CallbackBase](../../../api/library/common/callbacks/class.callbackbase_cpp.md) ** **callback** - Pointer to a callback object. The target function must have the following signature: *void callback_function()*. To pass the function as a callback, wrap it using *[MakeCallback()](../../../api/library/common/class.unigine.namespace_cpp.md#MakeCallback_Classm_RetClassm)*.
- *[AsyncQueue::ASYNC_PRIORITY](../../../api/library/filesystem/class.asyncqueue_cpp.md#ASYNC_PRIORITY)* **priority** - Priority of the task execution.

## void runFrameAsyncMultiThread ( CallbackBase2 <int, int> * callback , int num_threads = -1 )

Creates a [CPUShader](../../../api/library/common/mt/class.cpushader_cpp.md) that executes the specified callback concurrently across multiple threads with [FrameSyncMode::Swap](../../../api/library/common/mt/class.threadspool_cpp.md#FrameSyncMode) (synchronized with the frame). Does not block the calling thread. Intended for parallel execution of compute-heavy tasks that do not require immediate results but must complete within the current frame.
### Arguments

- *[CallbackBase2](../../../api/library/common/callbacks/class.callbackbase2_cpp.md)<int, int> ** **callback** -  Pointer to the callback that accepts two parameters: These parameters allow the task to be split into independent chunks, by assigning a portion of work to each thread. The function must be wrapped using *[MakeCallback()](../../../api/library/common/class.unigine.namespace_cpp.md#MakeCallback_Classm_RetClassm)* and have the following signature: ```cpp void callback(int thread_index, int thread_count) ```

  - **int thread_index** - the index of the current thread (starting from 0).
  - **int thread_count** - the total number of threads executing the task.
- *int* **num_threads** - Number of threads to use. If set to -1, the engine selects an optimal number based on available CPU cores.

## void runFrameAsyncMultiThread ( CallbackBase2 <int, int> * callback , CallbackBase * callback_done , int num_threads = -1 )

Creates a [CPUShader](../../../api/library/common/mt/class.cpushader_cpp.md) that executes the specified callback concurrently across multiple threads with [FrameSyncMode::Swap](../../../api/library/common/mt/class.threadspool_cpp.md#FrameSyncMode) (synchronized with the frame). Does not block the calling thread. Once all threads have finished, the callback_done is invoked. Intended for parallel execution of compute-heavy tasks that do not require immediate results but must complete within the current frame.
### Arguments

- *[CallbackBase2](../../../api/library/common/callbacks/class.callbackbase2_cpp.md)<int, int> ** **callback** -  Pointer to the callback that accepts two parameters: These parameters allow the task to be split into independent chunks, by assigning a portion of work to each thread. The function must be wrapped using *[MakeCallback()](../../../api/library/common/class.unigine.namespace_cpp.md#MakeCallback_Classm_RetClassm)* and have the following signature: ```cpp void callback(int thread_index, int thread_count) ```

  - **int thread_index** - the index of the current thread (starting from 0).
  - **int thread_count** - the total number of threads executing the task.
- *[CallbackBase](../../../api/library/common/callbacks/class.callbackbase_cpp.md) ** **callback_done** -  Callback to be called once all threaded executions of callback have completed. The function must be wrapped using *[MakeCallback()](../../../api/library/common/class.unigine.namespace_cpp.md#MakeCallback_Classm_RetClassm)* and have the following signature: ```cpp void callback_done() ```
- *int* **num_threads** - Number of threads to use. If set to -1, the engine selects an optimal number based on available CPU cores.

## void runFrameSyncMultiThread ( CallbackBase2 <int, int> * callback , int num_threads = -1 )

Creates a [CPUShader](../../../api/library/common/mt/class.cpushader_cpp.md) that executes the specified callback concurrently across multiple threads with [FrameSyncMode::Swap](../../../api/library/common/mt/class.threadspool_cpp.md#FrameSyncMode) (synchronized with the frame). Blocks the calling thread until all threads finish. Intended for parallel execution of compute-heavy tasks that must complete within the current frame.
### Arguments

- *[CallbackBase2](../../../api/library/common/callbacks/class.callbackbase2_cpp.md)<int, int> ** **callback** -  Pointer to the callback that accepts two parameters: These parameters allow the task to be split into independent chunks, by assigning a portion of work to each thread. The function must be wrapped using *[MakeCallback()](../../../api/library/common/class.unigine.namespace_cpp.md#MakeCallback_Classm_RetClassm)* and have the following signature: ```cpp void callback(int thread_index, int thread_count) ```

  - **int thread_index** - the index of the current thread (starting from 0).
  - **int thread_count** - the total number of threads executing the task.
- *int* **num_threads** - Number of threads to use. If set to -1, the engine selects an optimal number based on available CPU cores.

## void runAsyncMultiThread ( CallbackBase2 <int, int> * callback , int num_threads = -1 )

Creates a [CPUShader](../../../api/library/common/mt/class.cpushader_cpp.md) that executes the specified callback concurrently across multiple threads with [FrameSyncMode::Disabled](../../../api/library/common/mt/class.threadspool_cpp.md#FrameSyncMode) (independent of the frame). Does not block the calling thread. Intended for parallel execution of compute-heavy tasks that do not require immediate results.
### Arguments

- *[CallbackBase2](../../../api/library/common/callbacks/class.callbackbase2_cpp.md)<int, int> ** **callback** -  Pointer to the callback that accepts two parameters: These parameters allow the task to be split into independent chunks, by assigning a portion of work to each thread. The function must be wrapped using *[MakeCallback()](../../../api/library/common/class.unigine.namespace_cpp.md#MakeCallback_Classm_RetClassm)* and have the following signature: ```cpp void callback(int thread_index, int thread_count) ```

  - **int thread_index** - the index of the current thread (starting from 0).
  - **int thread_count** - the total number of threads executing the task.
- *int* **num_threads** - Number of threads to use. If set to -1, the engine selects an optimal number based on available CPU cores.

## void runAsyncMultiThread ( CallbackBase2 <int, int> * callback , CallbackBase * callback_done , int num_threads = -1 )

Creates a [CPUShader](../../../api/library/common/mt/class.cpushader_cpp.md) that executes the specified callback concurrently across multiple threads with [FrameSyncMode::Disabled](../../../api/library/common/mt/class.threadspool_cpp.md#FrameSyncMode) (independent of the frame). Does not block the calling thread. Once all threads have finished, the callback_done is invoked. Intended for parallel execution of compute-heavy tasks that do not require immediate results.
### Arguments

- *[CallbackBase2](../../../api/library/common/callbacks/class.callbackbase2_cpp.md)<int, int> ** **callback** -  Pointer to the callback that accepts two parameters: These parameters allow the task to be split into independent chunks, by assigning a portion of work to each thread. The function must be wrapped using *[MakeCallback()](../../../api/library/common/class.unigine.namespace_cpp.md#MakeCallback_Classm_RetClassm)* and have the following signature: ```cpp void callback(int thread_index, int thread_count) ```

  - **int thread_index** - the index of the current thread (starting from 0).
  - **int thread_count** - the total number of threads executing the task.
- *[CallbackBase](../../../api/library/common/callbacks/class.callbackbase_cpp.md) ** **callback_done** -  Callback to be called once all threaded executions of callback have completed. The function must be wrapped using *[MakeCallback()](../../../api/library/common/class.unigine.namespace_cpp.md#MakeCallback_Classm_RetClassm)* and have the following signature: ```cpp void callback_done() ```
- *int* **num_threads** - Number of threads to use. If set to -1, the engine selects an optimal number based on available CPU cores.

## void runSyncMultiThread ( CallbackBase2 <int, int> * callback , int num_threads = -1 )

Creates a [CPUShader](../../../api/library/common/mt/class.cpushader_cpp.md) that executes the specified callback concurrently across multiple threads with [FrameSyncMode::Disabled](../../../api/library/common/mt/class.threadspool_cpp.md#FrameSyncMode) (independent of the frame). Blocks the calling thread until all threads finish.
### Arguments

- *[CallbackBase2](../../../api/library/common/callbacks/class.callbackbase2_cpp.md)<int, int> ** **callback** -  Pointer to the callback that accepts two parameters: These parameters allow the task to be split into independent chunks, by assigning a portion of work to each thread. The function must be wrapped using *[MakeCallback()](../../../api/library/common/class.unigine.namespace_cpp.md#MakeCallback_Classm_RetClassm)* and have the following signature: ```cpp void callback(int thread_index, int thread_count) ```

  - **int thread_index** - the index of the current thread (starting from 0).
  - **int thread_count** - the total number of threads executing the task.
- *int* **num_threads** - Number of threads to use. If set to -1, the engine selects an optimal number based on available CPU cores.

## bool isMainThread ( )

Checks if the current thread is the main thread.
### Return value

Returns true if called from the main thread; otherwise false.
## bool isPoolSyncThread ( )

Checks if the current thread is a Sync pool worker thread.
### Return value

Returns true if called from a Sync pool thread; otherwise false.
## bool isPoolAsyncThread ( )

Checks if the current thread is an Async pool worker thread.
### Return value

Returns true if called from an Async pool thread; otherwise false.
## bool isPoolCriticalThread ( )

Checks if the current thread is a Critical pool worker thread.
### Return value

Returns true if called from a Critical pool thread; otherwise false.
## bool isPoolCommonThread ( )

Checks if the current thread is a Common pool worker thread.
### Return value

Returns true if called from a Common pool thread; otherwise false.
## bool isPoolBackgroundThread ( )

Checks if the current thread is a Background pool worker thread.
### Return value

Returns true if called from a Background pool thread; otherwise false.
## bool isPoolRenderFlushThread ( )

Checks if the current thread is a RenderFlush pool worker thread.
### Return value

Returns true if called from a RenderFlush pool thread; otherwise false.
## bool isPoolGPUStreamThread ( )

Checks if the current thread is a GPU stream pool worker thread.
### Return value

Returns true if called from a GPU stream pool thread; otherwise false.
## bool isPoolFileStreamThread ( )

Checks if the current thread is a file stream pool worker thread.
### Return value

Returns true if called from a file stream pool thread; otherwise false.
