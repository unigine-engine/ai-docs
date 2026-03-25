# Unigine::ScopedSpinLockInteger<Type> Class (CPP)

**Header:** #include <UnigineThread.h>


Template class that implements the lock management pattern using spinlocks for synchronizing access to shared data in a multithreaded environment. This class is used to acquire and release a lock for the duration of the object's lifetime, ensuring that the lock is automatically released when the object goes out of scope.


```cpp
volatile int lock = 0;									// Lockable variable

// Define a scope
{
	ScopedSpinLockInteger<int> lock_guard(lock);		// Lock is acquired here

	Log::message("Critical section accessed!");			// Some actions in critical section

}														// Lock is automatically released here

```


This class has following aliases:


| Alias | Description | Type |
|---|---|---|
| **ScopedSpinLockChar** **ScopedSpinLock8** | Alias for **ScopedSpinLockInteger** using char type (8-bit) | char |
| **ScopedSpinLockShort** **ScopedSpinLock16** | Alias for **ScopedSpinLockInteger** using short type (16-bit) | short |
| **ScopedSpinLockInt** **ScopedSpinLock32** | Alias for **ScopedSpinLockInteger** using int type (32-bit) | int |
| **ScopedSpinLockLongLong** **ScopedSpinLock64** | Alias for **ScopedSpinLockInteger** using long long type (64-bit) | long long |


## ScopedSpinLockInteger<Type> Class

### Members

---

## ScopedSpinLockInteger ( volatile Type& m )

Constructor that acquires the spinlock for the provided mutex object. Calls the *[MutexSpinLock](../../../../api/library/common/class.unigine.namespace_cpp.md#MutexSpinLock_volatiletmpl_void)* function to acquire the lock. The lock will remain active until the **ScopedSpinLockInteger** object goes out of scope.
### Arguments

- *volatile Type&* **m** - A reference to the object of type *volatile Type* that represents the lockable variable.

## ~ScopedSpinLockInteger ( )

Destructor that releases the spinlock by calling the *[MutexSpinUnlock](../../../../api/library/common/class.unigine.namespace_cpp.md#MutexSpinUnlock_volatiletmpl_void)* function.
