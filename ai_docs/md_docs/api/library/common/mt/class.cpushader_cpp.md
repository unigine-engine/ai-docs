# Unigine::CPUShader Class (CPP)

**Header:** #include <UnigineThread.h>


This class is used to create a custom CPU shader, for example, to implement multi-threaded mesh cluster update. Your custom CPU shader must be inherited from this class. The sample is included in the SDK.


Frame-synchronized shaders ([FrameSyncMode::Swap](../../../../api/library/common/mt/class.threadspool_cpp.md#FrameSyncMode_Swap)) are drained at the end-of-frame stage via [ThreadsPool::frameSync()](../../../../api/library/common/mt/class.threadspool_cpp.md#frameSync_void), so the Engine waits for them to complete before proceeding to the next frame.


Here is an example of implementing a custom CPU shader:


```cpp
struct UpdateClustersCPUShader: public CPUShader
{
	UpdateClustersCPUShader() {}
	virtual ~UpdateClustersCPUShader()
	{
		// wait until all asynchronous operations are completed
		wait();
	}

	Vector<AsyncCluster> clusters;

	volatile int counter{0};

	// overriding the process method to perform our calculations
	void process(int thread_num, int threads_count) override
	{
		UNIGINE_PROFILER_FUNCTION;

		while (true)
		{
			int num = AtomicAdd(&counter, 1);
			if (num >= clusters.size())
				break;
			clusters[num].update();
		}
	}

	void run()
	{
		for (auto &c : clusters)
			c.swap();

		counter = 0;

		// running shader code in asynchronous mode
		runAsync();
	}
};

```


## CPUShader Class

### Enums

## PoolType

| Name | Description |
|---|---|
| **Auto** = 0 | Automatic pool selection: [Sync](#PoolType_Sync) when called from the main thread, [Async](#PoolType_Async) otherwise. |
| **Async** = 1 | Async worker pool. |
| **Sync** = 2 | Sync worker pool. |
| **Critical** = 3 | Critical worker pool. |
| **Common** = 4 | Common worker pool. |
| **Background** = 5 | Background worker pool. |
| **RenderFlush** = 6 | Render-flush worker pool. |
| **FileStream** = 7 | File streaming worker pool. |
| **GPUStream** = 8 | GPU streaming worker pool. |

## WaitMode

| Name | Description |
|---|---|
| **Auto** = 0 | Simple spin-wait until the shader finishes. |
| **Full** = 1 | Actively processes other tasks from the same pool while waiting for the shader to finish. |

### Members

---

## CPUShader ( )

Creates a new CPUShader instance.
## CPUShader ( PoolType pool_ , Priority priority_ , FrameSyncMode frame_sync_ )

Creates a new CPUShader instance.
### Arguments

- *[PoolType](/api/library/common/mt/class.cpushader#PoolType)* **pool_** - Target execution pool.
- *[Priority](#priority)* **priority_** - Task priority in the pool queue.
- *[FrameSyncMode](#FrameSyncMode)* **frame_sync_** - Frame synchronization mode.

## CPUShader ( PoolType pool_ , Priority priority_ , FrameSyncMode frame_sync_ , WaitMode wait_mode_ )

Creates a new CPUShader instance.
### Arguments

- *[PoolType](/api/library/common/mt/class.cpushader#PoolType)* **pool_** - Target execution pool.
- *[Priority](#Priority)* **priority_** - Task priority in the pool queue.
- *[FrameSyncMode](#FrameSyncMode)* **frame_sync_** - Frame synchronization mode.
- *[WaitMode](/api/library/common/mt/class.cpushader#WaitMode)* **wait_mode_** - Wait strategy for [wait()](#wait_void).

## CPUShader ( Priority priority_ , FrameSyncMode frame_sync_ )

Creates a new CPUShader instance.
### Arguments

- *[Priority](#Priority)* **priority_** - Task priority in the pool queue.
- *[FrameSyncMode](#FrameSyncMode)* **frame_sync_** - Frame synchronization mode.

## CPUShader ( PoolType pool_ , FrameSyncMode frame_sync_ )

Creates a new CPUShader instance.
### Arguments

- *[PoolType](/api/library/common/mt/class.cpushader#PoolType)* **pool_** - Target execution pool.
- *[FrameSyncMode](#FrameSyncMode)* **frame_sync_** - Frame synchronization mode.

## CPUShader ( PoolType pool_ , Priority priority_ )

Creates a new CPUShader instance.
### Arguments

- *[PoolType](/api/library/common/mt/class.cpushader#PoolType)* **pool_** - Target execution pool.
- *[Priority](#Priority)* **priority_** - Task priority in the pool queue.

## CPUShader ( FrameSyncMode frame_sync_ )

Creates a new CPUShader instance.
### Arguments

- *[FrameSyncMode](#FrameSyncMode)* **frame_sync_** - Frame synchronization mode.

## CPUShader ( PoolType pool_ )

Creates a new CPUShader instance.
### Arguments

- *[PoolType](/api/library/common/mt/class.cpushader#PoolType)* **pool_** - Target execution pool.

## CPUShader ( Priority priority_ )

Creates a new CPUShader instance.
### Arguments

- *[Priority](#Priority)* **priority_** - Task priority in the pool queue.

## void runSync ( int num_threads_ = -1 )

Dispatches the shader to the [Sync](#PoolType_Sync) pool and blocks until all threads finish. One chunk is processed on the calling thread, the rest on pool workers.
### Arguments

- *int* **num_threads_** - Number of threads to use. A value of -1 uses the pool's default thread count.

## void runAsync ( int num_threads_ = -1 )

Dispatches the shader to the [Async](#PoolType_Async) pool and returns immediately. Call [wait()](#wait_void) to block until processing is complete.
### Arguments

- *int* **num_threads_** - Number of threads to use. A value of -1 uses the pool's default thread count.

## void wait ( )

Blocks until the shader finishes. First tries to help by processing remaining work items ([doProcess()](#doProcess_void)), then waits according to the current [WaitMode](#WaitMode).
## bool isRunning ( ) const

Returns a value indicating if the CPU shader code is currently executed.
### Return value

true if the shader code is currently executed; otherwise, false.
## int getNumThreads ( ) const

Returns the currently used number of threads.
### Return value

Number of currently used threads.
## virtual void process ( int thread_num , int num_threads )

Override this method to implement calculations.
### Arguments

- *int* **thread_num** - Current thread number. This number is not a thread ID, it just a virtual number.
- *int* **num_threads** - Number of threads to be used.

## void doProcess ( )

Tries to process remaining shader work items from the current thread. Used internally during [wait()](#wait_void) to help complete the shader faster.
## virtual void done ( )

Virtual callback invoked on the last thread to finish processing. Override this method to chain CPUShader tasks without returning to the main thread.
## bool isAutoDestroy ( ) const

Returns a value indicating if the shader will be automatically destroyed after all threads finish processing.
### Return value

true if auto-destroy is enabled; otherwise, false.
## CPUShader::PoolType getPool ( ) const

Returns the pool type this shader is assigned to.
### Return value

Current pool type.
## void setPool ( PoolType p )

Sets the pool type. If the shader is currently running, waits for completion before changing the pool.
### Arguments

- *[PoolType](/api/library/common/mt/class.cpushader#PoolType)* **p** - Pool type to set.

## Priority getPriority ( ) const

Returns the shader's priority within the pool queue.
### Return value

Current priority.
## void setPriority ( Priority p )

Sets the shader's priority. If the shader is currently running, waits for completion before changing the priority.
### Arguments

- *[Priority](#Priority)* **p** - Priority to set.

## FrameSyncMode getFrameSync ( ) const

Returns the frame synchronization mode.
### Return value

Current frame synchronization mode.
## void setFrameSync ( FrameSyncMode f )

Sets the frame synchronization mode. If the shader is currently running, waits for completion before changing the mode.
### Arguments

- *[FrameSyncMode](#FrameSyncMode)* **f** - Frame synchronization mode to set.

## WaitMode getWaitMode ( ) const

Returns the wait mode used by [wait()](#wait_void).
### Return value

Current wait mode.
## void setWaitMode ( WaitMode f )

Sets the wait mode. [WaitMode::Auto](#WaitMode_Auto) uses a simple spin-wait. [WaitMode::Full](#WaitMode_Full) actively processes other tasks from the same pool while waiting.
### Arguments

- *[WaitMode](/api/library/common/mt/class.cpushader#WaitMode)* **f** - Wait mode to set.

## bool isDone ( ) const

Returns a value indicating if the CPU shader execution is done.
### Return value

true if the shader has finished execution; otherwise, false.
