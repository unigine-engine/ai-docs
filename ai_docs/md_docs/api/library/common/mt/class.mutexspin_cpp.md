# Unigine::MutexSpin Class (CPP)

**Header:** #include <UnigineThread.h>


A lightweight spinlock-based mutex implementation for low-overhead synchronization in multithreaded environments. Instead of blocking, this mutex continuously checks the lock state in a loop (spins) until it becomes available.


This class has the following aliases:


| Alias | Description |
|---|---|
| **Mutex** | Default alias for **MutexSpin**. |


## MutexSpin Class

### Members

---

## MutexSpin ( )

Default constructor. Initializes the internal lock state to unlocked.
## void lock ( )

Acquires the spinlock by continuously checking the internal lock variable until it becomes available. Once the lock is acquired, sets the lock state.
## bool tryLock ( )

Attempts to acquire the spinlock without blocking.
### Return value

Returns true if the lock was successfully acquired; false if the lock is already held by another thread.
## void unlock ( )

Releases the spinlock by setting the internal lock variable to the unlocked state.
## bool isLocked ( ) const

Checks whether the spinlock is currently held by any thread.
### Return value

Returns true if the spinlock is currently locked; false otherwise.
## void wait ( )

Spins until the lock becomes free without attempting to acquire it.
