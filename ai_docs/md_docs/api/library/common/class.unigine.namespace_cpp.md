# Unigine Namespace Items (CPP)


## CallbackBase * MakeCallback ( Ret(*)() func )

Makes a function callback. The function can receive up to 4 arguments.
### Arguments

- *Ret(*)()* **func** - Pointer to the function.

### Return value

Pointer to the callback.
## CallbackBase * MakeCallback ( Class * func )

Makes a class member function callback. The function can receive up to 4 arguments.
### Arguments

- *Class ** **func** - Pointer to the class member function.

### Return value

Pointer to the callback.
## template < typename Type >

## SpinLockTemplate ( volatile Type * ptr , const Type old_value , const Type new_value )

Attempts to atomically update *ptr from old_value to new_value using *[AtomicCAS](#AtomicCAS_voidvolatileptr_voidptr_voidptr_bool)* operation. If the CAS fails, it enters a [spin-wait loop](../../../api/library/common/mt/class.backoffspinner_cpp.md) until the value at *ptr equals old_value and the update can be retried.
### Arguments

- *volatile Type ** **ptr** - Pointer to a shared variable
- *const Type* **old_value** - Expected current value of *ptr
- *const Type* **new_value** - Value to write if *ptr == old_value


## void SpinLock ( volatile char * ptr , char old_value , char new_value )

Specialized version of the **[SpinLockTemplate](#SpinLockTemplate_volatiletmplptr_consttmpl_consttmpl)** for 8-bit values.
### Arguments

- *volatile char ** **ptr** - Pointer to a shared variable
- *char* **old_value** - Expected current value of *ptr
- *char* **new_value** - Value to write if *ptr == old_value


## void SpinLock ( volatile short * ptr , short old_value , short new_value )

Specialized version of the **[SpinLockTemplate](#SpinLockTemplate_volatiletmplptr_consttmpl_consttmpl)** for 16-bit values.
### Arguments

- *volatile short ** **ptr** - Pointer to a shared variable
- *short* **old_value** - Expected current value of *ptr
- *short* **new_value** - Value to write if *ptr == old_value


## void SpinLock ( volatile int * ptr , int old_value , int new_value )

Specialized version of the **[SpinLockTemplate](#SpinLockTemplate_volatiletmplptr_consttmpl_consttmpl)** for 32-bit values.
### Arguments

- *volatile int ** **ptr** - Pointer to a shared variable
- *int* **old_value** - Expected current value of *ptr
- *int* **new_value** - Value to write if *ptr == old_value


## void SpinLock ( volatile long long * ptr , long long old_value , long long new_value )

Specialized version of the **[SpinLockTemplate](#SpinLockTemplate_volatiletmplptr_consttmpl_consttmpl)** for 64-bit values.
### Arguments

- *volatile long long ** **ptr** - Pointer to a shared variable
- *long long* **old_value** - Expected current value of *ptr
- *long long* **new_value** - Value to write if *ptr == old_value


## void WaitLock ( volatile char * ptr , char value )

Attempts to acquire a spin-based lock by waiting until the value pointed to by ptr equals the specified value. Internally calls [SpinLock](#SpinLock_volatilechar_char_char_void) with the same old and new value, spinning until *ptr == value.
### Arguments

- *volatile char ** **ptr** - Pointer to the 8-bit shared variable
- *char* **value** - The target value to wait for.


## void WaitLock ( volatile short * ptr , short old_value )

Attempts to acquire a spin-based lock by waiting until the value pointed to by ptr equals the specified value. Internally calls [SpinLock](#SpinLock_volatileshort_short_short_void) with the same old and new value, spinning until *ptr == value.
### Arguments

- *volatile short ** **ptr** - Pointer to the 16-bit shared variable
- *short* **old_value** - The target value to wait for.


## void WaitLock ( volatile int * ptr , int old_value )

Attempts to acquire a spin-based lock by waiting until the value pointed to by ptr equals the specified value. Internally calls [SpinLock](#SpinLock_volatileint_int_int_void) with the same old and new value, spinning until *ptr == value.
### Arguments

- *volatile int ** **ptr** - Pointer to the 32-bit shared variable
- *int* **old_value** - The target value to wait for.


## void WaitLock ( volatile long long * ptr , long long old_value )

Attempts to acquire a spin-based lock by waiting until the value pointed to by ptr equals the specified value. Internally calls [SpinLock](#SpinLock_volatilellong_llong_llong_void) with the same old and new value, spinning until *ptr == value.
### Arguments

- *volatile long long ** **ptr** - Pointer to the 64-bit shared variable
- *long long* **old_value** - The target value to wait for.


## template < typename Type >

## void MutexSpinLock ( volatile Type & mutex )

Atomically sets mutex from 0 to 1. Uses the appropriate *[SpinLock](#SpinLock_volatilechar_char_char_void)* method.
### Arguments

- *volatile Type &* **mutex** - Reference to a shared variable acting as a spin mutex. The value 0 indicates unlocked state, while 1 indicates locked.


## template < typename Type >

## bool MutexSpinTryLock ( volatile Type & mutex )

Attempts to atomically lock mutex without waiting. Uses *[AtomicCAS](#AtomicCAS_voidvolatileptr_voidptr_voidptr_bool)* with 0 and 1.
### Arguments

- *volatile Type &* **mutex** - Reference to a shared variable acting as a spin mutex. The value 0 indicates unlocked state, while 1 indicates locked.

### Return value

Returns true if *[AtomicCAS](#AtomicCAS_voidvolatileptr_voidptr_voidptr_bool)* succesfully swapped values; false otherwise.
## template < typename Type >

## void MutexSpinUnlock ( volatile Type & mutex )

Atomically sets the mutex value to 0 (unlocked). Uses an *[AtomicCAS](#AtomicCAS_voidvolatileptr_voidptr_voidptr_bool)*.
### Arguments

- *volatile Type &* **mutex** - Reference to a shared variable acting as a spin mutex. The value 0 indicates unlocked state, while 1 indicates locked.


## template < typename Type >

## bool MutexSpinIsLocked ( volatile Type & mutex )

Checks if mutex is currently locked.
### Arguments

- *volatile Type &* **mutex** - Reference to a shared variable acting as a spin mutex. The value 0 indicates unlocked state, while 1 indicates locked.

### Return value

Returns true if the mutex is currently locked (non-zero); false otherwise.
## template < typename Type >

## void MutexSpinWaitLock ( volatile Type & mutex )

Spins until mutex value becomes 0 without changing it. Uses a *[SpinLock](#SpinLock_volatileint_int_int_void)* with two zeros.
### Arguments

- *volatile Type &* **mutex** - Reference to a shared variable acting as a spin mutex. The value 0 indicates unlocked state, while 1 indicates locked.


## char AtomicAnd ( volatile char * ptr , char value )

Unigine atomic bitwise **AND** operation (8-bit).
### Arguments

- *volatile char ** **ptr** - Pointer to the variable.
- *char* **value** - Bitmask to apply via bitwise **AND**. Only bits set in both *ptr and value will remain set.

### Return value

Previous value (just before bitwise **AND**).
## short AtomicAnd ( volatile short * ptr , short value )

Unigine atomic bitwise **AND** operation (16-bit).
### Arguments

- *volatile short ** **ptr** - Pointer to the variable.
- *short* **value** - Bitmask to apply via bitwise **AND**. Only bits set in both *ptr and value will remain set.

### Return value

Previous value (just before bitwise **AND**).
## int AtomicAnd ( volatile int * ptr , int value )

Unigine atomic bitwise **AND** operation (32-bit).
### Arguments

- *volatile int ** **ptr** - Pointer to the variable.
- *int* **value** - Bitmask to apply via bitwise **AND**. Only bits set in both *ptr and value will remain set.

### Return value

Previous value (just before bitwise **AND**).
## long long AtomicAnd ( volatile long long * ptr , long long value )

Unigine atomic bitwise **AND** operation (64-bit).
### Arguments

- *volatile long long ** **ptr** - Pointer to the variable.
- *long long* **value** - Bitmask to apply via bitwise **AND**. Only bits set in both *ptr and value will remain set.

### Return value

Previous value (just before bitwise **AND**).
## char AtomicOr ( volatile char * ptr , char value )

Unigine atomic bitwise **OR** operation (8-bit).
### Arguments

- *volatile char ** **ptr** - Pointer to the variable.
- *char* **value** - Bitmask to apply via bitwise **OR**. Bits set in either *ptr or value will remain set.

### Return value

Previous value (just before bitwise **OR**).
## char AtomicOr ( volatile char * ptr , char value )

Unigine atomic bitwise **OR** operation (16-bit).
### Arguments

- *volatile char ** **ptr** - Pointer to the variable.
- *char* **value** - Bitmask to apply via bitwise **OR**. Bits set in either *ptr or value will remain set.

### Return value

Previous value (just before bitwise **OR**).
## char AtomicOr ( volatile char * ptr , char value )

Unigine atomic bitwise **OR** operation (32-bit).
### Arguments

- *volatile char ** **ptr** - Pointer to the variable.
- *char* **value** - Bitmask to apply via bitwise **OR**. Bits set in either *ptr or value will remain set.

### Return value

Previous value (just before bitwise **OR**).
## char AtomicOr ( volatile char * ptr , char value )

Unigine atomic bitwise **OR** operation (64-bit).
### Arguments

- *volatile char ** **ptr** - Pointer to the variable.
- *char* **value** - Bitmask to apply via bitwise **OR**. Bits set in either *ptr or value will remain set.

### Return value

Previous value (just before bitwise **OR**).
## char AtomicXor ( volatile char * ptr , char value )

Unigine atomic bitwise **XOR** operation (8-bit).
### Arguments

- *volatile char ** **ptr** - Pointer to the variable.
- *char* **value** - Bitmask to apply via bitwise **XOR**. Bits set in either *ptr or value, but not both, will be toggled after the operation.

### Return value

Previous value (just before bitwise **XOR**).
## char AtomicXor ( volatile char * ptr , char value )

Unigine atomic bitwise **XOR** operation (16-bit).
### Arguments

- *volatile char ** **ptr** - Pointer to the variable.
- *char* **value** - Bitmask to apply via bitwise **XOR**. Bits set in either *ptr or value, but not both, will be toggled after the operation.

### Return value

Previous value (just before bitwise **XOR**).
## char AtomicXor ( volatile char * ptr , char value )

Unigine atomic bitwise **XOR** operation (32-bit).
### Arguments

- *volatile char ** **ptr** - Pointer to the variable.
- *char* **value** - Bitmask to apply via bitwise **XOR**. Bits set in either *ptr or value, but not both, will be toggled after the operation.

### Return value

Previous value (just before bitwise **XOR**).
## char AtomicXor ( volatile char * ptr , char value )

Unigine atomic bitwise **XOR** operation (64-bit).
### Arguments

- *volatile char ** **ptr** - Pointer to the variable.
- *char* **value** - Bitmask to apply via bitwise **XOR**. Bits set in either *ptr or value, but not both, will be toggled after the operation.

### Return value

Previous value (just before bitwise **XOR**).
## char AtomicAdd ( volatile char * ptr , char value )

Unigine atomic add (8-bit).
### Arguments

- *volatile char ** **ptr** - Pointer to the variable.
- *char* **value** - Value to be added.

### Return value

Previous value (just before adding).
## short AtomicAdd ( volatile short * ptr , short value )

Unigine atomic add (16-bit).
### Arguments

- *volatile short ** **ptr** - Pointer to the variable.
- *short* **value** - Value to be added.

### Return value

Previous value (just before adding).
## int AtomicAdd ( volatile int * ptr , int value )

Unigine atomic add (32-bit).
### Arguments

- *volatile int ** **ptr** - Pointer to the variable.
- *int* **value** - Value to be added.

### Return value

Previous value (just before adding).
## long long AtomicAdd ( volatile long long * ptr , long long value )

Unigine atomic add (64-bit).
### Arguments

- *volatile long long ** **ptr** - Pointer to the variable.
- *long long* **value** - Value to be added.

### Return value

Previous value (just before adding).
## char AtomicInc ( volatile char * ptr )

Unigine atomic increment (8-bit).
### Arguments

- *volatile char ** **ptr** - Pointer to the variable.

### Return value

Previous value (just before adding).
## short AtomicInc ( volatile short * ptr )

Unigine atomic increment (16-bit).
### Arguments

- *volatile short ** **ptr** - Pointer to the variable.

### Return value

Previous value (just before adding).
## int AtomicInc ( volatile int * ptr )

Unigine atomic increment (32-bit).
### Arguments

- *volatile int ** **ptr** - Pointer to the variable.

### Return value

Previous value (just before adding).
## long long AtomicInc ( volatile long long * ptr )

Unigine atomic increment (64-bit).
### Arguments

- *volatile long long ** **ptr** - Pointer to the variable.

### Return value

Previous value (just before adding).
## char AtomicDec ( volatile char * ptr )

Unigine atomic decrement (8-bit).
### Arguments

- *volatile char ** **ptr** - Pointer to the variable.

### Return value

Previous value (just before subtracting).
## short AtomicDec ( volatile short * ptr )

Unigine atomic decrement (16-bit).
### Arguments

- *volatile short ** **ptr** - Pointer to the variable.

### Return value

Previous value (just before subtracting).
## int AtomicDec ( volatile int * ptr )

Unigine atomic decrement (32-bit).
### Arguments

- *volatile int ** **ptr** - Pointer to the variable.

### Return value

Previous value (just before subtracting).
## long long AtomicDec ( volatile long long * ptr )

Unigine atomic decrement (64-bit).
### Arguments

- *volatile long long ** **ptr** - Pointer to the variable.

### Return value

Previous value (just before subtracting).
## bool AtomicCAS ( volatile char * ptr , char old_value , char new_value )

Unigine atomic compare and swap (8-bit).
### Arguments

- *volatile char ** **ptr** - Pointer to the variable.
- *char* **old_value** - The old pointer value.
- *char* **new_value** - The new pointer value.

### Return value

**true** if the variable value was successfully swapped; otherwise, **false**.
## bool AtomicCAS ( volatile short * ptr , short old_value , short new_value )

Unigine atomic compare and swap (16-bit).
### Arguments

- *volatile short ** **ptr** - Pointer to the variable.
- *short* **old_value** - The old pointer value.
- *short* **new_value** - The new pointer value.

### Return value

**true** if the variable value was successfully swapped; otherwise, **false**.
## bool AtomicCAS ( volatile int * ptr , int old_value , int new_value )

Unigine atomic compare and swap (32-bit).
### Arguments

- *volatile int ** **ptr** - Pointer to the variable.
- *int* **old_value** - The old pointer value.
- *int* **new_value** - The new pointer value.

### Return value

**true** if the variable value was successfully swapped; otherwise, **false**.
## bool AtomicCAS ( volatile long long * ptr , long long old_value , long long new_value )

Unigine atomic compare and swap (64-bit).
### Arguments

- *volatile long long ** **ptr** - Pointer to the variable.
- *long long* **old_value** - The old pointer value.
- *long long* **new_value** - The new pointer value.

### Return value

**true** if the variable value was successfully swapped; otherwise, **false**.
## bool AtomicCAS ( void *volatile * ptr , void * old_value , void * new_value )

Unigine atomic compare and swap (pointer).
### Arguments

- *void *volatile ** **ptr** - Pointer to the variable.
- *void ** **old_value** - The old pointer value.
- *void ** **new_value** - The new pointer value.

### Return value

**true** if the variable value was successfully swapped; otherwise, **false**.
## void AtomicSet ( volatile char * ptr , char value )

Unigine atomic set (8-bit).
### Arguments

- *volatile char ** **ptr** - Pointer to the variable.
- *char* **value** - Value to be set.


## void AtomicSet ( volatile bool * ptr , bool value )

Unigine atomic set (8-bit).
### Arguments

- *volatile bool ** **ptr** - Pointer to the variable.
- *bool* **value** - Value to be set.


## void AtomicSet ( volatile short * ptr , short value )

Unigine atomic set (16-bit).
### Arguments

- *volatile short ** **ptr** - Pointer to the variable.
- *short* **value** - Value to be set.


## void AtomicSet ( volatile int * ptr , int value )

Unigine atomic set (32-bit).
### Arguments

- *volatile int ** **ptr** - Pointer to the variable.
- *int* **value** - Value to be set.


## void AtomicSet ( volatile long long * ptr , long long value )

Unigine atomic set (64-bit).
### Arguments

- *volatile long long ** **ptr** - Pointer to the variable.
- *long long* **value** - Value to be set.


## char AtomicGet ( volatile char * ptr )

Unigine atomic read (8-bit). Simply accessing the variable directly is actually unsafe!
### Arguments

- *volatile char ** **ptr** - Pointer to the variable.

### Return value

Variable value.
## bool AtomicGet ( volatile bool * ptr )

Unigine atomic read (8-bit). Simply accessing the variable directly is actually unsafe!
### Arguments

- *volatile bool ** **ptr** - Pointer to the variable.

### Return value

Variable value.
## short AtomicGet ( volatile short * ptr )

Unigine atomic read (16-bit). Simply accessing the variable directly is actually unsafe!
### Arguments

- *volatile short ** **ptr** - Pointer to the variable.

### Return value

Variable value.
## int AtomicGet ( volatile int * ptr )

Unigine atomic read (32-bit). Simply accessing the variable directly is actually unsafe!
### Arguments

- *volatile int ** **ptr** - Pointer to the variable.

### Return value

Variable value.
## long long AtomicGet ( volatile long long * ptr )

Unigine atomic read (64-bit). Simply accessing the variable directly is actually unsafe!
### Arguments

- *volatile long long ** **ptr** - Pointer to the variable.

### Return value

Variable value.
## char AtomicSwap ( volatile char * ptr , char value )

Unigine atomic swap (8-bit).
### Arguments

- *volatile char ** **ptr** - Pointer to the variable.
- *char* **value** - Value to be set.

### Return value

Previous value (just before setting).
## bool AtomicSwap ( volatile bool * ptr , bool value )

Unigine atomic swap (8-bit).
### Arguments

- *volatile bool ** **ptr** - Pointer to the variable.
- *bool* **value** - Value to be set.

### Return value

Previous value (just before setting).
## short AtomicSwap ( volatile short * ptr , short value )

Unigine atomic swap (16-bit).
### Arguments

- *volatile short ** **ptr** - Pointer to the variable.
- *short* **value** - Value to be set.

### Return value

Previous value (just before setting).
## int AtomicSwap ( volatile int * ptr , int value )

Unigine atomic swap (32-bit).
### Arguments

- *volatile int ** **ptr** - Pointer to the variable.
- *int* **value** - Value to be set.

### Return value

Previous value (just before setting).
## long long AtomicSwap ( volatile long long * ptr , long long value )

Unigine atomic swap (64-bit).
### Arguments

- *volatile long long ** **ptr** - Pointer to the variable.
- *long long* **value** - Value to be set.

### Return value

Previous value (just before setting).
## void quickSort ( Type * array , int size )

Sorts the input array with default compare algorithm.
### Arguments

- *Type ** **array** - The array pointer.
- *int* **size** - The array size.


## void quickSort ( Type * array , int size , Compare compare )

Sorts the input array with specified compare functor.
### Arguments

- *Type ** **array** - The array pointer.
- *int* **size** - The array size.
- *Compare* **compare** - Compare functor.


## void quickSort ( Type * array , int size , int(*)(A0, A1) func )

Sorts the input array with specified compare function.
### Arguments

- *Type ** **array** - The array pointer.
- *int* **size** - The array size.
- *int(*)(A0, A1)* **func** - Compare function.


## void quickDoubleSort ( Type * array , Data * data , int size )

Sorts the input array with default compare algorithm.
### Arguments

- *Type ** **array** - The array pointer.
- *Data ** **data** - The data pointer.
- *int* **size** - The array size.


## void quickDoubleSort ( Type * array , Data * data , int size , Compare compare )

Sorts the input array with specified compare functor.
### Arguments

- *Type ** **array** - The array pointer.
- *Data ** **data** - The data pointer.
- *int* **size** - The array size.
- *Compare* **compare** - Compare functor.


## void quickDoubleSort ( Type * array , Data * data , int size , int(*)(A0, A1) func )

Sorts the input array with specified compare function.
### Arguments

- *Type ** **array** - The array pointer.
- *Data ** **data** - The data pointer.
- *int* **size** - The array size.
- *int(*)(A0, A1)* **func** - Compare function.


## template < typename State , typename Process , typename Destroy >

## CPUShader * makeCPUShader ( Process func_process , Destroy func_destroy , CPUShader::PoolType pool_ = CPUShader::PoolType::Auto , CPUShader::Priority priority_ = CPUShader::Priority::Normal , CPUShader::FrameSyncMode frame_sync_ = CPUShader::FrameSyncMode::Swap , CPUShader::WaitMode wait_mode_ = CPUShader::WaitMode::Auto )

Creates a **[CPUShaderCallable](../../../api/library/common/mt/class.cpushadercallable_cpp.md)** on the heap with processing logic, cleanup logic, and shared state of type **State**.
### Arguments

- *Process* **func_process** - Function executed on each thread. Signature: *void(CPUShader *shader, int thread_num, int num_threads)*.
- *Destroy* **func_destroy** - Cleanup function called during destruction. Signature: *void(State state)*.
- *[CPUShader::PoolType](#PoolType)* **pool_** - Target execution pool.
- *[CPUShader::Priority](#Priority)* **priority_** - Task priority in the pool queue.
- *[CPUShader::FrameSyncMode](#FrameSyncMode)* **frame_sync_** - Frame synchronization mode.
- *[CPUShader::WaitMode](#WaitMode)* **wait_mode_** - Wait strategy for [wait()](../../../api/library/common/mt/class.cpushader_cpp.md#wait_void).

### Return value

Heap-allocated shader instance. The caller is responsible for deletion.
## template < typename State , typename Process >

## CPUShader * makeCPUShader ( Process func_process , CPUShader::PoolType pool_ = CPUShader::PoolType::Auto , CPUShader::Priority priority_ = CPUShader::Priority::Normal , CPUShader::FrameSyncMode frame_sync_ = CPUShader::FrameSyncMode::Swap , CPUShader::WaitMode wait_mode_ = CPUShader::WaitMode::Auto )

Creates a **[CPUShaderCallable](../../../api/library/common/mt/class.cpushadercallable_cpp.md)** on the heap with processing logic and shared state of type **State**. A no-op destroy function is used.
### Arguments

- *Process* **func_process** - Function executed on each thread. Signature: *void(CPUShader *shader, int thread_num, int num_threads)*.
- *[CPUShader::PoolType](#PoolType)* **pool_** - Target execution pool.
- *[CPUShader::Priority](#Priority)* **priority_** - Task priority in the pool queue.
- *[CPUShader::FrameSyncMode](#FrameSyncMode)* **frame_sync_** - Frame synchronization mode.
- *[CPUShader::WaitMode](#WaitMode)* **wait_mode_** - Wait strategy for [wait()](../../../api/library/common/mt/class.cpushader_cpp.md#wait_void).

### Return value

Heap-allocated shader instance. The caller is responsible for deletion.
## template < typename Process >

## CPUShader * makeCPUShaderStateless ( Process func_process , CPUShader::PoolType pool_ = CPUShader::PoolType::Auto , CPUShader::Priority priority_ = CPUShader::Priority::Normal , CPUShader::FrameSyncMode frame_sync_ = CPUShader::FrameSyncMode::Swap , CPUShader::WaitMode wait_mode_ = CPUShader::WaitMode::Auto )

Creates a **[CPUShaderCallableStateless](../../../api/library/common/mt/class.cpushadercallablestateless_cpp.md)** on the heap with processing logic and no shared state.
### Arguments

- *Process* **func_process** - Function executed on each thread. Signature: *void(CPUShader *shader, int thread_num, int num_threads)*.
- *[CPUShader::PoolType](#PoolType)* **pool_** - Target execution pool.
- *[CPUShader::Priority](#Priority)* **priority_** - Task priority in the pool queue.
- *[CPUShader::FrameSyncMode](#FrameSyncMode)* **frame_sync_** - Frame synchronization mode.
- *[CPUShader::WaitMode](#WaitMode)* **wait_mode_** - Wait strategy for [wait()](../../../api/library/common/mt/class.cpushader_cpp.md#wait_void).

### Return value

Heap-allocated shader instance. The caller is responsible for deletion.
## template < typename Process >

## CPUShaderCallableStateless<Process> makeScopeCPUShaderStateless ( Process func_process , CPUShader::PoolType pool_ = CPUShader::PoolType::Auto , CPUShader::Priority priority_ = CPUShader::Priority::Normal , CPUShader::FrameSyncMode frame_sync_ = CPUShader::FrameSyncMode::Swap , CPUShader::WaitMode wait_mode_ = CPUShader::WaitMode::Auto )

Creates a **[CPUShaderCallableStateless](../../../api/library/common/mt/class.cpushadercallablestateless_cpp.md)** on the stack (by value). The shader is destroyed when it goes out of scope.
### Arguments

- *Process* **func_process** - Function executed on each thread. Signature: *void(CPUShader *shader, int thread_num, int num_threads)*.
- *[CPUShader::PoolType](#PoolType)* **pool_** - Target execution pool.
- *[CPUShader::Priority](#Priority)* **priority_** - Task priority in the pool queue.
- *[CPUShader::FrameSyncMode](#FrameSyncMode)* **frame_sync_** - Frame synchronization mode.
- *[CPUShader::WaitMode](#WaitMode)* **wait_mode_** - Wait strategy for [wait()](../../../api/library/common/mt/class.cpushader_cpp.md#wait_void).

### Return value

Stack-allocated shader instance.
## template < typename Process >

## void runSyncMultiThreadFunc ( Process func_process , int num_threads = -1 , CPUShader::PoolType pool_ = CPUShader::PoolType::Auto , CPUShader::Priority priority_ = CPUShader::Priority::Normal , CPUShader::FrameSyncMode frame_sync_ = CPUShader::FrameSyncMode::Swap , CPUShader::WaitMode wait_mode_ = CPUShader::WaitMode::Auto )

Convenience function that creates a **[CPUShaderCallableStateless](../../../api/library/common/mt/class.cpushadercallablestateless_cpp.md)** on the stack, runs it synchronously via [runSync()](../../../api/library/common/mt/class.cpushader_cpp.md#runSync_int_void), and returns after all threads finish.
### Arguments

- *Process* **func_process** - Function executed on each thread. Signature: *void(CPUShader *shader, int thread_num, int num_threads)*.
- *int* **num_threads** - Number of threads to use. A value of -1 uses the pool's default thread count.
- *[CPUShader::PoolType](#PoolType)* **pool_** - Target execution pool.
- *[CPUShader::Priority](#Priority)* **priority_** - Task priority in the pool queue.
- *[CPUShader::FrameSyncMode](#FrameSyncMode)* **frame_sync_** - Frame synchronization mode.
- *[CPUShader::WaitMode](#WaitMode)* **wait_mode_** - Wait strategy for [wait()](../../../api/library/common/mt/class.cpushader_cpp.md#wait_void).


## template < typename Callable >

## CPUTask * makeCPUTask ( Callable callable , CPUTask::Priority priority_ = CPUTask::Priority::Normal , CPUTask::FrameSyncMode frame_sync_ = CPUTask::FrameSyncMode::Disabled )

Creates an **[AsyncTaskCallable](../../../api/library/common/mt/class.asynctaskcallable_cpp.md)** on the heap with processing logic. A no-op destroy function is used.
### Arguments

- *Callable* **callable** - Function executed when the task runs. Signature: *void(CPUTask *task)*.
- *[CPUTask::Priority](#Priority)* **priority_** - Task priority in the pool queue.
- *[CPUTask::FrameSyncMode](#FrameSyncMode)* **frame_sync_** - Frame synchronization mode.

### Return value

Heap-allocated task instance. The caller is responsible for deletion.
## template < typename Callable , typename Destroy >

## CPUTask * makeCPUTask ( Callable callable , Destroy destroy , CPUTask::Priority priority_ = CPUTask::Priority::Normal , CPUTask::FrameSyncMode frame_sync_ = CPUTask::FrameSyncMode::Disabled )

Creates an **[AsyncTaskCallable](../../../api/library/common/mt/class.asynctaskcallable_cpp.md)** on the heap with processing logic and a custom cleanup function.
### Arguments

- *Callable* **callable** - Function executed when the task runs. Signature: *void(CPUTask *task)*.
- *Destroy* **destroy** - Cleanup function called during destruction. Signature: *void()*.
- *[CPUTask::Priority](#Priority)* **priority_** - Task priority in the pool queue.
- *[CPUTask::FrameSyncMode](#FrameSyncMode)* **frame_sync_** - Frame synchronization mode.

### Return value

Heap-allocated task instance. The caller is responsible for deletion.
