# Unigine::AtomicLockFreeRaw<Type> Struct (CPP)

**Header:** #include <UnigineThread.h>


AtomicLockFreeRaw<Type> is a low-level, lock-free atomic implementation used when the type <Type> has the same binary size and layout as one of the supported raw integer types (*char, short, int, long long*).


**Template Parameters:**


- **Type** - The type of the stored value.
- Internally, the data is stored as **RawType**, derived from getRawType<**Type**> to match the underlying binary representation.


## AtomicLockFreeRaw<Type> Struct

### Members

---

## AtomicLockFreeRaw ( )

Default constructor.
## AtomicLockFreeRaw ( Type v )

Constructor. Initializes the value by copying the binary representation of the provided value.
### Arguments

- *Type* **v** - Initial value.

## AtomicLockFreeRaw ( const AtomicLockFreeRaw& v )

Copy constructor. Initializes the object by copying the raw value from another atomic object, ensuring atomic consistency.
### Arguments

- *const AtomicLockFreeRaw&* **v**

## Type operator Type() ( ) const

Implicitly converts the **AtomicLockFreeRaw** object to a value of type **Type**. Internally calls *[fetch()](#fetch_Type)* to return a thread-safe snapshot of the current value.
### Return value

Returns copy of the current value.
## RawType & getUnsafeRawValue ( )

Provides direct, non-synchronized access to the internal raw value. Calling this bypasses all thread safety and must only be used when external synchronization is guaranteed by the caller.
### Return value

Returns a reference to the internal raw value.
## const RawType & getUnsafeRawValue ( ) const

Const-qualified version of *[getUnsafeRawValue()](#getUnsafeRawValue_int_ref)*. Provides read-only, non-thread-safe access to the stored value.
### Return value

Returns a const reference to the internal raw value.
## RawType * getRawValuePtr ( )

Returns a pointer to the internal raw value.
### Return value

Returns a pointer to the internal raw value.
## const RawType * getRawValuePtr ( ) const

Const-qualified version of *[getRawValuePtr()](#getRawValuePtr_int_ptr)*. Provides read-only, non-thread-safe access to the stored value.
### Return value

Returns a const pointer to the internal raw value.
## Type & getUnsafeValue ( )

Provides direct, non-synchronized access to the internal logical value, **reinterpreted from the raw data**. Unsafe in multithreaded contexts unless externally synchronized.
### Return value

Returns non-thread-safe reference to the stored value.
## const Type & getUnsafeValue ( ) const

Const-qualified version of *[getUnsafeValue()](#getUnsafeValue_Type_ref)*. Provides read-only, non-thread-safe access to the stored value.
### Return value

Returns non-thread-safe const reference to the stored value.
## Type * getValuePtr ( )

Returns a raw pointer to the internal value, **reinterpreted from the raw data**. Unsafe in multithreaded contexts unless externally synchronized.
### Return value

Returns pointer to the internal value.
## const Type * getValuePtr ( ) const

Const-qualified version of *[getValuePtr()](#getValuePtr_Type_ptr)*. Provides read-only, non-thread-safe access to the stored value.
### Return value

Returns const pointer to the internal value.
## Type fetch ( ) const

Retrieves the current value in a lock-free, thread-safe manner. Performs an atomic read of the raw internal storage and reinterprets the result.
### Return value

Returns copy of the stored value.
## void store ( Type v )

Stores a new value by writing its raw binary representation atomically into internal storage.
### Arguments

- *Type* **v** - The new value to store.

## Type operator= ( Type v )

Copy assignment operator. Stores the new value atomically by calling *[store()](#store_Type_void)*.
### Arguments

- *Type* **v** - The new value to assign.

### Return value

Returns the assigned value.
## Type operator= ( const AtomicLockFreeRaw& v )

Copy assignment operator. Atomically replaces the internal value with the one from another atomic object.
### Arguments

- *const AtomicLockFreeRaw&* **v** - Another atomic to copy from.

### Return value

Returns the copied value.
## Type swap ( Type v )

Atomically replaces the current value with a new one and returns the old value.
### Arguments

- *Type* **v** - The new value to set.

### Return value

Returns the value that was stored before swap.
## bool compareAndSwap ( Type old_value , Type new_value )

Performs a **lock-free** *compare-and-swap* operation. If the current value equals old_value, it is replaced with new_value.
### Arguments

- *Type* **old_value** - Expected current value.
- *Type* **new_value** - New value to assign if the current matches the expected.

### Return value

Returns true if the internal value was updated; false if the current value did not match old_value.
## void spinLock ( Type old_value , Type new_value )

Continuously attempts to atomically swap the value from old_value to new_value using *[compareAndSwap()](#compareAndSwap_Type_Type_bool)*.
### Arguments

- *Type* **old_value** - Expected current value.
- *Type* **new_value** - New value to assign if the current matches the expected.

## void waitValue ( Type v )

Blocks the current thread in a spin loop until the internal value becomes equal to the provided one. Internally calls *[spinLock(v, v)](#spinLock_Type_Type_void)* and rechecks after each failure.
### Arguments

- *Type* **v** - The value to wait for.
