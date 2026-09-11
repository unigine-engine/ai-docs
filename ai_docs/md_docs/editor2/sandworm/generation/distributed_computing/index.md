# Distributed Generation and Headless Mode


Terrain generation is a complex task and may require substantial time depending on the area size and data resolution. *Sandworm* allows using distributed computing to generate terrain.


> **Notice:** Distributed computing makes sense when used for speeding up terrain generation that takes more than an hour. Applying distributed computing to generate a small terrain area with low-detail data (10 meters or more per pixel) may bring no benefit at all.


The **concept** is to use several computers united into a network, one of which is *Master* and assigns tasks, while the others are *Workers* that perform portions of work (processing of source data) assigned to them. UnigineEditor with the *Sandworm* tool and a terrain project should be open on *Master*, while *Workers* run the console application. **Source files (geodata) and common cache shall be stored in a shared folder.** If a *Worker* still has available resources, additional processes may be run on it and participate in terrain generation immediately, i.e., without restarting the generation process. *Master* creates the asset based on the result.


![](sandworm-distributed-generation.png)


> **Notice:** All workstations performing computations for a certain terrain generation task must be running on the same operating system (Windows or Linux). UNIGINE SDK version should also be the same.


Participants of the process:


| Master | Computer that manages the whole generation process, forms the task pool, and distributes tasks between *Workers*. *Master* tracks all connected *Workers* and assigns tasks to them. *Master* itself also performs calculations. *Master* is run via *Sandworm*. |
|---|---|
| Worker | Computer connected over the network to *Master* and performing specific tasks assigned by *Master*. *Worker* is enabled by running `bin/SandwormNode_x64.exe` (or `bin/SandwormNode_double_x64.exe` for a double-precision project � the precision must match the one used by *Master*). > **Notice:** The number of *Workers* connected to one *Master* is not limited (as long as the network bandwidth allows that). |


### Launching Order


> **Warning:** Before launching any of the network participants, disable [Microprofile](../../../../tools/profiling/microprofile/index_cpp.md) for it � in `\data\configs\default.user`, set:
>
>
> ```text
> <microprofile_enabled>0</microprofile_enabled>
>
> ```
>
>
> Otherwise, every instance would run *Microprofile*, causing memory waste.


You can launch *Master* and *Workers* in any sequence.


You can run additional *Workers* after the terrain generation process has started, and *Master* will distribute tasks for them.


One machine can have several *Workers* running. A *Worker* can have several processes (forks) that are activated via the menu on *Master*.


### See Also


Check this video from the series of [video tutorials on the terrain generation](../../../../videotutorials/essentials/sandworm.md) using Sandworm:


## Using Distributed Generation


Workflow:


1. **Prepare your environment**. Connect all computers to the network. It is recommended to use a network with at least **1 Gb** bandwidth. Otherwise, you may experience network lags (see the [Troubleshooting](#troubleshooting) section). Check that your network doesn't block broadcasting, otherwise distributed computation will be unavailable. > **Notice:** It is recommended to use an SSD drive to store the generation cache and output files. If an HDD is used, the generation performance is significantly lower due to multiple read/write and head positioning operations.
2. **On each *Worker* computer**, [run the *Worker* console application](#set_worker). > **Notice:** The versions of binary executable files must be the same on all computers.
3. **On the *Master* computer**:

  - Run [UnigineEditor](../../../../editor2/index.md) and open the ***Sandworm*** tool (*Tools -> Sandworm*).
  - Open the `*.sworm` asset you are going to generate and configure the [generation settings](../../../../editor2/sandworm/generation/index.md).
  - Toggle on the checkbox in the header of the *Distributed Generation* section of *Generation Settings* (the section is collapsed by default) and [specify the *Master*'s settings](#set_master). Save the project configuration.
  - Click the *Generate Object Landscape Terrain* (*Generate Object Terrain Global*) button. The window with the list of available *Workers* will open: ![Distributed Generation Window](distributed_generation_window.png) > **Notice:** If you regenerate the project, this window will appear after the warning on losing any manual modifications. As soon as this window is open, *Workers* start parsing the shared source data and generating cache. At the end of this process, the console message **Worker: Ready To Import** is displayed.
  - Clicking the right mouse button on a *Worker* makes the following options available: ![Worker Options](worker_options.png) *Worker Options* | Create�Fork | Creates one more process on the same *Worker*. Best PracticeWe estimate a reasonable number of forks as 4 to 6. Higher values reduce the *Worker*'s performance. | |---|---| | Shutdown | Removes the fork or *Worker* from the list. | | Clear�Cache | Clears the *Worker*'s local cache. | Set the number of forks you need and click *Generate*.
4. During the generation process, you can connect more *Workers*, if necessary: run the console application on a *Worker* (even if this *Worker* is already running one or several). This console application will automatically connect to *Master*, and *Master* will assign a process to this *Worker*.
5. When the terrain generation is completed, disable all *Worker* processes.


## Setting Up the Master


To set up *[Master](#master)*, toggle on the checkbox in the header of the *Distributed Generation* section of *Generation Settings*. The section is collapsed by default.


![](distributed_master_settings.png)


*Master* settings:


| Distributed Generation | The checkbox in the section header. If toggled on, distributed computing is enabled for the terrain generation, and the machine running the Editor with *Sandworm* is *Master*. |
|---|---|
| Broadcast Port | Port for listening to *Sandworm* by *Workers*. The default value is 7814, the range is 0 to 65535. |
| Server Port | Port used for information exchange. The default value is 7741, the range is 0 to 65535. |
| Workload on Master | Percentage of terrain generation performed by *Master*: 0 to 100, 100 by default. |


> **Notice:** All sources and project cache should be stored in a shared location accessible by both *Master* and all *Workers*. The path to this location should be identical on *Master* and *Workers*.


## Setting Up a Worker


> **Notice:** *Worker* should have the same version of OS and UNIGINE SDK as *Master*.


To set up a *[Worker](#worker)*:


1. [Create](../../../../sdk/projects/index_cpp.md#creation) a new UNIGINE project on a *Worker* computer with the corresponding project [feature](../../../../sdk/projects/index_cpp.md#general_settings) enabled: ![Enabling a Worker application](sandworm_headless_feature.png)
2. Run the `SandwormNode_x64.exe` console application stored in the `bin/` folder of your project, passing the command-line arguments you need: `--sw_local_cache_path <path>` sets where the local cache is stored, and `--sw_broadcast_port <port>` overrides the default broadcast port. The message that *Worker* is ready should appear in console: ![Worker is ready for generation](worker_is_ready.png)
3. *Worker* detects *Master* on the network, connects to it, downloads the scene, prepares all layers (checks their accessibility), and is ready for terrain generation.


![Worker application is running and ready for terrain generation](worker_prepared.png)

*Worker application is running and ready for terrain generation*


You can run multiple console applications on one machine and/or fork one *Worker* via *Master* to create more processes.


> **Notice:** - Operating System versions on *Master* and *Workers* should be identical.
> - The SDK version of the Editor run on *Master* should be the same as the version of the console app (including precision).
> - *Development/Release* version of SDK does not matter.


When the terrain generation is completed and you don't need *Workers* anymore, close the console application on *Workers* or shut down processes via *Master*.


## Generating Landscape in Headless Mode


A landscape created in *Sandworm* project can also be generated in the *Headless* mode, without running UNIGINE Editor.


To do that:


1. [Configure](../../../../sdk/projects/index_cpp.md#update_config) a UNIGINE project to enable the corresponding [feature](../../../../sdk/projects/index_cpp.md#general_settings): ![Enabling a Worker application](sandworm_headless_feature.png)
2. Create and configure a *Sandworm* project in the Editor, then close the Editor.
3. Execute the following command from the command line to start the generation process: ```bash PS D:\projects_location\unigine_project\bin> .\SandwormNode_double_x64.exe --sw_generate project_name.sworm ``` where `project_name.sworm` is your *Sandworm* project name as shown in the Editor.


The landscape is generated into the world that has been set as the [export world](../../../../editor2/sandworm/generation/output_dir_files/index.md#export_world) in the output settings. Any TMS sources used in the project are also downloaded before starting the generation process.


> **Warning:** The *Headless* mode doesn't work with distributed computing.


## Troubleshooting


- If the network latency is too large despite 1Gb bandwidth or higher, this can be caused by a 100 Mb or 10 Mb device connected to the network. Data exchange rate drops down to the maximum rate supported by such device, slowing down the generation speed.
- Check that your projects on *Master* and *Workers* use the same precision (*double* or *float*), the same engine versions, and the same GDAL versions, otherwise the *Workers* would display the **Different Builds** error.
- Use SSD to store shared source data and cache.
- Add the application to the [antivirus exclusions](../../../../troubleshooting/antivirus/index.md#exclusion), as it may reduce performance.
- Check that network ports used by *Master* and *Workers* are allowed by the firewall.
