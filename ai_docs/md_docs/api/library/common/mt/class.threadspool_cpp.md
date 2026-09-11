# Unigine::ThreadsPool Class (CPP)

**Header:** #include <UnigineThread.h>


ThreadsPool is the Engine CPU work scheduler. It runs CPUTask and CPUShader jobs on dedicated worker pools (sync/async/critical/background/render-flush/file-stream/GPU-stream) and also supports main-thread execution.


Jobs can be marked as frame-synchronized (FrameSyncMode::Swap). Such work is expected to finish in the current frame and is drained at the end-of-frame Swap stage via ThreadsPool::frameSync().


## ThreadsPool Class

### Enums

## Priority

Job priority used by the internal queues (lower value means higher priority).
| Name | Description |
|---|---|
| **Critical** = 0 | Highest priority. |
| **Highest** = 1 | Very high priority. |
| **AboveNormal** = 2 | Above normal priority. |
| **Normal** = 3 | Default priority. |
| **BelowNormal** = 4 | Below normal priority. |
| **Lowest** = 5 | Low priority. |
| **Background** = 6 | Background priority. |
| **Idle** = 7 | Idle (lowest) priority. |
| **Landscape** = 1 | Alias of Priority::Highest. |
| **Streaming** = 6 | Alias of Priority::Background. |

## PoolThread

Execution pool selector for CPUTask/CPUShader scheduling.
| Name | Description |
|---|---|
| **Main** = 0 | Main thread execution. |
| **Sync** = 1 | Sync worker pool. |
| **Async** = 2 | Async worker pool. |
| **Critical** = 3 | Critical worker pool. |
| **Common** = 4 | Common worker pool. |
| **Background** = 5 | Background worker pool. |
| **FileStream** = 6 | File streaming worker pool. |
| **GPUStream** = 7 | GPU streaming worker pool. |
| **RenderFlush** = 8 | Render-flush worker pool. |

## FrameSyncMode

Controls whether the Engine blocks at the swap stage and waits for the work to finish before proceeding to the next frame.
| Name | Description |
|---|---|
| **Disabled** = 0 | Work is not frame-synchronized. |
| **Swap** = 1 | End-of-frame (Swap) mode. The Engine blocks at the swap stage and waits until all such work completes before proceeding to the next frame. |

### Members

---

## int isInitialized ( )

Checks whether the ThreadsPool subsystem is initialized.
### Return value

Non-zero if the thread pools were initialized.
## int getCurrentThreadIndex ( )

Returns the pool worker index for the current thread.
### Return value

Current pool worker index, or -1 if not a pool worker.
## int getNumAllThreads ( )

Returns the total worker thread count across all pools.
### Return value

Total number of worker threads across all pools (main thread not included).
## int getNumAsyncThreads ( )

Returns the Async pool thread count.
### Return value

Number of threads in the Async pool.
## int getNumSyncThreads ( )

Returns the Sync pool thread count.
### Return value

Number of threads in the Sync pool.
## int getNumDefaultAsyncThreads ( )

Returns the default Async CPUShader thread count.
### Return value

Default thread count used by CPUShader::runAsync() when num_threads is -1.
## int getNumDefaultSyncThreads ( )

Returns the default Sync CPUShader thread count.
### Return value

Default thread count used by CPUShader::runSync() when num_threads is -1.
## void frameSync ( )

 End-of-frame wait for frame-synchronized work. Signals workers and keeps processing until the internal frame-sync counter reaches zero or the Engine is shutting down.
## bool yield ( int pool_mask = POOL_THREAD_MASK_ALL , int priority_mask = PRIORITY_MASK_ALL , bool only_frame_sync = false )

 Tries to execute one pending job that matches the given pool and priority masks. If called from a pool worker, the pool_mask is additionally limited to that worker�s allowed pools.
### Arguments

- *int* **pool_mask** - Pool selection mask (POOL_THREAD_MASK_*).
- *int* **priority_mask** - Priority selection mask (PRIORITY_MASK_*).
- *bool* **only_frame_sync** - If true, process only frame-synchronized queues.

### Return value

True if a job was executed; false otherwise.
## bool runProcess ( int pool_mask = POOL_THREAD_MASK_ALL , int priority_mask = PRIORITY_MASK_ALL , bool only_frame_sync = true )

 Tries to execute one pending job from the selected pools. Jobs are scanned by priority order and filtered by priority_mask. When only_frame_sync is false, non-frame-synced queues may also be processed.
### Arguments

- *int* **pool_mask** - Pool selection mask (POOL_THREAD_MASK_*).
- *int* **priority_mask** - Priority selection mask (PRIORITY_MASK_*).
- *bool* **only_frame_sync** - If true, process only frame-synchronized queues.

### Return value

True if a job was executed; false otherwise.
## void forceWakeAll ( )

Wakes all pool worker threads waiting for work.
## void runNewThread ( CallbackBase* process , int priority = -3 )

 Runs the callback on a reusable generic user thread. If no idle thread is available, a new one is created. The callback is deleted after execution.
### Arguments

- *CallbackBase** **process** - Callback object to run on a generic user thread (ownership is taken).
- *int* **priority** - Thread priority for the generic user thread.
