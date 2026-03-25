# Unigine::MutexAdvance<MutexType> Class (CPP)

**Header:** #include <UnigineThread.h>


Template class that wraps a generic mutex type with additional lock state tracking for faster lock state queries and reduced contention in some concurrent scenarios.


By maintaining an atomic flag (*is_locked*), this class allows quick checks for lock status without acquiring the underlying mutex, while providing standard locking interfaces.


***MutexType*** - The underlying mutex type used for locking. The type must provide *lock()*, *tryLock()*, *unlock()* methods.


This class has the following aliases:


| Alias | Description | Type |
|---|---|---|
| **MutexSlimAdvance** | Alias for **MutexAdvance** using **[MutexSlim](../../../../api/library/common/mt/class.mutexslim_cpp.md)** as the base mutex. Adds lock state tracking to a Windows ***SRW Lock***. | **[MutexSlim](../../../../api/library/common/mt/class.mutexslim_cpp.md)** |
| **MutexCriticalSectionAdvance** | Alias for **MutexAdvance** using **[MutexCriticalSection](../../../../api/library/common/mt/class.mutexcriticalsection_cpp.md)** as the base mutex. Adds lock state tracking to a Windows ***CRITICAL_SECTION***. | **[MutexCriticalSection](../../../../api/library/common/mt/class.mutexcriticalsection_cpp.md)** |
| **MutexPThreadAdvance** | Alias for **MutexAdvance** using **[MutexPThread](../../../../api/library/common/mt/class.mutexpthread_cpp.md)** as the base mutex. Adds lock state tracking to a Linux ***pthread_mutex_t***. | **[MutexPThread](../../../../api/library/common/mt/class.mutexpthread_cpp.md)** |


## MutexAdvance<MutexType> Class

### Members

---

## MutexAdvance ( )

Default constructor. Initializes the internal mutex and sets the lock state to unlocked.
## void lock ( )

Acquires the internal mutex and marks the lock state as active.
## void unlock ( )

Releases the internal mutex and marks the lock state as inactive.
## bool tryLock ( )

Attempts to acquire the lock without blocking. First checks the internal flag for a fast-path rejection, then tries to acquire the underlying mutex.
### Return value

Returns true if the lock was successfully acquired, false otherwise.
## bool isLocked ( )

Returns the current lock status of the mutex by checking the internal flag.
### Return value

Returns true if the lock is currently held, false otherwise.
## void waitForce ( )

Forces the current thread to wait by acquiring and immediately releasing the lock.
## void wait ( )

Waits for the mutex to be released if it is currently locked. Returns immediately if the lock is not held.
