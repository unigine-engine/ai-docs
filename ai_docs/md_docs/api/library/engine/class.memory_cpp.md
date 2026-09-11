# Unigine::Memory Class (CPP)

**Header:** #include <UnigineMemory.h>


This class controls [memory allocations](../../../principles/allocator/index.md).


> **Notice:** This class is static and cannot be instantiated. Call the methods directly instead.


## Memory Class

### Members

## int getFrameAllocations () const

Returns the current number of allocations made per frame.
### Return value

Current number of allocations.
## int getMaxAllocations () const

Returns the current maximum number of allocations made during runtime (peak consumption).
### Return value

Current number of allocations.
## int getLiveAllocations () const

Returns the current number of allocations made.
### Return value

Current number of allocations.
## size_t getInstancePoolUsage () const

Returns the current amount of memory allocated in instance pools. The instance pools store allocations defined by developers. Usually, these are the allocations which are required regularly. They work the same way as the [dynamic pools](../../../principles/allocator/index.md#dynamic_pool), but the instance pools have no size limitation.
### Return value

Current amount of memory.
## size_t getDynamicPoolUsage () const

Returns the current amount of memory allocated in [dynamic pools](../../../principles/allocator/index.md#dynamic_pool) (available on Windows only).
### Return value

Current amount of memory.
## size_t getStaticPoolUsage () const

Returns the current amount of memory allocated in [static pools](../../../principles/allocator/index.md#static_pool).
### Return value

Current amount of memory.
## bool isStatisticsEnabled () const

Returns the current value indicating whether gathering memory statistics required for pool configuration is enabled.
### Return value

**true** if gathering memory statistics required for pool configuration is enabled ; otherwise **false**.
## size_t getMemoryUsage () const

Returns the current overall amount of used memory in bytes.
### Return value

Current used memory in bytes.
---

## int isInitialized ( )

Returns the status of the memory manager.
### Return value

**1** if the memory manager is initialized; otherwise, **0**.
## static void allocate ( size_t size )

Allocates the dynamic memory.
### Arguments

- *size_t* **size** - Size of the allocated memory block.

## static int deallocate ( void * ptr )

Deallocates the dynamic memory.
### Arguments

- *void ** **ptr** - Pointer to the allocated memory block.

## static void deallocate ( void * ptr , size_t size )

Deallocates the dynamic memory.
### Arguments

- *void ** **ptr** - Pointer to the allocated memory block.
- *size_t* **size** - Size of the allocated memory block.

## static void logInfo ( )

Prints [information](../../../principles/allocator/index.md#analyze_ram_pools) on small allocations in the static and dynamic memory pools.
