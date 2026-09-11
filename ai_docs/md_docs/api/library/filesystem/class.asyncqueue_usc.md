# Unigine::AsyncQueue Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


Loading of files/meshes/images/nodes on demand is performed in a separate system thread, in addition to asynchronous content streaming. This class is used to control asynchronous data loading. It is possible to control loading queue by organizing files in groups and setting individual weights inside these groups.


To load files on demand, call the functions in the following order:


1. First *[loadFile()()](../../...md#loadFile_cstr_int_float_int)* function is called to place the file in the queue for loading and obtain an ***ID***, that will be used to identify a resource in subsequent operations.
2. After that, different operations can be performed:

  - *[forceFile()()](../../...md#forceFile_int_int)* to load the file immediately.
  - *[removeFile()()](../../...md#removeFile_int_int)* to remove the file from the queue in case there is no need to load it any more of to remove a file from the list of loaded files if it was loaded but no longer needed.
  - *[checkFile()()](../../...md#checkFile_int_int)* to check if the given file was requested to be loaded via *loadFile()* or if it has already been loaded.


The same algorithm is true for:


- **Meshes** - see methods *[loadMesh()()](../../...md#loadMesh_cstr_int_float_int)*, *[forceMesh()()](../../...md#forceMesh_int_int)*, *[getMesh()()](../../...md#getMesh_int_Mesh)*, *[takeMesh()()](../../...md#takeMesh_int_Mesh)*, *[checkMesh()()](../../...md#checkMesh_int_int)*, and *[removeMesh()()](../../...md#removeMesh_int_int)*.
- **Images** - see methods *[loadImage()()](../../...md#loadImage_cstr_int_float_int)*, *[forceImage()()](../../...md#forceImage_int_int)*, *[getImage()()](../../...md#getImage_int_Image)*, *[takeImage()()](../../...md#takeImage_int_Image)*, *[checkImage()()](../../...md#checkImage_int_int)*, and *[removeImage()()](../../...md#removeImage_int_int)*.
- **Nodes** - see methods *[loadNode()()](../../...md#loadNode_cstr_int_float_int)*, *[forceNode()()](../../...md#forceNode_int_int)*, *[getNode()()](../../...md#getNode_int_Node)*, *[takeNode()()](../../...md#takeNode_int_Node)*, *[checkNode()()](../../...md#checkNode_int_int)*, and *[removeNode()()](../../...md#removeNode_int_int)*.


To get a loaded resource (image, mesh, or node) the following 2 groups of methods can be used:


- **Get-methods** - these methods return the loaded resource:

  - *[getImage()()](../../...md#getImage_int_Image)*
  - *[getMesh()()](../../...md#getMesh_int_Mesh)*
  - *[getNode()()](../../...md#getNode_int_Node)*
- **Take-methods** - these methods return the loaded resource and remove it from the list of loaded ones:

  - *[takeImage()()](../../...md#takeImage_int_Image)*
  - *[takeMesh()()](../../...md#takeMesh_int_Mesh)*
  - *[takeNode()()](../../...md#takeNode_int_Node)*


For example:


```cpp
// specify a relative path when loading to the queue
engine.async.loadMesh("box.mesh");
// check if the mesh is loaded into the queue
Mesh box = engine.async.getMesh("box.mesh");
while(box == NULL) {
	box = engine.async.getMesh(id);
    // waiting...
}

```


### Handling Events


You can add "resource loaded" event handlers for files, images, meshes or nodes and perform certain actions as a resource is loaded. The example below shows how to add a "loaded" event handler for image resource, that reports the name and id of the loaded image.

> **Notice:** Do not call [***take-methods***](#take_methods) inside a handler function unless you are absolutely sure, that the resource is yours, otherwise internal engine managers will be forced to load it again and again every time. In such cases it is recommended to use [***get-methods***](#take_methods).


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


The multi-thread methods create *[CPUShader](../../../api/library/common/mt/class.cpushader_usc.md)* instances, while single-thread methods create *[CPUTask](../../../api/library/common/mt/class.cputask_usc.md)* instances. These classes are available directly only in C++, while *AsyncQueue* provides a unified interface for C++, C#, and UnigineScript. For more details on thread pools, task priority, and frame synchronization, see the **[UNIGINE Thread System](../../../code/fundamentals/thread_system/index.md)** article.


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
## static getEventNodeLoaded () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventMeshLoaded () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventImageLoaded () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventFileLoaded () const

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

## Image getImage ( int id )

Returns the image loaded by the specified operation.
> **Notice:** This method does not remove the image from the list of loaded ones. If you want the image to be removed from this list right after retrieving it, use the *[takeImage()()](../../...md#takeImage_int_Image)* method.


### Arguments

- *int* **id** - Loading operation identifier (see the *[loadImage()()](../../...md#loadImage_cstr_int_float_int)* method).

### Return value

Image instance.
## Mesh getMesh ( int id )

Returns the mesh loaded by the specified operation.
> **Notice:** This method does not remove the mesh from the list of loaded ones. If you want the mesh to be removed from this list right after retrieving it, use the *[takeMesh()()](../../...md#takeMesh_int_Mesh)* method.


### Arguments

- *int* **id** - Loading operation identifier (see the *[loadMesh()()](../../...md#loadMesh_cstr_int_float_int)* method).

### Return value

Mesh instance.
## Node getNode ( int id )

Returns the node loaded by the specified operation. If the node loaded by the specified operation consists of multiple objects, a new [dummy object](../../../api/library/objects/class.objectdummy_usc.md) to combine them is created and its smart pointer is returned.
> **Notice:** This method does not remove the node from the list of loaded ones. If you want the node to be removed from this list right after retrieving it, use the *[takeNode()()](../../...md#takeNode_int_Node)* method.


### Arguments

- *int* **id** - Loading operation identifier (see the *[loadNode()()](../../...md#loadNode_cstr_int_float_int)* method).

### Return value

Node instance.
## int checkFile ( int id )

Returns a value indicating if the file is in the loading queue or already loaded.
### Arguments

- *int* **id** - Loading operation identifier (see the *[loadFile()()](../../...md#loadFile_cstr_int_float_int)* method).

### Return value

1 if the file is in the loading queue or already loaded; otherwise, 0.
## int checkImage ( int id )

Returns a value indicating if the image is in the loading queue or already loaded.
### Arguments

- *int* **id** - Loading operation identifier (see the *[loadImage()()](../../...md#loadImage_cstr_int_float_int)* method).

### Return value

1 if the image is in the loading queue or already loaded; otherwise, 0.
## int checkMesh ( int id )

Returns a value indicating if the mesh is in the loading queue or already loaded.
### Arguments

- *int* **id** - Loading operation identifier (see the *[loadMesh()()](../../...md#loadMesh_cstr_int_float_int)* method).

### Return value

1 if the mesh is in the loading queue or already loaded; otherwise, 0.
## int checkNode ( int id )

Returns a value indicating if the node is in the loading queue or already loaded.
### Arguments

- *int* **id** - Loading operation identifier (see the *[loadNode()()](../../...md#loadNode_cstr_int_float_int)* method).

### Return value

1 if the node is in the loading queue or already loaded; otherwise, 0.
## int forceFile ( int id )

Forces loading of the file. The specified file will be loaded right after the currently loading file (if any) is processed. All other file system operations are suspended until the forced file is loaded.
> **Notice:** The file won't be loaded immediately after calling the method as it can be large.


### Arguments

- *int* **id** - Loading operation identifier (see the *[loadFile()()](../../...md#loadFile_cstr_int_float_int)* method).

### Return value

1 if the file is loaded successfully; otherwise, 0.
## int forceImage ( int id )

Forces loading of the image. The specified image will be loaded right after the currently loading image (if any) is processed. All other file system operations are suspended until the forced image is loaded.
> **Notice:** The image won't be loaded immediately after calling the method as it can be large.


### Arguments

- *int* **id** - Loading operation identifier (see the *[loadImage()()](../../...md#loadImage_cstr_int_float_int)* method).

### Return value

1 if the image is loaded successfully; otherwise, 0.
## int forceMesh ( int id )

Forces loading of the mesh. The specified mesh will be loaded right after the currently loading mesh (if any) is processed. All other file system operations are suspended until the forced mesh is loaded.
> **Notice:** The mesh won't be loaded immediately after calling the method as it can be large.


### Arguments

- *int* **id** - Loading operation identifier (see the *[loadMesh()()](../../...md#loadMesh_cstr_int_float_int)* method).

### Return value

1 if the mesh is loaded successfully; otherwise, 0.
## int forceNode ( int id )

Forces loading of the node. The specified node will be loaded right after the currently loading node (if any) is processed. All other file system operations are suspended until the forced node is loaded.
> **Notice:** The node won't be loaded immediately after calling the method as it can be large.


### Arguments

- *int* **id** - Loading operation identifier (see the *[loadNode()()](../../...md#loadNode_cstr_int_float_int)* method).

### Return value

1 if the node is loaded successfully; otherwise, 0.
## int loadFile ( string name , int group = 0 , float weight = 0.0f )

Loads a given file with the specified group and priority to the thread.
### Arguments

- *string* **name** - Absolute or relative path to the file (including its name).
- *int* **group** - Priority group. Greater priority means faster loading. The default value is 0.
- *float* **weight** - Weight of the priority inside the group. Greater weight means faster loading inside the same priority group. The default value is 0.0f.

### Return value

Loading operation identifier.
## int loadImage ( string name , int group = 0 , float weight = 0.0f )

Loads a given image file with the specified group and priority to the thread.
### Arguments

- *string* **name** - Absolute or relative path to the image file (including its name).
- *int* **group** - Priority group. Greater priority means faster loading. The default value is 0.
- *float* **weight** - Weight of the priority inside the group. Greater weight means faster loading inside the same priority group. The default value is 0.0f.

### Return value

Loading operation identifier.
## int loadMesh ( string name , int group = 0 , float weight = 0.0f )

Loads a given `mesh`-file with the specified group and priority to the thread.
### Arguments

- *string* **name** - Absolute or relative path to the **.mesh* file (including its name).
- *int* **group** - Priority group. Greater priority means faster loading. The default value is 0.
- *float* **weight** - Weight of the priority inside the group. Greater weight means faster loading inside the same priority group. The default value is 0.0f.

### Return value

Loading operation identifier.
## int loadNode ( string name , int group = 0 , float weight = 0.0f )

Loads a given `node`-file with the specified group and priority to the thread.
> **Notice:** In order to display such asynchronously loaded node, the [*updateEnabled()*](../../../api/library/nodes/class.node_usc.md#updateEnabled_void) method should be called for it **from the main thread**.


### Arguments

- *string* **name** - Absolute or relative path to the **.node* file (including its name).
- *int* **group** - Priority group. Greater priority means faster loading. The default value is 0.
- *float* **weight** - Weight of the priority inside the group. Greater weight means faster loading inside the same priority group. The default value is 0.0f.

### Return value

Loading operation identifier.
## int removeFile ( int id )

Removes the given file from the loading queue or from the list of loaded files, if it was already loaded.
> **Notice:** If the specified file is currently loading, it will be removed after the loading operation is completed.


### Arguments

- *int* **id** - Loading operation identifier (see the *[loadFile()()](../../...md#loadFile_cstr_int_float_int)* method).

### Return value

**1** if the file is successfully removed; otherwise, **0**.
## int removeImage ( int id )

Removes the given image from the loading queue or from the list of loaded images, if it was already loaded.
> **Notice:** If the specified image is currently loading, it will be removed after the loading operation is completed.


### Arguments

- *int* **id** - Loading operation identifier (see the *[loadImage()()](../../...md#loadImage_cstr_int_float_int)* method).

### Return value

**1** if the image is successfully removed; otherwise, **0**.
## int removeMesh ( int id )

Removes the given mesh from the loading queue or from the list of loaded meshes, if it was already loaded.
> **Notice:** If the specified mesh is currently loading, it will be removed after the loading operation is completed.


### Arguments

- *int* **id** - Loading operation identifier (see the *[loadMesh()()](../../...md#loadMesh_cstr_int_float_int)* method).

### Return value

**1** if the mesh is successfully removed; otherwise, **0**.
## int removeNode ( int id )

Removes the given node from the loading queue or from the list of loaded nodes, if it was already loaded.
> **Notice:** If the specified node is currently loading, it will be removed after the loading operation is completed. Nodes are removed with all their hierarchy.


### Arguments

- *int* **id** - Loading operation identifier (see the *[loadNode()()](../../...md#loadNode_cstr_int_float_int)* method).

### Return value

1 if the node is removed successfully; otherwise, 0.
## takeImage ( int id )

Returns the image loaded by the specified operation and removes it from the list of loaded images.
### Arguments

- *int* **id** - Loading operation identifier (see the *[loadImage()()](../../...md#loadImage_cstr_int_float_int)* method).

### Return value

Image instance.
## takeMesh ( int id )

Returns the mesh loaded by the specified operation and removes it from the list of loaded meshes.
### Arguments

- *int* **id** - Loading operation identifier (see the *[loadMesh()()](../../...md#loadMesh_cstr_int_float_int)* method).

### Return value

Mesh instance.
## takeNode ( int id )

Returns the node loaded by the specified operation and removes it from the list of loaded nodes.
> **Notice:** Nodes are removed with all their hierarchy.


### Arguments

- *int* **id** - Loading operation identifier (see the *[loadNode()()](../../...md#loadNode_cstr_int_float_int)* method).

### Return value

Node instance.
## int loadImageInfo ( string name , int group = 0 , float weight = 0.0f )

Loads file info (size format, etc.) for the specified image, group and priority to the thread.
### Arguments

- *string* **name** - Absolute or relative path to the image file (including its name).
- *int* **group** - Priority group. Greater priority means faster loading. The default value is 0.
- *float* **weight** - Weight of the priority inside the group. Greater weight means faster loading inside the same priority group. The default value is 0.0f.

### Return value

Loading operation identifier.
## void runAsyncMultiThread ( CallbackMultiThread callback , int num_threads = -1 )

Creates a [CPUShader](../../../api/library/common/mt/class.cpushader_usc.md) that executes the specified callback concurrently across multiple threads with [FrameSyncMode::Disabled](../../../api/library/common/mt/class.threadspool_usc.md#FrameSyncMode) (independent of the frame). Does not block the calling thread. Intended for parallel execution of compute-heavy tasks that do not require immediate results.
### Arguments

- *CallbackMultiThread* **callback**
- *int* **num_threads** - Number of threads to use. If set to -1, the engine selects an optimal number based on available CPU cores.

## void runAsyncMultiThread ( CallbackMultiThread callback , int num_threads = -1 )

Creates a [CPUShader](../../../api/library/common/mt/class.cpushader_usc.md) that executes the specified callback concurrently across multiple threads with [FrameSyncMode::Disabled](../../../api/library/common/mt/class.threadspool_usc.md#FrameSyncMode) (independent of the frame). Does not block the calling thread. Once all threads have finished, the callback_done is invoked. Intended for parallel execution of compute-heavy tasks that do not require immediate results.
### Arguments

- *CallbackMultiThread* **callback**
- *int* **num_threads** - Number of threads to use. If set to -1, the engine selects an optimal number based on available CPU cores.

## void runSyncMultiThread ( CallbackMultiThread callback , int num_threads = -1 )

Creates a [CPUShader](../../../api/library/common/mt/class.cpushader_usc.md) that executes the specified callback concurrently across multiple threads with [FrameSyncMode::Disabled](../../../api/library/common/mt/class.threadspool_usc.md#FrameSyncMode) (independent of the frame). Blocks the calling thread until all threads finish.
### Arguments

- *CallbackMultiThread* **callback**
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
