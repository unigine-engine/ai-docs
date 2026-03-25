# Multithreading & Performance Optimization

> **Notice:** The complete sample source code is available on GitHub:
> **[github.com/unigine-engine/csharp-component-samples](https://github.com/unigine-engine/csharp-component-samples)**.


## Asynchronous Meshes And Textures Loading

This sample shows how to load resources like meshes and textures in the background using the *[AsyncQueue](../../../api/library/filesystem/class.asyncqueue_cpp.md)* class. Files are loaded in a separate thread, so the main application stays responsive.


Meshes and textures are added to the loading queue, and the system listens for events to know when each resource is ready. When a mesh finishes loading, it's removed from the queue. For textures, an event handler is used to handle their completion. The sample also demonstrates how to group and manage resource requests, making it easier to control the loading process.


This kind of async loading is useful for streaming large levels, loading assets on demand in VR, or preloading data in simulations without freezing the interface.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/multi_threading_performance_optimization/asynchronous_meshes_and_textures_loading*
## Asynchronous Nodes Loading Stress-Test

This sample demonstrates how to asynchronously load large number of nodes using the *AsyncQueue* class while ensuring correct activation on the main thread.


In UNIGINE, world nodes must be created only from the main thread. To comply with this restriction and avoid blocking the main thread, the sample performs the initial node loading in a background thread, and then schedules a follow-up task on the main thread to finalize activation by calling *[updateEnabled()](../../../api/library/nodes/class.node_cpp.md#updateEnabled_void)* - a method that registers the node and its children in the world's spatial structure.


With the built-in Profiler enabled, you can observe how the engine handles increasing load smoothly and avoids frame spikes.


Refer to the *[AsyncQueue](../../../api/library/filesystem/class.asyncqueue_cpp.md)* class API for detailed information on available execution modes, thread types, and priorities.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/multi_threading_performance_optimization/asynchronous_nodes_loading_stress_test*
## Asynchronous Tasks Scheduler Configuration

This sample demonstates how to schedule and run different types of tasks using the *AsyncQueue class*. It shows how to execute operations in different thread types, control thread count, and choose whether tasks should complete within the current frame or run freely in the background.


- **Async** - non-blocking execution in a single thread. Useful for offloading tasks without stalling the main thread.
- **Async Multithread** - parallel execution across multiple threads. Each thread receives its own portion of work. Does not block the caller.
- **Frame-Async Multithread** - same as **Async Multithread**, but ensures all threads complete their tasks within the current frame.
- **Sync Multithread** - multi-threaded execution that blocks the calling thread until all threads finish.
- **Frame-Sync Multithread** - same as **Sync Multithread**, but ensures all threads complete their tasks within the current frame.


Refer to the *[AsyncQueue](../../../api/library/filesystem/class.asyncqueue_cpp.md)* class API for detailed information on available execution modes, thread types, and priorities.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/multi_threading_performance_optimization/asynchronous_tasks_scheduler_configuration*
## Microprofiler Custom Counters

This sample demonstrates methods for tracking performance and estimating the time spent on different sections of code. For this purpose, it uses **[Microprofile](../../../tools/profiling/microprofile/index.md)**, an advanced CPU/GPU profiler with per-frame inspection support.

Profiling is crucial for identifying performance bottlenecks and optimizing code execution. This analysis helps you understand if any code sections negatively impact the project's speed.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/multi_threading_performance_optimization/microprofiler_custom_counters*
