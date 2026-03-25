# Unigine::WinAPI::MutexSlim Class (CPP)

**Header:** #include <UnigineThread.h>


A ***Windows-specific*** mutex implementation that wraps a *Slim Reader/Writer Lock* object using RAII (Resource Acquisition Is Initialization) principles. It uses functions from the *Unigine::WinAPI* namespace and is intended for Windows-only builds.


> **Notice:** You can learn more about ***SRW Locks*** [here](https://learn.microsoft.com/en-us/windows/win32/sync/slim-reader-writer--srw--locks).


## MutexSlim Class

### Members

---

## MutexSlim ( )

Constructor. Initializes the internal **SRWLOCK** by calling *WinAPI::InitializeSRWLock*.
## ~MutexSlim ( )

Destructor. Asserts that the lock is not held during destruction.
## void lock ( )

Acquires the slim lock in exclusive (write) mode. Blocks the calling thread if the lock is already held.
## bool tryLock ( )

Attempts to acquire the slim lock in exclusive mode without blocking.
### Return value

Returns true if the mutex was successfully locked, false otherwise.
## void unlock ( )

Releases the exclusive slim lock.
