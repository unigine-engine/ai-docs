# Unigine::RWMutexSpin Class (CPP)

**Header:** #include <UnigineThread.h>


A spin-based reader-writer mutex implementation that allows multiple concurrent readers or exclusive access for a single writer. Internally uses atomic operations and **[BackoffSpinner](../../../../api/library/common/mt/class.backoffspinner_cpp.md)** class to manage access.


This class has the following aliases:


| Alias | Description |
|---|---|
| **RWMutex** | Default alias for **RWMutexSpin**. |


## RWMutexSpin Class

### Members

---

## RWMutexSpin ( )

Default constructor. Initializes the internal lock state with no active readers or writers.
## void lockRead ( )

Acquires a shared (read) lock. Multiple threads can acquire read access concurrently as long as no writer holds the lock.
## bool tryLockRead ( )

Attempts to acquire a read lock without blocking. Fails if a writer currently holds the lock.
### Return value

Returns true if the read lock was successfully acquired; false otherwise.
## void unlockRead ( )

Releases a previously acquired read lock by decrementing the reader count.
## void lockWrite ( )

Acquires an exclusive (write) lock. Blocks until no other thread holds a read or write lock.
## bool tryLockWrite ( )

Attempts to acquire a write lock without blocking. Succeeds only if no readers or writers currently hold the lock.
### Return value

Returns true if the write lock was successfully acquired; false otherwise.
## void unlockWrite ( )

Releases a previously acquired write lock by resetting the writer flag.
## void lock ( )

Alias for *[lockWrite()](#lockWrite_void)*. Allows ***RWMutexSpin*** to be used in generic locking interfaces.
## bool tryLock ( )

Alias for *[tryLockWrite()](#tryLockWrite_bool)*. Allows ***RWMutexSpin*** to be used in generic locking interfaces.
## void unlock ( )

Alias for *[unlockWrite()](#unlockWrite_void)*. Allows ***RWMutexSpin*** to be used in generic locking interfaces.
