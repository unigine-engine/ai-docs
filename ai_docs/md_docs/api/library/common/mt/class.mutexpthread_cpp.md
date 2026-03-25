# Unigine::UnixAPI::MutexPThread Class (CPP)

**Header:** #include <UnigineThread.h>


A ***Linux-specific*** mutex implementation that wraps a *pthread_mutex_t* object using RAII (Resource Acquisition Is Initialization) principles. It uses functions from the *Unigine::UnixAPI* namespace and is intended for Linux-only builds.


> **Notice:** You can learn more about ***pthread_mutex_t*** [here](https://pubs.opengroup.org/onlinepubs/7908799/xsh/pthread_mutex_lock.html).


## MutexPThread Class

### Members

---

## MutexPThread ( )

Constructor. Initializes the internal ***pthread_mutex_t*** with default attributes.
## ~MutexPThread ( )

Destructor. Destroys the internal mutex. Must not be called while the mutex is locked.
## void lock ( )

Blocks the calling thread until the mutex becomes available and then locks it.
## bool tryLock ( )

Attempts to lock the mutex without blocking.
### Return value

Returns true if the mutex was successfully locked, false otherwise.
## void unlock ( )

Releases the mutex, allowing other threads to acquire it.
