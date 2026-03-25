# Unigine::ScopedMutexReaderLock<MutexType> Class (CPP)

**Header:** #include <UnigineThread.h>


Template class that implements the RAII (Resource Acquisition Is Initialization) pattern to manage mutex locking in a multithreaded environment. This class ensures that a mutex is automatically locked for reading upon construction and unlocked when the object goes out of scope.


This class has the following aliases:


| Alias | Description | Type |
|---|---|---|
| **ScopedReaderSpinLock ScopedReaderLock** | Alias for **ScopedMutexReaderLock** using **[RWMutexSpin](../../../../api/library/common/mt/class.rwmutexspin_cpp.md)** as the underlying reader-writer mutex. Provides scoped read-locking via spinlock. | **[RWMutexSpin](../../../../api/library/common/mt/class.rwmutexspin_cpp.md)** |
| **ScopedReaderSlimLock** | Alias for **ScopedMutexReaderLock** using **[RWMutexSlim](../../../../api/library/common/mt/class.rwmutexslim_cpp.md)** as the underlying reader-writer mutex. Provides scoped RAII-style shared locking via Windows ***SRW Lock***. | **[RWMutexSlim](../../../../api/library/common/mt/class.rwmutexslim_cpp.md)** |


## ScopedMutexReaderLock<MutexType> Class

### Members

---

## ScopedMutexReaderLock ( MutexType& m )

Constructor that locks the provided mutex for reading. The lock remains held for the duration of the **ScopedMutexReaderLock** object's lifetime.
### Arguments

- *MutexType&* **m** - A reference to a mutex object to be locked for reading. The mutex must provide *lockRead()* and *unlockRead()* member functions.

## ~ScopedMutexReaderLock ( )

Destructor that automatically unlocks the mutex when the **ScopedMutexReaderLock** object goes out of scope.
