# Unigine.SystemInfo Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is used to obtain detailed information about the system and the engine environment. It provides metrics on RAM and VRAM usage, CPU and GPU features, operating system details, engine version, and platform characteristics.


> **Notice:** This class is static and cannot be instantiated. Call the methods directly instead.


## SystemInfo Class

### Structs

## struct MemoryStatistics

### Fields

- *bool* **out_of_ram_committed** - Flag indicating whether the process has run out of committed RAM.
- *bool* **out_of_ram** - Flag indicating whether the process has run out of physical RAM.
- *bool* **out_of_vram** - Flag indicating whether the process has run out of VRAM.

---

## static string getBinaryInfo ( )

***Console*:**`binary_info`Returns information on the Engine binary.
### Return value

Information on the Engine binary.
## static string getRevisionInfo ( )

Returns information on the Engine version.
### Return value

Information on the Engine version.
## static string getCPUInfo ( )

***Console*:**`cpu_info`Returns information on the CPU.
### Return value

CPU information.
## static int getCPUFrequency ( )

***Console*:**`cpu_frequency`Returns the current CPU frequency.
### Return value

Current CPU frequency, in MHz.
## static int getCPUThreads ( )

***Console*:**`cpu_threads`Returns the number of available CPU threads.
### Return value

Number of available CPU threads.
## static int hasMMX ( )

Returns a value indicating if the system supports MMX (Multi-Media Extensions).
### Return value

**1** if the system supports MMX extension; otherwise, **0**.
## static int hasSSE ( )

Returns a value indicating if the system supports SSE (Streaming SIMD Extensions).
### Return value

**1** if the system supports SSE extension; otherwise, **0**.
## static int hasSSE2 ( )

Returns a value indicating if the system supports SSE2 (Streaming SIMD Extensions).
### Return value

**1** if the system supports SSE2 extension; otherwise, **0**.
## static int hasSSE3 ( )

Returns a value indicating if the system supports SSE3 (Streaming SIMD Extensions).
### Return value

**1** if the system supports SSE3 extension; otherwise, **0**.
## static int hasSSE4 ( )

Returns a value indicating if the system supports SSE4 (Streaming SIMD Extensions).
### Return value

**1** if the system supports SSE4 extension; otherwise, **0**.
## static int hasSSE5 ( )

Returns a value indicating if the system supports SSE5 (Streaming SIMD Extensions).
### Return value

**1** if the system supports SSE5 extension; otherwise, **0**.
## static int hasAVX ( )

Returns a value indicating if the system supports AVX (Advanced Vector Extensions).
### Return value

**1** if the system supports AVX extension; otherwise, **0**.
## static int hasAVX2 ( )

Returns a value indicating if the system supports AVX2 (Advanced Vector Extensions).
### Return value

**1** if the system supports AVX2 extension; otherwise, **0**.
## static int hasNeon ( )

Returns a value indicating if the system supports Neon (Advanced Vector Extensions).
### Return value

**1** if the system supports Neon extension; otherwise, **0**.
## static int hasHyperThreading ( )

***Console*:**`cpu_hyper_threading`Returns a value indicating if the system supports hyper-threading.
### Return value

**1** if the system supports hyper-threading; otherwise, **0**.
## static int getGPUCount ( )

Returns the number of available GPUs.
### Return value

Number of available GPUs.
## static int getGPUMemory ( int video_adapter_num = 0 )

Returns the video memory size for the video adapter with the specified number.
### Arguments

- *int* **video_adapter_num** - Number of the video adapter.

### Return value

Video memory size, in Mbytes.
## static int getGPUID ( int video_adapter_num = 0 )

Returns the GPU ID for the video adapter with the specified number in the list of detected ones. To obtain a universal unique identifier (*UUID*), which is persistent across reboots and hardware configuration changes, use *[getGPUUuidString()](#getGPUUuidString_int_cstr)*.
### Arguments

- *int* **video_adapter_num** - Number of the graphics adapter (GPU) in the list of detected ones.

### Return value

GPU ID for the video adapter with the specified number.
## static string getOSInfo ( )

Returns the operating system information: its name, edition, and build.
### Return value

Operating system information.
## static string getEngineInfo ( )

Returns the complete information on the engine: version number, release/debug, revision, date.
### Return value

Complete engine information.
## static int getCPUCores ( )

***Console*:**`cpu_cores`Returns the number of CPU cores.
### Return value

The number of CPU cores.
## static void logInfo ( )

***Console*:**`system_info`Returns the infromation on the Engine, OS, CPU and GPU.
## static int getGPUActive ( )

Returns the index of the active GPU.
### Return value

The index of the active GPU.
## static int findGPUByLuid ( long luid )

Returns the GPU index by its locally unique identifier.
### Arguments

- *long* **luid** - The locally unique identifier of the GPU.

### Return value

The GPU index, or -1 if no GPU is found.
## static int findGPUByDeviceID ( unsigned int device_id )

Returns the GPU index by the device identifier.
### Arguments

- *unsigned int* **device_id** - The GPU device ID.

### Return value

The GPU index, or -1 if no GPU is found.
## static int getGPUType ( int video_adapter_num = -1 )

Returns the GPU type by the video adapter index.
### Arguments

- *int* **video_adapter_num** - The video adapter index.

### Return value

The GPU type.
## static int getGPUVendor ( int video_adapter_num = -1 )

Returns the GPU vendor name by the video adapter index.
### Arguments

- *int* **video_adapter_num** - The video adapter index.

### Return value

The GPU vendor name.
## static unsigned int getGPUDeviceID ( int video_adapter_num = -1 )

Returns the GPU device ID by the video adapter index.
### Arguments

- *int* **video_adapter_num** - The video adapter index.

### Return value

The GPU device ID.
## static long getGPULuid ( int video_adapter_num = -1 )

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
## static string getGPUDescription ( int video_adapter_num = -1 )

Returns the graphics card model by the video adapter index.
### Arguments

- *int* **video_adapter_num** - The video adapter index.

### Return value

The GPU model.
## static string getGPUVendorName ( int video_adapter_num = -1 )

Returns the graphics card vendor name by the video adapter index.
### Arguments

- *int* **video_adapter_num** - The video adapter index.

### Return value

The GPU vendor name.
## static string getGPUDriver ( int video_adapter_num = -1 )

Returns the graphics card driver version by the video adapter index.
### Arguments

- *int* **video_adapter_num** - The video adapter index.

### Return value

The GPU driver version.
## static int getPlatformType ( )

Returns the platform type.
### Return value

The platform type.
## static MemoryStatistics getMemoryStatistics ( )

Returns current [memory consumption statistics](#memory_statistics) of the engine process.
### Return value

The structure containing all memory statistics.
## static bool outOfRamCommitted ( )

Returns the value indicating whether the process has exceeded its committed free RAM.
### Return value

true if the committed RAM limit is exceeded; otherwise false.
## static bool outOfRam ( )

Returns the value indicating whether the process has run out of physical RAM.
### Return value

true if physical RAM is exceeded; otherwise false.
## static bool outOfVRam ( )

Returns the value indicating whether the process has run out of GPU memory (VRAM).
### Return value

true if GPU memory is exceeded; otherwise false.
## static long getRamFree ( )

Returns the amount of free physical RAM available to the engine process.
### Return value

Number of bytes of free RAM.
## static long getRamUsage ( )

Returns the amount of physical RAM currently used by the engine process.
### Return value

Number of bytes of used RAM.
## static long getRamLimit ( )

Returns the maximum amount of physical RAM available to the engine process.
### Return value

Number of bytes representing the RAM usage limit.
## static long getRamTotal ( )

Returns the total amount of installed physical RAM in the system.
### Return value

Number of bytes of total physical RAM.
## static long getRamCommittedFree ( )

Returns the amount of committed RAM still available before reaching the commit limit.
### Return value

Number of bytes of free committed RAM.
## static long getRamCommittedUsage ( )

Returns the amount of committed RAM currently used by the engine process.
### Return value

Number of bytes of used committed RAM.
## static long getRamCommittedBackground ( )

Returns the amount of committed RAM allocated by all background tasks.
### Return value

Number of bytes of committed background RAM.
## static long getRamCommittedLimit ( )

Returns the maximum amount of committed RAM the process can allocate.
### Return value

Number of bytes representing the committed RAM limit.
## static long getRamCommittedTotal ( )

Returns the total amount of committed RAM in the system.
### Return value

Number of bytes of total committed RAM.
## static long getGpuRamUsage ( )

Returns the amount of system RAM currently allocated for GPU usage by the engine process.
### Return value

Number of bytes of system RAM used by GPU.
## static long getGpuRamBackground ( )

Returns the amount of system RAM allocated for GPU background tasks.
### Return value

Number of bytes of background system RAM used by GPU.
## static long getGpuVRamFree ( )

Returns the amount of free GPU memory (VRAM) available to the engine process.
### Return value

Number of bytes of free VRAM.
## static long getGpuVRamUsage ( )

Returns the amount of GPU memory (VRAM) currently used by the engine process.
### Return value

Number of bytes of used VRAM.
## static long getGpuVRamBackground ( )

Returns the amount of GPU memory (VRAM) allocated by background tasks.
### Return value

Number of bytes of background VRAM.
## static long getGpuVRamLimit ( )

Returns the maximum amount of GPU memory (VRAM) the engine process can allocate.
### Return value

Number of bytes representing the VRAM usage limit.
## static long getGpuVRamBudget ( )

Returns the current GPU memory (VRAM) budget assigned to the engine process by the driver.
### Return value

Number of bytes of VRAM budget.
## static long getGpuVRamTotal ( )

Returns the total amount of physical GPU memory (VRAM) available on the system.
### Return value

Number of bytes of total VRAM.
## static int getRamFrequency ( )

Returns the clock frequency of installed system RAM, in MHz.
### Return value

RAM clock frequency, in MHz.
## static long getSwapSize ( )

Returns the total size of the swap file (paging file), in bytes. Returns 0 on platforms without swap support.
### Return value

Swap file size, in bytes. 0 on platforms without swap support.
## static string getCPUName ( )

Returns the CPU model name string.
### Return value

CPU model name string.
## static int getProcessID ( )

Returns the operating system process identifier (PID) of the current engine process.
### Return value

Operating system process identifier (PID).
## static string getEnvironmentVariable ( string env_variable )

Returns the value of the specified operating system environment variable, or an empty string if the variable is not set.
### Arguments

- *string* **env_variable** - Environment variable name.

### Return value

Value of the environment variable, or an empty string if the variable is not set.
