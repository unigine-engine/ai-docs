# Unigine::AtomicWithMutex<Type, MutexType> Struct (CPP)

**Header:** #include <UnigineThread.h>


Template structure that provides a **thread-safe atomic wrapper** around a user-defined value using **mutex-based synchronization** instead of lock-free atomics.


**Template Parameters:**

- **Type** - The type of the stored value. Must be copyable and comparable.
- **MutexType** - The mutex implementation used to guard access. Defaults to ***[MutexSpin](../../../../api/library/common/mt/class.mutexspin_cpp.md)***.


## AtomicWithMutex<Type, MutexType> Struct

### Members

---

## AtomicWithMutex ( )

Default constructor. Initializes the internal value with its default constructor.
## AtomicWithMutex ( const Type& v )

Constructor. Initializes the internal value with the provided input.
### Arguments

- *const Type&* **v** - Initial value.

## AtomicWithMutex ( const AtomicWithMutex& v )

Copy constructor. Locks both source and destination mutexes to safely copy the provided value.
### Arguments

- *const AtomicWithMutex&* **v**

## Type operator Type() ( ) const

Implicitly converts the **AtomicWithMutex** object to a value of type **Type**. Internally calls *[fetch()](#fetch_Type)* to return a thread-safe snapshot of the current value.
### Return value

Returns copy of the current value.
## Type & getUnsafeValue ( )

Provides direct, non-synchronized access to the internal value. Calling this bypasses all thread safety and must only be used when external synchronization is guaranteed by the caller.
### Return value

Returns non-thread-safe reference to the stored value.
## const Type & getUnsafeValue ( ) const

Const-qualified version of *[getUnsafeValue()](#getUnsafeValue_Type_ref)*. Provides read-only, non-thread-safe access to the stored value.
### Return value

Returns non-thread-safe const reference to the stored value.
## Type * getValuePtr ( )

Returns a raw pointer to the internal value without locking. Unsafe in multithreaded contexts unless externally synchronized.
### Return value

Returns pointer to the internal value.
## const Type * getValuePtr ( ) const

Const-qualified version of *[getValuePtr()](#getValuePtr_Type_ptr)*.
### Return value

Returns const pointer to the internal value.
## MutexType & getMutex ( )

Provides direct access to the internal mutex object. This allows external code to manually lock or unlock the mutex.
### Return value

Returns the reference to the mutex used for protecting the internal value.
## const MutexType & getMutex ( ) const

Const-qualified version of *[getMutex()](#getMutex_MutexType_ref)*.
### Return value

Returns the const reference to the mutex used for protecting the internal value.
## Type fetch ( ) const

Retrieves the current value in a thread-safe manner. Acquires the mutex, copies the internal value, then releases the mutex. Preferred over direct access when consistent reads are required.
### Return value

Returns copy of the stored value.
## void store ( const Type& v )

Sets the internal value to a new value in a thread-safe way. The entire assignment is protected by the mutex to avoid race conditions with readers or other writers.
### Arguments

- *const Type&* **v** - The new value to store.

## const Type & operator= ( const Type& v )

Thread-safe assignment operator that stores a new value internally. Equivalent to calling *[store()](#store_const_Type_ref_void)*.
### Arguments

- *const Type&* **v** - The new value to assign.

### Return value

Returns a const reference to the assigned value.
## Type operator= ( const AtomicWithMutex& v )

Thread-safe copy assignment from another **AtomicWithMutex**. Locks both the source and destination mutexes to prevent data races.
### Arguments

- *const AtomicWithMutex&* **v** - Another **AtomicWithMutex** to copy from.

### Return value

Returns the copied value.
## Type swap ( const Type& v )

Atomically replaces the current value with a new one and returns the old value.
### Arguments

- *const Type&* **v** - The new value to set.

### Return value

Returns the value that was stored before swap.
## bool compareAndSwap ( const Type& old_value , const Type& new_value )

Performs a *compare-and-swap* operation. If the current value equals old_value, it is replaced with new_value.
### Arguments

- *const Type&* **old_value** - Expected current value.
- *const Type&* **new_value** - New value to assign if the current matches the expected.

### Return value

true if the internal value was updated; false if the current value did not match old_value.
## void spinLock ( const Type& old_value , const Type& new_value )

Continuously attempts to atomically swap the value from old_value to new_value using *[compareAndSwap()](#compareAndSwap_const_Type_ref_const_Type_ref_bool)*.
### Arguments

- *const Type&* **old_value** - Expected current value.
- *const Type&* **new_value** - New value to assign if the current matches the expected.

## void waitValue ( const Type& v )

Blocks the current thread in a spin loop until the internal value becomes equal to the provided one. Internally calls *[spinLock(v, v)](#spinLock_const_Type_ref_const_Type_ref_void)* and rechecks after each failure.
### Arguments

- *const Type&* **v** - The value to wait for.
