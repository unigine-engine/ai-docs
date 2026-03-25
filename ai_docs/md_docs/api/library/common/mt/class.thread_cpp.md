# Unigine::Thread Class (CPP)

**Header:** #include <UnigineThread.h>


Base class for creating and managing threads in the Engine. Provides functionality for starting, stopping, signaling, and querying threads, as well as setting thread priority and CPU affinity.


To create a custom thread, inherit from this class and implement the pure virtual *process()* method.


## Thread Class

### Enums

## Type

Thread type identifier used to classify Engine and user threads.
| Name | Description |
|---|---|
| **Main** = 0 | Main Engine thread. |
| **PoolSync** = 1 | Synchronous pool worker thread. |
| **PoolAsync** = 2 | Asynchronous pool worker thread. |
| **PoolCritical** = 3 | Critical pool worker thread. |
| **PoolCommon** = 4 | Common pool worker thread. |
| **PoolBackground** = 5 | Background pool worker thread. |
| **PoolRenderFlush** = 6 | Render-flush pool worker thread. |
| **PoolFileStream** = 7 | File streaming pool worker thread. |
| **PoolGPUStream** = 8 | GPU streaming pool worker thread. |
| **Sound** = 9 | Sound system thread. |
| **Input** = 10 | Input system thread. |
| **Monitor** = 11 | Monitor thread. |
| **Dump** = 12 | Dump thread. |
| **Ultraleap** = 13 | Ultraleap tracking thread. |
| **Network** = 14 | Network thread. |
| **WakeUp** = 15 | Wake-up thread. |
| **GenericUser** = 16 | Generic user thread. |
| **USC** = 17 | UnigineScript thread. |
| **Unknown** = 18 | Unknown thread type. |

### Members

---

## Thread ( bool auto_shutdown = true , Type type = Type::Unknown , const char * name = nullptr , int microprofile_priority = -1 )

Creates a new Thread instance.
### Arguments

- *bool* **auto_shutdown** - If true, the thread will be automatically shut down on Engine exit.
- *[Type](/api/library/common/mt/class.thread#Type)* **type** - Thread type identifier.
- *const char ** **name** - Thread name displayed in the [Microprofile](../../../../tools/profiling/microprofile/index_cpp.md) tool. If not set, the thread type name is used.
- *int* **microprofile_priority** - Thread priority in [Microprofile](../../../../tools/profiling/microprofile/index_cpp.md).

## virtual bool run ( size_t size = 0x100000 )

Creates an OS thread and begins executing the *process()* method. Returns false if the thread is already running.
### Arguments

- *size_t* **size** - Thread stack size in bytes.

### Return value

true if the thread was successfully started; otherwise, false.
## void process ( )

Protected pure virtual method that defines the thread's workload. Override this method in your subclass to implement the thread logic. Called automatically when *[run()](../../../...md#run_size_t_bool)* is invoked.
## bool stop ( )

Gracefully stops the thread: signals it to wake up and waits (joins) until *process()* returns.
### Return value

true if the thread exited cleanly; otherwise, false.
## void signal ( )

Signals the thread to wake up from a waiting state.
## bool terminate ( )

Forcefully kills the thread immediately. May cause resource leaks. Does nothing if the thread has already stopped cleanly.
### Return value

true if the thread was terminated; otherwise, false.
## virtual bool shutdown ( )

Performs a two-stage shutdown: first attempts a graceful [stop()](#stop_bool) with a timeout, then forcefully [terminates](#terminate_bool) if the thread has not finished.
### Return value

true if the operation was successful; otherwise, false.
## static void allThreadsShutdown ( )

Initiates shutdown of all Engine threads.
## static bool isShutdown ( )

Returns a value indicating if the Engine shutdown has been initiated.
### Return value

true if the Engine threads are being shut down; otherwise, false.
## Type getType ( ) const

Returns the thread type.
### Return value

Thread type identifier.
## const char * getName ( ) const

Returns the thread name.
### Return value

Thread name string, or nullptr if not set.
## bool isRunning ( ) const

Checks if the thread is currently running.
### Return value

true if the thread is running; otherwise, false.
## bool isWaiting ( ) const

Checks if the thread is currently waiting.
### Return value

true if the thread is in a waiting state; otherwise, false.
## int setPriority ( int priority )

Sets the thread priority.
### Arguments

- *int* **priority** - Thread priority in the range [-3; 3].

### Return value

1 if the operation was successful; otherwise, 0.
## int getPriority ( ) const

Returns the thread priority.
### Return value

Thread priority in the range [-3; 3].
## int setAffinityMask ( long long mask )

Sets the thread CPU affinity mask.
### Arguments

- *long long* **mask** - CPU affinity mask to set.

### Return value

1 if the operation was successful; otherwise, 0.
## long long getAffinityMask ( ) const

Returns the thread CPU affinity mask.
### Return value

CPU affinity mask, or -1 if the mask is not set.
## ID getRunningID ( ) const

Returns the running thread identifier.
### Return value

Platform-specific thread identifier.
## bool isCurrentThread ( ) const

Checks if the calling thread is this thread instance.
### Return value

true if the calling thread is this thread; otherwise, false.
## static ID getID ( )

Returns the identifier of the current (calling) thread.
### Return value

Platform-specific identifier of the calling thread.
## static void sleep ( unsigned int ms )

Suspends the calling thread execution for the specified number of milliseconds.
### Arguments

- *unsigned int* **ms** - Time to sleep in milliseconds.

## static void switchThread ( )

Yields execution of the calling thread, giving other threads an opportunity to run.
## static Thread * getCurrentThread ( )

Returns the Thread object associated with the calling thread.
### Return value

Pointer to the Thread object for the calling thread, or nullptr if called from the main thread or a thread not managed by this class.
## static Type getCurrentThreadType ( )

Returns the type of the current (calling) thread.
### Return value

Type of the calling thread.
## static bool isCurrentThreadType ( Type type )

Checks if the calling thread is of the specified type.
### Arguments

- *[Type](/api/library/common/mt/class.thread#Type)* **type** - Thread type to check against.

### Return value

true if the calling thread matches the specified type; otherwise, false.
## static bool isMainThread ( )

Checks if the calling thread is the main thread.
### Return value

true if the calling thread is the main thread; otherwise, false.
## static bool isPoolSyncThread ( )

Checks if the calling thread is a sync pool worker.
### Return value

true if the calling thread is a sync pool thread; otherwise, false.
## static bool isPoolAsyncThread ( )

Checks if the calling thread is an async pool worker.
### Return value

true if the calling thread is an async pool thread; otherwise, false.
## static bool isPoolCriticalThread ( )

Checks if the calling thread is a critical pool worker.
### Return value

true if the calling thread is a critical pool thread; otherwise, false.
## static bool isPoolCommonThread ( )

Checks if the calling thread is a common pool worker.
### Return value

true if the calling thread is a common pool thread; otherwise, false.
## static bool isPoolBackgroundThread ( )

Checks if the calling thread is a background pool worker.
### Return value

true if the calling thread is a background pool thread; otherwise, false.
## static bool isPoolRenderFlushThread ( )

Checks if the calling thread is a render-flush pool worker.
### Return value

true if the calling thread is a render-flush pool thread; otherwise, false.
## static bool isPoolFileStreamThread ( )

Checks if the calling thread is a file-stream pool worker.
### Return value

true if the calling thread is a file-stream pool thread; otherwise, false.
## static bool isPoolGPUStreamThread ( )

Checks if the calling thread is a GPU-stream pool worker.
### Return value

true if the calling thread is a GPU-stream pool thread; otherwise, false.
## static bool isPoolThread ( )

Checks if the calling thread is any pool worker thread (sync, async, critical, common, background, render-flush, file-stream, or GPU-stream).
### Return value

true if the calling thread is any pool worker thread; otherwise, false.
