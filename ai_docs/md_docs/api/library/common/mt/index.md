# Multithreading Functionality


UNIGINE Multithreading Functionality provides cross-platform, low and high-level abstractions for building efficient multithreaded systems.


It includes thread management, mutual exclusion primitives (mutexes), scoped lock wrappers, and full set of atomic operations and classes.


### Thread Management


The **[Thread](../../../../api/library/common/mt/class.thread_cpp.md)** class is the base class for creating and managing threads. Inherit from it and implement the *process()* method to define your custom thread logic.


The **[ThreadsPool](../../../../api/library/common/mt/class.threadspool_cpp.md)** class is the engine CPU work scheduler that distributes **[CPUTask](../../../../api/library/common/mt/class.cputask_cpp.md)** and **[CPUShader](../../../../api/library/common/mt/class.cpushader_cpp.md)** jobs across dedicated worker pools (sync, async, critical, common, background, render-flush, file-stream, GPU-stream) and the main thread.


**[ProcessTask](../../../../api/library/common/mt/class.processtask_cpp.md)** is a convenience base class for recurring tasks � it wraps **CPUTask** with a loop and a mutex guard, so you only need to implement a work step and a continuation check.


### Mutexes and Locks


**Mutexes** (mutual exclusions) are the primary tool for preventing simultaneous access to shared resources. UNIGINE provides various mutex types optimized for spinlocks, native system APIs, and reentrant behavior.


In most cases, you will only need a limited set of high-level classes and aliases that provide efficient and safe synchronization out of the box:


- *[Mutex](../../../../api/library/common/mt/class.mutexspin_cpp.md)* - default mutex type using spinlock.
- *[ScopedLock](../../../../api/library/common/mt/class.scopedmutexlock_cpp.md)* - scoped lock for *Mutex*.
- *[ReentrantMutex](../../../../api/library/common/mt/class.reentrantmutexbase_cpp.md)* - reentrant mutex based on spinlock.
- *[ScopedReentrantLock](../../../../api/library/common/mt/class.scopedmutexlock_cpp.md)* - scoped lock for *ReentrantMutex*.
- *[RWMutex](../../../../api/library/common/mt/class.rwmutexspin_cpp.md)* - default readers-writer mutex based on spinlock.
- *[ScopedReaderLock](../../../../api/library/common/mt/class.scopedmutexreaderlock_cpp.md)* - scoped read lock for *RWMutex*.
- *[ScopedWriterLock](../../../../api/library/common/mt/class.scopedmutexwriterlock_cpp.md)* - scoped write lock for *RWMutex*.


If you need more control, platform-specific integration, or lower-level performance tuning, the library also provides spin-based mutexes, wrappers for native system APIs, scoped lock templates, and advanced mutex types with lock-state tracking.


For platform-specific native mutex implementations, the following aliases resolve to **[MutexSlim](../../../../api/library/common/mt/class.mutexslim_cpp.md)** (SRW Lock) on Windows and **[MutexPThread](../../../../api/library/common/mt/class.mutexpthread_cpp.md)** (pthread_mutex_t) on Linux:


| Native Alias | Windows | Linux |
|---|---|---|
| **MutexNative** | MutexSlim | MutexPThread |
| **ScopedNativeLock** | ScopedSlimLock | ScopedPThreadLock |
| **MutexNativeAdvance** | MutexSlimAdvance | MutexPThreadAdvance |
| **ScopedNativeAdvanceLock** | ScopedSlimAdvanceLock | ScopedPThreadAdvanceLock |
| **ReentrantMutexNative** | ReentrantMutexSlim | ReentrantMutexPThread |
| **ScopedReentrantNativeLock** | ScopedReentrantSlimLock | ScopedReentrantPThreadLock |
| **RWMutexNative** | RWMutexSlim | RWMutex (RWMutexSpin) |
| **ScopedReaderNativeLock** | ScopedReaderSlimLock | ScopedReaderLock |
| **ScopedWriterNativeLock** | ScopedWriterSlimLock | ScopedWriterLock |


### Atomics


Atomic types are essential for building safe and performant multithreaded applications. They allow shared data to be accessed and modified concurrently without introducing race conditions.


This atomic system provides a general-purpose **Atomic<Type>** template that automatically selects the most suitable underlying implementation: ***lock-free*** or ***mutex-based***, depending on the size and type of the provided ***Type***. This selection is fully resolved at compile time.


> **Notice:** Use the generic ***Atomic<T>*** template as your default choice. It automatically selects the most efficient implementation (lock-free or mutex-based) based on the type at compile time.


The **Atomic<Type>** template chooses between several internal implementations using type traits and size evaluations. The decision logic is based on both type category (integer, pointer, etc.) and data size, with specific checks for 8-bit, 16-bit, 32-bit, and 64-bit sizes. Based on this, a suitable raw storage type is chosen:


- **[AtomicInteger<Type>](../../../../api/library/common/mt/class.atomicinteger_cpp.md)** Used for standard integer types up to 64 bits (like int, short, long long, etc.), except for bool. This type supports atomic arithmetic and bitwise operations and is always lock-free.
- **[AtomicPointer<Type>](../../../../api/library/common/mt/class.atomicpointer_cpp.md)** Specialized for pointer types. Supports atomic pointer arithmetic and CAS operations. Also lock-free and size-aware.
- **AtomicLockFree<Type>** For all other trivially copyable types up to 64 bits:

  - **[AtomicLockFreeRaw<Type>](../../../../api/library/common/mt/class.atomiclockfreeraw_cpp.md)** is used if the size matches exactly with the raw type.
  - **[AtomicLockFreeAlign<Type>](../../../../api/library/common/mt/class.atomiclockfreealign_cpp.md)** is used when type casting with unions is required to match size.
- **[AtomicWithMutex<Type>](../../../../api/library/common/mt/class.atomicwithmutex_cpp.md)** Fallback for types larger than 64 bits or not trivially copyable. This version is not lock-free but supports any type.


To simplify usage the following aliases are provided:


```cpp
// Boolean
using AtomicBool = Atomic<bool>;

// Signed integers
using AtomicInt8   = Atomic<char>;
using AtomicInt16  = Atomic<short>;
using AtomicInt32  = Atomic<int>;
using AtomicInt64  = Atomic<long long>;

// Unsigned integers
using AtomicUInt8  = Atomic<unsigned char>;
using AtomicUInt16 = Atomic<unsigned short>;
using AtomicUInt32 = Atomic<unsigned int>;
using AtomicUInt64 = Atomic<unsigned long long>;

// Floating point
using AtomicFloat  = Atomic<float>;
using AtomicDouble = Atomic<double>;

```


## Articles in This Section

- [Thread Class (CPP)](../../../../api/library/common/mt/class.thread_cpp.md)

- [ThreadsPool Class (CPP)](../../../../api/library/common/mt/class.threadspool_cpp.md)

- [CPUShader Class (CPP)](../../../../api/library/common/mt/class.cpushader_cpp.md)

- [CPUShaderCallable Class (CPP)](../../../../api/library/common/mt/class.cpushadercallable_cpp.md)

- [CPUShaderCallableStateless Class (CPP)](../../../../api/library/common/mt/class.cpushadercallablestateless_cpp.md)

- [CPUTask Class (USC)](../../../../api/library/common/mt/class.cputask_usc.md)

- [CPUTask Class (CS)](../../../../api/library/common/mt/class.cputask_cs.md)

- [CPUTask Class (CPP)](../../../../api/library/common/mt/class.cputask_cpp.md)

- [ProcessTask Class (CPP)](../../../../api/library/common/mt/class.processtask_cpp.md)

- [AsyncTaskCallable Class (CPP)](../../../../api/library/common/mt/class.asynctaskcallable_cpp.md)

- [AtomicInteger<Type> Struct (CPP)](../../../../api/library/common/mt/class.atomicinteger_cpp.md)

- [AtomicPointer<Type> Struct (CPP)](../../../../api/library/common/mt/class.atomicpointer_cpp.md)

- [AtomicLockFreeAlign<Type> Struct (CPP)](../../../../api/library/common/mt/class.atomiclockfreealign_cpp.md)

- [AtomicLockFreeRaw<Type> Struct (CPP)](../../../../api/library/common/mt/class.atomiclockfreeraw_cpp.md)

- [AtomicWithMutex<Type, MutexType> Struct (CPP)](../../../../api/library/common/mt/class.atomicwithmutex_cpp.md)

- [MutexSlim Class (CPP)](../../../../api/library/common/mt/class.mutexslim_cpp.md)

- [MutexCriticalSection Class (CPP)](../../../../api/library/common/mt/class.mutexcriticalsection_cpp.md)

- [MutexSpin Class (CPP)](../../../../api/library/common/mt/class.mutexspin_cpp.md)

- [MutexPThread Class (CPP)](../../../../api/library/common/mt/class.mutexpthread_cpp.md)

- [MutexAdvance<MutexType> Class (CPP)](../../../../api/library/common/mt/class.mutexadvance_cpp.md)

- [ReentrantMutexBase<MutexType> Class (CPP)](../../../../api/library/common/mt/class.reentrantmutexbase_cpp.md)

- [RWMutexSlim Class (CPP)](../../../../api/library/common/mt/class.rwmutexslim_cpp.md)

- [RWMutexSpin Class (CPP)](../../../../api/library/common/mt/class.rwmutexspin_cpp.md)

- [ScopedMutexLock<MutexType> Class (CPP)](../../../../api/library/common/mt/class.scopedmutexlock_cpp.md)

- [ScopedMutexReaderLock<MutexType> Class (CPP)](../../../../api/library/common/mt/class.scopedmutexreaderlock_cpp.md)

- [ScopedMutexWriterLock<MutexType> Class (CPP)](../../../../api/library/common/mt/class.scopedmutexwriterlock_cpp.md)

- [ScopedSpinLockInteger<Type> Class (CPP)](../../../../api/library/common/mt/class.scopedspinlockinteger_cpp.md)

- [BackoffSpinner Class (CPP)](../../../../api/library/common/mt/class.backoffspinner_cpp.md)
