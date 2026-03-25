# Unigine.SystemInfo Class (CS)


This class is used to obtain detailed information about the system and the engine environment. It provides metrics on RAM and VRAM usage, CPU and GPU features, operating system details, engine version, and platform characteristics.


> **Notice:** This class is static and cannot be instantiated. Call the methods directly instead.


## SystemInfo Class

### Enums

## PLATFORM_TYPE

| Name | Description |
|---|---|
| **WINDOWS** = 0 | Windows platform. |
| **LINUX** = 1 | Linux platform. |

## GPU_TYPE

| Name | Description |
|---|---|
| **DISCRETE** = 0 | Discrete graphics processing unit (GPU). |
| **INTEGRATED** = 1 | Integrated graphics processing unit (GPU). |
| **OTHER** = 2 | Other type of graphics processing unit (GPU). |
| **UNSUPPORTED** = 3 | Unsupported type of graphics processing unit (GPU). |

## GPU_VENDOR

| Name | Description |
|---|---|
| **UNKNOWN** = 0 | Graphics processing unit (GPU) of an unknown vendor. |
| **AMD** = 1 | Graphics processing unit (GPU) developed by AMD. |
| **NVIDIA** = 2 | Graphics processing unit (GPU) developed by NVIDIA. |
| **INTEL** = 3 | Graphics processing unit (GPU) developed by Intel. |
| **ARM** = 4 | Graphics processing unit (GPU) developed by ARM (Advanced RISC Machines) Holdings. |
| **APPLE** = 5 | Graphics processing unit (GPU) developed by Apple Inc. |
| **IMGTEC** = 6 | Graphics processing unit (GPU) developed by Imagination Technologies Group plc. |
| **QUALCOMM** = 7 | Graphics processing unit (GPU) developed by Qualcomm. |

### Structs

## struct MemoryStatistics

### Fields

- *bool* **out_of_ram_committed** - Flag indicating whether the process has run out of committed RAM.
- *bool* **out_of_ram** - Flag indicating whether the process has run out of physical RAM.
- *bool* **out_of_vram** - Flag indicating whether the process has run out of VRAM.
- *long* **ram_free** - Free physical RAM.
- *long* **ram_usage** - Physical RAM currently in use.
- *long* **ram_limit** - Physical RAM available to the engine.
- *long* **ram_total** - Total amount of physical RAM.
- *long* **ram_committed_free** - Free virtual memory available in system.
- *long* **ram_committed_usage** - Amount of virtual memory committed by the engine process.
- *long* **ram_committed_background** - Amount of virtual memory committed by all background processes.
- *long* **ram_committed_limit** - Amount of virtual memory the engine process is allowed to commit.
- *long* **ram_committed_total** - Total amount of virtual RAM.
- *long* **gpu_ram_usage** - Amount of RAM used by GPU (allocated by the engine process).
- *long* **gpu_ram_background** - Amount of RAM used by GPU (allocated by all background process).
- *long* **gpu_vram_free** - Amount of unused VRAM.
- *long* **gpu_vram_usage** - Amount of VRAM in use by the engine process.
- *long* **gpu_vram_background** - Amount of VRAM in use by all background processes.
- *long* **gpu_vram_limit** - VRAM available for the engine.
- *long* **gpu_vram_budget** - OS-provided VRAM budget.
- *long* **gpu_vram_total** - Total VRAM.

### Members

---

## static string GetBinaryInfo ( )

***Console*:**`binary_info`Returns information on the Engine binary.
### Return value

Information on the Engine binary.
## static string GetRevisionInfo ( )

Returns information on the Engine version.
### Return value

Information on the Engine version.
## static string GetCPUInfo ( )

***Console*:**`cpu_info`Returns information on the CPU.
### Return value

CPU information.
## static int GetCPUFrequency ( )

***Console*:**`cpu_frequency`Returns the current CPU frequency.
### Return value

Current CPU frequency, in MHz.
## static int GetCPUThreads ( )

***Console*:**`cpu_threads`Returns the number of available CPU threads.
### Return value

Number of available CPU threads.
## static bool HasMMX ( )

Returns a value indicating if the system supports MMX (Multi-Media Extensions).
### Return value

true if the system supports MMX extension; otherwise, false.
## static bool HasSSE ( )

Returns a value indicating if the system supports SSE (Streaming SIMD Extensions).
### Return value

true if the system supports SSE extension; otherwise, false.
## static bool HasSSE2 ( )

Returns a value indicating if the system supports SSE2 (Streaming SIMD Extensions).
### Return value

true if the system supports SSE2 extension; otherwise, false.
## static bool HasSSE3 ( )

Returns a value indicating if the system supports SSE3 (Streaming SIMD Extensions).
### Return value

true if the system supports SSE3 extension; otherwise, false.
## static bool HasSSE4 ( )

Returns a value indicating if the system supports SSE4 (Streaming SIMD Extensions).
### Return value

true if the system supports SSE4 extension; otherwise, false.
## static bool HasSSE5 ( )

Returns a value indicating if the system supports SSE5 (Streaming SIMD Extensions).
### Return value

true if the system supports SSE5 extension; otherwise, false.
## static bool HasAVX ( )

Returns a value indicating if the system supports AVX (Advanced Vector Extensions).
### Return value

true if the system supports AVX extension; otherwise, false.
## static bool HasAVX2 ( )

Returns a value indicating if the system supports AVX2 (Advanced Vector Extensions).
### Return value

true if the system supports AVX2 extension; otherwise, false.
## static bool HasNeon ( )

Returns a value indicating if the system supports Neon (Advanced Vector Extensions).
### Return value

true if the system supports Neon extension; otherwise, false.
## static bool HasHyperThreading ( )

***Console*:**`cpu_hyper_threading`Returns a value indicating if the system supports hyper-threading.
### Return value

true if the system supports hyper-threading; otherwise, false.
## static int GetGPUCount ( )

Returns the number of available GPUs.
### Return value

Number of available GPUs.
## static int GetGPUMemory ( int video_adapter_num = 0 )

Returns the video memory size for the video adapter with the specified number.
### Arguments

- *int* **video_adapter_num** - Number of the video adapter.

### Return value

Video memory size, in Mbytes.
## static int GetGPUID ( int video_adapter_num = 0 )

Returns the GPU ID for the video adapter with the specified number in the list of detected ones. To obtain a universal unique identifier (*UUID*), which is persistent across reboots and hardware configuration changes, use *[getGPUUuidString()](#getGPUUuidString_int_cstr)*.
### Arguments

- *int* **video_adapter_num** - Number of the graphics adapter (GPU) in the list of detected ones.

### Return value

GPU ID for the video adapter with the specified number.
## static string GetOSInfo ( )

Returns the operating system information: its name, edition, and build.
### Return value

Operating system information.
## static string GetEngineInfo ( )

Returns the complete information on the engine: version number, release/debug, revision, date.
### Return value

Complete engine information.
## static int GetCPUCores ( )

***Console*:**`cpu_cores`Returns the number of CPU cores.
### Return value

The number of CPU cores.
## static void LogInfo ( )

***Console*:**`system_info`Returns the infromation on the Engine, OS, CPU and GPU.
## static int GetGPUActive ( )

Returns the index of the active GPU.
### Return value

The index of the active GPU.
## static int FindGPUByLuid ( ulong luid )

Returns the GPU index by its locally unique identifier.
### Arguments

- *ulong* **luid** - The locally unique identifier of the GPU.

### Return value

The GPU index, or -1 if no GPU is found.
## static int FindGPUByDeviceID ( uint device_id )

Returns the GPU index by the device identifier.
### Arguments

- *uint* **device_id** - The GPU device ID.

### Return value

The GPU index, or -1 if no GPU is found.
## static SystemInfo.GPU_TYPE GetGPUType ( int video_adapter_num = -1 )

Returns the GPU type by the video adapter index.
### Arguments

- *int* **video_adapter_num** - The video adapter index.

### Return value

The GPU type.
## static SystemInfo.GPU_VENDOR GetGPUVendor ( int video_adapter_num = -1 )

Returns the GPU vendor name by the video adapter index.
### Arguments

- *int* **video_adapter_num** - The video adapter index.

### Return value

The GPU vendor name.
## static uint GetGPUDeviceID ( int video_adapter_num = -1 )

Returns the GPU device ID by the video adapter index.
### Arguments

- *int* **video_adapter_num** - The video adapter index.

### Return value

The GPU device ID.
## static ulong GetGPULuid ( int video_adapter_num = -1 )

Returns the GPU locally unique identifier by the video adapter index.
### Arguments

- *int* **video_adapter_num** - The video adapter index.

### Return value

The locally unique identifier of the GPU.
## static string getGPUUuidString ( int video_adapter_num = -1 )

Returns the GPU universal unique identifier (*UUID*) string by the video adapter index. Can also be obtained via the console command `-video_adapter_uuid`.
### Arguments

- *int* **video_adapter_num** - The video adapter index.

### Return value

The GPU UUID string.
## static string GetGPUDescription ( int video_adapter_num = -1 )

Returns the graphics card model by the video adapter index.
### Arguments

- *int* **video_adapter_num** - The video adapter index.

### Return value

The GPU model.
## static string GetGPUVendorName ( int video_adapter_num = -1 )

Returns the graphics card vendor name by the video adapter index.
### Arguments

- *int* **video_adapter_num** - The video adapter index.

### Return value

The GPU vendor name.
## static string GetGPUDriver ( int video_adapter_num = -1 )

Returns the graphics card driver version by the video adapter index.
### Arguments

- *int* **video_adapter_num** - The video adapter index.

### Return value

The GPU driver version.
## static SystemInfo.PLATFORM_TYPE GetPlatformType ( )

Returns the platform type.
### Return value

The platform type.
## static MemoryStatistics GetMemoryStatistics ( )

Returns current [memory consumption statistics](#memory_statistics) of the engine process.
### Return value

The structure containing all memory statistics.
## static bool OutOfRamCommitted ( )

Returns the value indicating whether the process has exceeded its committed free RAM.
### Return value

true if the committed RAM limit is exceeded; otherwise false.
## static bool OutOfRam ( )

Returns the value indicating whether the process has run out of physical RAM.
### Return value

true if physical RAM is exceeded; otherwise false.
## static bool OutOfVRam ( )

Returns the value indicating whether the process has run out of GPU memory (VRAM).
### Return value

true if GPU memory is exceeded; otherwise false.
## static long GetRamFree ( )

Returns the amount of free physical RAM available to the engine process.
### Return value

Number of bytes of free RAM.
## static long GetRamUsage ( )

Returns the amount of physical RAM currently used by the engine process.
### Return value

Number of bytes of used RAM.
## static long GetRamLimit ( )

Returns the maximum amount of physical RAM available to the engine process.
### Return value

Number of bytes representing the RAM usage limit.
## static long GetRamTotal ( )

Returns the total amount of installed physical RAM in the system.
### Return value

Number of bytes of total physical RAM.
## static long GetRamCommittedFree ( )

Returns the amount of committed RAM still available before reaching the commit limit.
### Return value

Number of bytes of free committed RAM.
## static long GetRamCommittedUsage ( )

Returns the amount of committed RAM currently used by the engine process.
### Return value

Number of bytes of used committed RAM.
## static long GetRamCommittedBackground ( )

Returns the amount of committed RAM allocated by all background tasks.
### Return value

Number of bytes of committed background RAM.
## static long GetRamCommittedLimit ( )

Returns the maximum amount of committed RAM the process can allocate.
### Return value

Number of bytes representing the committed RAM limit.
## static long GetRamCommittedTotal ( )

Returns the total amount of committed RAM in the system.
### Return value

Number of bytes of total committed RAM.
## static long GetGpuRamUsage ( )

Returns the amount of system RAM currently allocated for GPU usage by the engine process.
### Return value

Number of bytes of system RAM used by GPU.
## static long GetGpuRamBackground ( )

Returns the amount of system RAM allocated for GPU background tasks.
### Return value

Number of bytes of background system RAM used by GPU.
## static long GetGpuVRamFree ( )

Returns the amount of free GPU memory (VRAM) available to the engine process.
### Return value

Number of bytes of free VRAM.
## static long GetGpuVRamUsage ( )

Returns the amount of GPU memory (VRAM) currently used by the engine process.
### Return value

Number of bytes of used VRAM.
## static long GetGpuVRamBackground ( )

Returns the amount of GPU memory (VRAM) allocated by background tasks.
### Return value

Number of bytes of background VRAM.
## static long GetGpuVRamLimit ( )

Returns the maximum amount of GPU memory (VRAM) the engine process can allocate.
### Return value

Number of bytes representing the VRAM usage limit.
## static long GetGpuVRamBudget ( )

Returns the current GPU memory (VRAM) budget assigned to the engine process by the driver.
### Return value

Number of bytes of VRAM budget.
## static long GetGpuVRamTotal ( )

Returns the total amount of physical GPU memory (VRAM) available on the system.
### Return value

Number of bytes of total VRAM.
## static uint GetRamFrequency ( )

Returns the clock frequency of installed system RAM, in MHz.
### Return value

RAM clock frequency, in MHz.
## static long GetSwapSize ( )

Returns the total size of the swap file (paging file), in bytes. Returns 0 on platforms without swap support.
### Return value

Swap file size, in bytes. 0 on platforms without swap support.
## static string GetCPUName ( )

Returns the CPU model name string.
### Return value

CPU model name string.
## static int GetProcessID ( )

Returns the operating system process identifier (PID) of the current engine process.
### Return value

Operating system process identifier (PID).
## static string GetEnvironmentVariable ( string env_variable )

Returns the value of the specified operating system environment variable, or an empty string if the variable is not set.
### Arguments

- *string* **env_variable** - Environment variable name.

### Return value

Value of the environment variable, or an empty string if the variable is not set.
