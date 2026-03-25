# Unigine::ScopedMutexWriterLock<MutexType> Class (CPP)

**Header:** #include <UnigineThread.h>


Template class that implements the RAII (Resource Acquisition Is Initialization) pattern to manage mutex locking in a multithreaded environment. This class ensures that a mutex is automatically locked for writing upon construction and unlocked when the object goes out of scope.


This class has following aliases:


| Alias | Description | Type |
|---|---|---|
| **ScopedWriterSpinLock ScopedWriterLock** | Alias for **ScopedMutexWriterLock** using **[RWMutexSpin](../../../../api/library/common/mt/class.rwmutexspin_cpp.md)** as the underlying reader-writer mutex. Provides scoped write-locking via spinlock. | **[RWMutexSpin](../../../../api/library/common/mt/class.rwmutexspin_cpp.md)** |
| **ScopedWriterSlimLock** | Alias for **ScopedMutexWriterLock** using **[RWMutexSlim](../../../../api/library/common/mt/class.rwmutexslim_cpp.md)** as the underlying reader-writer mutex. Provides scoped RAII-style exclusive locking via Windows ***SRW Lock***. | **[RWMutexSlim](../../../../api/library/common/mt/class.rwmutexslim_cpp.md)** |


## ScopedMutexWriterLock<MutexType> Class

### Members

---

## ScopedMutexWriterLock ( MutexType& m )

Constructor that locks the provided mutex for writing. The lock remains held for the duration of the **ScopedMutexWriterLock** object's lifetime.
### Arguments

- *MutexType&* **m** - A reference to a mutex object to be locked for writing. The mutex must provide *lockWrite()* and *unlockWrite()* member functions.

## ~ScopedMutexWriterLock ( )

Destructor that automatically unlocks the mutex when the **ScopedMutexWriterLock** object goes out of scope.
