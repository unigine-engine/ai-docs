# Unigine::ProfilerDump Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


The **ProfilerDump** class provides access to performance data stored in [profiler dump files](../../../tools/profiling/profiler_dump/index.md) (`*.profiler_dump`). Profiler dumps are saved in a binary format to reduce file size and speed up recording. Because of that, the file cannot be viewed directly in a text editor - it must be opened using this class or the *[Profiler Reader](../../../tools/profiling/profiler_reader_tool/index.md)* tool.


It is important to understand how to correctly retrieve information from the dump to avoid data corruption or invalid results.


### See Also


- **[Profiler Dump](../../../tools/profiling/profiler_dump/index.md)** article explaining how to record and read profiler dump files, including their structure and format.
- **[Profiler Reader](../../../tools/profiling/profiler_reader_tool/index.md)** tool that allows you to convert raw profiler dumps into a text files.


## ProfilerDump Class

### Members

## int getDumpVersion () const

The version of the profiler dump format used in the currently loaded dump.
### Return value

Version of the profiler dump format used in the currently loaded dump.
## const char * getEngineVersion () const

The [version of the engine](../../../code/version.md) that was used to record the profiler dump.
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

Default constructor. Creates an empty **ProfilerDump** instance that can later be initialized by loading a profiler dump file (with the `*.profiler_dump` extension) using the *[load()()](../../...md#load_cstr_int)* of *[info()()](../../...md#info_cstr_int)* method.
## int load ( string path )

Loads all profiler dump data from the specified file. This method reads and parses a `*.profiler_dump` file, allowing access to all recorded profiling information through the **ProfilerDump** class API.
### Arguments

- *string* **path** - Path to the profiler dump file.

### Return value

true, if the dump file was successfully loaded and parsed; otherwise false.
## int info ( string path )

Loads profiler dump data from the specified file, **except the per-frame information**. This method reads and parses a `*.profiler_dump` file, allowing access to system info, console variables and parameters general statistics through the **ProfilerDump** class API.
### Arguments

- *string* **path** - Path to the profiler dump file.

### Return value

true, if the dump file was successfully loaded and parsed; otherwise false.
## string getGPUDescription ( int num )

Returns the description of the specified GPU recorded in the profiler dump. The description contains the full name of the graphics adapter.
### Arguments

- *int* **num** - zero-based index of the GPU device.

### Return value

A string containing the description of the GPU at the specified index.
## string getGPUType ( int num )

Returns the GPU type for the specified device recorded in the profiler dump.
### Arguments

- *int* **num** - zero-based index of the GPU device.

### Return value

A string containing the GPU type. (e.g. *"Discrete"* or *"Intergrated"*)
## string getGPUVendor ( int num )

Returns the vendor name for the specified GPU recorded in the profiler dump.
### Arguments

- *int* **num** - zero-based index of the GPU device.

## string getGPUDriver ( int num )

Returns the driver version for the specified GPU recorded in the profiler dump.
### Arguments

- *int* **num** - zero-based index of the GPU device.

## int getGPUMemory ( int num )

Returns the amount of VRAM (in megabytes) for the specified GPU recorded in the profiler dump.
### Arguments

- *int* **num** - zero-based index of the GPU device.

### Return value

The total GPU memory size (in megabytes).
## bool getGPUCommonHeaps ( int num )

Checks whether the common heaps for the specified GPU recorded in the profiler dump are used.
### Arguments

- *int* **num** - zero-based index of the GPU device.

### Return value

true if the common heaps for the specified GPU are used; otherwise false.
## int getGPUPriority ( int num )

Returns the device priority for the specified GPU recorded in the profiler dump.
### Arguments

- *int* **num** - zero-based index of the GPU device.

### Return value

The GPU's priority level.
## long getGPULuid ( int num )

Returns the locally unique identifier for the specified GPU recorded in the profiler dump.
### Arguments

- *int* **num** - zero-based index of the GPU device.

### Return value

The GPU's locally unique identifier.
## unsigned int getGPUDeviceId ( int num )

Returns the identifier for the specified GPU recorded in the profiler dump.
### Arguments

- *int* **num** - zero-based index of the GPU device.

### Return value

The GPU's device identifier.
## int getNumConsoleVariables ( )

Returns the total number of console variables recorded in the profiler dump. Each console variable represents a configurable engine parameter that was captured at the time the dump was recorded.
### Return value

The number of console variables stored in the dump.
## string getConsoleVariableName ( int num )

Returns the name of the console variable recorded in the profiler dump at the specified index.
### Arguments

- *int* **num** - zero-based index of the console variable.

### Return value

The name of the console variable stored in the profiler dump.
## int getConsoleVariableType ( int num )

Returns the type of the console variable recorded in the profiler dump at the specified index.
### Arguments

- *int* **num** - zero-based index of the console variable.

### Return value

The type of the console variable stored in the profiler dump.
## string getConsoleVariableValueString ( int num )


Returns the value of the console variable recorded in the profiler dump at the specified index as a *string*. The value is automatically converted to a *string* type. If the conversion fails, an empty string is returned.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the variable type using *[getConsoleVariableType()()](../../...md#getConsoleVariableType_int_int)*


### Arguments

- *int* **num** - zero-based index of the console variable.

### Return value

The value of the console variable as a string, or an empty string if the conversion failed.
## int getConsoleVariableValueInt ( int num )


Returns the value of the console variable recorded in the profiler dump at the specified index as an *int*. The value is automatically converted to an *int* type. If the conversion fails, 0 is returned.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the variable type using *[getConsoleVariableType()()](../../...md#getConsoleVariableType_int_int)*


### Arguments

- *int* **num** - zero-based index of the console variable.

### Return value

The value of the console variable converted to an *int*, or 0 if the conversion failed.
## float getConsoleVariableValueFloat ( int num )


Returns the value of the console variable recorded in the profiler dump at the specified index as a *float*. The value is automatically converted to a *float* type. If the conversion fails, 0.0f is returned.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the variable type using *[getConsoleVariableType()()](../../...md#getConsoleVariableType_int_int)*

### Arguments

- *int* **num** - zero-based index of the console variable.

### Return value

The value of the console variable converted to a *float*, or 0.0f if the conversion failed.
## vec2 getConsoleVariableValueVec2 ( int num )

### Arguments

- *int* **num** - zero-based index of the console variable.

### Return value

## vec3 getConsoleVariableValueVec3 ( int num )

### Arguments

- *int* **num** - zero-based index of the console variable.

### Return value

## vec4 getConsoleVariableValueVec4 ( int num )

### Arguments

- *int* **num** - zero-based index of the console variable.

### Return value

## Palette getConsoleVariableValuePalette ( int num )


Returns the value of the console variable recorded in the profiler dump at the specified index as a [*Palette*](../../../api/library/common/class.palette_usc.md). The value is automatically converted to a [*Palette*](../../../api/library/common/class.palette_usc.md) type. If the conversion fails, a zero palette is returned.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the variable type using *[getConsoleVariableType()()](../../...md#getConsoleVariableType_int_int)*

### Arguments

- *int* **num** - zero-based index of the console variable.

### Return value

The value of the console variable converted to a [*Palette*](../../../api/library/common/class.palette_usc.md), or a zero palette if the conversion failed.
## int getNumConsoleVariableHistory ( int num )

Returns the number of recorded history entries for the specified index for the console variable. A variable's history is recorded only if its value changed during the profiling session.
### Arguments

- *int* **num** - zero-based index of the console variable.

### Return value

The number of history entries for the specified console variable.
## long getConsoleVariableHistoryFrame ( int num , int h )

Returns the frame index at which the specified console variable changed its value for the *h-th* time.
### Arguments

- *int* **num** - zero-based index of the console variable.
- *int* **h** - zero-based sequential index of the value change in the variable history.

### Return value

The frame number when the console variable changed for the specified time. For example, if a variable changed 10 times and you want to know the frame of the 5th change, specify h=5.
## string getConsoleVariableHistoryValueString ( int num , int h )


Returns the value of the console variable recorded in the profiler dump at the specified index and history position, converted to *string*. If the conversion fails, an empty string is returned.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the variable type using *[getConsoleVariableType()()](../../...md#getConsoleVariableType_int_int)*

### Arguments

- *int* **num** - zero-based index of the console variable.
- *int* **h** - zero-based sequential index of the value change in the variable history.

### Return value

The historical value of the console variable as *string*, or an empty string if conversion failed.
## int getConsoleVariableHistoryValueInt ( int num , int h )


Returns the value of the console variable recorded in the profiler dump at the specified index and history position, converted to *int*. If the conversion fails, a 0 is returned.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the variable type using *[getConsoleVariableType()()](../../...md#getConsoleVariableType_int_int)*

### Arguments

- *int* **num** - zero-based index of the console variable.
- *int* **h** - zero-based sequential index of the value change in the variable history.

### Return value

The historical value of the console variable as *int*, or 0 if conversion failed.
## float getConsoleVariableHistoryValueFloat ( int num , int h )


Returns the value of the console variable recorded in the profiler dump at the specified index and history position, converted to *float*. If the conversion fails, a 0.0f is returned.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the variable type using *[getConsoleVariableType()()](../../...md#getConsoleVariableType_int_int)*

### Arguments

- *int* **num** - zero-based index of the console variable.
- *int* **h** - zero-based sequential index of the value change in the variable history.

### Return value

The historical value of the console variable as *float*, or 0.0f if conversion failed.
## vec2 getConsoleVariableHistoryValueVec2 ( int num , int h )

### Arguments

- *int* **num** - zero-based index of the console variable.
- *int* **h** - zero-based sequential index of the value change in the variable history.

### Return value

## vec3 getConsoleVariableHistoryValueVec3 ( int num , int h )

### Arguments

- *int* **num** - zero-based index of the console variable.
- *int* **h** - zero-based sequential index of the value change in the variable history.

### Return value

## vec4 getConsoleVariableHistoryValueVec4 ( int num , int h )

### Arguments

- *int* **num** - zero-based index of the console variable.
- *int* **h** - zero-based sequential index of the value change in the variable history.

### Return value

## Palette getConsoleVariableHistoryValuePalette ( int num , int h )


Returns the value of the console variable recorded in the profiler dump at the specified index and history position, converted to a [*Palette*](../../../api/library/common/class.palette_usc.md). If the conversion fails, a zero palette is returned.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the variable type using *[getConsoleVariableType()()](../../...md#getConsoleVariableType_int_int)*

### Arguments

- *int* **num** - zero-based index of the console variable.
- *int* **h** - zero-based sequential index of the value change in the variable history.

### Return value

The historical value of the console variable converted to a [*Palette*](../../../api/library/common/class.palette_usc.md), or a zero palette if the conversion failed.
## long getStartFrame ( )

Returns the Engine frame number at which the profiler dump recording started. This value represents the absolute frame index from the beginning of the Engine runtime when the dump began capturing profiling data.
### Return value

The frame number corresponding to the start of the profiler dump recording.
## long getFrame ( int num )

Returns the Engine frame number corresponding to the specified frame index within the profiler dump. This allows you to determine which engine frame each recorded dump frame represents.
### Arguments

- *int* **num** - zero-based index of the profiler dump frame.

### Return value

The Engine frame number that corresponds to the specified dump frame.
## long getFrameTimeMicroseconds ( int num )

Returns the timestamp of the specified frame in microseconds. This value represents the elapsed time since the start of the dump up to beginning of the given frame.
### Arguments

- *int* **num** - zero-based index of the profiler dump frame.

### Return value

The frame time in microseconds relative to the start of the profiler dump recording.
## double getFrameTimeSeconds ( int num )

Returns the timestamp of the specified frame in seconds. This value represents the elapsed time since the start of the dump up to beginning of the given frame.
### Arguments

- *int* **num** - zero-based index of the profiler dump frame.

### Return value

The frame time in seconds relative to the start of the profiler dump recording.
## double getFrameTimeMilliseconds ( int num )

Returns the timestamp of the specified frame in milliseconds. This value represents the elapsed time since the start of the dump up to beginning of the given frame.
### Arguments

- *int* **num** - zero-based index of the profiler dump frame.

### Return value

The frame time in milliseconds relative to the start of the profiler dump recording.
## int getNumFrameParameters ( int frame )

Returns the number of profiler parameters recorded for the specified frame in the profiler dump. The number of parameters may vary between frames, since some metrics are recorded when they are enabled and active (e.g. upscalers).
### Arguments

- *int* **frame** - zero-based index of the profiler dump frame.

### Return value

The number of profiler parameters recorded for the specified frame.
## int getFrameParameterIndex ( int frame , int num_parameter )

Returns the global dump parameter index that corresponds to the local parameter position within a specific frame. The profiler dump contains a fixed global list of parameters (metrics). Each frame stores values only for parameters that were active in that frame, so per-frame parameter list is a subset of the global list. This methos translates a frame-local parameter position to its global parameter index.
### Arguments

- *int* **frame** - zero-based index of the profiler dump frame.
- *int* **num_parameter** - zero-based local position of the parameter inside the specified frame in range [0, *[getNumFrameParameters()](../../...md#getNumFrameParameters_int_int)* - 1].

### Return value

The global parameter index in the dump in range [0, *[getNumDumpParameters()](../../...md#getNumDumpParameters_int)* - 1]
## int getFrameParameterValueInt ( int frame , int num_parameter )

Returns the raw integer representation of the specified frame-local parameter value.
### Arguments

- *int* **frame** - zero-based index of the profiler dump frame.
- *int* **num_parameter** - zero-based local position of the parameter inside the specified frame in range [0, *[getNumFrameParameters()](../../...md#getNumFrameParameters_int_int)* - 1].

### Return value

The raw integer stored for this parameter in the specified frame.
## float getFrameParameterValueFloat ( int frame , int num_parameter )

Returns the raw float representation of the specified frame-local parameter value.
### Arguments

- *int* **frame** - zero-based index of the profiler dump frame.
- *int* **num_parameter** - zero-based local position of the parameter inside the specified frame in range [0, *[getNumFrameParameters()](../../...md#getNumFrameParameters_int_int)* - 1].

### Return value

The raw float stored for this parameter in the specified frame.
## int containsFrameParameterIndex ( int frame , int paramter_index )

Checks whether the specified global dump parameter index is present among the parameters recorded for the given frame. Since each frame contains only a subset of the global dump metrics (those that were active in that frame), this method lets you test if a particular metric is available in that frame.
### Arguments

- *int* **frame** - zero-based index of the profiler dump frame.
- *int* **paramter_index** - zero-based global parameter index in the dump in range [0, *[getNumDumpParameters()](../../...md#getNumDumpParameters_int)* - 1]

### Return value

true if the frame contains a value for the specified global dump parameter; otherwise false.
## string getDumpParameterName ( int num )

Returns the name of the profiler dump parameter identified by the given index.
### Arguments

- *int* **num** - zero-based profiler dump parameter index in range [0, *[getNumDumpParameters()](../../...md#getNumDumpParameters_int)* - 1].

### Return value

The name of the dump parameter.
## string getDumpParameterUnits ( int num )

Returns the measurement units for the specified dump profiler parameter.
### Arguments

- *int* **num** - zero-based profiler dump parameter index in range [0, *[getNumDumpParameters()](../../...md#getNumDumpParameters_int)* - 1].

### Return value

The units string for the parameter (e.g. *"ms"*, *"MB"*).
## int getDumpParameterType ( int num )

Returns the storage type of the specified profiler parameter. The type indicates whether the parameter's per-frame values are stored as *int* of *float*.
### Arguments

- *int* **num** - zero-based profiler dump parameter index in range [0, *[getNumDumpParameters()](../../...md#getNumDumpParameters_int)* - 1].

### Return value

The type used to store the profiler parameter at the specified index.
## int getDumpParameterIntMin ( int num )


Returns the minimum observed value (as *int*) for the specified profiler parameter identified by the given index.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the parameter type using *[getDumpParameterType()()](../../...md#getDumpParameterType_int_int)*.

### Arguments

- *int* **num** - zero-based profiler dump parameter index in range [0, *[getNumDumpParameters()](../../...md#getNumDumpParameters_int)* - 1].

### Return value

Minimum value as integer.
## int getDumpParameterIntMax ( int num )


Returns the maximum observed value (as *int*) for the specified profiler parameter identified by the given index.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the parameter type using *[getDumpParameterType()()](../../...md#getDumpParameterType_int_int)*.

### Arguments

- *int* **num** - zero-based profiler dump parameter index in range [0, *[getNumDumpParameters()](../../...md#getNumDumpParameters_int)* - 1].

### Return value

Maximum value as integer.
## int getDumpParameterIntAvg ( int num )


Returns the average value (as *int*) for the specified profiler parameter identified by the given index.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the parameter type using *[getDumpParameterType()()](../../...md#getDumpParameterType_int_int)*.

### Arguments

- *int* **num** - zero-based profiler dump parameter index in range [0, *[getNumDumpParameters()](../../...md#getNumDumpParameters_int)* - 1].

### Return value

Average value as integer.
## float getDumpParameterFloatMin ( int num )


Returns the minimum observed value (as *float*) for the specified profiler parameter identified by the given index.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the parameter type using *[getDumpParameterType()()](../../...md#getDumpParameterType_int_int)*.

### Arguments

- *int* **num** - zero-based profiler dump parameter index in range [0, *[getNumDumpParameters()](../../...md#getNumDumpParameters_int)* - 1].

### Return value

Minimum value as float.
## float getDumpParameterFloatMax ( int num )


Returns the maximum observed value (as *float*) for the specified profiler parameter identified by the given index.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the parameter type using *[getDumpParameterType()()](../../...md#getDumpParameterType_int_int)*.

### Arguments

- *int* **num** - zero-based profiler dump parameter index in range [0, *[getNumDumpParameters()](../../...md#getNumDumpParameters_int)* - 1].

### Return value

Maximum value as float.
## float getDumpParameterFloatAvg ( int num )


Returns the average value (as *float*) for the specified profiler parameter identified by the given index.


> **Notice:** This method converts the value automatically. To properly retrieve information, check the parameter type using *[getDumpParameterType()()](../../...md#getDumpParameterType_int_int)*.

### Arguments

- *int* **num** - zero-based profiler dump parameter index in range [0, *[getNumDumpParameters()](../../...md#getNumDumpParameters_int)* - 1].

### Return value

Average value as float.
