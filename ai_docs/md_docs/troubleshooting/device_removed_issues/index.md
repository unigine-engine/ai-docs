# Device Removed Issues


While developing a UNIGINE application, you may encounter a **"Device removed"** error either in runtime or in the Editor.


![](fatal_error_image.png)

*Example of Device Removed error*


This typically means that the GPU driver has reset or stopped responding. In most cases, the root cause is not a single issue, but a combination of GPU load, system configuration, or project-specific problems.


The **"Device removed"** error is usually a symptom of instability, not a direct cause. It **may result from memory limits, driver behavior, or specific issues in your project**.


This article provides a [checklist](#checklist) that helps you quickly identify the source of the problem, apply common fixes, and [collect useful data for further debugging](#diagnostics).


If the issue persists, providing logs, reproduction steps, and system data will significantly speed up the investigation.


For convenience, the most common causes are also grouped into [categories](#reasons) below.


## Quick Fix Checklist


It is hard to detect what precisely caused the problem. Follow these steps in order - in many cases, one of them resolves the issue.


### 1. Update or roll back GPU driver


1. Open Device Manager -> Display adapters -> *Your GPU* -> Driver.
2. Install the latest driver from NVIDIA/AMD official website.
3. If the issue started after an update, roll back to the previous version.


### 2. Clear the project cache


1. Open your project folder.
2. Delete cache files in the `data` folder: ![](cache_files.png)
3. Restart the application or Editor.


### 3. Toggle hardware-accelerated GPU scheduling


1. Go to Settings -> System -> Display -> Graphics settings.
2. Open Default Graphics Settings.
3. Try toggling Hardware-accelerated GPU scheduling. ![](graphic_settings.png)
4. Also (advanced): Check Resizable BAR (ReBAR) in BIOS and try switching it ON/OFF. For more information contact your system administrator or start [here](https://www.intel.com/content/www/us/en/support/articles/000090831/graphics.html).


### 4. Temporarily disable multithreading


Disable [multithreading](../../code/console/index.md#render_multithreaded) (for testing). If the issue disappears, it may indicate a synchronization or threading-related problem.


### 5. Update Windows


1. Go to Settings -> Windows Update. ![](windows_update.png)
2. Install all pending updates.


### 6. Switch Graphics API


In [global options](../../sdk/index.md#options) or via [startup command line](../../code/command_line.md#video_app), switch between DirectX 12 and Vulkan.


### 7. Disable overlays and background apps


1. Open Task Manager -> Processes.
2. Close:

  - Discord overlay
  - Steam overlay
  - GeForce Experience
  - Screen recording tools


## Collecting Diagnostic Data


If the quick fixes did not help, collect additional diagnostic data before contacting support.


Depending on your setup and available tools, use one of the following methods.


### Basic Data Collection


Use this method first in most cases.


1. **Save the current logs.** Go to the project's `/bin` folder and copy: Create a separate empty folder somewhere on disk and save the copied logs there.

  - `log.txt` - if the crash happened in runtime;
  - `editor_log.txt` - if the crash happened in the Editor.
2. **Restart the application or Editor with extended rendering diagnostics.** Launch the application ([Development](../../sdk/projects/index_cpp.md#engine_build) build, the *Debug* option in the [Editor](../../sdk/projects/index_cpp.md#customize_edit)/[runtime](../../sdk/projects/index_cpp.md#custom_run) should be enabled) with the following startup command: ```text -video_debug 2 ``` This command enables rendering-related errors to be displayed in the console, though it may impact performance. If possible, [attach Visual Studio to the running process](https://learn.microsoft.com/en-us/visualstudio/debugger/attach-to-running-processes-with-the-visual-studio-debugger?view=visualstudio&pivots=programming-language-cpp):

  1. Open Visual Studio.
  2. Select *Debug -> Attach to Process*. ![](attach_to_process.png)
  3. Choose the application process. ![](attaching_process.png)
3. **Reproduce the issue.** Repeat the exact steps that previously led to the *"Device removed"* error. Try to keep the reproduction steps as consistent as possible. [![](error_vs.png)](error_vs.png)
4. **Save diagnostic output.** After reproducing the issue:

  - Save the Visual Studio Output window contents (you can simply copy the Output text into a `*.txt` file and place it in the diagnostic folder).
  - Save the updated `log.txt` or `editor_log.txt` in the same diagnostic folder. ![](log_files.png)


### Simplified DirectX 12 Diagnostics (Windows Only)


This method is simpler than the previous one and may be used as an additional step.


1. **Launch with crash dump collection enabled.** Launch the application ([Release or Development](../../sdk/projects/index_cpp.md#engine_build) build, the *Debug* option in the [Editor](../../sdk/projects/index_cpp.md#customize_edit)/[runtime](../../sdk/projects/index_cpp.md#custom_run) should be disabled) with the following startup command: ```text -video_debug_crash_dump 1 ``` This command enables reporting of [D3D12 Device Removed Extended Data (DRED)](https://microsoft.github.io/DirectX-Specs/d3d/DeviceRemovedExtendedData.html).
2. **Reproduce the issue.** Repeat the steps that led to the *"Device removed"* error.
3. **Save the error window.** When the error appears:

  - make a screenshot of the *"Device removed"* error window;
  - save the screenshot into a separate diagnostic folder.
4. **Save logs.** Copy `log.txt` or `editor_log.txt` from the `/bin` folder into the diagnostic folder.


### Extended NVIDIA Diagnostics


Use this method for deeper GPU crash analysis on NVIDIA hardware.


1. **Download NVIDIA Nsight Aftermath SDK.** Download the version [NVIDIA Nsight Aftermath 2025.1 SDK](https://developer.nvidia.com/nsight-aftermath-2025_1). > **Notice:** Only the 2025.1 version is supported, libraries from other versions may be incompatible.
2. **Add the Aftermath library to your project.** Place the `GFSDK_Aftermath_Lib.x64.dll` library from the downloaded SDK to the `bin` folder.
3. **Launch with crash dump collection enabled.** Launch the application ([Release or Development](../../sdk/projects/index_cpp.md#engine_build) build, the *Debug* option in the [Editor](../../sdk/projects/index_cpp.md#customize_edit)/[runtime](../../sdk/projects/index_cpp.md#custom_run) should be disabled) with the following startup command: ```text -video_debug_crash_dump 1 ```
4. **Reproduce the issue.** Repeat the steps that led to the *"Device removed"* error.
5. **Save diagnostic data.** Collect the following files: Save everything into a single folder before sending it to support.

  - Screenshot of the error window
  - `log.txt` or `editor_log.txt` from the `/bin` folder
  - The `gpu_crash_dump` folder from the `/bin` folder


### Extended AMD Diagnostics


Use this method for deeper GPU crash analysis on AMD GPUs.


1. **Download *[Radeon GPU Detective](https://gpuopen.com/radeon-gpu-detective/)*.**
2. **Configure Radeon Development Panel.**

  1. Launch Radeon Development Panel.
  2. Click Connect.
  3. Enable the required checkboxes according to the recommended configuration. ![](radeon_dev_panel.png)
3. **Reproduce the issue.** Repeat the steps that led to the *"Device removed"* error.
4. **Save the generated dump.** After reproduction:

  1. Right-click the dump entry in Radeon GPU Detective.
  2. Select Show in Explorer.
  3. Save both generated `*.rgd` and `*.txt` files.
  4. Compress them into an archive before sending to support.


## What Causes Device Removed


We analyzed the reasons that might cause this error and arranged them into the most common categories listed below.


### Memory And Performance Issues


| Typical signs: | - Crash in heavy scenes - Happens during loading or spikes - GPU usage is high before crash |
|---|---|
| What's happening: | The GPU runs out of VRAM or hits a performance spike, which causes the driver resets |
| Where to look: | - Task Manager -> Performance -> GPU - Profilers (Nsight, GPU-Z) |
| What to do: | - Lower the output resolution - Reduce graphics parameters - Consider [optimizing the scene](../../content/optimization/index.md) - Check [this article](../../troubleshooting/memory_issues/index.md) for more details |


### Broken Scene or Asset (*.world)


| Typical signs: | - Crash happens in one scene only - Started after adding something |
|---|---|
| What's happening: | A node, asset, or scene structure is invalid or corrupted |
| Where to look: | - UNIGINE Editor -> World Nodes - Recently added objects |
| What to do: | - Disable objects one by one - Reimport assets - Re-save `*.world` - Test in a clean scene |


### Shader Problems


| Typical signs: | - Crash after shader changes - Happens during rendering |
|---|---|
| What's happening: | GPU executes invalid shader code |
| Where to look: | - Custom shader files - Shader logs |
| What to do: | - Disable custom shaders - Check for: - infinite loops - invalid operations - unsupported instructions |


### Driver / OS Issues


| Typical signs: | - Started after update - Happens in multiple projects |
|---|---|
| What's happening: | Driver instability or OS-level issue |
| Where to look: | - Driver version (Device Manager) - Windows Update history |
| What to do: | - Update or roll back driver - Install OS updates |


### System Configuration Conflicts


| Typical signs: | - Crash on startup - API-dependent behavior |
|---|---|
| What's happening: | GPU features conflict with the engine |
| Where to look: | - Graphics API settings - Windows graphics settings - BIOS |
| What to do: | - Switch API (DX12 / Vulkan) - Toggle GPU scheduling - Toggle ReBAR |


### Third-Party Interference


| Typical signs: | - Random crashes - Hard to reproduce |
|---|---|
| What's happening: | Background apps interfere with GPU execution |
| Where to look: | - Task Manager -> Processes |
| What to do: | - Close overlays and GPU tools - Disable hardware acceleration in apps |
