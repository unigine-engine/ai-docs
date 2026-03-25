# CIGI Demo

> **Warning:** The functionality described in this article is not available in the Community SDK edition.
> You should upgrade to [**Sim**](https://l.unigine.com/SdhugY462) SDK edition to use it.


*CIGI* demo showcases the use of UNIGINE-based application as an *[Image Generator (IG)](../../ig/index.md)* that interacts with a host via the CIGI protocol (versions 3.0, 3.1, 3.2, and 3.3 are supported).


This demo also contains *[IG Host](../../ig/ig_host.md)* — a cross-platform host emulator that can be used for debugging. Currently it supports the CIGI protocol only.


*IG Host* can be [used](../../ig/ig_host.md#run_project_with_host) with any *UNIGINE IG* project.


![](cigi_001.png)


*CIGI demo* is run out of the box with [IG Host](../../ig/ig_host.md), no additional arrangement is required.


If you want to use HEMU with this demo, do the following:


- Download and install *CIGI Host Emulator* from [here](http://cigi.sourceforge.net/product_he.php).
- Copy all files from the `<CIGI_Demo_Root_Directory>/cigi_host_configuration` directory to the `<CIGI_Host_Emulator_Installation_Directory>/Default` directory. > **Notice:** You can open the root directory of the demo in SDK Browser by going to *Samples -> Demos -> CIGI*, and clicking **Open**.
- Launch *CIGI Host Emulator*.
- Launch *CIGI demo* and specify necessary configuration settings in the dialog window that appears.


## Features


- Cross-platform host emulator that can be used for debugging
- Entity creation/deletion and control
- Control over articulated parts of the entity
- *View/Viewgroup* control via *View Definition/Control* packets
- Changing the time of the day via *Celestial Sphere Control* packets
- Changing the weather conditions via *Weather Control* packets
- *HAT/HOT* request packets


## See Also


- [Quick start with IG Template for a flight simulator](https://youtu.be/aYR_ApIBuCI?t=478)


## Accessing Demo Source Code

You can study and modify the source code of this demo to create your own projects. To access the source code do the following:

1. Find the **CIGI Demo** demo in the *Demos* section and click **[Install](/sdk/#samples)** (if you haven't installed it yet).
2. After successful installation the demo will appear in the *Installed* section, and you can click **Copy as Project** to create a project based on this demo. ![](../../sdk/demos/copy_as_project_gen.png)
3. In the **Create New Project** window, that opens, enter the name for your new project in the corresponding field and click **Create New Project**. ![](../../sdk/projects/create_project_cpp.png)
4. Now you can click **Open Code IDE** to check and modify source code in your default IDE, or click **Open Editor** to open the project in the [UnigineEditor](/editor2/). ![](../../sdk/projects/edit_code.png)
