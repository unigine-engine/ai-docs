# Collecting Profiling Statistics (CS)


You can analyze engine performance in real time using the [Profiler](../../../tools/profiling/profiler/index.md) or [Microprofile](../../../tools/profiling/microprofile/index_cs.md) tools. However, it can also be useful to collect performance statistics over time for detailed post-analysis.


This article explains how to record time-based performance data from the Engine into profiler dump files, and how to retrieve and interpret this data for further analysis.


## Starting Profiling Dumps


### Using API


To programmatically collect profiling data, use the static methods of the **[Profiler](../../../api/library/engine/class.profiler_cs.md)** class. These methods start recording a profiler dump and save it to a file. You can choose to record until manually stopped, or for a specified number of frames or seconds. The available methods are:


- ***[StartProfilerDump (string path)](../../../api/library/engine/class.profiler_cs.md#startProfilerDump_cstr_void)*** - starts recording a profiler dump and continues until stopped. If no path is specified, the dump file will be saved under the directory defined by the *[profiling_dump_dir](../../../code/console/index.md#profiling_dump_dir)* console variable (by default, a folder named `"profiling_dump"`), with a filename like `profiling_dump_<datetime>.profiler_dump`. You can provide an absolute or relative file path if you want to control the location/name. Recording will continue indefinitely until you call the stop function (or use the console command *[profiling_stop](../../../code/console/index.md#profiling_stop)*).
- ***[StartProfilerDump (int frames, string path)](../../../api/library/engine/class.profiler_cs.md#startProfilerDump_int_cstr_void)*** - starts recording a profiler dump for a fixed number of frames. The first argument frames specifies how many frames to capture. Recording will automatically stop after that many frames have been recorded (you can also stop manually earlier). The data is written to the specified file path (or to the default location if no path is given).
- ***[StartProfilerDump (float seconds, string path)](../../../api/library/engine/class.profiler_cs.md#startProfilerDump_float_cstr_void)*** - starts recording a profiler dump for a fixed duration in seconds. The seconds argument defines how long (in real time) to capture data. The Profiler will record all frames during that period and then stop automatically. As with other overloads, you can optionally specify an output file path or let it use the default.


### Using Console


If you are working in UNIGINE Editor or want to use the console in runtime, you can use built-in console commands to trigger the same functionality without writing code. The console commands correspond one-to-one with the Profiler API methods:


- *[profiling_start](../../../code/console/index.md#profiling_start)* [path]
- *[profiling_start_frames](../../../code/console/index.md#profiling_start_frames)* <frames> [path]
- *[profiling_start_seconds](../../../code/console/index.md#profiling_start_seconds)* <seconds> [path]


All these commands will produce a `.profiler_dump` file at the specified location. The console will confirm that profiling has started or stopped and print the file name where data was saved.


## Stopping Profiling Dumps


If you started a capture with a fixed frame count or duration, it will stop automatically once that limit is reached. However, if you started an open-ended capture, you must manually stop it:


- In your code, call ***[StopProfilerDump()](../../../api/library/engine/class.profiler_cs.md#stopProfilerDump_void)***
- In the console, use *[profiling_stop](../../../code/console/index.md#profiling_stop)*


> **Notice:** It's important to stop the capture properly, otherwise, the dump file may become corrupted. For example, if the application is closed while profiler data is being written, parameter values will be missing in the resulting file.


## Profiler Dump File Contents


The profiler dump file contains a large amount of data recorded from the engine during the session. The data inside a `.profiler_dump` file is stored in a binary compressed format to minimize disk space usage and reduce I/O overhead during recording.


During dump collection no additional memory is allocated, and all profiler data is written directly to disk, ensuring minimal impact on performance while recording.


Because of this binary format, the dump file cannot be viewed or edited itself. To access and interpret its contents, you need to use the [*Profiler Reader*](#reading) Tool or *[ProfilerDump](#reading)* API.


The profiler dump file structure consists of the following major sections:


1. **General System and Engine Information** Contains metadata about the environment in which the capture was made - including engine version, build revision, OS information, CPU and GPU details, and other system parameters.
2. **Console Variables** Stores a snapshot of all console variables and their values at the time of recording. Any changes made to these variables during the capture are also logged, including the frame numbers where the changes occurred. For example: ```text Console variable console_height: Int: 10 [150:12, 157:15] ``` This entry indicates that the *console_height* variable initially had the value 10 and was changed several times at the specified frames.
3. **Profiler Parameters (Metrics)** Contains all runtime metrics recorded from the Profiler during the capture session. These metrics correspond to the same counters you see in the real-time **[Profiler](../../../tools/profiling/profiler/index.md)**. For each metric, the dump provides a summary (minimum, maximum, average over the recorded frames) and the value of that metric for each frame recorded. > **Notice:** You can also add your own custom metrics, and he will be recorded in the profiler dump as well. See [*Profiler* class](../../../api/library/engine/class.profiler_cs.md#usage) usage example of how to register custom profiler metrics. Each metric is identified by a name (e.g., *"Frame Allocations", "GPU ram usage", "Total CPU"*, etc.) and might represent an integer or floating-point value. > **Notice:** The final profiler dump file **does not necessarily contain all metrics** that can be displayed in the [Profiler](../../../tools/profiling/profiler/index.md) window. Just like in the live Profiler, some metrics are only available when certain engine features or objects are active. For example, the metric *VRAM Terrain Cache* appears only if a Landscape object exists in the world during profiling. The profiler dump records per-frame metric values, capturing only those metrics that were active for each specific frame. As a result, the dump may include different sets of metrics depending on frame conditions. Several scenarios are possible:

  - **Metric never appeared during the entire recording** If a metric was inactive for the entire duration of the dump (e.g., the related feature was never enabled), it will not be included in the final dump file at all.
  - **Metric was active only for part of the recording** If a metric became active only for a portion of the captured frames, it will be recorded only for those frames where it was active. For the frames where it was not present, its values will be stored as **NaN** (not a number).


## Reading Profiler Dumps


Because the profiler dump is stored in a binary compressed format, it cannot be viewed directly. To interpret its contents, you need to use either the *[ProfilerDump](../../../api/library/engine/class.profilerdump_cs.md)* class API or the **[Profiler Reader](../../../tools/profiling/profiler_reader_tool/index.md)** Tool.


- The **Profiler Reader** Tool allows you to convert a profiler dump into a readable text format and view general information about the file. ![](profiler_reader.png)

  - See the **[Profiler Reader](../../../tools/profiling/profiler_reader_tool/index.md)** Tool article for more details.
- The **ProfilerDump** class flexible control over reading and processing dump data via code, allowing you to extract only the information you need. This example demonstrates how to load a `*.profiler_dump` file and print out the minimum, maximum, and average values of each parameter recorded. ```csharp ProfilerDump dump = new ProfilerDump(); dump.Load("path_to_your_profiler_dump_file"); for (int p = 0; p < dump.NumDumpParameters; p++) { string name = dump.GetDumpParameterName(p); var type = dump.GetDumpParameterType(p); if (type == ProfilerDump.DUMP_PARAMETER_TYPE.INT) { Log.Message( $"{name}: " + $"Min={dump.GetDumpParameterIntMin(p)}, " + $"Max={dump.GetDumpParameterIntMax(p)}, " + $"Avg={dump.GetDumpParameterIntAvg(p)}\n" ); } else { Log.Message( $"{name}: " + $"Min={dump.GetDumpParameterFloatMin(p)}, " + $"Max={dump.GetDumpParameterFloatMax(p)}, " + $"Avg={dump.GetDumpParameterFloatAvg(p)}\n" ); } } ```

  - See the **[ProfilerDump](../../../api/library/engine/class.profilerdump_cs.md)** class API for more details.
