# Unigine::ProcessTask Class (CPP)

**Header:** #include <UnigineThread.h>

**Inherits from:** CPUTask


**ProcessTask** is an abstract base class built on top of **[CPUTask](../../../../api/library/common/mt/class.cputask_cpp.md)** that implements a re-entrant loop pattern with built-in mutex protection against concurrent execution.


Inherit from this class and override two pure virtual methods:


- *[do_process()](#do_process_void)* � performs one unit of work.
- *[is_active()](#is_active_bool)* � returns whether the task should continue looping after the current unit is complete.


Then call *[runProcess()](#runProcess_void)* to submit the task. The internal loop calls *[do_process()](#do_process_void)* repeatedly until *[is_active()](#is_active_bool)* returns false or another call to *[runProcess()](#runProcess_void)* takes over. The mutex ensures that only one execution is active at a time � calling *[runProcess()](#runProcess_void)* while the task is already running is safely ignored.


## ProcessTask Class

### Members

---

## ProcessTask ( PoolThread pool = PoolThread::Background )

Creates a new ProcessTask instance.
### Arguments

- *[PoolThread](#PoolThread)* **pool** - Target pool thread for this task.

## void runProcess ( )

Submits the task for execution on the assigned pool. If the Engine is shutting down, the call is ignored. If the task is already running, the call is safely ignored (the internal mutex prevents concurrent execution).
## virtual void do_process ( )

Pure virtual method to override with your work logic. Called once per loop iteration inside the internal *[process()](../../../../api/library/common/mt/class.cputask_cpp.md#process_void)* loop.
## virtual bool is_active ( )

Pure virtual method that controls the loop. Called after each *[do_process()](#do_process_void)* invocation. If it returns false, the task stops and the mutex is released.
### Return value

Returns true to continue looping, false to stop.
