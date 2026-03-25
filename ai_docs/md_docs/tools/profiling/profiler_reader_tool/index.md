# Profiler Reader


In addition to monitoring engine performance in real time using the **[Profiler](../../../tools/profiling/profiler/index.md)**, you can also collect and analyze its per-frame performance data using the:


- *[Profiler](../../../api/library/engine/class.profiler_cpp.md#startProfilerDump_int_cstr_void)* class methods
- Console commands (e.g. *[profiling_start](../../../code/console/index.md#profiling_start), [profiling_stop](../../../code/console/index.md#profiling_stop)*)


The resulting **profiler dump** contains general information about the system and Engine configuration on which it was recorded, the values of all console variables (including any changes made during the recording), as well as all Profiler parameters (metrics) that were active or became active during the dump session.


The raw `*.profiler_dump` file is stored in a binary format, which means it cannot be read or analyzed directly. To access the data contained in a profiler dump, you can use the **[ProfilerDump](../../../api/library/engine/class.profilerdump_cpp.md)** class or the **Profiler Reader** tool.


![](../profiler_dump/profiler_reader.png)


The **Profiler Reader** tool allows you to:


- View general dump information
- Convert dumps to text format with step filtering
- List average values of parameters


This article explains how to extract and work with profiler dump data using the **Profiler Reader**.


### See Also


- **[Profiler Dump](../../../tools/profiling/profiler_dump/index_cpp.md)** article explaining how to record and read profiler dump files, including their structure and format.


- **[ProfilerDump](../../../api/library/engine/class.profilerdump_cpp.md)** class API for flexible control over reading and processing dump data via code.


## Profiler Reader Usage


To invoke Profiler Reader Tool, run `<UnigineSDK>/bin/profiler_reader_x64.exe` (on Windows) or `<UnigineSDK>/bin/profiler_reader_x64` (on Linux) from a command-line console.


It provides several command-line options for processing and analyzing the dump file.


> **Notice:** All commands must be executed from the directory containing the `*.profiler_dump` file or with the full path specified.


```text
profiler_reader_x64.exe [option] <input_file> [output_file]

```


## Command-Line Options


Profiler Reader Tool recognizes the following command-line options:


- **-c *<input_file> <output_file>*** - convert a binary `*.profiler_dump` file into a human-readable text file. The output file must be specified. ```text profiler_reader_x64.exe -c dump.profiler_dump profiler_dump.txt ```
- **-i *<input_file>*** - print general information about the system and the Engine configuration on which the profiler dump was recorded. ```text profiler_reader_x64.exe -i dump.profiler_dump ```
- **-a *<input_file>*** - print average values of all profiler parameters (metrics) recorded in the dump. ```text profiler_reader_x64.exe -a dump.profiler_dump ```
- **-s *<num>*** - define the step size for skipping parameter frames during data output. This option affects only the converted to text results, not the underlying calculations. Minimum, maximum, and average values are still computed using all frames in the dump. Use this option to reduce the amount of displayed data or to focus on broader performance trends by showing every n-th frame. ```text profiler_reader_x64.exe -c dump.profiler_dump profiler_dump.txt -s 10 ```
