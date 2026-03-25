# Unigine::Memory Class (CS)


This class controls [memory allocations](../../../principles/allocator/index.md).


> **Notice:** This class is static and cannot be instantiated. Call the methods directly instead.


## Memory Class

### Properties

## 🔒︎ int FrameAllocations

The number of allocations made per frame.
## 🔒︎ int MaxAllocations

The maximum number of allocations made during runtime (peak consumption).
## 🔒︎ int LiveAllocations

The number of allocations made.
## 🔒︎ ulong InstancePoolUsage

The amount of memory allocated in instance pools. The instance pools store allocations defined by developers. Usually, these are the allocations which are required regularly. They work the same way as the [dynamic pools](../../../principles/allocator/index.md#dynamic_pool), but the instance pools have no size limitation.
## 🔒︎ ulong DynamicPoolUsage

The amount of memory allocated in [dynamic pools](../../../principles/allocator/index.md#dynamic_pool) (available on Windows only).
## 🔒︎ ulong StaticPoolUsage

The amount of memory allocated in [static pools](../../../principles/allocator/index.md#static_pool).
## 🔒︎ bool IsStatisticsEnabled

The value indicating whether gathering memory statistics required for pool configuration is enabled.
## 🔒︎ ulong MemoryUsage

The overall amount of used memory in bytes.
### Members

---

## static void LogInfo ( )

Prints [information](../../../principles/allocator/index.md#analyze_ram_pools) on small allocations in the static and dynamic memory pools.
