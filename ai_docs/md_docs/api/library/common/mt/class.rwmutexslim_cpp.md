# Unigine::WinAPI::RWMutexSlim Class (CPP)

**Header:** #include <UnigineThread.h>


A ***Windows-specific*** reader-writer mutex implementation that wraps a *Slim Reader/Writer Lock* object using RAII (Resource Acquisition Is Initialization) principles. It uses functions from the *Unigine::WinAPI* namespace and is intended for Windows-only builds.


This class allows concurrent shared (read) access and exclusive (write) access.


> **Notice:** You can learn more about ***SRW Locks*** [here](https://learn.microsoft.com/en-us/windows/win32/sync/slim-reader-writer--srw--locks).


## RWMutexSlim Class

### Members

---

## RWMutexSlim ( )

Constructor. Initializes the internal **SRWLOCK** by calling *WinAPI::InitializeSRWLock*.
## ~RWMutexSlim ( )

Destructor. Asserts that the lock is not held during destruction.
## void lockRead ( )

Acquires a shared (read) lock. Multiple threads can hold the read lock concurrently.
## bool tryLockRead ( )

Attempts to acquire a shared (read) lock without blocking.
## void unlockRead ( )

Releases a shared (read) lock previously acquired.
## void lockWrite ( )

Acquires an exclusive (write) lock. Blocks until no other thread holds a read or write lock.
## bool tryLockWrite ( )

Attempts to acquire an exclusive (write) lock without blocking.
## void unlockWrite ( )

Releases an exclusive (write) lock previously acquired.
## void lock ( )

Alias for *[lockWrite()](#lockWrite_void)*. Allows ***RWMutexSlim*** to be used in generic locking interfaces.
## bool tryLock ( )

Alias for *[tryLockWrite()](#tryLockWrite_bool)*. Allows ***RWMutexSlim*** to be used in generic locking interfaces.
## void unlock ( )

Alias for *[unlockWrite()](#unlockWrite_void)*. Allows ***RWMutexSlim*** to be used in generic locking interfaces.
