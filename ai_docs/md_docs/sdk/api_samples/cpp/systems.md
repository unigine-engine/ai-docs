# Multithreading & Performance Optimization

> **Notice:** The complete sample source code is available on GitHub:
> **[github.com/unigine-engine/cpp-api-samples](https://github.com/unigine-engine/cpp-api-samples)**.


## Asynchronous Meshes And Textures Loading

This sample shows how to load resources like meshes and textures in the background using the *[AsyncQueue](../../../api/library/filesystem/class.asyncqueue_cpp.md)* class. Files are loaded in a separate thread, so the main application stays responsive.


Meshes and textures are added to the loading queue, and the system listens for events to know when each resource is ready. When a mesh finishes loading, it's removed from the queue. For textures, an event handler is used to handle their completion. The sample also demonstrates how to group and manage resource requests, making it easier to control the loading process.


This kind of async loading is useful for streaming large levels, loading assets on demand in VR, or preloading data in simulations without freezing the interface.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/multi_threading_performance_optimization/asynchronous_meshes_and_textures_loading*
## Asynchronous Nodes Loading Stress-Test

This sample demonstrates how to asynchronously load large number of nodes using the *AsyncQueue* class while ensuring correct activation on the main thread.


In UNIGINE, world nodes must be created only from the main thread. To comply with this restriction and avoid blocking the main thread, the sample performs the initial node loading in a background thread, and then schedules a follow-up task on the main thread to finalize activation by calling *[updateEnabled()](../../../api/library/nodes/class.node_cpp.md#updateEnabled_void)* - a method that registers the node and its children in the world's spatial structure.


With the built-in Profiler enabled, you can observe how the engine handles increasing load smoothly and avoids frame spikes.


Refer to the *[AsyncQueue](../../../api/library/filesystem/class.asyncqueue_cpp.md)* class API for detailed information on available execution modes, thread types, and priorities.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/multi_threading_performance_optimization/asynchronous_nodes_loading_stress_test*
## Asynchronous Tasks Scheduler Configuration

This sample demonstates how to schedule and run different types of tasks using the *AsyncQueue class*. It shows how to execute operations in different thread types, control thread count, and choose whether tasks should complete within the current frame or run freely in the background.


- **Async** - non-blocking execution in a single thread. Useful for offloading tasks without stalling the main thread.
- **Async Multithread** - parallel execution across multiple threads. Each thread receives its own portion of work. Does not block the caller.
- **Frame-Async Multithread** - same as **Async Multithread**, but ensures all threads complete their tasks within the current frame.
- **Sync Multithread** - multi-threaded execution that blocks the calling thread until all threads finish.
- **Frame-Sync Multithread** - same as **Sync Multithread**, but ensures all threads complete their tasks within the current frame.


Refer to the *[AsyncQueue](../../../api/library/filesystem/class.asyncqueue_cpp.md)* class API for detailed information on available execution modes, thread types, and priorities.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/multi_threading_performance_optimization/asynchronous_tasks_scheduler_configuration*
## CPU Shader Usage

This sample demonstrates how to implement a custom CPU shader by inheriting from the *[CPUShader](../../../api/library/common/mt/class.cpushader_cpp.md)* class to perform multi-threaded data processing outside the main rendering loop.


The system updates multiple *[ObjectMeshCluster](../../../api/library/objects/class.objectmeshcluster_cpp.md)* instances asynchronously by using a helper *AsyncCluster* structure. Each cluster maintains two versions of itself: one for rendering and one for background updates. At the end of each frame, the two are swapped so the visible cluster always shows the latest result without stalling the frame.


This approach is particularly effective for real-time procedural animation, large-scale mesh updates, or any CPU-side logic that benefits from multithreading while remaining synchronized with rendering.


The parallel logic is encapsulated in a derived shader class *UpdateClusterCPUShader*, where the *process()* method is overridden to perform per-cluster updates. This method is automatically dispatched using *[CPUShader::runAsync()](../../../api/library/common/mt/class.cpushader_cpp.md#runAsync_int_void)*, allowing the workload to be spread across available CPU threads. Swap operations, visibility checks, and update decisions are handled independently for each cluster.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/multi_threading_performance_optimization/cpu_shader_usage*
## Custom Threads

This sample shows how to define and manage background threads in **UNIGINE** by inheriting from the *[Thread](../../../api/library/common/mt/class.thread_cpp.md)* class and overriding the *[process()](../../../api/library/common/mt/class.thread_cpp.md#process_void)* method.


Two custom thread types are demonstrated:


1. **InfiniteThread** - continuously outputs messages while running.
2. **CountedThread** - performs a finite number of iterations before completing.


Threads are started during component initialization and executed in parallel with the main engine loop. The infinite thread is explicitly stopped via *[stop()](../../../api/library/common/mt/class.thread_cpp.md#stop_bool)* once the counted thread completes all iterations.


This sample illustrates basic principles of multithreading and can serve as a foundation for offloading computations or *I/O* operations from the main thread.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/multi_threading_performance_optimization/custom_threads*
## Microprofiler Custom Counters

This sample demonstrates methods for tracking performance and estimating the time spent on different sections of code. For this purpose, it uses **[Microprofile](../../../tools/profiling/microprofile/index.md)**, an advanced CPU/GPU profiler with per-frame inspection support.


Profiling is crucial for identifying performance bottlenecks and optimizing code execution. This analysis helps you understand if any code sections negatively impact the project's speed.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/multi_threading_performance_optimization/microprofiler_custom_counters*
## Multiple Async Raycast Requests

This sample demonstrates how to launch and manage a large number of asynchronous ray-based intersection queries simultaneously.


The results are visualized in real time and latency statistics are displayed for performance analysis.


This approach is useful for stress-testing intersection systems, profiling async request latency, or building interactive tools relying on high-frequency spatial queries.


In this sample, an emitter object continuously rotates and moves vertically, casting rays in multiple directions (slices and stacks) to detect intersections with objects in the world. Each ray is handled asynchronously.


All active requests are monitored for completion. Once finished, the results (intersection points and normals) are visualized using *[Visualizer](../../../api/library/engine/class.visualizer_cpp.md)* tools. A latency histogram is computed based on how many frames passed between the request and response, and the results are displayed in the *UI*.


The sample uses double-buffering for safe multi-threaded access and demonstrates efficient scheduling of a high number of asynchronous operations.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/multi_threading_performance_optimization/multiple_async_raycast_requests*
## Single Async Raycast Request

This sample demonstrates how to perform a single asynchronous intersection query based on the user's mouse cursor position in the scene. The result includes the hit point and surface normal, which are visualized in the scene, along with latency information.


This setup demonstrates how to implement non-blocking intersection queries suitable for object selection or similar real-time input-driven interactions.


The sample demonstrates detection of intersections with all objects in the world using a combination of *[World::getIntersection()](../../../api/library/engine/class.world_cpp.md#getIntersection_Vec3_Vec3_int_Object)* and *[Landscape::getIntersection()](../../../api/library/objects/class.object_cpp.md#getIntersection_Vec3_Vec3_ObjectIntersectionTexCoord_int_int)* methods. A single ray is cast from the current camera position through the mouse cursor. If the ray intersects with any geometry, the hit point and surface normal are rendered using *[Visualizer](../../../api/library/engine/class.visualizer_cpp.md)*. Intersection queries are handled asynchronously. A callback processes the result and records latency in frames. The average and maximum latency values are updated in real time and shown in the sample *UI*.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/multi_threading_performance_optimization/single_async_raycast_request*
