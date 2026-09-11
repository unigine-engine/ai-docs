# From Graph to Runtime


When you save an animation graph, it is not simply stored as node data - the graph is compiled into a native C++ library that is loaded at runtime. This compilation step is what makes animation graphs performant: instead of interpreting nodes every frame, precompiled machine code is executed.


![](compiling_progress.gif)


## What Is an AnimScript


An **AnimScript** is the runtime representation of a compiled animation graph. Each `*.agraph` file produces one **AnimScript** that is loaded as a dynamic library (`*.dll` on Windows, `*.so` on Linux). You assign an animation graph to a **NodeSkeletonPose**, and the resulting **AnimScript** drives the skeleton animation every frame.


![](node_skeleton_pose.png)

*NodeSkeletonPose withAnimScriptmode*


Through the related **[AnimScript](../../../api/library/animations/skeletal/class.animscript_cpp.md)** class, application code can set parameters, query state machine status, read root motion deltas, and more.


## Compilation Pipeline


When you save the graph in the [**Animation Graph Editor**](../../../content/animations/graph/index.md), the following steps happen automatically:


1. **Serialize** - the editor state is written to a `*.agraph` file on disk.
2. **Code generation** - the saved graph is converted into a C++ source file (`*.cppscript`) stored in the `data/.runtimes/` directory.
3. **Compilation** - the detected C++ compiler builds a dynamic library from the generated source. This runs asynchronously in a background thread.
4. **Hot reload** - once compilation succeeds, the old library is unloaded and the new one is loaded. All AnimScript instances are re-initialized, so you see changes immediately without restarting.


> **Warning:** If you are building the **Debug** version of the application in the IDE, make sure to launch the **Debug** version of the Editor. The same applies to **Release** versions - both must match for the animation script to work correctly.
>
>
> ![](../../../learn/11_fps/img/debug.png)


## Compiler Setup


Animation Graph requires a C++ compiler to build the runtime library. At startup, installed C++ compilers are detected automatically, and the first one found is selected. You can view detected compilers and switch between them using the [console commands](#diagnostics) listed below.


If no compiler is found, you will receive a notification. The solution depends on your operating system.


![](cpp_compiler_not_found_windows.png)


### Windows


On Windows, the **MSVC** compiler is used (installed with Visual Studio as part of the C++ workload). If no compiler is detected when you first save a graph, UnigineEditor offers to download and install **Visual Studio Build Tools** automatically.


![](cpp_compiler_required_windows.png)


### Linux


On Linux, **GCC** is used. If no compiler is detected, UnigineEditor will show the install command for your distribution (*apt*, *dnf*, or *pacman*) with a copy button.


![](cpp_compiler_required_linux.png)


## Build Errors


If errors occur during graph compilation, you will receive a red notification. Click it to open the Console and see the error details.


![](build_failed.png)


## Build Optimizations


Because each animation graph is compiled into a standalone native library, rebuilding it takes time. The build is optimized differently depending on where the graph runs, so that both cases get what matters most to them.


- **In Editor**, graphs are built in **preview** mode. Compiler optimizations are turned off and only the changed graph is recompiled, so rebuilds after an edit are fast. This keeps iteration quick while you work on the graph, at the cost of slower execution, which does not matter during editing.
- **In a built application**, graphs are compiled with full optimizations for the fastest possible execution at runtime. UnigineEditor and the application use separate libraries, so the unoptimized editor build never ends up in your game.


This is configured automatically: you do not need to set anything for the normal workflow. If you need to override the mode, for example to profile optimized scripts directly in the editor or to test a fast build in a running application, use the `anim_scripts_preview_build` console variable, or the equivalent [Animations](../../../api/library/animations/class.animations_cpp.md#isAnimScriptsPreviewBuild_int) class API.


## Console Commands and Variables


The following console tools are available for diagnosing compilation issues:


| -anim_scripts_rebuild |  |
|---|---|
| **Description:** - **Command.** Manually triggers a rebuild of the animation scripts library. Equivalent to [Animations::rebuildAnimScripts()](../../../api/library/animations/class.animations_cpp.md#rebuildAnimScripts_void). |  |
| -anim_scripts_rebuild_and_quit |  |
| **Description:** - **Command.** Rebuilds the animation scripts library and then quits the engine. Useful for automated (headless) rebuilds. |  |
| -anim_scripts_preview_build |  |
| **Description:** Enables preview build mode for animation scripts: the scripts are compiled without optimizations, which makes rebuilds faster at the cost of slower runtime execution. The editor enables this mode automatically for fast iteration, while a built application uses fully optimized scripts. Override it only for special cases, such as profiling optimized scripts in the editor or testing a fast build in a running application. The same setting is available via the AnimScript class API. | **Arguments:** **0** - disabled (by default) **1** - enabled |
| -anim_scripts_show_compilers |  |
| **Description:** - **Command.** Prints a list of all detected C++ compilers and marks the currently active one. Useful for diagnosing why animation graph compilation is not working. |  |
| -anim_scripts_compiler |  |
| **Description:** The index of the active C++ compiler used for building animation scripts. Automatically set to -1 when no compiler is detected. If multiple compilers are available, you can switch between them by setting this value. | **Arguments:** **[-1; 1]** - available range **-1** - by default |
| -anim_scripts_compiler_path | Config file: [*.boot](../../../code/configuration_file_cpp.md#boot) |
| **Description:** - **Variable.** Prints the current path to the custom compiler. - **Command.** Sets the path to a custom C++ compiler used for building animation graph scripts. Use this when the compiler is installed in a non-standard location and automatic detection does not find it. | **Arguments:** Path to a `*.bat` setup script (Windows) or `g++` binary (Linux). Relative paths are resolved against the `bin/` directory. |
| -anim_scripts_build_pdb |  |
| **Description:** Enables PDB generation for debugging animation graph scripts (Windows only). The first build with PDB succeeds, but subsequent rebuilds are blocked because the debugger holds the PDB file. To rebuild again, restart the application. | **Arguments:** **0** - disabled (by default) **1** - enabled |
