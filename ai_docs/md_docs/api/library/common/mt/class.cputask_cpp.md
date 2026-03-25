# Unigine::CPUTask Class (CPP)

**Header:** #include <UnigineThread.h>


**CPUTask** is a single-threaded task that can be dispatched to any of the Engine's thread pools. Unlike **[CPUShader](../../../../api/library/common/mt/class.cpushader_cpp.md)**, which distributes work across multiple threads, a CPUTask runs its *process()* method once on a single worker thread within the chosen pool.


Inherit from this class and override the pure virtual *process()* method to define your task logic, then call one of the *run*Thread()* methods to submit it to a specific pool.


## CPUTask Class

### Members

---

## CPUTask ( )

Default constructor.
## CPUTask ( const CPUTask& task )

Copy constructor. Copies the priority and frame synchronization mode from the given task.
### Arguments

- *const CPUTask&* **task** - Source task to copy priority and frame sync settings from.

## CPUTask ( Priority priority_ )

Constructor with priority.
### Arguments

- *[Priority](#Priority)* **priority_** - Task priority within the pool queue.

## CPUTask ( FrameSyncMode frame_sync_ )

Constructor with frame synchronization mode.
### Arguments

- *[FrameSyncMode](#FrameSyncMode)* **frame_sync_** - Frame synchronization mode.

## CPUTask ( Priority priority_ , FrameSyncMode frame_sync_ )

Constructor with priority and frame synchronization mode.
### Arguments

- *[Priority](#Priority)* **priority_** - Task priority within the pool queue.
- *[FrameSyncMode](#FrameSyncMode)* **frame_sync_** - Frame synchronization mode.

## PoolThread getRunPoolThread ( ) const

Returns the pool thread this task was dispatched to.
### Return value

Pool thread the task was submitted to.
## Priority getPriority ( ) const

Returns the task's priority within the pool queue.
### Return value

Current priority.
## void setPriority ( Priority v )

Sets the task's priority within the pool queue.
### Arguments

- *[Priority](#Priority)* **v** - Priority to set.

## FrameSyncMode getFrameSync ( ) const

Returns the frame synchronization mode.
### Return value

Current frame synchronization mode.
## void setFrameSync ( FrameSyncMode v )

Sets the frame synchronization mode.
### Arguments

- *[FrameSyncMode](#FrameSyncMode)* **v** - Frame synchronization mode to set.

## static int generateID ( )

Generates a unique task identifier. Can be called before creating the task to pre-allocate an ID.
### Return value

Unique task identifier.
## void run ( PoolThread thread )

Submits the task to the specified pool thread.
### Arguments

- *[PoolThread](#PoolThread)* **thread** - Target pool thread to run the task on.

## void runMainThread ( )

Submits the task to the main thread queue. The task will be executed on the main thread during the next update cycle.
## void runSyncThread ( )

Submits the task to the Sync Pool.
## void runAsyncThread ( )

Submits the task to the Async Pool.
## void runCriticalThread ( )

Submits the task to the Critical Pool.
## void runCommonThread ( )

Submits the task to the Common Pool.
## void runBackgroundThread ( )

Submits the task to the Background Pool.
## void runRenderFlushThread ( )

Submits the task to the Render-Flush Pool.
## void runFileStreamThread ( )

Submits the task to the File Stream Pool.
## void runGPUStreamThread ( )

Submits the task to the GPU Stream Pool.
## void unsafeStop ( )

Removes the task from the pool queue. This method is not thread-safe and should only be called when you are certain the task has not yet started processing.
## void destroy ( )

Destroys the task. Uses the engine's asynchronous destroy queue to safely delete the task object.
## virtual void process ( )

Pure virtual method to override with your task logic. Called once on the assigned worker thread when the task is executed.
