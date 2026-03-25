# Unigine::AsyncTaskCallable Class (CPP)

**Header:** #include <UnigineThread.h>

**Inherits from:** CPUTask


**AsyncTaskCallable** is a template class that provides a simplified way to execute custom single-threaded task logic using the **[CPUTask](../../../../api/library/common/mt/class.cputask_cpp.md)** class.


Typically, to use a **[CPUTask](../../../../api/library/common/mt/class.cputask_cpp.md)**, you need to inherit from the base **[CPUTask](../../../../api/library/common/mt/class.cputask_cpp.md)** class and manually implement the *process()* method. However, **AsyncTaskCallable** allows you to pass in the processing logic and cleanup logic directly as function objects without writing a custom class or managing inheritance.


Use the [makeCPUTask()](../../../../api/library/common/class.unigine.namespace_cpp.md#makeCPUTask_Callable_Priority_FrameSyncMode) helper function to create instances conveniently.


**Template Parameters**:


- **Callable** - function called when the task is executed. Signature: *void(CPUTask *task)*
- **Destroy** - function called once during destruction. Signature: *void()*


## AsyncTaskCallable Class

### Members

---

## AsyncTaskCallable ( Callable callable_ , Destroy destroy_ , Priority priority_ = Priority::Normal , FrameSyncMode frame_sync_ = FrameSyncMode::Disabled )

Creates a new AsyncTaskCallable instance.
### Arguments

- *Callable* **callable_** - Function executed when the task runs.
- *Destroy* **destroy_** - Cleanup function called during destruction.
- *[Priority](#Priority)* **priority_** - Task priority in the pool queue.
- *[FrameSyncMode](#FrameSyncMode)* **frame_sync_** - Frame synchronization mode.

## void process ( )

Overridden from **[CPUTask](../../../../api/library/common/mt/class.cputask_cpp.md)**. Invokes the provided callable function, passing the task pointer as the argument.
