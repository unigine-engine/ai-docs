# Unigine::AtomicPointer<Type> Struct (CPP)

**Header:** #include <UnigineThread.h>


**AtomicPointer<Type>** is a **lock-free** atomic wrapper designed specifically for working with raw pointers in a thread-safe way.


**Template Parameters:**


- **Type** - A raw pointer type (e.g., *int**, *MyStruct**)
- The pointer is stored internally as a 64-bit integer (long long).


## AtomicPointer<Type> Struct

### Members

---

## AtomicPointer ( )

Default constructor.
## AtomicPointer ( Type v )

Constructor. Constructs an atomic pointer initialized with the given raw pointer value.
### Arguments

- *Type* **v** - The pointer value to initialize with (e.g., *int**, *MyStruct**).

## AtomicPointer ( const AtomicPointer& v )

Copy constructor. Atomically copies the pointer value from another **AtomicPointer<Type>** instance.
### Arguments

- *const AtomicPointer&* **v**

## Type operator Type() ( ) const

Implicitly converts the **AtomicPointer** object to a value of type **Type**. Internally calls *[fetch()](#fetch_Type)* to return a thread-safe snapshot of the current value.
## volatile long long & getUnsafeRawValue ( )

Returns a non-atomic reference to the internal raw 64-bit representation of the pointer. Calling this bypasses all thread safety and must only be used when external synchronization is guaranteed by the caller.
### Return value

Reference to the internal value storing the pointer.
## const volatile long long & getUnsafeRawValue ( ) const

Const-qualified version of *[getUnsafeRawValue()](#getUnsafeRawValue_volatile_llong_ref)*. Provides read-only, non-thread-safe access to the stored value.
### Return value

Reference to the internal value storing the pointer.
## volatile long long * getRawValuePtr ( )

Returns a pointer to the raw storage of the atomic pointer. Calling this bypasses all thread safety and must only be used when external synchronization is guaranteed by the caller.
### Return value

Pointer to the internal value.
## const volatile long long * getRawValuePtr ( ) const

Const-qualified version of *[getRawValue()](#getRawValuePtr_volatile_llong_ptr)*. Provides read-only, non-thread-safe access to the stored value.
### Return value

Const pointer to the internal value.
## Type & getUnsafeValue ( )

Returns a non-atomic reference to the stored pointer as a typed value. Calling this bypasses all thread safety and must only be used when external synchronization is guaranteed by the caller.
### Return value

Reference to the pointer value.
## const Type & getUnsafeValue ( ) const

Const-qualified version of *[getUnsafeValue()](#getUnsafeValue_Type_ref)*. Provides read-only, non-thread-safe access to the stored value.
### Return value

Const reference to the pointer value.
## Type * getValuePtr ( )

Returns a pointer to the stored pointer value, cast to its original type.
### Return value

A typed pointer to the internal data.
## const Type * getValuePtr ( ) const

Const-qualified version of *[getValuePtr()](#getValuePtr_Type_ptr)*. Provides read-only, non-thread-safe access to the stored value.
### Return value

A typed const pointer to the internal data.
## Type fetch ( ) const

Atomically retrieves the current pointer value.
### Return value

The current pointer value.
## void store ( Type v )

Atomically stores a new pointer value.
### Arguments

- *Type* **v** - The new pointer value to store atomically.

## Type operator= ( Type v )

Atomically assigns a new raw pointer value.
### Arguments

- *Type* **v** - The new pointer value to assign.

### Return value

Returns the assigned pointer value (same as v).
## Type operator= ( const AtomicPointer& v )

Atomically copies the pointer value from another **AtomicPointer<Type>** instance.
### Arguments

- *const AtomicPointer&* **v** - Another atomic pointer of the same type to copy from.

### Return value

The newly assigned pointer value.
## Type swap ( Type v )

Atomically replaces the current pointer value with the provided value and returns the previous value.
### Arguments

- *Type* **v** - The pointer value to assign atomically.

### Return value

The pointer value that was held before the swap.
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

## Type fetchAdd ( long long v )

Atomically moves the pointer forward by a given number of positions.
### Arguments

- *long long* **v** - The number of elements to add; internally multiplied by sizeof(*Type). (e.g. If **Type** = *int** and v = 2, the pointer is advanced by 2 * 4 = 8 bytes.

### Return value

Returns the value held before the addition.
## Type fetchSub ( long long v )

Atomically moves the pointer backward by a given number of positions.
### Arguments

- *long long* **v** - The number of elements to subtract; internally multiplied by sizeof(*Type). (e.g. If **Type** = *int** and v = 2, the pointer is moved backward by 2 * 4 = 8 bytes.

### Return value

Returns the value held before the subtraction.
## Type fetchInc ( )

Atomically increments the pointer by one position.
### Return value

Returns the value held before the increment.
## Type fetchDec ( )

Atomically decrements the pointer by one position.
### Return value

Returns the value held before the decrement.
## Type operator+= ( long long v )

Atomically moves the pointer by a given number of positions.
### Arguments

- *long long* **v** - The number of elements to add; internally multiplied by sizeof(*Type). (e.g. If **Type** = *int** and v = 2, the pointer is advanced by 2 * 4 = 8 bytes.

### Return value

Returns the value held after the addition.
## Type operator-= ( long long v )

Atomically moves the pointer backward by a given number of positions.
### Arguments

- *long long* **v** - The number of elements to subtract; internally multiplied by sizeof(*Type). (e.g. If **Type** = *int** and v = 2, the pointer is moved backward by 2 * 4 = 8 bytes.

### Return value

Returns the value held after the subtraction.
## Type operator++ ( int )

Atomically increments the pointer by one position (postfix form).
### Arguments

- *int*  - dummy parameter to distinguish from the prefix version.

### Return value

Postfix increment. Returns the value held before the increment.
## Type operator-- ( int )

Atomically decrements the pointer by one position (postfix form).
### Arguments

- *int*  - dummy parameter to distinguish from the prefix version.

### Return value

Postfix decrement. Returns the value held before the decrement.
## Type operator++ ( )

Prefix increment. Atomically increments the pointer by one position.
### Return value

Returns the value held after the increment.
## Type operator-- ( )

Prefix decrement. Atomically decrements the pointer by one position.
### Return value

Returns the value held after the decrement.
