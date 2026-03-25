# Unigine::CPUShaderCallableStateless Class (CPP)

**Header:** #include <UnigineThread.h>

**Inherits from:** CPUShader


**CPUShaderCallableStateless** is a template class that provides a simplified way to execute custom multithreaded logic using the **[CPUShader](../../../../api/library/common/mt/class.cpushader_cpp.md)** class without requiring shared state or a destroy function.


Typically, to use a **[CPUShader](../../../../api/library/common/mt/class.cpushader_cpp.md)**, you need to inherit from the base **[CPUShader](../../../../api/library/common/mt/class.cpushader_cpp.md)** class and manually implement the *process()* method. However, **CPUShaderCallableStateless** allows you to pass in the processing logic directly as a function object without writing a custom class or managing inheritance.


Unlike **[CPUShaderCallable](../../../../api/library/common/mt/class.cpushadercallable_cpp.md)**, this variant does not manage shared state or a destroy callback.


Use the [makeCPUShaderStateless()](../../../../api/library/common/class.unigine.namespace_cpp.md#makeCPUShaderStateless_Process), [makeScopeCPUShaderStateless()](../../../../api/library/common/class.unigine.namespace_cpp.md#makeScopeCPUShaderStateless_Process), or [runSyncMultiThreadFunc()](../../../../api/library/common/class.unigine.namespace_cpp.md#runSyncMultiThreadFunc_Process_int) helper functions to create and run instances conveniently.


**Template Parameters**:


- **Process** - function called per thread. Signature: *void(CPUShader *shader, int thread_num, int num_threads)*


## CPUShaderCallableStateless Class

### Members

---

## CPUShaderCallableStateless ( Process func_process_ , PoolType pool_ = PoolType::Auto , Priority priority_ = Priority::Normal , FrameSyncMode frame_sync_ = FrameSyncMode::Swap , WaitMode wait_mode_ = WaitMode::Auto )

Creates a new CPUShaderCallableStateless instance.
### Arguments

- *Process* **func_process_** - Function executed on each thread.
- *[PoolType](#PoolType)* **pool_** - Target execution pool.
- *[Priority](#Priority)* **priority_** - Task priority in the pool queue.
- *[FrameSyncMode](#FrameSyncMode)* **frame_sync_** - Frame synchronization mode.
- *[WaitMode](#WaitMode)* **wait_mode_** - Wait strategy for [wait()](../../../../api/library/common/mt/class.cpushader_cpp.md#wait_void).

## void process ( int thread_num , int num_threads )

Overridden from **[CPUShader](../../../../api/library/common/mt/class.cpushader_cpp.md)**. Called once per thread during execution. Invokes the provided processing function, passing the shader pointer as the first argument.
### Arguments

- *int* **thread_num** - Index of the current thread.
- *int* **num_threads** - Total number of threads assigned to this task.
