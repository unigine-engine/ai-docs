# Unigine::ScopedMutexLock<MutexType> Class (CPP)

**Header:** #include <UnigineThread.h>


Template class that implements the RAII (Resource Acquisition Is Initialization) pattern to manage mutex locking in a multithreaded environment. This class ensures that a mutex is automatically locked upon construction and unlocked when the object goes out of scope.


This class has the following aliases:


| Alias | Description | Type |
|---|---|---|
| **ScopedSpinLock ScopedLock** | Alias for **ScopedMutexLock** using **[MutexSpin](../../../../api/library/common/mt/class.mutexspin_cpp.md)** class for spin-based scoped locking. Ensures the spinlock is acquired on construction and released on destruction. | **[MutexSpin](../../../../api/library/common/mt/class.mutexspin_cpp.md)** |
| **ScopedReentrantSpinLock ScopedReentrantLock** | Alias for **ScopedMutexLock** using **[ReentrantMutexSpin](../../../../api/library/common/mt/class.reentrantmutexbase_cpp.md)** enabling scoped locking of reentrant spinlocks. | **[ReentrantMutexSpin](../../../../api/library/common/mt/class.reentrantmutexbase_cpp.md)** |
| **ScopedCriticalSectionLock** | Alias for **ScopedMutexLock** using **[MutexCriticalSection](../../../../api/library/common/mt/class.mutexcriticalsection_cpp.md)**. Provides scoped RAII-style locking using a Windows ***CRITICAL_SECTION***. | **[MutexCriticalSection](../../../../api/library/common/mt/class.mutexcriticalsection_cpp.md)** |
| **ScopedSlimLock** | Alias for **ScopedMutexLock** using **[MutexSlim](../../../../api/library/common/mt/class.mutexslim_cpp.md)**. Provides scoped RAII-style locking using a Windows ***SRW Lock***. | **[MutexSlim](../../../../api/library/common/mt/class.mutexslim_cpp.md)** |
| **ScopedReentrantSlimLock** | Alias for **ScopedMutexLock** using **[ReentrantMutexSlim](../../../../api/library/common/mt/class.reentrantmutexbase_cpp.md#reentrant_mutex_slim)**. Provides scoped RAII-style locking with support for reentrance using a Windows ***SRW Lock***. | **[ReentrantMutexSlim](../../../../api/library/common/mt/class.reentrantmutexbase_cpp.md#reentrant_mutex_slim)** |
| **ScopedSlimAdvanceLock** | Alias for **ScopedMutexLock** using **[MutexSlimAdvance](../../../../api/library/common/mt/class.mutexadvance_cpp.md#mutex_slim_advance)**. Provides RAII-style scoped locking with the ability to check whether the lock is currently held using a Windows ***SRW Lock***. | **[MutexSlimAdvance](../../../../api/library/common/mt/class.mutexadvance_cpp.md#mutex_slim_advance)** |
| **ScopedCriticalSectionAdvanceLock** | Alias for **ScopedMutexLock** using **[MutexCriticalSectionAdvance](../../../../api/library/common/mt/class.mutexadvance_cpp.md#mutex_critical_section_advance)**. Provides RAII-style scoped locking with the ability to check whether the lock is currently held using a Windows ***CRITICAL_SECTION***. | **[MutexCriticalSectionAdvance](../../../../api/library/common/mt/class.mutexadvance_cpp.md#mutex_critical_section_advance)** |
| **ScopedPThreadLock** | Alias for **ScopedMutexLock** using **[MutexPThread](../../../../api/library/common/mt/class.mutexpthread_cpp.md)**. Provides scoped RAII-style locking via Linux ***pthread_mutex_t*** mutex. | **[MutexPThread](../../../../api/library/common/mt/class.mutexpthread_cpp.md)** |
| **ScopedReentrantPThreadLock** | Alias for **ScopedMutexLock** using **[ReentrantMutexPThread](../../../../api/library/common/mt/class.reentrantmutexbase_cpp.md#reentrant_mutex_pthread)**. Provides scoped locking with reentrance via Linux ***pthread_mutex_t*** mutex. | **[ReentrantMutexPThread](../../../../api/library/common/mt/class.reentrantmutexbase_cpp.md#reentrant_mutex_pthread)** |
| **ScopedPThreadAdvanceLock** | Alias for **ScopedMutexLock** using **[MutexPThreadAdvance](../../../../api/library/common/mt/class.mutexadvance_cpp.md#mutex_pthread_advance)**. Provides scoped locking with internal state tracking via Linux ***pthread_mutex_t*** mutex. | **[MutexPThreadAdvance](../../../../api/library/common/mt/class.mutexadvance_cpp.md#mutex_pthread_advance)** |


## ScopedMutexLock<MutexType> Class

### Members

---

## ScopedMutexLock ( MutexType& m )

Constructor that locks the provided mutex. The lock remains held for the duration of the **ScopedMutexLock** object's lifetime.
### Arguments

- *MutexType&* **m** - A reference to a mutex object to be locked. The mutex must provide *lock()* and *unlock()* member functions.

## ~ScopedMutexLock ( )

Destructor that automatically unlocks the mutex when the **ScopedMutexLock** object goes out of scope.
