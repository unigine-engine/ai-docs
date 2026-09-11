# Licensing and License Types


In UNIGINE, licenses are available for the use of Engineering and Sim SDK editions to develop an application, and in some cases � to use instances of created applications.


To have a clear understanding of license products in UNIGINE, we need to adopt the following notions:


| [Seat](#seat) | Major version used by developers to create a new project, write code, add content in the Editor, compile and build the project, run debug and release versions, i.e. the full application programming cycle. |
|---|---|
| [Editor Seat](#editor_seat) | Stripped-down version that allows only **running an already created project in the Editor**. It is designed for artists, who don't work with code and only create scenes in the Editor � add 3D models and configure them, set the environment, shadows, reflections, etc. |
| [Channel](#channel) | Permission to **run one instance of a final application** (a finished product that doesn't require running any developer tools). Channels are required for applications that use networking, IG, VR, or any multi-window implementation. Regular desktop applications that don't use any additional features do not require a channel for running. |


## Seat


A Seat is a type of license required for developers to run an SDK (Software Development Kit), in which the development process takes place. This is a major version used by developers to create a new project, write code, add content in the Editor, compile and build the project, run debug and release versions, i.e. the full application programming cycle. Seats are used by programmers and artists to create a project, add code and content, and run a development/test version. It makes sense to buy Seats based on the number of developers simultaneously working on the project.


To install SDK to be used with the Seat license, see [this guide](../../sdk/index.md#install_sdk).


To activate the Seat license, see [this article](../../sdk/licenses/index.md).


Instead of per-machine activation, Seat licenses can also be served to your whole local network from a single machine by the [Licensing Server](../../sdk/licenses/licensing_server.md).


## Editor Seat


Editor Seat allows only working in Editor with already existing projects. You cannot create a new project with this type of license � you can only modify an already existing project. This type of license is designed for artists who won't perform any programming and debugging, but just modify a project in Editor (add or delete 3D models, configure light and use other options available in Editor).


Installation and activation instructions for the *Editor Seat* are provided here:


- [How to Install and Activate Editor For Sim](../../sdk/licenses/editor_for_sim.md)


After you have activated the Editor Seat, run the editor launching file in an already existing project (keep in mind that you won't be able to create any new project with this type of license).


When we say **an already existing project**, we mean a project that has been created using a [Seat](#seat). You might have created it earlier having a full-fledged license or downloaded it from a repository using a VSC, or in some other way.


By the **editor launching file** we imply a script commonly available in the project folder, such as `launch_editor.bat` or `launch_editor.py`. Sometimes, there are no such files in the project folders or they are named differently. In any case, the project folder should contain `project_folder/bin/Editor_x64.exe` or `project_folder/bin/Editor_double_x64.exe` that you'll be able to run and work uninterrupted using this type of license.


## Channels


Channels are required to run a final application: one (1) Channel for one (1) PC. Channels differ depending on the plugins used:


- **IG channel** is a fully-featured license that is suitable for applications using networking (CIGI/HLA/DIS/Syncker) or high-level IG (Image Generator) system available in the SDK. It can also be used to run a VR app.
- **VR channel** is a license suitable for applications using any head-mounted display (VR headset). It can't use any networking or IG tools available in UNIGINE SDK.


The table below lists the plugins available in the base configuration of Sim Per-Channel SDK Edition and the plugins that require either VR or IG Channel.


| Base (no channel required) | VR Channel | IG Channel |
|---|---|---|
|  | **Base** plugins | **Base + VR** plugins and modes |
| *[CadImporter](../../code/plugins/cadimporter/index.md) [FbxImporter](../../code/plugins/fbximporter/index.md) [FbxExporter](../../principles/export_system/index.md) [UsdExchanger](../../code/plugins/usdexporter/index.md) GLTFImporter [GPUMonitor](../../code/plugins/gpumonitor/index.md) [VCS Integration](../../editor2/assets_workflow/version_control/vcs_plugin/index.md) [Steam](../../api/library/plugins/steam/index.md) [WebStream](../../code/plugins/webstream/index.md) [FMOD](../../code/plugins/fmod/index.md)* | *[VR Mode: OpenVR](../../vr_development/index.md#backend_openvr) [VR Mode: OpenXR](../../vr_development/index.md#backend_openxr) [VR Mode: Varjo](../../vr_development/index.md#backend_varjo) [Ultraleap](../../code/plugins/ultraleap/index_cpp.md) [Kinect](../../code/plugins/kinect2/index_cpp.md) [ARTTracker](../../code/plugins/arttrack/index.md) [VrpnClient](../../code/plugins/vrpn/index_cpp.md)* | *[Separate](../../principles/render/output/stereo/appseparate/index.md) [Surround](../../principles/render/output/multi_monitor/appsurround/index.md) [Syncker](../../code/plugins/syncker/index.md) [IG](../../api/library/plugins/ig/api/index.md) [CIGIConnector](../../api/library/plugins/ig/cigi/index.md) [DISConnector](../../api/library/plugins/ig/dis/index.md) [HLAConnector](../../api/library/plugins/ig/hla/index.md) [SpiderVision](../../principles/render/output/multi_monitor/spidervision_plugin/index.md) [Geodetics](../../code/plugins/geodetics/index_cpp.md)* |


> **Notice:** - All per-channel licenses purchased prior to UNIGINE 2.12 shall be treated as IG Channels.


**Each instance of a UNIGINE-application [requires its own license](../../sdk/licenses/channels.md#channel_summary) to run.** Whether you plan to run 10 instances of the same UNIGINE-app on 10 different PCs, or operate a distributed simulation system with 10 UNIGINE-apps (same or different), each running on a separate PC - you will need 10 licenses.


See [here](../../sdk/licenses/activation.md#usb) how to activate the Per-Channel license.


Channels can also be served to all machines on the site from a single machine by the [Licensing Server](../../sdk/licenses/licensing_server.md) � no per-machine activation or Internet connection is required on the machines running the application.


## Third-Party Components


You may not use the UNIGINE SDK (including any of its components as part of a final application), nor permit its use, in combination with Third-Party Components distributed under terms that directly or indirectly require the UNIGINE SDK to be licensed under terms different from those of your license.


In particular, you may not use the UNIGINE SDK in combination with components licensed under:


- the GNU General Public License (GPL);
- the GNU Lesser General Public License (LGPL), except where used solely through dynamic linking to a shared library;
- the Creative Commons Attribution-ShareAlike license (CC BY-SA).


For the purposes of this clause, "Third-Party Components" means software (including libraries) and other intellectual property created by third parties.
