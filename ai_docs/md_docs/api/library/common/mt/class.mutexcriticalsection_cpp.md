# Unigine::WinAPI::MutexCriticalSection Class (CPP)

**Header:** #include <UnigineThread.h>


A ***Windows-specific*** mutex implementation that wraps a *CRITICAL_SECTION* object using RAII (Resource Acquisition Is Initialization) principles. It uses functions from the *Unigine::WinAPI* namespace and is intended for Windows-only builds.


> **Notice:** You can learn more about ***CRITICAL_SECTION*** object [here](https://learn.microsoft.com/en-us/windows/win32/sync/critical-section-objects).


## MutexCriticalSection Class

### Members

---

## MutexCriticalSection ( )

Constructor. Initializes the internal ***CRITICAL_SECTION*** object.
## ~MutexCriticalSection ( )

Destructor. Destroys the internal ***CRITICAL_SECTION*** object.
## void lock ( )

Acquires the critical section, blocking the calling thread if necessary until the lock becomes available.
## bool tryLock ( )

Attempts to acquire the critical section without blocking.
### Return value

Returns true if the lock was successfully acquired; false otherwise.
## void unlock ( )

Releases the critical section, allowing other threads to enter.
