# Unigine::AsyncQueue Class (CS)

> **Notice:** This class is a singleton.


Loading of files/meshes/images/nodes on demand is performed in a separate system thread, in addition to asynchronous content streaming. This class is used to control asynchronous data loading. It is possible to control loading queue by organizing files in groups and setting individual weights inside these groups.


To load files on demand, call the functions in the following order:


1. First *[LoadFile()](../../...md#loadFile_cstr_int_float_int)* function is called to place the file in the queue for loading and obtain an ***ID***, that will be used to identify a resource in subsequent operations.
2. After that, different operations can be performed:

  - *[ForceFile()](../../...md#forceFile_int_int)* to load the file immediately.
  - *[RemoveFile()](../../...md#removeFile_int_int)* to remove the file from the queue in case there is no need to load it any more of to remove a file from the list of loaded files if it was loaded but no longer needed.
  - *[CheckFile()](../../...md#checkFile_int_int)* to check if the given file was requested to be loaded via *loadFile()* or if it has already been loaded.


The same algorithm is true for:


- **Meshes** - see methods *[LoadMesh()](../../...md#loadMesh_cstr_int_float_int)*, *[ForceMesh()](../../...md#forceMesh_int_int)*, *[GetMesh()](../../...md#getMesh_int_Mesh)*, *[TakeMesh()](../../...md#takeMesh_int_Mesh)*, *[CheckMesh()](../../...md#checkMesh_int_int)*, and *[RemoveMesh()](../../...md#removeMesh_int_int)*.
- **Images** - see methods *[LoadImage()](../../...md#loadImage_cstr_int_float_int)*, *[ForceImage()](../../...md#forceImage_int_int)*, *[GetImage()](../../...md#getImage_int_Image)*, *[TakeImage()](../../...md#takeImage_int_Image)*, *[CheckImage()](../../...md#checkImage_int_int)*, and *[RemoveImage()](../../...md#removeImage_int_int)*.
- **Nodes** - see methods *[LoadNode()](../../...md#loadNode_cstr_int_float_int)*, *[ForceNode()](../../...md#forceNode_int_int)*, *[GetNode()](../../...md#getNode_int_Node)*, *[TakeNode()](../../...md#takeNode_int_Node)*, *[CheckNode()](../../...md#checkNode_int_int)*, and *[RemoveNode()](../../...md#removeNode_int_int)*.


To get a loaded resource (image, mesh, or node) the following 2 groups of methods can be used:


- **Get-methods** - these methods return the loaded resource:

  - *[GetImage()](../../...md#getImage_int_Image)*
  - *[GetMesh()](../../...md#getMesh_int_Mesh)*
  - *[GetNode()](../../...md#getNode_int_Node)*
- **Take-methods** - these methods return the loaded resource and remove it from the list of loaded ones:

  - *[TakeImage()](../../...md#takeImage_int_Image)*
  - *[TakeMesh()](../../...md#takeMesh_int_Mesh)*
  - *[TakeNode()](../../...md#takeNode_int_Node)*


For example:


```csharp
// specify relative paths to resources to be loaded to a queue
static string[] meshes = {
	"meshes/box.mesh",
	"meshes/capsule.mesh",
	"meshes/cbox.mesh",
};

struct AsyncLoadRequest
{
	public string name;
	public int id;
};

List<AsyncLoadRequest> mesh_load_requests;

private void Init()
{

	mesh_load_requests = new List<AsyncLoadRequest>();

	// enqueue meshes to load
	for (int i = 0; i < meshes.Length; ++i)
	{
		string name = meshes[i];
		AsyncLoadRequest request;
		request.name = name;
		request.id = AsyncQueue.LoadMesh(name);
		mesh_load_requests.Add(request);
	}

}

private void Update()
{
	// check mesh load requests
	for (int i = 0; i < mesh_load_requests.Count; ++i)
	{
		var r = mesh_load_requests[i];

		if (AsyncQueue.CheckMesh(r.id) == 0)
			continue;

		// remove the mesh from the list of the loaded meshes and print a message
		AsyncQueue.RemoveMesh(r.id);
		Unigine.Log.Message("Loaded mesh {0}\n", r.name);

		mesh_load_requests.Remove(r);
	}

}


```


### Handling Events


You can add "resource loaded" event handlers for files, images, meshes or nodes and perform certain actions as a resource is loaded. The example below shows how to add a "loaded" event handler for image resource, that reports the name and id of the loaded image.

> **Notice:** Do not call [***take-methods***](#take_methods) inside a handler function unless you are absolutely sure, that the resource is yours, otherwise internal engine managers will be forced to load it again and again every time. In such cases it is recommended to use [***get-methods***](#take_methods).


```csharp
// specify relative paths to resources to be loaded to a queue
static string[] textures = {
	"textures/black_d.texture",
	"textures/blue_d.texture",
	"textures/green_d.texture",
	"textures/orange_d.texture",
	"textures/red_d.texture",
	"textures/white_d.texture",
	"textures/yellow_d.texture",
};

private void Init()
{

	// enqueue textures to load
	for (int i = 0; i < textures.Length; ++i)
	AsyncQueue.LoadImage(textures[i]);
	// subscribing for the ImageLoaded event
	AsyncQueue.EventImageLoaded.Connect(image_loaded);

}

// an image loaded event handler function
private void image_loaded(string name, int id)
	{
		AsyncQueue.RemoveImage(id);
		Log.Message("Image {0} loaded, ID: {0}\n", name, id);
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


The multi-thread methods create *[CPUShader](../../../api/library/common/mt/class.cpushader_cs.md)* instances, while single-thread methods create *[CPUTask](../../../api/library/common/mt/class.cputask_cs.md)* instances. These classes are available directly only in C++, while *AsyncQueue* provides a unified interface for C++, C#, and UnigineScript. For more details on thread pools, task priority, and frame synchronization, see the **[UNIGINE Thread System](../../../code/fundamentals/thread_system/index.md)** article.


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
| **MAIN** = 0 | Main thread of the Engine. Required for any operation that interacts with scene objects or Engine state directly. Use this thread when executing callbacks that must safely modify or access scene elements. Typically used for dispatching final-stage results from background tasks. |
| **SYNC** = 1 | Sync pool thread. Tasks on this pool are frame-synchronized and the main thread contributes as a worker during synchronous operations. |
| **ASYNC** = 2 | General-purpose async thread used by the Engine for tasks like prefetching, landscape updates, data streaming, and other background operations. Overusing this thread may delay core Engine systems. |
| **COMMON** = 3 | Common pool thread. Workers in this pool can pick up tasks from multiple other pools (Sync, Async, Common), providing flexible load balancing across the thread system. |
| **CRITICAL** = 4 | Critical thread for high-priority tasks that must be processed as soon as possible. |
| **BACKGROUND** = 5 | Background thread with the lowest priority. Rarely used by the Engine itself, primarily intended for user-driven procedural operations such as geometry modification. Safe for long-running background tasks, as it does not interfere with streaming or other critical Engine systems. |
| **FILE_STREAM** = 6 | Dedicated thread for file I/O operations. Similar in priority to ASYNC, but separated to reduce contention between CPU work and disk access. Suitable for loading/saving geometry, streaming data from disk, or handling heavy I/O without affecting core async systems. Overloading this thread may impact streaming performance. |
| **GPU_STREAM** = 7 | Specialized thread with a dedicated command queue for transferring data from RAM to VRAM. Used to asynchronously create GPU resources (e.g., *[Texture](../../../api/library/rendering/class.texture_cs.md)*, *[MeshRender](../../../api/library/rendering/class.meshrender_cs.md)*) from corresponding RAM objects ( *[Image](../../../api/library/common/class.image_cs.md)*, *[Mesh](../../../api/library/rendering/class.mesh_cs.md)*). Ideal for implementing custom data streaming system or dynamic GPU data updates. |
| **NEW** = 8 | Creates a new isolated thread from the internal thread pool. Meant for custom user operations that must not block or interfere with existing Engine threads. Ideal for long-running or experimental tasks. This thread runs independently and does not impact Engine systems. |
| **NUM_ASYNC_THREADS** = 9 | Number of predefined async thread types. Used to validate or iterate over thread type constants. |

## ASYNC_PRIORITY

| Name | Description |
|---|---|
| **CRITICAL** = 0 | Highest priority. Tasks with this level are scheduled for execution before all others. |
| **HIGHEST** = 1 | Second highest priority level. |
| **ABOVENORMAL** = 2 | Above normal priority level. |
| **NORMAL** = 3 | Default priority level for general-purpose tasks. |
| **BELOWNORMAL** = 4 | Below normal priority level. |
| **LOWEST** = 5 | Second lowest priority level. |
| **BACKGROUND** = 6 | Background priority level for non-urgent tasks. |
| **IDLE** = 7 | Lowest priority. Tasks are only scheduled when no higher-priority tasks are pending. |

### Properties

## 🔒︎ int NumLoadedResources

The total number of currently loaded resources.
## 🔒︎ int NumLoadedNodes

The total number of loaded nodes.
## 🔒︎ int NumLoadedMeshes

The total number of loaded meshes.
## 🔒︎ int NumLoadedImages

The total number of loaded images.
## 🔒︎ int NumLoadedFiles

The total number of loaded files.
## 🔒︎ int NumLoadedData

The total number of loaded data segments.
## 🔒︎ int NumQueuedResources

The total number of queued resources waiting for background loading.
## 🔒︎ int NumQueuedNodes

The total number of queued nodes waiting for the background loading.
## 🔒︎ int NumQueuedMeshes

The total number of queued meshes waiting for the background loading.
## 🔒︎ int NumQueuedImages

The total number of queued images waiting for the background loading.
## 🔒︎ int NumQueuedFiles

The total number of queued files waiting for the background loading.
## 🔒︎ int NumQueuedData

The total number of queued data segments waiting for the background loading.
## 🔒︎ float TotalTime

The total time it took to process the loading queue.
## 🔒︎ Event<string, int> EventNodeLoaded

The event triggered when the node is loaded. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(string **name**, int **id**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the NodeLoaded event handler
void nodeloaded_event_handler(string name,  int id)
{
	Log.Message("\Handling NodeLoaded event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections nodeloaded_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
AsyncQueue.EventNodeLoaded.Connect(nodeloaded_event_connections, nodeloaded_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
AsyncQueue.EventNodeLoaded.Connect(nodeloaded_event_connections, (string name,  int id) => {
		Log.Message("Handling NodeLoaded event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
nodeloaded_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the NodeLoaded event with a handler function
AsyncQueue.EventNodeLoaded.Connect(nodeloaded_event_handler);

// remove subscription to the NodeLoaded event later by the handler function
AsyncQueue.EventNodeLoaded.Disconnect(nodeloaded_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection nodeloaded_event_connection;

// subscribe to the NodeLoaded event with a lambda handler function and keeping the connection
nodeloaded_event_connection = AsyncQueue.EventNodeLoaded.Connect((string name,  int id) => {
		Log.Message("Handling NodeLoaded event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
nodeloaded_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
nodeloaded_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
nodeloaded_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring NodeLoaded events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
AsyncQueue.EventNodeLoaded.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
AsyncQueue.EventNodeLoaded.Enabled = true;

```

</details>

## 🔒︎ Event<string, int> EventMeshLoaded

The event triggered when the mesh is loaded. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(string **name**, int **id**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the MeshLoaded event handler
void meshloaded_event_handler(string name,  int id)
{
	Log.Message("\Handling MeshLoaded event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections meshloaded_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
AsyncQueue.EventMeshLoaded.Connect(meshloaded_event_connections, meshloaded_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
AsyncQueue.EventMeshLoaded.Connect(meshloaded_event_connections, (string name,  int id) => {
		Log.Message("Handling MeshLoaded event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
meshloaded_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the MeshLoaded event with a handler function
AsyncQueue.EventMeshLoaded.Connect(meshloaded_event_handler);

// remove subscription to the MeshLoaded event later by the handler function
AsyncQueue.EventMeshLoaded.Disconnect(meshloaded_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection meshloaded_event_connection;

// subscribe to the MeshLoaded event with a lambda handler function and keeping the connection
meshloaded_event_connection = AsyncQueue.EventMeshLoaded.Connect((string name,  int id) => {
		Log.Message("Handling MeshLoaded event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
meshloaded_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
meshloaded_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
meshloaded_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring MeshLoaded events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
AsyncQueue.EventMeshLoaded.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
AsyncQueue.EventMeshLoaded.Enabled = true;

```

</details>

## 🔒︎ Event<string, int> EventImageLoaded

The event triggered when the image is loaded. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(string **name**, int **id**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the ImageLoaded event handler
void imageloaded_event_handler(string name,  int id)
{
	Log.Message("\Handling ImageLoaded event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections imageloaded_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
AsyncQueue.EventImageLoaded.Connect(imageloaded_event_connections, imageloaded_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
AsyncQueue.EventImageLoaded.Connect(imageloaded_event_connections, (string name,  int id) => {
		Log.Message("Handling ImageLoaded event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
imageloaded_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the ImageLoaded event with a handler function
AsyncQueue.EventImageLoaded.Connect(imageloaded_event_handler);

// remove subscription to the ImageLoaded event later by the handler function
AsyncQueue.EventImageLoaded.Disconnect(imageloaded_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection imageloaded_event_connection;

// subscribe to the ImageLoaded event with a lambda handler function and keeping the connection
imageloaded_event_connection = AsyncQueue.EventImageLoaded.Connect((string name,  int id) => {
		Log.Message("Handling ImageLoaded event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
imageloaded_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
imageloaded_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
imageloaded_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring ImageLoaded events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
AsyncQueue.EventImageLoaded.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
AsyncQueue.EventImageLoaded.Enabled = true;

```

</details>

## 🔒︎ Event<string, int> EventFileLoaded

The event triggered when the file is loaded. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(string **name**, int **id**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the FileLoaded event handler
void fileloaded_event_handler(string name,  int id)
{
	Log.Message("\Handling FileLoaded event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections fileloaded_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
AsyncQueue.EventFileLoaded.Connect(fileloaded_event_connections, fileloaded_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
AsyncQueue.EventFileLoaded.Connect(fileloaded_event_connections, (string name,  int id) => {
		Log.Message("Handling FileLoaded event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
fileloaded_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the FileLoaded event with a handler function
AsyncQueue.EventFileLoaded.Connect(fileloaded_event_handler);

// remove subscription to the FileLoaded event later by the handler function
AsyncQueue.EventFileLoaded.Disconnect(fileloaded_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection fileloaded_event_connection;

// subscribe to the FileLoaded event with a lambda handler function and keeping the connection
fileloaded_event_connection = AsyncQueue.EventFileLoaded.Connect((string name,  int id) => {
		Log.Message("Handling FileLoaded event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
fileloaded_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
fileloaded_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
fileloaded_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring FileLoaded events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
AsyncQueue.EventFileLoaded.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
AsyncQueue.EventFileLoaded.Enabled = true;

```

</details>

### Members

---

## Image GetImage ( int id )

Returns the image loaded by the specified operation.
> **Notice:** This method does not remove the image from the list of loaded ones. If you want the image to be removed from this list right after retrieving it, use the *[TakeImage()](../../...md#takeImage_int_Image)* method.


### Arguments

- *int* **id** - Loading operation identifier (see the *[LoadImage()](../../...md#loadImage_cstr_int_float_int)* method).

### Return value

Image instance.
## Mesh GetMesh ( int id )

Returns the mesh loaded by the specified operation.
> **Notice:** This method does not remove the mesh from the list of loaded ones. If you want the mesh to be removed from this list right after retrieving it, use the *[TakeMesh()](../../...md#takeMesh_int_Mesh)* method.


### Arguments

- *int* **id** - Loading operation identifier (see the *[LoadMesh()](../../...md#loadMesh_cstr_int_float_int)* method).

### Return value

Mesh instance.
## Node GetNode ( int id )

Returns the node loaded by the specified operation. If the node loaded by the specified operation consists of multiple objects, a new [dummy object](../../../api/library/objects/class.objectdummy_cs.md) to combine them is created and its smart pointer is returned.
> **Notice:** This method does not remove the node from the list of loaded ones. If you want the node to be removed from this list right after retrieving it, use the *[TakeNode()](../../...md#takeNode_int_Node)* method.


### Arguments

- *int* **id** - Loading operation identifier (see the *[LoadNode()](../../...md#loadNode_cstr_int_float_int)* method).

### Return value

Node instance.
## int GetNodes ( int id , Node [] OUT_nodes )

Puts the nodes loaded by the specified operation to the specified array. If the node loaded by the specified operation consists of multiple objects, they are put into the array.
> **Notice:** This method does not remove the nodes from the list of loaded ones. If you want the nodes to be removed from this list right after retrieving them, use the *[TakeNodes()](../../...md#takeNodes_int_VECNode_int)* method.


### Arguments

- *int* **id** - Loading operation identifier.
- *[Node](../../../api/library/nodes/class.node_cs.md)[]* **OUT_nodes** - Array of loaded nodes' instances. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

1 if the operation is successful; otherwise, 0.
## int CheckFile ( int id )

Returns a value indicating if the file is in the loading queue or already loaded.
### Arguments

- *int* **id** - Loading operation identifier (see the *[LoadFile()](../../...md#loadFile_cstr_int_float_int)* method).

### Return value

1 if the file is in the loading queue or already loaded; otherwise, 0.
## int CheckImage ( int id )

Returns a value indicating if the image is in the loading queue or already loaded.
### Arguments

- *int* **id** - Loading operation identifier (see the *[LoadImage()](../../...md#loadImage_cstr_int_float_int)* method).

### Return value

1 if the image is in the loading queue or already loaded; otherwise, 0.
## int CheckMesh ( int id )

Returns a value indicating if the mesh is in the loading queue or already loaded.
### Arguments

- *int* **id** - Loading operation identifier (see the *[LoadMesh()](../../...md#loadMesh_cstr_int_float_int)* method).

### Return value

1 if the mesh is in the loading queue or already loaded; otherwise, 0.
## int CheckNode ( int id )

Returns a value indicating if the node is in the loading queue or already loaded.
### Arguments

- *int* **id** - Loading operation identifier (see the *[LoadNode()](../../...md#loadNode_cstr_int_float_int)* method).

### Return value

1 if the node is in the loading queue or already loaded; otherwise, 0.
## int ForceFile ( int id )

Forces loading of the file. The specified file will be loaded right after the currently loading file (if any) is processed. All other file system operations are suspended until the forced file is loaded.
> **Notice:** The file won't be loaded immediately after calling the method as it can be large.


### Arguments

- *int* **id** - Loading operation identifier (see the *[LoadFile()](../../...md#loadFile_cstr_int_float_int)* method).

### Return value

1 if the file is loaded successfully; otherwise, 0.
## int ForceImage ( int id )

Forces loading of the image. The specified image will be loaded right after the currently loading image (if any) is processed. All other file system operations are suspended until the forced image is loaded.
> **Notice:** The image won't be loaded immediately after calling the method as it can be large.


### Arguments

- *int* **id** - Loading operation identifier (see the *[LoadImage()](../../...md#loadImage_cstr_int_float_int)* method).

### Return value

1 if the image is loaded successfully; otherwise, 0.
## int ForceMesh ( int id )

Forces loading of the mesh. The specified mesh will be loaded right after the currently loading mesh (if any) is processed. All other file system operations are suspended until the forced mesh is loaded.
> **Notice:** The mesh won't be loaded immediately after calling the method as it can be large.


### Arguments

- *int* **id** - Loading operation identifier (see the *[LoadMesh()](../../...md#loadMesh_cstr_int_float_int)* method).

### Return value

1 if the mesh is loaded successfully; otherwise, 0.
## int ForceNode ( int id )

Forces loading of the node. The specified node will be loaded right after the currently loading node (if any) is processed. All other file system operations are suspended until the forced node is loaded.
> **Notice:** The node won't be loaded immediately after calling the method as it can be large.


### Arguments

- *int* **id** - Loading operation identifier (see the *[LoadNode()](../../...md#loadNode_cstr_int_float_int)* method).

### Return value

1 if the node is loaded successfully; otherwise, 0.
## int LoadFile ( string name , int group = 0 , float weight = 0.0f )

Loads a given file with the specified group and priority to the thread.
### Arguments

- *string* **name** - Absolute or relative path to the file (including its name).
- *int* **group** - Priority group. Greater priority means faster loading. The default value is 0.
- *float* **weight** - Weight of the priority inside the group. Greater weight means faster loading inside the same priority group. The default value is 0.0f.

### Return value

Loading operation identifier.
## int LoadImage ( string name , int group = 0 , float weight = 0.0f )

Loads a given image file with the specified group and priority to the thread.
### Arguments

- *string* **name** - Absolute or relative path to the image file (including its name).
- *int* **group** - Priority group. Greater priority means faster loading. The default value is 0.
- *float* **weight** - Weight of the priority inside the group. Greater weight means faster loading inside the same priority group. The default value is 0.0f.

### Return value

Loading operation identifier.
## int LoadMesh ( string name , int group = 0 , float weight = 0.0f )

Loads a given `mesh`-file with the specified group and priority to the thread.
### Arguments

- *string* **name** - Absolute or relative path to the **.mesh* file (including its name).
- *int* **group** - Priority group. Greater priority means faster loading. The default value is 0.
- *float* **weight** - Weight of the priority inside the group. Greater weight means faster loading inside the same priority group. The default value is 0.0f.

### Return value

Loading operation identifier.
## int LoadNode ( string name , int group = 0 , float weight = 0.0f )

Loads a given `node`-file with the specified group and priority to the thread.
> **Notice:** In order to display such asynchronously loaded node, the [*updateEnabled()*](../../../api/library/nodes/class.node_cs.md#updateEnabled_void) method should be called for it **from the main thread**.


### Arguments

- *string* **name** - Absolute or relative path to the **.node* file (including its name).
- *int* **group** - Priority group. Greater priority means faster loading. The default value is 0.
- *float* **weight** - Weight of the priority inside the group. Greater weight means faster loading inside the same priority group. The default value is 0.0f.

### Return value

Loading operation identifier.
## int RemoveFile ( int id )

Removes the given file from the loading queue or from the list of loaded files, if it was already loaded.
> **Notice:** If the specified file is currently loading, it will be removed after the loading operation is completed.


### Arguments

- *int* **id** - Loading operation identifier (see the *[LoadFile()](../../...md#loadFile_cstr_int_float_int)* method).

### Return value

**1** if the file is successfully removed; otherwise, **0**.
## int RemoveImage ( int id )

Removes the given image from the loading queue or from the list of loaded images, if it was already loaded.
> **Notice:** If the specified image is currently loading, it will be removed after the loading operation is completed.


### Arguments

- *int* **id** - Loading operation identifier (see the *[LoadImage()](../../...md#loadImage_cstr_int_float_int)* method).

### Return value

**1** if the image is successfully removed; otherwise, **0**.
## int RemoveMesh ( int id )

Removes the given mesh from the loading queue or from the list of loaded meshes, if it was already loaded.
> **Notice:** If the specified mesh is currently loading, it will be removed after the loading operation is completed.


### Arguments

- *int* **id** - Loading operation identifier (see the *[LoadMesh()](../../...md#loadMesh_cstr_int_float_int)* method).

### Return value

**1** if the mesh is successfully removed; otherwise, **0**.
## int RemoveNode ( int id )

Removes the given node from the loading queue or from the list of loaded nodes, if it was already loaded.
> **Notice:** If the specified node is currently loading, it will be removed after the loading operation is completed. Nodes are removed with all their hierarchy.


### Arguments

- *int* **id** - Loading operation identifier (see the *[LoadNode()](../../...md#loadNode_cstr_int_float_int)* method).

### Return value

1 if the node is removed successfully; otherwise, 0.
## Image TakeImage ( int id )

Returns the image loaded by the specified operation and removes it from the list of loaded images.
### Arguments

- *int* **id** - Loading operation identifier (see the *[LoadImage()](../../...md#loadImage_cstr_int_float_int)* method).

### Return value

Image instance.
## Mesh TakeMesh ( int id )

Returns the mesh loaded by the specified operation and removes it from the list of loaded meshes.
### Arguments

- *int* **id** - Loading operation identifier (see the *[LoadMesh()](../../...md#loadMesh_cstr_int_float_int)* method).

### Return value

Mesh instance.
## Node TakeNode ( int id )

Returns the node loaded by the specified operation and removes it from the list of loaded nodes.
> **Notice:** Nodes are removed with all their hierarchy.


### Arguments

- *int* **id** - Loading operation identifier (see the *[LoadNode()](../../...md#loadNode_cstr_int_float_int)* method).

### Return value

Node instance.
## int TakeNodes ( int id , Node [] OUT_nodes )

Puts the nodes loaded by the specified operation to the specified array and removes them from the list of loaded nodes. If the node loaded by the specified operation consists of multiple objects, they are put into the array.
> **Notice:** Nodes are removed with all their hierarchy.


### Arguments

- *int* **id** - Loading operation identifier.
- *[Node](../../../api/library/nodes/class.node_cs.md)[]* **OUT_nodes** - Array of loaded nodes' instances. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

1 if the operation is successful; otherwise, 0.
## int LoadImageInfo ( string name , int group = 0 , float weight = 0.0f )

Loads file info (size format, etc.) for the specified image, group and priority to the thread.
### Arguments

- *string* **name** - Absolute or relative path to the image file (including its name).
- *int* **group** - Priority group. Greater priority means faster loading. The default value is 0.
- *float* **weight** - Weight of the priority inside the group. Greater weight means faster loading inside the same priority group. The default value is 0.0f.

### Return value

Loading operation identifier.
## void RunAsync ( AsyncQueue.ASYNC_THREAD thread_type , AsyncCallback callback , AsyncQueue.ASYNC_PRIORITY priority = Enum.AsyncQueue.ASYNC_PRIORITY.BACKGROUND )


Creates a [CPUTask](../../../api/library/common/mt/class.cputask_cs.md) that executes the specified callback on the given thread with [FrameSyncMode::Disabled](../../../api/library/common/mt/class.threadspool_cs.md#FrameSyncMode) (independent of the frame).


Use this method to offload operations such as geometry generation, file parsing, or image processing to a dedicated Engine-managed thread.


### Arguments

- *[AsyncQueue.ASYNC_THREAD](../../../api/library/filesystem/class.asyncqueue_cs.md#ASYNC_THREAD)* **thread_type** - [Type of thread](#ASYNC_THREAD) to run the task on.
- *AsyncCallback* **callback** - Callback function with the following signature: *void AsyncCallback()*.
- *[AsyncQueue.ASYNC_PRIORITY](../../../api/library/filesystem/class.asyncqueue_cs.md#ASYNC_PRIORITY)* **priority** - Priority of the task execution.

## void RunFrameAsyncMultiThread ( CallbackMultiThread callback , int num_threads = -1 )

Creates a [CPUShader](../../../api/library/common/mt/class.cpushader_cs.md) that executes the specified callback concurrently across multiple threads with [FrameSyncMode::Swap](../../../api/library/common/mt/class.threadspool_cs.md#FrameSyncMode) (synchronized with the frame). Does not block the calling thread. Intended for parallel execution of compute-heavy tasks that do not require immediate results but must complete within the current frame.
### Arguments

- *CallbackMultiThread* **callback** -  A function that takes two parameters: These parameters allow the task to be split into independent chunks, by assigning a portion of work to each thread. The function must have the following signature: ```csharp void CallbackMultiThread(int thread_index, int thread_count) ``` .

  - **int thread_index** - the index of the current thread (starting from 0).
  - **int thread_count** - the total number of threads executing the task.
- *int* **num_threads** - Number of threads to use. If set to -1, the engine selects an optimal number based on available CPU cores.

## void RunFrameAsyncMultiThread ( CallbackMultiThread callback , CallbackMultiThreadDone callback_done , int num_threads = -1 )

Creates a [CPUShader](../../../api/library/common/mt/class.cpushader_cs.md) that executes the specified callback concurrently across multiple threads with [FrameSyncMode::Swap](../../../api/library/common/mt/class.threadspool_cs.md#FrameSyncMode) (synchronized with the frame). Does not block the calling thread. Once all threads have finished, the callback_done is invoked. Intended for parallel execution of compute-heavy tasks that do not require immediate results but must complete within the current frame.
### Arguments

- *CallbackMultiThread* **callback** -  A function that takes two parameters: These parameters allow the task to be split into independent chunks, by assigning a portion of work to each thread. The function must have the following signature: ```csharp void CallbackMultiThread(int thread_index, int thread_count) ```

  - **int thread_index** - the index of the current thread (starting from 0).
  - **int thread_count** - the total number of threads executing the task.
- *CallbackMultiThreadDone* **callback_done** -  Callback to be called once all threaded executions of callback have completed. The function must have the following signature: ```csharp void CallbackMultiThreadDone(int thread_index, int thread_count) ``` .
- *int* **num_threads** - Number of threads to use. If set to -1, the engine selects an optimal number based on available CPU cores.

## void RunFrameSyncMultiThread ( CallbackMultiThread callback , int num_threads = -1 )

Creates a [CPUShader](../../../api/library/common/mt/class.cpushader_cs.md) that executes the specified callback concurrently across multiple threads with [FrameSyncMode::Swap](../../../api/library/common/mt/class.threadspool_cs.md#FrameSyncMode) (synchronized with the frame). Blocks the calling thread until all threads finish. Intended for parallel execution of compute-heavy tasks that must complete within the current frame.
### Arguments

- *CallbackMultiThread* **callback** -  A function that takes two parameters: These parameters allow the task to be split into independent chunks, by assigning a portion of work to each thread. The function must have the following signature: ```csharp void CallbackMultiThread(int thread_index, int thread_count) ```

  - **int thread_index** - the index of the current thread (starting from 0).
  - **int thread_count** - the total number of threads executing the task.
- *int* **num_threads** - Number of threads to use. If set to -1, the engine selects an optimal number based on available CPU cores.

## void RunAsyncMultiThread ( CallbackMultiThread callback , int num_threads = -1 )

Creates a [CPUShader](../../../api/library/common/mt/class.cpushader_cs.md) that executes the specified callback concurrently across multiple threads with [FrameSyncMode::Disabled](../../../api/library/common/mt/class.threadspool_cs.md#FrameSyncMode) (independent of the frame). Does not block the calling thread. Intended for parallel execution of compute-heavy tasks that do not require immediate results.
### Arguments

- *CallbackMultiThread* **callback** -  A function that takes two parameters: These parameters allow the task to be split into independent chunks, by assigning a portion of work to each thread. The function must have the following signature: ```csharp void CallbackMultiThread(int thread_index, int thread_count) ```

  - **int thread_index** - the index of the current thread (starting from 0).
  - **int thread_count** - the total number of threads executing the task.
- *int* **num_threads** - Number of threads to use. If set to -1, the engine selects an optimal number based on available CPU cores.

## void RunAsyncMultiThread ( CallbackMultiThread callback , CallbackMultiThreadDone callback_done , int num_threads = -1 )

Creates a [CPUShader](../../../api/library/common/mt/class.cpushader_cs.md) that executes the specified callback concurrently across multiple threads with [FrameSyncMode::Disabled](../../../api/library/common/mt/class.threadspool_cs.md#FrameSyncMode) (independent of the frame). Does not block the calling thread. Once all threads have finished, the callback_done is invoked. Intended for parallel execution of compute-heavy tasks that do not require immediate results.
### Arguments

- *CallbackMultiThread* **callback** -  A function that takes two parameters: These parameters allow the task to be split into independent chunks, by assigning a portion of work to each thread. The function must have the following signature: ```csharp void CallbackMultiThread(int thread_index, int thread_count) ```

  - **int thread_index** - the index of the current thread (starting from 0).
  - **int thread_count** - the total number of threads executing the task.
- *CallbackMultiThreadDone* **callback_done** -  Callback to be called once all threaded executions of callback have completed. The function must have the following signature: ```csharp void CallbackMultiThreadDone(int thread_index, int thread_count) ``` .
- *int* **num_threads** - Number of threads to use. If set to -1, the engine selects an optimal number based on available CPU cores.

## void RunSyncMultiThread ( CallbackMultiThread callback , int num_threads = -1 )

Creates a [CPUShader](../../../api/library/common/mt/class.cpushader_cs.md) that executes the specified callback concurrently across multiple threads with [FrameSyncMode::Disabled](../../../api/library/common/mt/class.threadspool_cs.md#FrameSyncMode) (independent of the frame). Blocks the calling thread until all threads finish.
### Arguments

- *CallbackMultiThread* **callback** -  A function that takes two parameters: These parameters allow the task to be split into independent chunks, by assigning a portion of work to each thread. The function must have the following signature: ```csharp void CallbackMultiThread(int thread_index, int thread_count) ```

  - **int thread_index** - the index of the current thread (starting from 0).
  - **int thread_count** - the total number of threads executing the task.
- *int* **num_threads** - Number of threads to use. If set to -1, the engine selects an optimal number based on available CPU cores.

## bool IsMainThread ( )

Checks if the current thread is the main thread.
### Return value

Returns true if called from the main thread; otherwise false.
## bool IsPoolSyncThread ( )

Checks if the current thread is a Sync pool worker thread.
### Return value

Returns true if called from a Sync pool thread; otherwise false.
## bool IsPoolAsyncThread ( )

Checks if the current thread is an Async pool worker thread.
### Return value

Returns true if called from an Async pool thread; otherwise false.
## bool IsPoolCriticalThread ( )

Checks if the current thread is a Critical pool worker thread.
### Return value

Returns true if called from a Critical pool thread; otherwise false.
## bool IsPoolCommonThread ( )

Checks if the current thread is a Common pool worker thread.
### Return value

Returns true if called from a Common pool thread; otherwise false.
## bool IsPoolBackgroundThread ( )

Checks if the current thread is a Background pool worker thread.
### Return value

Returns true if called from a Background pool thread; otherwise false.
## bool IsPoolRenderFlushThread ( )

Checks if the current thread is a RenderFlush pool worker thread.
### Return value

Returns true if called from a RenderFlush pool thread; otherwise false.
## bool IsPoolGPUStreamThread ( )

Checks if the current thread is a GPU stream pool worker thread.
### Return value

Returns true if called from a GPU stream pool thread; otherwise false.
## bool IsPoolFileStreamThread ( )

Checks if the current thread is a file stream pool worker thread.
### Return value

Returns true if called from a file stream pool thread; otherwise false.
