# Thread System in UNIGINE


The Engine performs thousands of operations every second - from rendering frames to updating physics and managing resources. Your own project code adds even more tasks to this workflow.


If all these operations were executed strictly one after another, the processing time would grow dramatically, and the application would quickly become too slow to deliver a smooth experience.


To prevent this, most of the Engine's jobs run in parallel on different threads, organized into **thread pools**. You can submit your own jobs to these pools as well.


In this article, we'll cover how threads and pools work, how to run your own parallel jobs, and how to profile their performance.


> **Notice:** For everyday development - writing components, game logic, and scripts - you don't need to think about threads at all. The Engine handles parallelism internally. This article is for advanced scenarios where you want to run your own parallel jobs on Engine thread pools or fine-tune threading performance.


## Threads


A thread is a lightweight unit of execution that can run independently from other parts of the code. Every thread in the Engine is represented by the **[Thread](../../../api/library/common/mt/class.thread_cpp.md)** class. You can create your own threads by inheriting from it and overriding the *[process()](../../../api/library/common/mt/class.thread_cpp.md#process_void)* method. The class provides lifecycle management (*[run()](../../../api/library/common/mt/class.thread_cpp.md#run_size_t_bool)*, *[stop()](../../../api/library/common/mt/class.thread_cpp.md#stop_bool)*, *[shutdown()](../../../api/library/common/mt/class.thread_cpp.md#shutdown_bool)*), sleeping and signaling (*[sleep()](../../../api/library/common/mt/class.thread_cpp.md#sleep_uint_void)*, *[signal()](../../../api/library/common/mt/class.thread_cpp.md#signal_void)*), and OS-level priority control.


### Thread Type


Each thread has a *[Type](../../../api/library/common/mt/class.thread_cpp.md#Type)* - a preset that provides default values for the thread **name** (shown in the debugger and [Microprofile](../../../tools/profiling/microprofile/index_cpp.md)), **OS priority**, and **display order** in [Microprofile](../../../tools/profiling/microprofile/index_cpp.md). All of these can be overridden individually. The type does not bind the thread to a pool or change its behavior.


The Engine uses about 20 built-in types internally (pool workers, sound, input, networking, etc.). The default type for new user-created threads is *Unknown*.


### Main Thread


The **Main** thread is where all Engine initialization, world loading, game logic callbacks, and the main loop happen. Some API methods can only be called from the main thread.


> **Notice:** For more details about thread-safe usage of the API, refer to the [Thread Safety in API](../../../code/fundamentals/thread_safety/index.md) article.


However, creating and managing threads manually is rarely needed. For most parallel workloads, the Engine provides a higher-level system: **thread pools** and **jobs**.


## Thread Pools


A thread pool is a group of pre-created worker threads managed by the Engine. Instead of creating and destroying threads every time a job needs to run, the pool keeps a set of active threads ready to execute work immediately.


When you or the Engine submit a job to a thread pool, it is placed into a shared queue. The first available worker thread takes the job and executes it. Once finished, the thread becomes free again and can take the next job from the queue.


All thread pools are managed by the **[ThreadsPool](../../../api/library/common/mt/class.threadspool_cpp.md)** class.


### Why Separate Pools?


If all parallel jobs shared a single pool of threads, a burst of heavy asynchronous work could occupy **all** available workers, leaving no room for small but time-critical synchronous jobs. Frame-sensitive systems such as physics and rendering would stall, waiting for a free thread - effectively running single-threaded and causing frame drops.


To prevent this, the Engine splits workers into dedicated pools - each with its own threads, priority, and purpose - so that one type of work cannot starve another.


The following diagram shows all pools created at Engine startup, their queues, and how jobs flow through the system:


![](thread_pool_architecture_unigine.svg)


Each pool contains two queues: **Frame-Bound** (for jobs that must finish within the current frame) and **Independent** (for jobs that can span multiple frames). Within each queue, jobs are organized by [priority](#task_priority) - higher-priority jobs are always picked up first. The details of these settings are covered in [Running Custom Jobs](#custom_tasks).


### Pool Details


| Pool | Thread Count | Description |
|---|---|---|
| **Sync Pool** | CPU cores - 1 | Pool for frame-synchronized jobs. Used by the Engine to distribute work that must complete within the current frame. The main thread also participates in Sync Pool work during synchronous execution, so the effective thread count is one higher than the number of dedicated pool threads. |
| **Async Pool** | CPU cores | General-purpose asynchronous pool used by the Engine for jobs like prefetching, landscape updates, data streaming, and other background operations. Overusing this pool may delay core engine systems. |
| **Critical Pool** | 1 | Pool for the most important jobs that should be completed as fast as possible. Has a dedicated thread that exclusively processes Critical jobs. Best suited for small, urgent operations (e.g., a forced intersection query against a landscape). Avoid submitting heavy or long-running work to this pool, as it can block other critical jobs. |
| **Common Pool** | 1 | General-purpose helper pool. Unlike other pools, the Common Pool worker is always active (spin-waiting) and can execute jobs from Sync, Async, and Common queues, acting as a flexible helper that assists wherever work is available. |
| **Background Pool** | 1 | Low-priority pool. Rarely used by the Engine itself, primarily intended for user-driven procedural operations such as geometry modification. Safe for long-running background jobs, as it does not interfere with streaming or other critical engine systems. |
| **File Stream Pool** | 1 | Dedicated pool for file I/O operations. Separated from the Async Pool to reduce contention between CPU work and disk access. Suitable for loading/saving geometry, streaming data from disk, or handling heavy I/O. Overloading this pool may impact streaming performance. |
| **GPU Stream Pool** | 1 | Specialized pool with a dedicated command queue for transferring data from RAM to VRAM. Used to asynchronously create GPU resources (e.g., Texture, MeshRender) from corresponding RAM objects (Image, Mesh). Ideal for implementing custom data streaming systems or dynamic GPU data updates. |
| **Render Flush Pool** | 1 | Pool for flushing GPU commands. |


> **Notice:** The number of threads in each pool can be configured at startup via [command-line options](../../../code/command_line.md#multithreading).


### Cross-Pool Execution


Each pool's threads normally execute only jobs from their own queue. The **Common** Pool is an exception - its worker can pick up jobs from the **Sync**, **Async**, and **Common** queues, acting as a flexible helper that assists wherever work is available.


Unlike other pool threads, the Common Pool worker is always active (*spin-waiting*) rather than sleeping, so it responds to new work immediately.


The **main thread** also helps the pool system: it participates as a Sync Pool worker during *[runSync()](../../../api/library/common/mt/class.cpushader_cpp.md#runSync_int_void)* calls, processes tasks submitted via *[CPUTask::runMainThread()](../../../api/library/common/mt/class.cputask_cpp.md#runMainThread_void)*, and helps drain frame-bound queues of all pools at *[Engine::swap()](../../../code/fundamentals/execution_sequence/main_loop.md#swap)*.


## Thread Priority


**Thread priority** is an OS-level setting that tells the operating system how to schedule CPU time between threads. A higher-priority thread gets more CPU time when the system is under load. This is set via *[Thread::setPriority()](../../../api/library/common/mt/class.thread_cpp.md#setPriority_int_int)*. Each thread type is assigned a default OS priority at creation:


| Value | Level | Thread Types |
|---|---|---|
| 1 | Above Normal | PoolSync, PoolAsync, PoolCritical, PoolCommon |
| 0 | Normal | Main, PoolRenderFlush, GenericUser, USC, Unknown |
| -1 | Below Normal | Monitor, Ultraleap, Network |
| -2 | Lowest | PoolBackground, PoolFileStream, PoolGPUStream, Sound, Input, Dump |
| -3 | Idle | WakeUp |


> **Notice:** The full range accepted by *[Thread::setPriority()](../../../api/library/common/mt/class.thread_cpp.md#setPriority_int_int)* is -3 to 3, where 2 maps to **Highest** and 3 to **Time Critical**. These higher levels are not used by default but can be set manually if needed.


In most cases, you don't need to change thread priority - the defaults are carefully tuned. If you do change it, the effect depends on overall system load: on a lightly loaded system, all threads get enough time regardless of priority.


## Running Custom Jobs


UNIGINE provides several ways to run your own code on Engine threads. The two primary mechanisms are **[CPUShader](../../../api/library/common/mt/class.cpushader_cpp.md)** and **[CPUTask](../../../api/library/common/mt/class.cputask_cpp.md)**. Both let you submit work to thread pools, but differ in how they distribute it:


- **[CPUShader](../../../api/library/common/mt/class.cpushader_cpp.md)** - distributes work across **multiple threads** in parallel. Each thread receives its index and the total thread count, so you can split the workload between them.
- **[CPUTask](../../../api/library/common/mt/class.cputask_cpp.md)** - runs on a **single thread** within a chosen pool. The job executes once on the assigned worker thread.


Here is how the two classes compare:


|  | **CPUShader** | **CPUTask** |
|---|---|---|
| **Pool** | *[PoolType](../../../api/library/common/mt/class.cpushader_cpp.md#PoolType)* set in constructor (Auto, Sync, Async, etc.). | Chosen by calling the corresponding *[run*Thread()](../../../api/library/common/mt/class.cputask_cpp.md#run_PoolThread_void)* method (one per pool + Main). |
| **Execution** | Runs on **multiple threads** in parallel. *[runSync()](../../../api/library/common/mt/class.cpushader_cpp.md#runSync_int_void)* blocks the calling thread, *[runAsync()](../../../api/library/common/mt/class.cpushader_cpp.md#runAsync_int_void)* returns immediately. | Runs on a **single thread**. Always non-blocking. |
| **[Frame Sync](#frame_sync)** | Awaited at the [swap stage](../../../code/fundamentals/execution_sequence/main_loop.md#swap) by default. | Not awaited at the [swap stage](../../../code/fundamentals/execution_sequence/main_loop.md#swap) by default. |
| **[Priority](#task_priority)** | 8 levels (Critical .. Idle). Default: *Normal*. |  |
| **Wait Mode** | What the calling thread does while blocked: *Auto* (spin-wait) or *Full* (helps the pool by executing other jobs). Default: *Auto*. | N/A (always non-blocking). |


### Job Priority


Both **CPUShader** and **CPUTask** accept a *Priority* value that determines the order in which jobs are picked up within the same pool. There are 8 priority levels:


| Priority | Value |
|---|---|
| Critical | 0 (highest) |
| Highest | 1 |
| AboveNormal | 2 |
| Normal | 3 (default) |
| BelowNormal | 4 |
| Lowest | 5 |
| Background | 6 |
| Idle | 7 (lowest) |


> **Notice:** **Job priority** is independent from **[thread priority](#thread_priority)**. Thread priority affects how much CPU time the OS gives to the thread; job priority affects the order of jobs in the queue.
>
>
> A job with *Critical* priority in the Background Pool will be picked up before other Background jobs - but it still runs on a low-priority thread. If you need both fast pickup and fast execution, submit the job to a pool with [high thread priority](#thread_priority).


### Frame Synchronization


Both **CPUShader** and **CPUTask** support a *FrameSyncMode* setting that controls whether the Engine waits for the job to finish before completing the current frame:


- *FrameSyncMode::Disabled* - the job runs independently of the frame cycle. The Engine does not wait for it at any synchronization point. This is the default for **CPUTask**.
- *FrameSyncMode::Swap* - the job is tied to the current frame. *[Swap stage](../../../code/fundamentals/execution_sequence/main_loop.md#swap)* will block until all frame-synchronized jobs have completed. This is the default for **CPUShader**.


Use *FrameSyncMode::Swap* when the results of the job must be available before the next frame begins (e.g., physics calculations, visibility updates). Use *FrameSyncMode::Disabled* for fire-and-forget jobs that can span multiple frames.


Each pool maintains two internal queues based on these modes. A worker iterates through [priority levels](#task_priority) from highest to lowest. At each level, it checks the frame-bound queue first, then the independent queue, before moving on to the next level. This means a high-priority independent job will be picked up before a low-priority frame-bound one - priority always comes first.


The following diagram shows how jobs are organized inside a single pool and the order in which they become available to workers:


![](job_queue.svg)

*CPUTasksare done beforeCPUShaders*


### CPUShader: Multi-Thread Jobs


Use **[CPUShader](../../../api/library/common/mt/class.cpushader_cpp.md)** when you need to distribute work across multiple threads in parallel. Your processing function receives the thread index and total thread count, so you can split work between them.


#### Quick Start with Helpers


The easiest way to run parallel work is with template helper functions - no subclassing needed:


<details>
<summary>Details</summary>

```cpp
#include <UnigineThread.h>
using namespace Unigine;

// Simplest: synchronous parallel work (blocks until done)
runSyncMultiThreadFunc([](CPUShader *shader, int thread_num, int num_threads)
{
	// Split work using thread_num / num_threads
});

// Asynchronous: returns a pointer you run and manage yourself
CPUShader *shader = makeCPUShaderStateless(
	[](CPUShader *shader, int thread_num, int num_threads)
	{
		// Your parallel work here
	}
);
shader->runAsync(-1);
// ... do other work ...
shader->wait();
delete shader;

```

</details>


Available helpers:


- *[runSyncMultiThreadFunc()](../../../api/library/common/class.unigine.namespace_cpp.md#runSyncMultiThreadFunc_Process_int)* - the simplest option. Runs work synchronously on multiple threads and blocks until all finish.
- *[makeCPUShaderStateless()](../../../api/library/common/class.unigine.namespace_cpp.md#makeCPUShaderStateless_Process)* - creates a heap-allocated shader without shared state. Returns a pointer you can run asynchronously. Must be deleted manually.
- *[makeScopeCPUShaderStateless()](../../../api/library/common/class.unigine.namespace_cpp.md#makeScopeCPUShaderStateless_Process)* - same as above but stack-allocated. Cleans up automatically when it goes out of scope.
- *[makeCPUShader<State>(process, ...)](../../../api/library/common/class.unigine.namespace_cpp.md#makeCPUShader_State_Process)* - creates a shader with shared state of the given type. Must be deleted manually.
- *[makeCPUShader<State>(process, destroy, ...)](../../../api/library/common/class.unigine.namespace_cpp.md#makeCPUShader_State_Process_Destroy)* - same as above, with a destroy callback for state cleanup.


All helpers accept optional parameters for [pool](#thread_pools), [priority](#task_priority), [frame sync](#frame_sync), and wait mode - defaults work for most cases.


Call *[runSync()](../../../api/library/common/mt/class.cpushader_cpp.md#runSync_int_void)* to block until all workers finish, or *[runAsync()](../../../api/library/common/mt/class.cpushader_cpp.md#runAsync_int_void)* to return immediately and call *[wait()](../../../api/library/common/mt/class.cpushader_cpp.md#wait_void)* later.


> **Notice:** When called from a non-main thread, work always goes to the Async Pool - even if *PoolType::Sync* is set explicitly.


#### Manual Subclassing


For full control - custom *[done()](../../../api/library/common/mt/class.cpushader_cpp.md#done_void)* callbacks, reusable shaders, or complex state management - inherit from **CPUShader** directly:


<details>
<summary>Details</summary>

```cpp
#include <UnigineThread.h>
using namespace Unigine;

class MyShader : public CPUShader
{
public:
	MyShader()
		: CPUShader(PoolType::Async, Priority::Normal, FrameSyncMode::Swap)
	{}

	void process(int thread_num, int num_threads) override
	{
		int chunk_size = total_items / num_threads;
		int start = thread_num * chunk_size;
		int end = (thread_num == num_threads - 1) ? total_items : start + chunk_size;

		for (int i = start; i < end; i++)
		{
			// Process item i
		}
	}

	void done() override
	{
		// Called on the last thread to finish - chain follow-up work here
	}

private:
	int total_items = 1000;
};

// Usage:
MyShader shader;
shader.runAsync(4);  // Run on 4 threads
shader.wait();       // Wait for completion

```

</details>


When all threads finish, the virtual *[done()](../../../api/library/common/mt/class.cpushader_cpp.md#done_void)* callback fires on the last thread, allowing you to chain work without returning to the main thread.


### CPUTask: Single-Thread Jobs


Use **[CPUTask](../../../api/library/common/mt/class.cputask_cpp.md)** when your work should run on a single worker thread in a specific pool.


#### Quick Start with Helpers


The easiest way to create a task is with the *[makeCPUTask()](../../../api/library/common/class.unigine.namespace_cpp.md#makeCPUTask_Callable_Priority_FrameSyncMode)* helper:


<details>
<summary>Details</summary>

```cpp
#include <UnigineThread.h>
using namespace Unigine;

CPUTask *task = makeCPUTask([](CPUTask *t)
{
	// Your work here
});
task->runAsyncThread();   // Submit to the Async Pool

```

</details>


An optional destroy callback can be passed as the second argument for cleanup when the task is deleted. Both variants accept optional [priority](#task_priority) and [frame sync](#frame_sync) parameters.


Each [pool](#thread_pools) has a matching *run*Thread()* method (e.g. *[runAsyncThread()](../../../api/library/common/mt/class.cputask_cpp.md#runAsyncThread_void)*, *[runSyncThread()](../../../api/library/common/mt/class.cputask_cpp.md#runSyncThread_void)*). Use *[runMainThread()](../../../api/library/common/mt/class.cputask_cpp.md#runMainThread_void)* to queue the task for the main thread. See **[CPUTask](../../../api/library/common/mt/class.cputask_cpp.md)** for the full list.


> **Notice:** All *run*Thread()* calls are non-blocking - they put the task into the pool queue and return immediately.


#### Manual Subclassing


For reusable tasks or complex logic, inherit from **CPUTask** directly:


<details>
<summary>Details</summary>

```cpp
#include <UnigineThread.h>
using namespace Unigine;

class MyTask : public CPUTask
{
public:
	void process() override
	{
		// Your work here
	}
};

// Usage:
MyTask *task = new MyTask();
task->runAsyncThread();

```

</details>


### Cooperative Job Processing


Inside a long-running job, you can voluntarily help the pool process other pending jobs using two static methods of **[ThreadsPool](../../../api/library/common/mt/class.threadspool_cpp.md)**:


- *[yield()](../../../api/library/common/mt/class.threadspool_cpp.md#yield_int_int_bool_bool)* - picks up and executes one pending job from the calling thread's own pool. Safe to use anywhere - a Sync thread will only take Sync work, a Background thread only Background work, and so on.
- *[runProcess()](../../../api/library/common/mt/class.threadspool_cpp.md#runProcess_int_int_bool_bool)* - lower-level variant where you explicitly specify which pools and priority levels to pull work from.


Call *[yield()](../../../api/library/common/mt/class.threadspool_cpp.md#yield_int_int_bool_bool)* inside long-running jobs to help the Engine process other work while you wait for something. This keeps the thread useful instead of blocking idle.


### Memory Management


Neither **CPUShader** nor **CPUTask** are deleted automatically after execution. How you handle cleanup depends on how the object was created:


- *[runSyncMultiThreadFunc()](../../../api/library/common/class.unigine.namespace_cpp.md#runSyncMultiThreadFunc_Process_int)* and *[makeScopeCPUShaderStateless()](../../../api/library/common/class.unigine.namespace_cpp.md#makeScopeCPUShaderStateless_Process)* - stack-allocated, no cleanup needed.
- *[makeCPUShaderStateless()](../../../api/library/common/class.unigine.namespace_cpp.md#makeCPUShaderStateless_Process)*, *[makeCPUShader()](../../../api/library/common/class.unigine.namespace_cpp.md#makeCPUShader_State_Process)*, *[makeCPUTask()](../../../api/library/common/class.unigine.namespace_cpp.md#makeCPUTask_Callable_Priority_FrameSyncMode)* - heap-allocated, call *delete* when done.
- For **CPUTask**, you can also call *[destroy()](../../../api/library/common/mt/class.cputask_cpp.md#destroy_void)* instead of *delete* to schedule asynchronous deletion via the Engine's internal destroy queue.


> **Notice:** The **CPUShader** destructor calls *[wait()](../../../api/library/common/mt/class.cpushader_cpp.md#wait_void)* internally, so calling *delete* on a running shader is safe - it will block until all threads finish.


When subclassing **CPUShader**, you can set the *protected* field *auto_destroy = true* to make the shader delete itself after all threads complete (fire-and-forget pattern). Check the current state with *[isAutoDestroy()](../../../api/library/common/mt/class.cpushader_cpp.md#isAutoDestroy_bool)*.


### Standalone Threads


If you need to run arbitrary code on a completely separate thread (not bound to any pool), use *[ThreadsPool::runNewThread()](../../../api/library/common/mt/class.threadspool_cpp.md#runNewThread_CallbackBase_ptr_int_void)*. This creates a new **GenericUser** thread, executes your callback, and cleans up automatically:


```cpp
#include <UnigineThread.h>
#include <UnigineCallback.h>
using namespace Unigine;

void myFunction()
{
	// Long-running work on a separate thread
}

// Create a new thread and run the callback
ThreadsPool::runNewThread(MakeCallback(myFunction));

```


This approach is best for isolated, long-running operations that don't need to interact with Engine pool scheduling.


### AsyncQueue (C# / UnigineScript)


The **[AsyncQueue](../../../api/library/filesystem/class.asyncqueue_cpp.md)** class is the primary way to run custom jobs on thread pools from **C#** and **UnigineScript**. Its multi-thread methods create **[CPUShader](../../../api/library/common/mt/class.cpushader_cpp.md)** instances, while single-thread methods create **[CPUTask](../../../api/library/common/mt/class.cputask_cpp.md)** instances - the same primitives described above, but accessible through a unified cross-language interface.


**AsyncQueue** also provides asynchronous resource loading (images, meshes, nodes) with its own loading queue.


> **Notice:** Do not confuse **AsyncQueue** (a resource loading utility using a **GenericUser** thread) with the **Async Pool** (a general-purpose thread pool for Engine jobs). They are separate systems.


For full details, see the [AsyncQueue](../../../api/library/filesystem/class.asyncqueue_cpp.md) class documentation.


## Profiling with Microprofile


[Microprofile](../../../tools/profiling/microprofile/index_cpp.md) is a built-in profiling tool that lets you visualize the execution timeline of all threads and see where time is being spent. Every Engine thread appears in Microprofile with its name - if a custom name was set via the **[Thread](../../../api/library/common/mt/class.thread_cpp.md)** constructor, that name is displayed; otherwise the thread type is shown.


To mark sections of your code in Microprofile, use the following macros and API calls:


```cpp
#include <UnigineProfiler.h>

void myFunction()
{
	// Automatically profiles the entire function
	UNIGINE_PROFILER_FUNCTION;

	// Or profile a specific section manually
	int id = Profiler::beginMicro("my_section_name");
	// ... work ...
	Profiler::endMicro(id);
}

```


For example, the following code runs a **[CPUShader](../../../api/library/common/mt/class.cpushader_cpp.md)** on 4 threads with a custom [Microprofile](../../../tools/profiling/microprofile/index_cpp.md) marker:


```cpp
auto shader = makeScopeCPUShaderStateless(
	[](CPUShader* self, int thread_num, int num_threads)
	{
		int id = Profiler::beginMicro("MyCustomJob");
		Thread::sleep(200);
		Profiler::endMicro(id);
	},
	CPUShader::PoolType::Sync
);
shader.runSync(4);

```


![](cpu_shader_in_microprofile.png)


In the *[Microprofile](../../../tools/profiling/microprofile/index_cpp.md)* screenshot above: a custom job ("**MyCustomJob**") dispatched to the Sync pool via *runSync(4)*, running on 4 threads:

- **2 Pool Sync Threads** - workers from the target pool.
- **Main Thread** - *runSync()* executes one chunk on the calling thread.
- **Pool Common Thread** - picked up a chunk via [cross-pool execution](#cross_pool).


## See Also


- [Thread Safety in API](../../../code/fundamentals/thread_safety/index.md)
- [Thread Class](../../../api/library/common/mt/class.thread_cpp.md)
- [ThreadsPool Class](../../../api/library/common/mt/class.threadspool_cpp.md)
- [CPUShader Class](../../../api/library/common/mt/class.cpushader_cpp.md)
- [CPUTask Class](../../../api/library/common/mt/class.cputask_cpp.md)
- [Engine Main Loop](../../../code/fundamentals/execution_sequence/main_loop.md)
- [Microprofile](../../../tools/profiling/microprofile/index_cpp.md)
