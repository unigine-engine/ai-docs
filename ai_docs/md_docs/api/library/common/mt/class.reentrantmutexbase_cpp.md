# Unigine::ReentrantMutexBase<MutexType> Class (CPP)

**Header:** #include <UnigineThread.h>


Template class that implements a basic reentrant (recursive) mutex using a user-defined mutex type. This class allows a single thread to acquire the same lock multiple times without causing a deadlock, by tracking the locking depth and thread ownership.


It provides basic mutual exclusion features suitable for multithreaded environments where reentrancy is required.


***MutexType*** - The underlying mutex type used for locking. The type must provide *lock()*, *tryLock()*, *unlock()* methods.


This class has following aliases:


| Alias | Description | Type |
|---|---|---|
| **ReentrantMutexSpin ReentrantMutex** | Alias for **ReentrantMutexBase** using **[MutexSpin](../../../../api/library/common/mt/class.mutexspin_cpp.md)** as the underlying mutex. Provides recursive spinlock functionality. | **[MutexSpin](../../../../api/library/common/mt/class.mutexspin_cpp.md)** |
| **ReentrantMutexSlim** | Alias for **ReentrantMutexBase** using **[MutexSlim](../../../../api/library/common/mt/class.mutexslim_cpp.md)** as the underlying lock. Provides recursive locking via Windows ***SRW lock***. | **[MutexSlim](../../../../api/library/common/mt/class.mutexslim_cpp.md)** |
| **ReentrantMutexPThread** | Alias for **ReentrantMutexBase** using **[MutexPThread](../../../../api/library/common/mt/class.mutexpthread_cpp.md)** as the underlying lock. Provides recursive locking via Linux ***pthread_mutex_t***. | **[MutexPThread](../../../../api/library/common/mt/class.mutexpthread_cpp.md)** |


## ReentrantMutexBase<MutexType> Class

### Members

---

## ReentrantMutexBase ( )

Default constructor. Initializes the internal state, setting the lock as available.
## void lock ( )

Acquires the mutex. If the current thread already owns the lock, increments the reentrancy depth instead of re-locking the underlying mutex.
## bool tryLock ( )

Attempts to acquire the mutex without blocking. If the current thread already owns the lock, increments the reentrancy depth.
### Return value

Returns true if the mutex was successfully acquired; false if the mutex is currently held by another thread.
## void unlock ( )

Releases the mutex. If the lock has been acquired multiple times by the same thread, decrements the reentrancy depth. Once the depth reaches zero, releases the underlying mutex and clears thread ownership.
## bool isLocked ( )

Checks whether the mutex is currently considered locked by any thread.
### Return value

Returns true if the mutex is locked; false otherwise.
## void waitForce ( )

Forces the current thread to wait until the mutex becomes available by acquiring and then immediately releasing the lock.
## void wait ( )

Waits for the mutex to be released by another thread. If the mutex is currently unowned or already owned by the calling thread, the method returns immediately. Otherwise, it blocks by calling *[waitForce().](#waitForce_void)*
