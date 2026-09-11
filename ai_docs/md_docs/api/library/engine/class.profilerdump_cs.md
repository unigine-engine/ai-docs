# Unigine::ProfilerDump Class (CS)


The **ProfilerDump** class provides access to performance data stored in [profiler dump files](../../../tools/profiling/profiler_dump/index_cs.md) (`*.profiler_dump`). Profiler dumps are saved in a binary format to reduce file size and speed up recording. Because of that, the file cannot be viewed directly in a text editor - it must be opened using this class or the *[Profiler Reader](../../../tools/profiling/profiler_reader_tool/index.md)* tool.


It is important to understand how to correctly retrieve information from the dump to avoid data corruption or invalid results.


- When working with console variables, always check their type using *[GetConsoleVariableType()](../../...md#getConsoleVariableType_int_int)* before reading their value. Calling a *GetConsoleVariableValue**** or *GetConsoleVariableHistoryValue**** method on a variable of a different type automatically performs type casting, if conversion fails, a default value (empty or zero) for that type is returned. The code example below illustrates how to properly retrieve all console variables and their history from the dump and print them to console. <details> <summary>Parsing Console Variables</summary> ```csharp ProfilerDump dump = new ProfilerDump(); dump.Load("path_to_your_profiler_dump_file"); for (int i = 0; i < dump.GetNumConsoleVariables(); i++) { ProfilerDump.DUMP_CONSOLE_VARIABLE_TYPE type = dump.GetConsoleVariableType(i); Log.Message($"Console variable {dump.GetConsoleVariableName(i)}: "); switch (type) { case ProfilerDump.DUMP_CONSOLE_VARIABLE_TYPE.STRING: Log.Message($"{dump.GetConsoleVariableValueString(i)} "); break; case ProfilerDump.DUMP_CONSOLE_VARIABLE_TYPE.INT: Log.Message($"{dump.GetConsoleVariableValueInt(i)} "); break; case ProfilerDump.DUMP_CONSOLE_VARIABLE_TYPE.FLOAT: Log.Message($"{dump.GetConsoleVariableValueFloat(i)} "); break; case ProfilerDump.DUMP_CONSOLE_VARIABLE_TYPE.VEC2: Log.Message($"{dump.GetConsoleVariableValueVec2(i)} "); break; case ProfilerDump.DUMP_CONSOLE_VARIABLE_TYPE.VEC3: Log.Message($"{dump.GetConsoleVariableValueVec3(i)} "); break; case ProfilerDump.DUMP_CONSOLE_VARIABLE_TYPE.VEC4: Log.Message($"{dump.GetConsoleVariableValueVec4(i)} "); break; case ProfilerDump.DUMP_CONSOLE_VARIABLE_TYPE.PALETTE: Log.Message($"{dump.GetConsoleVariableValuePalette(i)} "); break; default: break; } for (int h = 0; h < dump.GetNumConsoleVariableHistory(i); h++) { if (h == 0) { Log.Message(" ["); Log.Message($"{dump.GetConsoleVariableHistoryFrame(i, h)}: "); } else { Log.Message($"{dump.GetConsoleVariableHistoryFrame(i, h)}: "); } switch (type) { case ProfilerDump.DUMP_CONSOLE_VARIABLE_TYPE.STRING: Log.Message($"{dump.GetConsoleVariableHistoryValueString(i, h)}, "); break; case ProfilerDump.DUMP_CONSOLE_VARIABLE_TYPE.INT: Log.Message($"{dump.GetConsoleVariableHistoryValueInt(i, h)}, "); break; case ProfilerDump.DUMP_CONSOLE_VARIABLE_TYPE.FLOAT: Log.Message($"{dump.GetConsoleVariableHistoryValueFloat(i, h)}, "); break; case ProfilerDump.DUMP_CONSOLE_VARIABLE_TYPE.VEC2: Log.Message($"{dump.GetConsoleVariableHistoryValueVec2(i, h)}, "); break; case ProfilerDump.DUMP_CONSOLE_VARIABLE_TYPE.VEC3: Log.Message($"{dump.GetConsoleVariableHistoryValueVec3(i, h)}, "); break; case ProfilerDump.DUMP_CONSOLE_VARIABLE_TYPE.VEC4: Log.Message($"{dump.GetConsoleVariableHistoryValueVec4(i, h)}, "); break; case ProfilerDump.DUMP_CONSOLE_VARIABLE_TYPE.PALETTE: Log.Message($"{dump.GetConsoleVariableHistoryValuePalette(i, h)}, "); break; default: break; } } if (dump.GetNumConsoleVariableHistory(i) > 0) Log.Message("]\n"); else Log.Message("\n"); } ``` </details>
- When reading profiler parameters (metrics), it is important to understand [how per-frame parameter values are stored](../../../tools/profiling/profiler_dump/index_cs.md#profiler_dump_values). Each metric **may exist only for specific frames**, depending on whether it was active at the time of recording. Since parameter values are stored in union memory (to reduce file size), using a wrong getter method (e.g. try to get *int* value from a *float* parameter) will return invalid data. So its better to check the parameter type before reading values. The code example below illustrates how to properly retrieve all profiling metrics from the dump and print them to console. <details> <summary>Parsing Profiler Parameters</summary> ```csharp ProfilerDump dump = new ProfilerDump(); dump.Load("path_to_your_profiler_dump_file"); for (int p = 0; p < dump.NumDumpParameters; p++) { if (dump.GetDumpParameterType(p) == ProfilerDump.DUMP_PARAMETER_TYPE.INT) { Log.Message( $"{dump.GetDumpParameterName(p)}: " + $"Min: {dump.GetDumpParameterIntMin(p)}, " + $"Max: {dump.GetDumpParameterIntMax(p)}, " + $"Avg: {dump.GetDumpParameterIntAvg(p)} [" ); for (int frame = 0; frame < dump.NumFrames; frame++) { if (dump.ContainsFrameParameterIndex(frame, p)) Log.Message($"{dump.GetFrameParameterValueInt(frame, p)}, "); else Log.Message("NAN, "); } } else { Log.Message( $"{dump.GetDumpParameterName(p)}: " + $"Min: {dump.GetDumpParameterFloatMin(p)}, " + $"Max: {dump.GetDumpParameterFloatMax(p)}, " + $"Avg: {dump.GetDumpParameterFloatAvg(p)} [" ); for (int frame = 0; frame < dump.NumFrames; frame++) { if (dump.ContainsFrameParameterIndex(frame, p)) Log.Message($"{dump.GetFrameParameterValueFloat(frame, p)}, "); else Log.Message("NAN, "); } } Log.Message("]\n"); } ``` </details>


### See Also


- **[Profiler Dump](../../../tools/profiling/profiler_dump/index_cs.md)** article explaining how to record and read profiler dump files, including their structure and format.
- **[Profiler Reader](../../../tools/profiling/profiler_reader_tool/index.md)** tool that allows you to convert raw profiler dumps into a text files.


## ProfilerDump Class

### Enums

## DUMP_PARAMETER_TYPE

| Name | Description |
|---|---|
| **INT** = 0 | Integer dump parameter. |
| **FLOAT** = 1 | Float dump parameter. |

## DUMP_CONSOLE_VARIABLE_TYPE

| Name | Description |
|---|---|
| **STRING** = 0 | String console variable. |
| **INT** = 1 | Integer console variable. |
| **FLOAT** = 2 | Floating-point console variable. |
| **VEC2** = 3 | [Four-component vector](../../../api/library/math/cs/vec2_cs.md) console variable. |
| **VEC3** = 4 | [Four-component vector](../../../api/library/math/cs/vec3_cs.md) console variable. |
| **VEC4** = 5 | [Four-component vector](../../../api/library/math/cs/vec4_cs.md) console variable. |
| **PALETTE** = 6 | [Palette](../../../api/library/common/class.palette_cs.md) console variable. |

### Properties

## 🔒︎ int DumpVersion

The version of the profiler dump format used in the currently loaded dump.
## 🔒︎ string EngineVersion

The [version of the engine](../../../code/version_cs.md) that was used to record the profiler dump.
## 🔒︎ string EngineInfo

The version of the engine along with its build information stored in the profiler dump.
## 🔒︎ string BinaryInfo

The Engine binary build information stored in the profiler dump. This string contains details about the operating system, CPU architecture, build configuration, SDK, and compiler used to build the Engine binary that generated the dump.
## 🔒︎ string Features

The list of the features supported by the Engine build that generated the loaded profiler dump.
## 🔒︎ string RevisionInfo

The Engine source control revision information stored in the profiler dump.
## 🔒︎ string OsInfo

The operating system information that was used to record the profiler dump.
## 🔒︎ string CpuInfo

The detailed CPU information of the system that recorded the profiler dump. This includes the processor name, clock frequency, number of cores and threads, and the list of supported instruction sets.
## 🔒︎ long TotalMemory

The total amount of physical memory (RAM) on the system where the profiler dump was recorded, in bytes.
## 🔒︎ int NumGPUs

The number of GPUs detected on the system where the profiler dump was recorded.
## 🔒︎ int NumFrames

The total number of frames recorded in the profiler dump.
## 🔒︎ int NumDumpParameters

The
The total number of profiler metrics (parameters) recorded in the profiler dump.


> **Notice:** The set of metrics included in the dump depends on the runtime configuration, for example, certain metrics (such as *VRAM Terrain Cache* or *Upscaler*) are recorded only when the corresponding systems or features are active during profiling.


### Members

---

## ProfilerDump ( )

Default constructor. Creates an empty **ProfilerDump** instance that can later be initialized by loading a profiler dump file (with the `*.profiler_dump` extension) using the *[Load()](../../...md#load_cstr_int)* of *[Info()](../../...md#info_cstr_int)* method.
## bool Load ( string path )

Loads all profiler dump data from the specified file. This method reads and parses a `*.profiler_dump` file, allowing access to all recorded profiling information through the **ProfilerDump** class API.
### Arguments

- *string* **path** - Path to the profiler dump file.

### Return value

true, if the dump file was successfully loaded and parsed; otherwise false.
## bool Info ( string path )

Loads profiler dump data from the specified file, **except the per-frame information**. This method reads and parses a `*.profiler_dump` file, allowing access to system info, console variables and parameters general statistics through the **ProfilerDump** class API.
### Arguments

- *string* **path** - Path to the profiler dump file.

### Return value

true, if the dump file was successfully loaded and parsed; otherwise false.
## string GetGPUDescription ( int num )

Returns the description of the specified GPU recorded in the profiler dump. The description contains the full name of the graphics adapter.
### Arguments

- *int* **num** - zero-based index of the GPU device.

### Return value

A string containing the description of the GPU at the specified index.
## string GetGPUType ( int num )

Returns the GPU type for the specified device recorded in the profiler dump.
### Arguments

- *int* **num** - zero-based index of the GPU device.

### Return value

A string containing the GPU type. (e.g. *"Discrete"* or *"Intergrated"*)
## string GetGPUVendor ( int num )

Returns the vendor name for the specified GPU recorded in the profiler dump.
### Arguments

- *int* **num** - zero-based index of the GPU device.

## string GetGPUDriver ( int num )

Returns the driver version for the specified GPU recorded in the profiler dump.
### Arguments

- *int* **num** - zero-based index of the GPU device.

## int GetGPUMemory ( int num )

Returns the amount of VRAM (in megabytes) for the specified GPU recorded in the profiler dump.
### Arguments

- *int* **num** - zero-based index of the GPU device.

### Return value

The total GPU memory size (in megabytes).
## bool GetGPUCommonHeaps ( int num )

Checks whether the common heaps for the specified GPU recorded in the profiler dump are used.
### Arguments

- *int* **num** - zero-based index of the GPU device.

### Return value

true if the common heaps for the specified GPU are used; otherwise false.
## int GetGPUPriority ( int num )

Returns the device priority for the specified GPU recorded in the profiler dump.
### Arguments

- *int* **num** - zero-based index of the GPU device.

### Return value

The GPU's priority level.
## long GetGPULuid ( int num )

Returns the locally unique identifier for the specified GPU recorded in the profiler dump.
### Arguments

- *int* **num** - zero-based index of the GPU device.

### Return value

The GPU's locally unique identifier.
## uint GetGPUDeviceId ( int num )

Returns the identifier for the specified GPU recorded in the profiler dump.
### Arguments

- *int* **num** - zero-based index of the GPU device.

### Return value

The GPU's device identifier.
## int GetNumConsoleVariables ( )

Returns the total number of console variables recorded in the profiler dump. Each console variable represents a configurable engine parameter that was captured at the time the dump was recorded.
### Return value

The number of console variables stored in the dump.
## string GetConsoleVariableName ( int num )

Returns the name of the console variable recorded in the profiler dump at the specified index.
### Arguments

- *int* **num** - zero-based index of the console variable.

### Return value

The name of the console variable stored in the profiler dump.
## ProfilerDump.DUMP_CONSOLE_VARIABLE_TYPE GetConsoleVariableType ( int num )

Returns the type of the console variable recorded in the profiler dump at the specified index.
### Arguments

- *int* **num** - zero-based index of the console variable.

### Return value

The type of the console variable stored in the profiler dump.
## string GetConsoleVariableValueString ( int num )


Returns the value of the console variable recorded in the profiler dump at the specified index as a *string*. The value is automatically converted to a *string* type. If the conversion fails, an empty string is returned.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the variable type using *[GetConsoleVariableType()](../../...md#getConsoleVariableType_int_int)*


### Arguments

- *int* **num** - zero-based index of the console variable.

### Return value

The value of the console variable as a string, or an empty string if the conversion failed.
## int GetConsoleVariableValueInt ( int num )


Returns the value of the console variable recorded in the profiler dump at the specified index as an *int*. The value is automatically converted to an *int* type. If the conversion fails, 0 is returned.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the variable type using *[GetConsoleVariableType()](../../...md#getConsoleVariableType_int_int)*


### Arguments

- *int* **num** - zero-based index of the console variable.

### Return value

The value of the console variable converted to an *int*, or 0 if the conversion failed.
## float GetConsoleVariableValueFloat ( int num )


Returns the value of the console variable recorded in the profiler dump at the specified index as a *float*. The value is automatically converted to a *float* type. If the conversion fails, 0.0f is returned.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the variable type using *[GetConsoleVariableType()](../../...md#getConsoleVariableType_int_int)*

### Arguments

- *int* **num** - zero-based index of the console variable.

### Return value

The value of the console variable converted to a *float*, or 0.0f if the conversion failed.
## vec2 GetConsoleVariableValueVec2 ( int num )


Returns the value of the console variable recorded in the profiler dump at the specified index as a [*vec2*](../../../api/library/math/cs/vec2_cs.md). The value is automatically converted to a [*vec2*](../../../api/library/math/cs/vec2_cs.md) type. If the conversion fails, a zero vector (0.0f, 0.0f) is returned.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the variable type using *[GetConsoleVariableType()](../../...md#getConsoleVariableType_int_int)*

### Arguments

- *int* **num** - zero-based index of the console variable.

### Return value

The value of the console variable converted to a [*vec2*](../../../api/library/math/cs/vec2_cs.md), or (0.0f, 0.0f) if the conversion failed.
## vec3 GetConsoleVariableValueVec3 ( int num )


Returns the value of the console variable recorded in the profiler dump at the specified index as a [*vec3*](../../../api/library/math/cs/vec3_cs.md). The value is automatically converted to a [*vec3*](../../../api/library/math/cs/vec3_cs.md) type. If the conversion fails, a zero vector (0.0f, 0.0f, 0.0f) is returned.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the variable type using *[GetConsoleVariableType()](../../...md#getConsoleVariableType_int_int)*

### Arguments

- *int* **num** - zero-based index of the console variable.

### Return value

The value of the console variable converted to a [*vec3*](../../../api/library/math/cs/vec3_cs.md), or (0.0f, 0.0f, 0.0f) if the conversion failed.
## vec4 GetConsoleVariableValueVec4 ( int num )


Returns the value of the console variable recorded in the profiler dump at the specified index as a [*vec4*](../../../api/library/math/cs/vec4_cs.md). The value is automatically converted to a [*vec4*](../../../api/library/math/cs/vec4_cs.md) type. If the conversion fails, a zero vector (0.0f, 0.0f, 0.0f, 0.0f) is returned.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the variable type using *[GetConsoleVariableType()](../../...md#getConsoleVariableType_int_int)*

### Arguments

- *int* **num** - zero-based index of the console variable.

### Return value

The value of the console variable converted to a [*vec4*](../../../api/library/math/cs/vec4_cs.md), or (0.0f, 0.0f, 0.0f, 0.0f) if the conversion failed.
## Palette GetConsoleVariableValuePalette ( int num )


Returns the value of the console variable recorded in the profiler dump at the specified index as a [*Palette*](../../../api/library/common/class.palette_cs.md). The value is automatically converted to a [*Palette*](../../../api/library/common/class.palette_cs.md) type. If the conversion fails, a zero palette is returned.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the variable type using *[GetConsoleVariableType()](../../...md#getConsoleVariableType_int_int)*

### Arguments

- *int* **num** - zero-based index of the console variable.

### Return value

The value of the console variable converted to a [*Palette*](../../../api/library/common/class.palette_cs.md), or a zero palette if the conversion failed.
## int GetNumConsoleVariableHistory ( int num )

Returns the number of recorded history entries for the specified index for the console variable. A variable's history is recorded only if its value changed during the profiling session.
### Arguments

- *int* **num** - zero-based index of the console variable.

### Return value

The number of history entries for the specified console variable.
## long GetConsoleVariableHistoryFrame ( int num , int h )

Returns the frame index at which the specified console variable changed its value for the *h-th* time.
### Arguments

- *int* **num** - zero-based index of the console variable.
- *int* **h** - zero-based sequential index of the value change in the variable history.

### Return value

The frame number when the console variable changed for the specified time. For example, if a variable changed 10 times and you want to know the frame of the 5th change, specify h=5.
## string GetConsoleVariableHistoryValueString ( int num , int h )


Returns the value of the console variable recorded in the profiler dump at the specified index and history position, converted to *string*. If the conversion fails, an empty string is returned.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the variable type using *[GetConsoleVariableType()](../../...md#getConsoleVariableType_int_int)*

### Arguments

- *int* **num** - zero-based index of the console variable.
- *int* **h** - zero-based sequential index of the value change in the variable history.

### Return value

The historical value of the console variable as *string*, or an empty string if conversion failed.
## int GetConsoleVariableHistoryValueInt ( int num , int h )


Returns the value of the console variable recorded in the profiler dump at the specified index and history position, converted to *int*. If the conversion fails, a 0 is returned.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the variable type using *[GetConsoleVariableType()](../../...md#getConsoleVariableType_int_int)*

### Arguments

- *int* **num** - zero-based index of the console variable.
- *int* **h** - zero-based sequential index of the value change in the variable history.

### Return value

The historical value of the console variable as *int*, or 0 if conversion failed.
## float GetConsoleVariableHistoryValueFloat ( int num , int h )


Returns the value of the console variable recorded in the profiler dump at the specified index and history position, converted to *float*. If the conversion fails, a 0.0f is returned.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the variable type using *[GetConsoleVariableType()](../../...md#getConsoleVariableType_int_int)*

### Arguments

- *int* **num** - zero-based index of the console variable.
- *int* **h** - zero-based sequential index of the value change in the variable history.

### Return value

The historical value of the console variable as *float*, or 0.0f if conversion failed.
## vec2 GetConsoleVariableHistoryValueVec2 ( int num , int h )


Returns the value of the console variable recorded in the profiler dump at the specified index and history position, converted to a [*vec2*](../../../api/library/math/cs/vec2_cs.md). If the conversion fails, a zero vector (0.0f, 0.0f) is returned.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the variable type using *[GetConsoleVariableType()](../../...md#getConsoleVariableType_int_int)*

### Arguments

- *int* **num** - zero-based index of the console variable.
- *int* **h** - zero-based sequential index of the value change in the variable history.

### Return value

The historical value of the console variable converted to a [*vec2*](../../../api/library/math/cs/vec2_cs.md), or (0.0f, 0.0f) if the conversion failed.
## vec3 GetConsoleVariableHistoryValueVec3 ( int num , int h )


Returns the value of the console variable recorded in the profiler dump at the specified index and history position, converted to a [*vec3*](../../../api/library/math/cs/vec3_cs.md). If the conversion fails, a zero vector (0.0f, 0.0f, 0.0f) is returned.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the variable type using *[GetConsoleVariableType()](../../...md#getConsoleVariableType_int_int)*

### Arguments

- *int* **num** - zero-based index of the console variable.
- *int* **h** - zero-based sequential index of the value change in the variable history.

### Return value

The historical value of the console variable converted to a [*vec3*](../../../api/library/math/cs/vec3_cs.md), or (0.0f, 0.0f, 0.0f) if the conversion failed.
## vec4 GetConsoleVariableHistoryValueVec4 ( int num , int h )


Returns the value of the console variable recorded in the profiler dump at the specified index and history position, converted to a [*vec4*](../../../api/library/math/cs/vec4_cs.md). If the conversion fails, a zero vector (0.0f, 0.0f, 0.0f, 0.0f) is returned.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the variable type using *[GetConsoleVariableType()](../../...md#getConsoleVariableType_int_int)*

### Arguments

- *int* **num** - zero-based index of the console variable.
- *int* **h** - zero-based sequential index of the value change in the variable history.

### Return value

The historical value of the console variable converted to a [*vec4*](../../../api/library/math/cs/vec4_cs.md), or (0.0f, 0.0f, 0.0f, 0.0f) if the conversion failed.
## Palette GetConsoleVariableHistoryValuePalette ( int num , int h )


Returns the value of the console variable recorded in the profiler dump at the specified index and history position, converted to a [*Palette*](../../../api/library/common/class.palette_cs.md). If the conversion fails, a zero palette is returned.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the variable type using *[GetConsoleVariableType()](../../...md#getConsoleVariableType_int_int)*

### Arguments

- *int* **num** - zero-based index of the console variable.
- *int* **h** - zero-based sequential index of the value change in the variable history.

### Return value

The historical value of the console variable converted to a [*Palette*](../../../api/library/common/class.palette_cs.md), or a zero palette if the conversion failed.
## long GetStartFrame ( )

Returns the Engine frame number at which the profiler dump recording started. This value represents the absolute frame index from the beginning of the Engine runtime when the dump began capturing profiling data.
### Return value

The frame number corresponding to the start of the profiler dump recording.
## long GetFrame ( int num )

Returns the Engine frame number corresponding to the specified frame index within the profiler dump. This allows you to determine which engine frame each recorded dump frame represents.
### Arguments

- *int* **num** - zero-based index of the profiler dump frame.

### Return value

The Engine frame number that corresponds to the specified dump frame.
## long GetFrameTimeMicroseconds ( int num )

Returns the timestamp of the specified frame in microseconds. This value represents the elapsed time since the start of the dump up to beginning of the given frame.
### Arguments

- *int* **num** - zero-based index of the profiler dump frame.

### Return value

The frame time in microseconds relative to the start of the profiler dump recording.
## double GetFrameTimeSeconds ( int num )

Returns the timestamp of the specified frame in seconds. This value represents the elapsed time since the start of the dump up to beginning of the given frame.
### Arguments

- *int* **num** - zero-based index of the profiler dump frame.

### Return value

The frame time in seconds relative to the start of the profiler dump recording.
## double GetFrameTimeMilliseconds ( int num )

Returns the timestamp of the specified frame in milliseconds. This value represents the elapsed time since the start of the dump up to beginning of the given frame.
### Arguments

- *int* **num** - zero-based index of the profiler dump frame.

### Return value

The frame time in milliseconds relative to the start of the profiler dump recording.
## int GetNumFrameParameters ( int frame )

Returns the number of profiler parameters recorded for the specified frame in the profiler dump. The number of parameters may vary between frames, since some metrics are recorded when they are enabled and active (e.g. upscalers).
### Arguments

- *int* **frame** - zero-based index of the profiler dump frame.

### Return value

The number of profiler parameters recorded for the specified frame.
## int GetFrameParameterIndex ( int frame , int num_parameter )

Returns the global dump parameter index that corresponds to the local parameter position within a specific frame. The profiler dump contains a fixed global list of parameters (metrics). Each frame stores values only for parameters that were active in that frame, so per-frame parameter list is a subset of the global list. This methos translates a frame-local parameter position to its global parameter index.
### Arguments

- *int* **frame** - zero-based index of the profiler dump frame.
- *int* **num_parameter** - zero-based local position of the parameter inside the specified frame in range [0, *[GetNumFrameParameters](../../...md#getNumFrameParameters_int_int)* - 1].

### Return value

The global parameter index in the dump in range [0, *[NumDumpParameters](../../...md#getNumDumpParameters_int)* - 1]
## int GetFrameParameterValueInt ( int frame , int num_parameter )

Returns the raw integer representation of the specified frame-local parameter value.
### Arguments

- *int* **frame** - zero-based index of the profiler dump frame.
- *int* **num_parameter** - zero-based local position of the parameter inside the specified frame in range [0, *[GetNumFrameParameters](../../...md#getNumFrameParameters_int_int)* - 1].

### Return value

The raw integer stored for this parameter in the specified frame.
## float GetFrameParameterValueFloat ( int frame , int num_parameter )

Returns the raw float representation of the specified frame-local parameter value.
### Arguments

- *int* **frame** - zero-based index of the profiler dump frame.
- *int* **num_parameter** - zero-based local position of the parameter inside the specified frame in range [0, *[GetNumFrameParameters](../../...md#getNumFrameParameters_int_int)* - 1].

### Return value

The raw float stored for this parameter in the specified frame.
## bool ContainsFrameParameterIndex ( int frame , int paramter_index )

Checks whether the specified global dump parameter index is present among the parameters recorded for the given frame. Since each frame contains only a subset of the global dump metrics (those that were active in that frame), this method lets you test if a particular metric is available in that frame.
### Arguments

- *int* **frame** - zero-based index of the profiler dump frame.
- *int* **paramter_index** - zero-based global parameter index in the dump in range [0, *[NumDumpParameters](../../...md#getNumDumpParameters_int)* - 1]

### Return value

true if the frame contains a value for the specified global dump parameter; otherwise false.
## string GetDumpParameterName ( int num )

Returns the name of the profiler dump parameter identified by the given index.
### Arguments

- *int* **num** - zero-based profiler dump parameter index in range [0, *[NumDumpParameters](../../...md#getNumDumpParameters_int)* - 1].

### Return value

The name of the dump parameter.
## string GetDumpParameterUnits ( int num )

Returns the measurement units for the specified dump profiler parameter.
### Arguments

- *int* **num** - zero-based profiler dump parameter index in range [0, *[NumDumpParameters](../../...md#getNumDumpParameters_int)* - 1].

### Return value

The units string for the parameter (e.g. *"ms"*, *"MB"*).
## ProfilerDump.DUMP_PARAMETER_TYPE GetDumpParameterType ( int num )

Returns the storage type of the specified profiler parameter. The type indicates whether the parameter's per-frame values are stored as *int* of *float*.
### Arguments

- *int* **num** - zero-based profiler dump parameter index in range [0, *[NumDumpParameters](../../...md#getNumDumpParameters_int)* - 1].

### Return value

The type used to store the profiler parameter at the specified index.
## int GetDumpParameterIntMin ( int num )


Returns the minimum observed value (as *int*) for the specified profiler parameter identified by the given index.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the parameter type using *[GetDumpParameterType()](../../...md#getDumpParameterType_int_int)*.

### Arguments

- *int* **num** - zero-based profiler dump parameter index in range [0, *[NumDumpParameters](../../...md#getNumDumpParameters_int)* - 1].

### Return value

Minimum value as integer.
## int GetDumpParameterIntMax ( int num )


Returns the maximum observed value (as *int*) for the specified profiler parameter identified by the given index.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the parameter type using *[GetDumpParameterType()](../../...md#getDumpParameterType_int_int)*.

### Arguments

- *int* **num** - zero-based profiler dump parameter index in range [0, *[NumDumpParameters](../../...md#getNumDumpParameters_int)* - 1].

### Return value

Maximum value as integer.
## int GetDumpParameterIntAvg ( int num )


Returns the average value (as *int*) for the specified profiler parameter identified by the given index.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the parameter type using *[GetDumpParameterType()](../../...md#getDumpParameterType_int_int)*.

### Arguments

- *int* **num** - zero-based profiler dump parameter index in range [0, *[NumDumpParameters](../../...md#getNumDumpParameters_int)* - 1].

### Return value

Average value as integer.
## float GetDumpParameterFloatMin ( int num )


Returns the minimum observed value (as *float*) for the specified profiler parameter identified by the given index.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the parameter type using *[GetDumpParameterType()](../../...md#getDumpParameterType_int_int)*.

### Arguments

- *int* **num** - zero-based profiler dump parameter index in range [0, *[NumDumpParameters](../../...md#getNumDumpParameters_int)* - 1].

### Return value

Minimum value as float.
## float GetDumpParameterFloatMax ( int num )


Returns the maximum observed value (as *float*) for the specified profiler parameter identified by the given index.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the parameter type using *[GetDumpParameterType()](../../...md#getDumpParameterType_int_int)*.

### Arguments

- *int* **num** - zero-based profiler dump parameter index in range [0, *[NumDumpParameters](../../...md#getNumDumpParameters_int)* - 1].

### Return value

Maximum value as float.
## float GetDumpParameterFloatAvg ( int num )


Returns the average value (as *float*) for the specified profiler parameter identified by the given index.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the parameter type using *[GetDumpParameterType()](../../...md#getDumpParameterType_int_int)*.

### Arguments

- *int* **num** - zero-based profiler dump parameter index in range [0, *[NumDumpParameters](../../...md#getNumDumpParameters_int)* - 1].

### Return value

Average value as float.
