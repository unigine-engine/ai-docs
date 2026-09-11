# Unigine::CPUShaderCallable Class (CPP)

**Header:** #include <UnigineThread.h>

**Inherits from:** CPUShader


**CPUShaderCallable** is a template class that provides a simplified way to execute custom multithreaded logic using the **[CPUShader](../../../../api/library/common/mt/class.cpushader_cpp.md)** class.


Typically, to use a **[CPUShader](../../../../api/library/common/mt/class.cpushader_cpp.md)**, you need to inherit from the base **[CPUShader](../../../../api/library/common/mt/class.cpushader_cpp.md)** class and manually implement the *process()* method. However, **CPUShaderCallable** allows you to pass in the processing logic and cleanup logic directly as function objects without writing a custom class or managing inheritance.


It also manages an internal shared state of type **State** whose lifetime is tied to the shader � it is automatically destroyed via the provided destroy function when the shader is deleted.


Use the [makeCPUShader()](../../../../api/library/common/class.unigine.namespace_cpp.md#makeCPUShader_State_Process_Destroy) helper function to create instances conveniently.


**Template Parameters**:


- **State** - user-defined type that stores shared state.
- **Process** - function called per thread. Signature: *void(CPUShader *shader, int thread_num, int num_threads)*
- **Destroy** - function called once during destruction, after all threads finish. Signature: *void(State state)*


## CPUShaderCallable Class

### Members

---

## CPUShaderCallable ( Process func_process_ , Destroy func_destroy_ , PoolType pool_ = PoolType::Auto , Priority priority_ = Priority::Normal , FrameSyncMode frame_sync_ = FrameSyncMode::Swap , WaitMode wait_mode_ = WaitMode::Auto )

Creates a new CPUShaderCallable instance.
### Arguments

- *Process* **func_process_** - Function executed on each thread.
- *Destroy* **func_destroy_** - Cleanup function called during destruction.
- *[PoolType](#PoolType)* **pool_** - Target execution pool.
- *[Priority](#Priority)* **priority_** - Task priority in the pool queue.
- *[FrameSyncMode](#FrameSyncMode)* **frame_sync_** - Frame synchronization mode.
- *[WaitMode](#WaitMode)* **wait_mode_** - Wait strategy for [wait()](../../../../api/library/common/mt/class.cpushader_cpp.md#wait_void).

## void process ( int thread_num , int num_threads )

Overridden from **[CPUShader](../../../../api/library/common/mt/class.cpushader_cpp.md)**. Called once per thread during execution. Invokes the provided processing function, passing the shader pointer as the first argument.
### Arguments

- *int* **thread_num** - Index of the current thread.
- *int* **num_threads** - Total number of threads assigned to this task.
