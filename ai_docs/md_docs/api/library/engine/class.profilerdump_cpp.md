# Unigine::ProfilerDump Class (CPP)

**Header:** #include <UnigineProfiler.h>


The **ProfilerDump** class provides access to performance data stored in [profiler dump files](../../../tools/profiling/profiler_dump/index_cpp.md) (`*.profiler_dump`). Profiler dumps are saved in a binary format to reduce file size and speed up recording. Because of that, the file cannot be viewed directly in a text editor - it must be opened using this class or the *[Profiler Reader](../../../tools/profiling/profiler_reader_tool/index.md)* tool.


It is important to understand how to correctly retrieve information from the dump to avoid data corruption or invalid results.


- When working with console variables, always check their type using *[getConsoleVariableType()](../../...md#getConsoleVariableType_int_int)* before reading their value. Calling a *getConsoleVariableValue**** or *getConsoleVariableHistoryValue**** method on a variable of a different type automatically performs type casting, if conversion fails, a default value (empty or zero) for that type is returned. The code example below illustrates how to properly retrieve all console variables and their history from the dump and print them to console. <details> <summary>Parsing Console Variables</summary> ```cpp ProfilerDumpPtr dump = ProfilerDump::create(); dump->load("path_to_your_profiler_dump_file"); for (int i = 0; i < dump->getNumConsoleVariables(); i++) { int type = dump->getConsoleVariableType(i); String name = dump->getConsoleVariableName(i); Log::message("Console variable %s: ", name.get()); switch (type) { case ProfilerDump::DUMP_CONSOLE_VARIABLE_TYPE_STRING: Log::message("%s ", dump->getConsoleVariableValueString(i)); break; case ProfilerDump::DUMP_CONSOLE_VARIABLE_TYPE_INT: Log::message("%d ", dump->getConsoleVariableValueInt(i)); break; case ProfilerDump::DUMP_CONSOLE_VARIABLE_TYPE_FLOAT: Log::message("%f ", dump->getConsoleVariableValueFloat(i)); break; case ProfilerDump::DUMP_CONSOLE_VARIABLE_TYPE_VEC2: { Math::vec2 v = dump->getConsoleVariableValueVec2(i); Log::message("(%g, %g) ", v.x, v.y); break; } case ProfilerDump::DUMP_CONSOLE_VARIABLE_TYPE_VEC3: { Math::vec3 v = dump->getConsoleVariableValueVec3(i); Log::message("(%g, %g, %g) ", v.x, v.y, v.z); break; } case ProfilerDump::DUMP_CONSOLE_VARIABLE_TYPE_VEC4: { Math::vec4 v = dump->getConsoleVariableValueVec4(i); Log::message("(%g, %g, %g, %g) ", v.x, v.y, v.z, v.w); break; } case ProfilerDump::DUMP_CONSOLE_VARIABLE_TYPE_PALETTE: Log::message("%s ", dump->getConsoleVariableValuePalette(i).toString().get()); break; default: break; } int num_history = dump->getNumConsoleVariableHistory(i); for (int h = 0; h < num_history; h++) { if (h == 0) { Log::message(" ["); Log::message("%d: ", dump->getConsoleVariableHistoryFrame(i, h)); } else { Log::message("%d: ", dump->getConsoleVariableHistoryFrame(i, h)); } switch (type) { case ProfilerDump::DUMP_CONSOLE_VARIABLE_TYPE_STRING: Log::message("%s, ", dump->getConsoleVariableHistoryValueString(i, h)); break; case ProfilerDump::DUMP_CONSOLE_VARIABLE_TYPE_INT: Log::message("%d, ", dump->getConsoleVariableHistoryValueInt(i, h)); break; case ProfilerDump::DUMP_CONSOLE_VARIABLE_TYPE_FLOAT: Log::message("%f, ", dump->getConsoleVariableHistoryValueFloat(i, h)); break; case ProfilerDump::DUMP_CONSOLE_VARIABLE_TYPE_VEC2: { Math::vec2 v = dump->getConsoleVariableValueVec2(i); Log::message("(%g, %g) ", v.x, v.y); break; } case ProfilerDump::DUMP_CONSOLE_VARIABLE_TYPE_VEC3: { Math::vec3 v = dump->getConsoleVariableValueVec3(i); Log::message("(%g, %g, %g) ", v.x, v.y, v.z); break; } case ProfilerDump::DUMP_CONSOLE_VARIABLE_TYPE_VEC4: { Math::vec4 v = dump->getConsoleVariableValueVec4(i); Log::message("(%g, %g, %g, %g) ", v.x, v.y, v.z, v.w); break; } case ProfilerDump::DUMP_CONSOLE_VARIABLE_TYPE_PALETTE: Log::message("%s, ", dump->getConsoleVariableHistoryValuePalette(i, h).toString().get()); break; default: break; } } if (num_history > 0) Log::message("]\n"); else Log::message("\n"); } ``` </details>
- When reading profiler parameters (metrics), it is important to understand [how per-frame parameter values are stored](../../../tools/profiling/profiler_dump/index_cpp.md#profiler_dump_values). Each metric **may exist only for specific frames**, depending on whether it was active at the time of recording. Since parameter values are stored in union memory (to reduce file size), using a wrong getter method (e.g. try to get *int* value from a *float* parameter) will return invalid data. So its better to check the parameter type before reading values. The code example below illustrates how to properly retrieve all profiling metrics from the dump and print them to console. <details> <summary>Parsing Profiler Parameters</summary> ```cpp ProfilerDumpPtr dump = ProfilerDump::create(); dump->load("path_to_your_profiler_dump_file"); for (int p = 0; p < dump->getNumDumpParameters(); p++) { int type = dump->getDumpParameterType(p); String name = dump->getDumpParameterName(p); if (type == ProfilerDump::DUMP_PARAMETER_TYPE_INT) { Log::message("%s: Min: %d, Max: %d, Avg: %d [", name.get(), dump->getDumpParameterIntMin(p), dump->getDumpParameterIntMax(p), dump->getDumpParameterIntAvg(p) ); for (int frame = 0; frame < dump->getNumFrames(); frame++) { if (dump->containsFrameParameterIndex(frame, p)) Log::message("%d, ", dump->getFrameParameterValueInt(frame, p)); else Log::message("NAN, "); } } else { Log::message("%s: Min: %f, Max: %f, Avg: %f [", name.get(), dump->getDumpParameterFloatMin(p), dump->getDumpParameterFloatMax(p), dump->getDumpParameterFloatAvg(p) ); for (int frame = 0; frame < dump->getNumFrames(); frame++) { if (dump->containsFrameParameterIndex(frame, p)) Log::message("%f, ", dump->getFrameParameterValueFloat(frame, p)); else Log::message("NAN, "); } } Log::message("]\n"); } ``` </details>


### See Also


- **[Profiler Dump](../../../tools/profiling/profiler_dump/index_cpp.md)** article explaining how to record and read profiler dump files, including their structure and format.
- **[Profiler Reader](../../../tools/profiling/profiler_reader_tool/index.md)** tool that allows you to convert raw profiler dumps into a text files.


## ProfilerDump Class

### Enums

## DUMP_PARAMETER_TYPE

| Name | Description |
|---|---|
| **DUMP_PARAMETER_TYPE_INT** = 0 | Integer dump parameter. |
| **DUMP_PARAMETER_TYPE_FLOAT** = 1 | Float dump parameter. |

## DUMP_CONSOLE_VARIABLE_TYPE

| Name | Description |
|---|---|
| **DUMP_CONSOLE_VARIABLE_TYPE_STRING** = 0 | String console variable. |
| **DUMP_CONSOLE_VARIABLE_TYPE_INT** = 1 | Integer console variable. |
| **DUMP_CONSOLE_VARIABLE_TYPE_FLOAT** = 2 | Floating-point console variable. |
| **DUMP_CONSOLE_VARIABLE_TYPE_VEC2** = 3 | [Two-component vector](../../../api/library/math/class.vec2_cpp.md) console variable. |
| **DUMP_CONSOLE_VARIABLE_TYPE_VEC3** = 4 | [Three-component vector](../../../api/library/math/class.vec3_cpp.md) console variable. |
| **DUMP_CONSOLE_VARIABLE_TYPE_VEC4** = 5 | [Four-component vector](../../../api/library/math/class.vec4_cpp.md) console variable. |
| **DUMP_CONSOLE_VARIABLE_TYPE_PALETTE** = 6 | [Palette](../../../api/library/common/class.palette_cpp.md) console variable. |

### Members

## int getDumpVersion () const

The version of the profiler dump format used in the currently loaded dump.
### Return value

Version of the profiler dump format used in the currently loaded dump.
## const char * getEngineVersion () const

The [version of the engine](../../../code/version_cpp.md) that was used to record the profiler dump.
### Return value

Version of the engine that was used to record the profiler dump.
## const char * getEngineInfo () const

The version of the engine along with its build information stored in the profiler dump.
### Return value

Version of the engine along with its build information stored in the profiler dump.
## const char * getBinaryInfo () const

Engine binary build information stored in the profiler dump. This string contains details about the operating system, CPU architecture, build configuration, SDK, and compiler used to build the Engine binary that generated the dump.
### Return value

Engine binary build information stored in the profiler dump.
## const char * getFeatures () const

The list of the features supported by the Engine build that generated the loaded profiler dump.
### Return value

List of the features supported by the Engine build that generated the loaded profiler dump.
## const char * getRevisionInfo () const

Engine source control revision information stored in the profiler dump.
### Return value

Engine source control revision information stored in the profiler dump.
## const char * getOsInfo () const

The operating system information that was used to record the profiler dump.
### Return value

Operating system information that was used to record the profiler dump.
## const char * getCpuInfo () const

The detailed CPU information of the system that recorded the profiler dump. This includes the processor name, clock frequency, number of cores and threads, and the list of supported instruction sets.
### Return value

Detailed CPU information of the system that recorded the profiler dump.
## getTotalMemory () const

The total amount of physical memory (RAM) on the system where the profiler dump was recorded, in bytes.
### Return value

Total amount of physical memory (RAM) on the system where the profiler dump was recorded, in bytes.
## getNumGPUs () const

The number of GPUs detected on the system where the profiler dump was recorded.
### Return value

Number of GPUs detected on the system where the profiler dump was recorded.
## getNumFrames () const

The total number of frames recorded in the profiler dump.
### Return value

Total number of frames recorded in the profiler dump.
## getNumDumpParameters () const


The total number of profiler metrics (parameters) recorded in the profiler dump.


> **Notice:** The set of metrics included in the dump depends on the runtime configuration, for example, certain metrics (such as *VRAM Terrain Cache* or *Upscaler*) are recorded only when the corresponding systems or features are active during profiling.


### Return value

Total number of profiler metrics (parameters) recorded in the profiler dump.
---

## ProfilerDump ( )

Default constructor. Creates an empty **ProfilerDump** instance that can later be initialized by loading a profiler dump file (with the `*.profiler_dump` extension) using the *[load()](../../...md#load_cstr_int)* of *[info()](../../...md#info_cstr_int)* method.
## bool load ( const char * path )

Loads all profiler dump data from the specified file. This method reads and parses a `*.profiler_dump` file, allowing access to all recorded profiling information through the **ProfilerDump** class API.
### Arguments

- *const char ** **path** - Path to the profiler dump file.

### Return value

true, if the dump file was successfully loaded and parsed; otherwise false.
## bool info ( const char * path )

Loads profiler dump data from the specified file, **except the per-frame information**. This method reads and parses a `*.profiler_dump` file, allowing access to system info, console variables and parameters general statistics through the **ProfilerDump** class API.
### Arguments

- *const char ** **path** - Path to the profiler dump file.

### Return value

true, if the dump file was successfully loaded and parsed; otherwise false.
## const char * getGPUDescription ( int num ) const

Returns the description of the specified GPU recorded in the profiler dump. The description contains the full name of the graphics adapter.
### Arguments

- *int* **num** - zero-based index of the GPU device.

### Return value

A string containing the description of the GPU at the specified index.
## const char * getGPUType ( int num ) const

Returns the GPU type for the specified device recorded in the profiler dump.
### Arguments

- *int* **num** - zero-based index of the GPU device.

### Return value

A string containing the GPU type. (e.g. *"Discrete"* or *"Intergrated"*)
## const char * getGPUVendor ( int num ) const

Returns the vendor name for the specified GPU recorded in the profiler dump.
### Arguments

- *int* **num** - zero-based index of the GPU device.

## const char * getGPUDriver ( int num ) const

Returns the driver version for the specified GPU recorded in the profiler dump.
### Arguments

- *int* **num** - zero-based index of the GPU device.

## int getGPUMemory ( int num ) const

Returns the amount of VRAM (in megabytes) for the specified GPU recorded in the profiler dump.
### Arguments

- *int* **num** - zero-based index of the GPU device.

### Return value

The total GPU memory size (in megabytes).
## bool getGPUCommonHeaps ( int num ) const

Checks whether the common heaps for the specified GPU recorded in the profiler dump are used.
### Arguments

- *int* **num** - zero-based index of the GPU device.

### Return value

true if the common heaps for the specified GPU are used; otherwise false.
## int getGPUPriority ( int num ) const

Returns the device priority for the specified GPU recorded in the profiler dump.
### Arguments

- *int* **num** - zero-based index of the GPU device.

### Return value

The GPU's priority level.
## long long getGPULuid ( int num ) const

Returns the locally unique identifier for the specified GPU recorded in the profiler dump.
### Arguments

- *int* **num** - zero-based index of the GPU device.

### Return value

The GPU's locally unique identifier.
## unsigned int getGPUDeviceId ( int num ) const

Returns the identifier for the specified GPU recorded in the profiler dump.
### Arguments

- *int* **num** - zero-based index of the GPU device.

### Return value

The GPU's device identifier.
## int getNumConsoleVariables ( ) const

Returns the total number of console variables recorded in the profiler dump. Each console variable represents a configurable engine parameter that was captured at the time the dump was recorded.
### Return value

The number of console variables stored in the dump.
## const char * getConsoleVariableName ( int num ) const

Returns the name of the console variable recorded in the profiler dump at the specified index.
### Arguments

- *int* **num** - zero-based index of the console variable.

### Return value

The name of the console variable stored in the profiler dump.
## ProfilerDump::DUMP_CONSOLE_VARIABLE_TYPE getConsoleVariableType ( int num ) const

Returns the type of the console variable recorded in the profiler dump at the specified index.
### Arguments

- *int* **num** - zero-based index of the console variable.

### Return value

The type of the console variable stored in the profiler dump.
## const char * getConsoleVariableValueString ( int num ) const


Returns the value of the console variable recorded in the profiler dump at the specified index as a *string*. The value is automatically converted to a *string* type. If the conversion fails, an empty string is returned.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the variable type using *[getConsoleVariableType()](../../...md#getConsoleVariableType_int_int)*


### Arguments

- *int* **num** - zero-based index of the console variable.

### Return value

The value of the console variable as a string, or an empty string if the conversion failed.
## int getConsoleVariableValueInt ( int num ) const


Returns the value of the console variable recorded in the profiler dump at the specified index as an *int*. The value is automatically converted to an *int* type. If the conversion fails, 0 is returned.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the variable type using *[getConsoleVariableType()](../../...md#getConsoleVariableType_int_int)*


### Arguments

- *int* **num** - zero-based index of the console variable.

### Return value

The value of the console variable converted to an *int*, or 0 if the conversion failed.
## float getConsoleVariableValueFloat ( int num ) const


Returns the value of the console variable recorded in the profiler dump at the specified index as a *float*. The value is automatically converted to a *float* type. If the conversion fails, 0.0f is returned.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the variable type using *[getConsoleVariableType()](../../...md#getConsoleVariableType_int_int)*

### Arguments

- *int* **num** - zero-based index of the console variable.

### Return value

The value of the console variable converted to a *float*, or 0.0f if the conversion failed.
## Math:: vec2 getConsoleVariableValueVec2 ( int num ) const


Returns the value of the console variable recorded in the profiler dump at the specified index as a [*vec2*](../../../api/library/math/class.vec2_cpp.md). The value is automatically converted to a [*vec2*](../../../api/library/math/class.vec2_cpp.md) type. If the conversion fails, a zero vector (0.0f, 0.0f) is returned.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the variable type using *[getConsoleVariableType()](../../...md#getConsoleVariableType_int_int)*

### Arguments

- *int* **num** - zero-based index of the console variable.

### Return value

The value of the console variable converted to a [*vec2*](../../../api/library/math/class.vec2_cpp.md), or (0.0f, 0.0f) if the conversion failed.
## Math:: vec3 getConsoleVariableValueVec3 ( int num ) const


Returns the value of the console variable recorded in the profiler dump at the specified index as a [*vec3*](../../../api/library/math/class.vec3_cpp.md). The value is automatically converted to a [*vec3*](../../../api/library/math/class.vec3_cpp.md) type. If the conversion fails, a zero vector (0.0f, 0.0f, 0.0f) is returned.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the variable type using *[getConsoleVariableType()](../../...md#getConsoleVariableType_int_int)*

### Arguments

- *int* **num** - zero-based index of the console variable.

### Return value

The value of the console variable converted to a [*vec3*](../../../api/library/math/class.vec3_cpp.md), or (0.0f, 0.0f, 0.0f) if the conversion failed.
## Math:: vec4 getConsoleVariableValueVec4 ( int num ) const


Returns the value of the console variable recorded in the profiler dump at the specified index as a [*vec4*](../../../api/library/math/class.vec4_cpp.md). The value is automatically converted to a [*vec4*](../../../api/library/math/class.vec4_cpp.md) type. If the conversion fails, a zero vector (0.0f, 0.0f, 0.0f, 0.0f) is returned.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the variable type using *[getConsoleVariableType()](../../...md#getConsoleVariableType_int_int)*

### Arguments

- *int* **num** - zero-based index of the console variable.

### Return value

The value of the console variable converted to a [*vec4*](../../../api/library/math/class.vec4_cpp.md), or (0.0f, 0.0f, 0.0f, 0.0f) if the conversion failed.
## Palette getConsoleVariableValuePalette ( int num ) const


Returns the value of the console variable recorded in the profiler dump at the specified index as a [*Palette*](../../../api/library/common/class.palette_cpp.md). The value is automatically converted to a [*Palette*](../../../api/library/common/class.palette_cpp.md) type. If the conversion fails, a zero palette is returned.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the variable type using *[getConsoleVariableType()](../../...md#getConsoleVariableType_int_int)*

### Arguments

- *int* **num** - zero-based index of the console variable.

### Return value

The value of the console variable converted to a [*Palette*](../../../api/library/common/class.palette_cpp.md), or a zero palette if the conversion failed.
## int getNumConsoleVariableHistory ( int num ) const

Returns the number of recorded history entries for the specified index for the console variable. A variable's history is recorded only if its value changed during the profiling session.
### Arguments

- *int* **num** - zero-based index of the console variable.

### Return value

The number of history entries for the specified console variable.
## long long getConsoleVariableHistoryFrame ( int num , int h ) const

Returns the frame index at which the specified console variable changed its value for the *h-th* time.
### Arguments

- *int* **num** - zero-based index of the console variable.
- *int* **h** - zero-based sequential index of the value change in the variable history.

### Return value

The frame number when the console variable changed for the specified time. For example, if a variable changed 10 times and you want to know the frame of the 5th change, specify h=5.
## const char * getConsoleVariableHistoryValueString ( int num , int h ) const


Returns the value of the console variable recorded in the profiler dump at the specified index and history position, converted to *string*. If the conversion fails, an empty string is returned.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the variable type using *[getConsoleVariableType()](../../...md#getConsoleVariableType_int_int)*

### Arguments

- *int* **num** - zero-based index of the console variable.
- *int* **h** - zero-based sequential index of the value change in the variable history.

### Return value

The historical value of the console variable as *string*, or an empty string if conversion failed.
## int getConsoleVariableHistoryValueInt ( int num , int h ) const


Returns the value of the console variable recorded in the profiler dump at the specified index and history position, converted to *int*. If the conversion fails, a 0 is returned.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the variable type using *[getConsoleVariableType()](../../...md#getConsoleVariableType_int_int)*

### Arguments

- *int* **num** - zero-based index of the console variable.
- *int* **h** - zero-based sequential index of the value change in the variable history.

### Return value

The historical value of the console variable as *int*, or 0 if conversion failed.
## float getConsoleVariableHistoryValueFloat ( int num , int h ) const


Returns the value of the console variable recorded in the profiler dump at the specified index and history position, converted to *float*. If the conversion fails, a 0.0f is returned.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the variable type using *[getConsoleVariableType()](../../...md#getConsoleVariableType_int_int)*

### Arguments

- *int* **num** - zero-based index of the console variable.
- *int* **h** - zero-based sequential index of the value change in the variable history.

### Return value

The historical value of the console variable as *float*, or 0.0f if conversion failed.
## Math:: vec2 getConsoleVariableHistoryValueVec2 ( int num , int h ) const


Returns the value of the console variable recorded in the profiler dump at the specified index and history position, converted to a [*vec2*](../../../api/library/math/class.vec2_cpp.md). If the conversion fails, a zero vector (0.0f, 0.0f) is returned.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the variable type using *[getConsoleVariableType()](../../...md#getConsoleVariableType_int_int)*

### Arguments

- *int* **num** - zero-based index of the console variable.
- *int* **h** - zero-based sequential index of the value change in the variable history.

### Return value

The historical value of the console variable converted to a [*vec2*](../../../api/library/math/class.vec2_cpp.md), or (0.0f, 0.0f) if the conversion failed.
## Math:: vec3 getConsoleVariableHistoryValueVec3 ( int num , int h ) const


Returns the value of the console variable recorded in the profiler dump at the specified index and history position, converted to a [*vec3*](../../../api/library/math/class.vec3_cpp.md). If the conversion fails, a zero vector (0.0f, 0.0f, 0.0f) is returned.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the variable type using *[getConsoleVariableType()](../../...md#getConsoleVariableType_int_int)*

### Arguments

- *int* **num** - zero-based index of the console variable.
- *int* **h** - zero-based sequential index of the value change in the variable history.

### Return value

The historical value of the console variable converted to a [*vec3*](../../../api/library/math/class.vec3_cpp.md), or (0.0f, 0.0f, 0.0f) if the conversion failed.
## Math:: vec4 getConsoleVariableHistoryValueVec4 ( int num , int h ) const


Returns the value of the console variable recorded in the profiler dump at the specified index and history position, converted to a [*vec4*](../../../api/library/math/class.vec4_cpp.md). If the conversion fails, a zero vector (0.0f, 0.0f, 0.0f, 0.0f) is returned.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the variable type using *[getConsoleVariableType()](../../...md#getConsoleVariableType_int_int)*

### Arguments

- *int* **num** - zero-based index of the console variable.
- *int* **h** - zero-based sequential index of the value change in the variable history.

### Return value

The historical value of the console variable converted to a [*vec4*](../../../api/library/math/class.vec4_cpp.md), or (0.0f, 0.0f, 0.0f, 0.0f) if the conversion failed.
## Palette getConsoleVariableHistoryValuePalette ( int num , int h ) const


Returns the value of the console variable recorded in the profiler dump at the specified index and history position, converted to a [*Palette*](../../../api/library/common/class.palette_cpp.md). If the conversion fails, a zero palette is returned.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the variable type using *[getConsoleVariableType()](../../...md#getConsoleVariableType_int_int)*

### Arguments

- *int* **num** - zero-based index of the console variable.
- *int* **h** - zero-based sequential index of the value change in the variable history.

### Return value

The historical value of the console variable converted to a [*Palette*](../../../api/library/common/class.palette_cpp.md), or a zero palette if the conversion failed.
## long long getStartFrame ( ) const

Returns the Engine frame number at which the profiler dump recording started. This value represents the absolute frame index from the beginning of the Engine runtime when the dump began capturing profiling data.
### Return value

The frame number corresponding to the start of the profiler dump recording.
## long long getFrame ( int num ) const

Returns the Engine frame number corresponding to the specified frame index within the profiler dump. This allows you to determine which engine frame each recorded dump frame represents.
### Arguments

- *int* **num** - zero-based index of the profiler dump frame.

### Return value

The Engine frame number that corresponds to the specified dump frame.
## long long getFrameTimeMicroseconds ( int num ) const

Returns the timestamp of the specified frame in microseconds. This value represents the elapsed time since the start of the dump up to beginning of the given frame.
### Arguments

- *int* **num** - zero-based index of the profiler dump frame.

### Return value

The frame time in microseconds relative to the start of the profiler dump recording.
## double getFrameTimeSeconds ( int num ) const

Returns the timestamp of the specified frame in seconds. This value represents the elapsed time since the start of the dump up to beginning of the given frame.
### Arguments

- *int* **num** - zero-based index of the profiler dump frame.

### Return value

The frame time in seconds relative to the start of the profiler dump recording.
## double getFrameTimeMilliseconds ( int num ) const

Returns the timestamp of the specified frame in milliseconds. This value represents the elapsed time since the start of the dump up to beginning of the given frame.
### Arguments

- *int* **num** - zero-based index of the profiler dump frame.

### Return value

The frame time in milliseconds relative to the start of the profiler dump recording.
## int getNumFrameParameters ( int frame ) const

Returns the number of profiler parameters recorded for the specified frame in the profiler dump. The number of parameters may vary between frames, since some metrics are recorded when they are enabled and active (e.g. upscalers).
### Arguments

- *int* **frame** - zero-based index of the profiler dump frame.

### Return value

The number of profiler parameters recorded for the specified frame.
## int getFrameParameterIndex ( int frame , int num_parameter ) const

Returns the global dump parameter index that corresponds to the local parameter position within a specific frame. The profiler dump contains a fixed global list of parameters (metrics). Each frame stores values only for parameters that were active in that frame, so per-frame parameter list is a subset of the global list. This methos translates a frame-local parameter position to its global parameter index.
### Arguments

- *int* **frame** - zero-based index of the profiler dump frame.
- *int* **num_parameter** - zero-based local position of the parameter inside the specified frame in range [0, *[getNumFrameParameters](../../...md#getNumFrameParameters_int_int)* - 1].

### Return value

The global parameter index in the dump in range [0, *[getNumDumpParameters](../../...md#getNumDumpParameters_int)* - 1]
## int getFrameParameterValueInt ( int frame , int num_parameter ) const

Returns the raw integer representation of the specified frame-local parameter value.
### Arguments

- *int* **frame** - zero-based index of the profiler dump frame.
- *int* **num_parameter** - zero-based local position of the parameter inside the specified frame in range [0, *[getNumFrameParameters](../../...md#getNumFrameParameters_int_int)* - 1].

### Return value

The raw integer stored for this parameter in the specified frame.
## float getFrameParameterValueFloat ( int frame , int num_parameter ) const

Returns the raw float representation of the specified frame-local parameter value.
### Arguments

- *int* **frame** - zero-based index of the profiler dump frame.
- *int* **num_parameter** - zero-based local position of the parameter inside the specified frame in range [0, *[getNumFrameParameters](../../...md#getNumFrameParameters_int_int)* - 1].

### Return value

The raw float stored for this parameter in the specified frame.
## bool containsFrameParameterIndex ( int frame , int paramter_index ) const

Checks whether the specified global dump parameter index is present among the parameters recorded for the given frame. Since each frame contains only a subset of the global dump metrics (those that were active in that frame), this method lets you test if a particular metric is available in that frame.
### Arguments

- *int* **frame** - zero-based index of the profiler dump frame.
- *int* **paramter_index** - zero-based global parameter index in the dump in range [0, *[getNumDumpParameters](../../...md#getNumDumpParameters_int)* - 1]

### Return value

true if the frame contains a value for the specified global dump parameter; otherwise false.
## const char * getDumpParameterName ( int num ) const

Returns the name of the profiler dump parameter identified by the given index.
### Arguments

- *int* **num** - zero-based profiler dump parameter index in range [0, *[getNumDumpParameters](../../...md#getNumDumpParameters_int)* - 1].

### Return value

The name of the dump parameter.
## const char * getDumpParameterUnits ( int num ) const

Returns the measurement units for the specified dump profiler parameter.
### Arguments

- *int* **num** - zero-based profiler dump parameter index in range [0, *[getNumDumpParameters](../../...md#getNumDumpParameters_int)* - 1].

### Return value

The units string for the parameter (e.g. *"ms"*, *"MB"*).
## ProfilerDump::DUMP_PARAMETER_TYPE getDumpParameterType ( int num ) const

Returns the storage type of the specified profiler parameter. The type indicates whether the parameter's per-frame values are stored as *int* of *float*.
### Arguments

- *int* **num** - zero-based profiler dump parameter index in range [0, *[getNumDumpParameters](../../...md#getNumDumpParameters_int)* - 1].

### Return value

The type used to store the profiler parameter at the specified index.
## int getDumpParameterIntMin ( int num ) const


Returns the minimum observed value (as *int*) for the specified profiler parameter identified by the given index.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the parameter type using *[getDumpParameterType()](../../...md#getDumpParameterType_int_int)*.

### Arguments

- *int* **num** - zero-based profiler dump parameter index in range [0, *[getNumDumpParameters](../../...md#getNumDumpParameters_int)* - 1].

### Return value

Minimum value as integer.
## int getDumpParameterIntMax ( int num ) const


Returns the maximum observed value (as *int*) for the specified profiler parameter identified by the given index.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the parameter type using *[getDumpParameterType()](../../...md#getDumpParameterType_int_int)*.

### Arguments

- *int* **num** - zero-based profiler dump parameter index in range [0, *[getNumDumpParameters](../../...md#getNumDumpParameters_int)* - 1].

### Return value

Maximum value as integer.
## int getDumpParameterIntAvg ( int num ) const


Returns the average value (as *int*) for the specified profiler parameter identified by the given index.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the parameter type using *[getDumpParameterType()](../../...md#getDumpParameterType_int_int)*.

### Arguments

- *int* **num** - zero-based profiler dump parameter index in range [0, *[getNumDumpParameters](../../...md#getNumDumpParameters_int)* - 1].

### Return value

Average value as integer.
## float getDumpParameterFloatMin ( int num ) const


Returns the minimum observed value (as *float*) for the specified profiler parameter identified by the given index.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the parameter type using *[getDumpParameterType()](../../...md#getDumpParameterType_int_int)*.

### Arguments

- *int* **num** - zero-based profiler dump parameter index in range [0, *[getNumDumpParameters](../../...md#getNumDumpParameters_int)* - 1].

### Return value

Minimum value as float.
## float getDumpParameterFloatMax ( int num ) const


Returns the maximum observed value (as *float*) for the specified profiler parameter identified by the given index.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the parameter type using *[getDumpParameterType()](../../...md#getDumpParameterType_int_int)*.

### Arguments

- *int* **num** - zero-based profiler dump parameter index in range [0, *[getNumDumpParameters](../../...md#getNumDumpParameters_int)* - 1].

### Return value

Maximum value as float.
## float getDumpParameterFloatAvg ( int num ) const


Returns the average value (as *float*) for the specified profiler parameter identified by the given index.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the parameter type using *[getDumpParameterType()](../../...md#getDumpParameterType_int_int)*.

### Arguments

- *int* **num** - zero-based profiler dump parameter index in range [0, *[getNumDumpParameters](../../...md#getNumDumpParameters_int)* - 1].

### Return value

Average value as float.
