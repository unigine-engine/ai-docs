# How to Count Seats and Channels


![](channels_0.gif)


The image demonstrates two types of arrangement. Simulation 1 requires only 1 VR Channel to run the application, and there's no network connection. A complex network of Simulations 2-4 and one PC with two monitors has 10 running PCs (instances of the application) in total, and therefore requires 10 channels. Considering the network connection available, these 10 are VR Channels.


## Counting Channels


Depending on your project's requirements and the final setup, your application may have several different views to render, such as:


- Out-the-window view for the cockpit having 4 windows each represented by a separate monitor
- Electro-Optical/Infra-red (EO/IR) sensor
- Radar
- Dashboard with simple gauges and instruments
- Rearview mirror
- Instructor Operator Station (IOS)


But how many channels is that?


Each runtime (instance of the released application) that *requires a separate computer* to render a certain view or a part of a view (in case of multi-monitor/multi-projector setup) **requires its own individual [Channel](../../sdk/licenses/index.md#channel)**. If you use the *[Wall](../../principles/render/output/multi_monitor/spidervision_plugin/presets.md)* preset of the *[SpiderVision Plugin](../../principles/render/output/multi_monitor/spidervision_plugin/index.md)*, then one instance is one PC, on which the application with this plugin is running (not the number of monitors used).


Simply put, we should define how many separate views we want to have. For example, a simple plane simulator with a three-screen out-the-cabin view, with a dashboard, radar, and an IOS (Instructor Operator Station) will be implemented by running 6 application instances. For a rear-view mirror or a simple additional camera producing a low-resolution image no additional channel is instance - that is implemented by an additional camera with a viewport. Thus, for such a setup we require 6 channels. And these channels should be IG Channels, as synchronization between them is required to render coherent images.


![](../../start/what_is_inside/input.jpg)


Of course, it is possible to combine several views and render them on a single PC, but only if the rendering load won't get too heavy (e.g. sensors and gauges displaying data rendered in low resolution or a rearview mirror rendered as a picture-in-picture). If rendering load becomes too high, a single computer might become unable to provide the required image at the required framerate, in this case the channel has to be split. **An attempt to save on additional channels may result in performance and quality degradation**, so please be aware that choosing an appropriate number of channels is essential for the successful implementation of your project. For example, if the truck simulator setup has four 4K monitors (two for the windshield and one for each side window) that'll end up with 16K pixels to be rendered, which might be too much for a single channel (a single PC with the *[Wall](../../principles/render/output/multi_monitor/spidervision_plugin/presets.md)* arrangement of displays used).


Decide on your setup, define what and how you plan to visualize - count all instances with significant rendering load (generation of high-resolution images for out-the-window views, high-resolution radar, and so on). Each of these instances should be rendered by a separate computer (otherwise too heavy load may lead to lags, which is totally unacceptable for a simulator).


### Summary


When counting channels keep in mind that:


| **1 Channel = 1 PC = 1 Instance** |
|---|


- If you run multiple instances on the same channel, only the last instance will operate.
- When multiple *[USB HASP](../../sdk/licenses/activation.md#usb)* keys are inserted into the same PC, only one key will be recognized.


Channels can be served to all machines on the delivery site from a single machine by the [Licensing Server](../../sdk/licenses/licensing_server.md#scenario_channels) � no per-machine activation is required.


## Counting Seats


[Seats](../../sdk/licenses/index.md#seat) are required for developers and can be compared with an office chair for simplicity: if two persons work in different shifts they can share the same workplace.


Some developers (such as artists) only need the Editor for work: they just assemble scenes and don't develop any logic. For such cases, there's **[Editor Seat](../../sdk/licenses/index.md#editor_seat)**, an option that allows working in the Editor.


To use both Developer Seats and Editor Seats, SDK Browser should be installed and running on the PC, and the corresponding version of SDK should be downloaded and [activated](../../sdk/licenses/activation.md).


![Select the SDK According to the License](dev_ed_seat.png)

*Selecting the SDK According to the License*


Thus, if you team has 1 artist and 3 programmers, one of which is working a night-shift, 2 Developer Seats and 1 Editor Seat might be enough for you.


### Testing the Application


On a certain development stage, you require to test your application with a final arrangement. If this is an application that is run using Channels, you may come up with the following arrangement:


Run the master instance using a Seat license (the PC should have SDK installed on it), and use Channel licenses for slaves (these PCs won't require installing SDK).


## Use Cases


Let us review some typical examples of simulator setups and count channels for them.


### Railway Simulator


A train driving simulator with high-resolution displays may have the following setup:


- Set of 3 monitors (1 for the windshield and 1 for each side window)
- Two rearview mirrors
- Dashboard


**Total:** 3 separate channels (one per window). Rearview mirrors can be rendered as picture-in-picture.


### Simple Helicopter Simulator


Simple CIGI-based single-user helicopter simulator with the following setup:


- Out-the-window view for the cockpit having 4 windows each represented by a separate monitor
- Electro-Optical/Infra-red (EO/IR) sensor
- Radar
- Dashboard with simple gauges and instruments
- Instructor Operator Station (IOS)


**Total:** 4 channels for windows, 1 for IOS, 1 for sensor, radar, and dashboard, with the need to exchange data via network, which totals to 6 IG Channels.


### VR Classroom


Let's review a VR classroom or some sort of a virtual laboratory with 10 independent computers, each having a VR headset connected. Each user has their own isolated simulation.


![](vr_class.jpg)


**Total:** each computer has an HMD, requiring a single VR visual channel per computer. So, we need **10 VR-channels** (as computers do not interact with each other via network).


> **Notice:** If you decide to implement network interaction between the users in the class, you'll have to replace all your VR Channels with IG Channels. The IG Channel is like an extended VR Channel with networking support.
