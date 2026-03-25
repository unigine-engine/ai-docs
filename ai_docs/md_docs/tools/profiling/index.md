# Performance Profiling


While working on a project, you add code and models, and at some point your application starts lagging, you notice more and more glitches and spikes. At this stage it makes sense to identify what is the reason and apply a suitable recommendation to improve the performance.


UNIGINE provides the profiling tools to evaluate the framerate, find out if the problem is CPU-bound (code is unoptimized and takes too much time) or GPU-bound (image rendering is too heavy), and identify which steps take too much time.


- [Performance Profiler](../../tools/profiling/profiler/index.md) provides the overall performance data straight in the editor/application instance in a timeline.
- [Microprofile](../../tools/profiling/microprofile/index_cpp.md) displays more detailed data in a browser window for up to 1000 frames, for each thread, with a possibility to save this data.


Using these tools in the Editor may give you an overall understanding of the performance issues, and enabling the tools in runtime provides a more accurate estimation.


It is recommended to profile your project throughout the development cycle to detect and fix issues as early as possible.


## Profiling Workflow


1. **Enable the tool in runtime.** Enabling profilers in the editor is also possible and may be helpful for the content-related assessment. However, running the profiling tool in **runtime** provides a more reliable assessment.
2. **Define the target.** The most common optimization marker is that each frame should take no more than 16.66 ms, which means that your application aims to run at 60 frames per second (fps). Compare it with the current values.
3. **Detect the problem side: CPU or GPU.** [Performance Profiler](../../tools/profiling/profiler/index.md#generic) may give you an overall insight on the project performance and show which side, CPU or GPU, is more loaded with calculations and requires attention. [Microprofile](../../tools/profiling/microprofile/index_cpp.md) shows all kinds of detail on [CPU](../../tools/profiling/microprofile/index_cpp.md#cpu) and [GPU](../../tools/profiling/microprofile/index_cpp.md#gpu).
4. **Follow the recommendations.** Our documentation has a guidance on optimized usage of all objects.

  - If the issue is GPU-bound, [content optimizations](../../content/optimization/index.md) are required.
  - If the issue is CPU-bound, [add markers to code](../../tools/profiling/microprofile/index_cpp.md#app_logic_cpp) to make the details visible in Microprofile as well, and detect bottlenecks in your code.


Check out the Microprofile overview and use what's applicable for your project:


## Articles in This Section

- [Performance Profiler](../../tools/profiling/profiler/index.md)

- [Microprofile (CS)](../../tools/profiling/microprofile/index_cs.md)

- [Microprofile (CPP)](../../tools/profiling/microprofile/index_cpp.md)

- [Profiler Dump (CS)](../../tools/profiling/profiler_dump/index_cs.md)

- [Profiler Dump (CPP)](../../tools/profiling/profiler_dump/index_cpp.md)

- [Profiler Reader Tool](../../tools/profiling/profiler_reader_tool/index.md)
