# Syncker Plugin


*Syncker* is a multi-node rendering system that makes it easy to create an immersive system or a large-scale visualization wall on a computer cluster synchronized over the network in real-time.


> **Warning:** **THIS IS NOT A MULTIPLAYER SOLUTION!**
>
>
> To create a multiplayer application, currently a third-party solution should be used.


Simply connect multiple computers into one high-resolution seamless display using LAN. And it does not matter if these computers are running on Windows and Linux at the same time, as *Syncker* works even across different platforms. Moreover, created virtual environments can have any monitor configuration, since all viewports are fully configurable and multi-monitor grids on *Slave* computers are supported.


![Syncker](syncker.png)

*Computers in LAN connected viaSyncker*


Moreover, *Syncker* offers you a flexible customization of the whole synchronization process, based on **custom user messages**. Instead of sending the whole bunch of transformation data for objects that can only be rotated or sending huge amounts of transformation data for all parts of complex objects, when their positions can be determined using just a handful of simple parameters, you can send a single quaternion or a set of parameters.


### See Also


- The [Running *Syncker* for a custom project](../../../code/plugins/syncker/customize.md) article for more details on *Syncker* initialization and synchronization code.
- The [*Syncker*-specific options](../../../code/plugins/syncker/options.md) article for more details on *Syncker* command-line options and console commands.
- The article on [SpiderVision Plugin](../../../principles/render/output/multi_monitor/spidervision_plugin/index.md) for more details on the setup of multi-monitor *Slave* configurations.
- [Syncker](../../../sdk/demos/syncker.md) demo


**Syncker API:**


- The *[Manager](../../../api/library/plugins/syncker/class.syncker_manager_cpp.md)* interface article for more details on managing *Syncker* via code (C++, C#, UnigineScript).
- The *[Master](../../../api/library/plugins/syncker/class.syncker_master_cpp.md)* interface article for more details on managing *Syncker Master* via code (C++, C#, UnigineScript).
- The *[Slave](../../../api/library/plugins/syncker/class.syncker_slave_cpp.md)* interface article for more details on managing *Syncker Slave* via code (C++, C#, UnigineScript).


## Structure and Principles


*Syncker* allows you to render a world across different computers synchronized over LAN. These computers can be of two types:


| Master | *Master* application is an application running on the main computer. In addition to rendering, it also performs animations and calculations of physics, and controls *Slave* applications. > **Notice:** The main computer should have the most advanced hardware configuration, as it performs most calculations. - Nodes, materials, and cameras are created/deleted and moved according to the application logic. All other applications are synchronized with *Master*. |
|---|---|
| Slave | *Slave* applications are all other applications running on computers connected over the network. There can be an unlimited number of *Slave* applications connected to one *Master* (as long as the network bandwidth allows). The purpose of such applications is to render all nodes that are seen in their viewports. - All rendering is done directly on the *Slave* GPU. - Physics simulation is performed by *Master*. > **Notice:** Physics simulation in *Slave* applications should be disabled to improve performance. - Objects of the following types are synchronized automatically: *[ObjectWaterGlobal](../../../objects/objects/water/water_object.md), [ObjectCloudLayer](../../../objects/objects/cloud_layer/index.md), [ObjectParticles](../../../objects/effects/particles/index.md), [WorldLight](../../../objects/lights/world/index.md)*, if they are present in the `*.world` file on all computers. - Animations are updated on the *Master* computer, while *Slave* apps only get calculated bone transformations. - Particle systems are updated on *Slave* but according to parameters received from *Master*. - Physics simulation in *Slave* applications should be disabled not to override position and orientation of nodes sent over the network from a *Master*. Configuration of *Slave* is set up to fit the [configuration of monitors](#screen_configs). |


### Launching Order


The order of launching *Master* and *Slave* applications does not matter: you can launch several *Slave* apps, then *Master*, and then the remaining *Slave* apps � synchronization will start automatically. *Master* starts the session as soon as all *Slave* apps are connected.


In case only *Master* is present (`-sync_count1`) and connection of additional *Slave* applications on the fly is enabled (`-sync_allow_extra_slaves1`), the session starts immediately and lasts forever (until *Master* is on).


### Synchronization


*Syncker* works in **Asynchronous** mode providing synchronization between the channels by means of reconstruction using the data of previous frames. In asynchronous mode all computers draw their own frames, each with its own frame rate. So, in this mode we synchronize time.


In case there are a lot of *Slave* applications used, resulting in significant growth of the network load, it is recommended to try and reduce load by enabling *[broadcast](#addressing_broadcast)* or *[multicast](#addressing_multicast)* addressing modes. If changing the addressing mode does not solve the problem, you are recommended to adjust send rate, interpolation/extrapolation parameters.


UNIGINE *Syncker* uses **Interpolated Snapshots** (IS) to tackle the problem of lost packets between *Master* and *Slave*. It works by taking two old, but known positions and interpolating the object between them. It is accomplished by having a buffer of received positions and rotations, along with the time they represent. We usually take our current local time minus some predefined amount � **interpolation period** (40 ms by default), then go into our buffer, find the two indices that are just before and just after this time and interpolate.


If we don't have a received position and rotation for the time we're looking for, the **extrapolation** (guessing) is used. It also has a limited time � **extrapolation period** (200 ms by default). If the extrapolation period is over but there are still no packets received, all objects will freeze.


In most cases, this method provides a very accurate representation of the world to each *Slave*, as in general only already known positions of remote objects are rendered and in rare cases the system will try to extrapolate (guess) where an object is. This, however, comes at a cost, as we always render 40 ms (interpolation period) behind current time, so that new packets have time to arrive with data.


## Two-Way Communication


*Slave* is not silent, it can send messages to *Master*, it can even control *Master* as well as other *Slave* applications (e.g., run the profiler on all computers or shutdown all applications) by sending the `sync` command.


For sending and receiving messages between *Master* and *Slave*, *Syncker* uses a single UDP socket with the following five technologies:


- **Reliable** � guarantees packet delivery using the so-called acknowledge packets. When *Master* sends a message, *Slave* reports that the message is received. In case *Slave* does not reply in a certain period of time, *Master* tries to re-send the message.
- **Sequenced** � guarantees that all packets are received in the right order, finding all duplicates. Each packet has a number and until *Slave* receives the packet, *Master* shall not send next ones to it (with greater numbers).
- **Merged** � small messages are combined into a greater one instead of sending them all one right after the other (send a single 100-bytes packet rather than sending 10 packets 10-bytes each). This makes sending acknowledge packets to the sender simpler and faster.
- **Fragmented** � a large message exceeding the MTU size (*[Maximum Transmission Unit](https://en.wikipedia.org/wiki/Maximum_transmission_unit)*), shall be split into several packets having the MTU size. This ensures delivery of all packets protecting *Slave* from buffer overflow caused by a single large packet.
- **Compressed** � all messages are compressed using the LZ4 algorithm before sending. This reduced network load, but slightly increases the load on the computer itself.


![](sequences.png)


So, here's how the packets are delivered:


1. During the frame up to the *Data Sync Point*, *Master* prepares messages for sending and places them to a queue. This "big message" is compressed, split into parts according to the MTU size, wrapped into packets with the following three numbers specified for each of them: sequence number (packet group), fragment number, and total number of fragments in this sequence.
2. The packets are sent.
3. Upon receiving any of the packets, *Slave* changes the size of its sliding window in accordance with the number of fragments and adds the received fragment to this window.
4. In case of missing/lost packets, *Slave* adds the corresponding information on the missing part it requests to be sent again to the *acknowledge* packet dispatched to *Master*.


![](packets.png)


### Delivery Modes


Basically, you can use the following delivery modes for sending/receiving messages:


- **Reliable** � Reliable and sequenced mode, enabled by default. All packets shall be delivered to the recipient in the exact order they were sent.
- **Unreliable** � Pure *UDP*. Packets may be lost, duplicated, or received in an order that differs from the one they were sent. Packets are not compressed, fragmented, or merged. Everything is sent "as is". This mode is the fastest one as it requires no additional time for processing. You can use this mode for sending timestamped auxiliary data (e.g., for interpolation) having the size close to *MTU*. *Example*: sending 10 times a second positions of 10 aircrafts with the information on the current time, status of flaps, slats, ailerons, landing gears, etc.
- **Sequenced** � Packets may be lost, but never duplicated, they arrive in the exact order they were sent. This mode can be used for sending auxiliary data having the size close to *MTU*. *Example*: sending each frame positions of 10 aircrafts with the information on the status of flaps, slats, ailerons, landing gears, etc.


Multiple systems may use the *Syncker*'s network simultaneously (e.g. *IG* and a user's *App* application). For convenience, all messages are sent and received via named channels. If the specified channel does not exist, it shall be created.


### Addressing Modes


The following addressing modes for communication are available:


- [Unicast](#addressing_unicast)
- [Multicast](#addressing_multicast)
- [Broadcast](#addressing_broadcast)


Depending on your project's requirements, you can choose the one that fits best: ensures the lowest possible load, or provides additional features like easy testing on a single PC or communication between hosts from different subnets using different ports.

 Best Practice*Unicast* mode is recommended to be used during the development stage as the most flexible one, while *Multicast* and *Broadcast* are considered as options for production. *Broadcast* mode is the best option if the network consists of IG-hosts only.
| **Broadcast** |
|---|
| *Master* sends packets to all computers in the network. Messages are received by *Slave* computers as well as by all other computers which are irrelevant to the *Synker*. > **Notice:** All host computers must be in the same subnet and use the same port. **Advantages:** - Reduced load on the *Master* host (only one packet is to be sent instead of sending one separate copy of it to each *Slave*). - Simple setup (simply set the broadcasting mode for *Master* via `-sync_method broadcast`). **Disadvantages:** - Impossible to test on a single computer. - Messages are received to all computers in the network (even the ones irrelevant to the *Synker*) resulting in a significant load on a network, router, and computers themselves in case the network contains a lot of such computers. |
| **Unicast** |
| *Master* sends messages only to its *Slave* apps: a separate copy of the message is sent to each *Slave*. > **Notice:** All host computers can be in different subnets and use any ports (except for *Master*). **Advantages:** - Simple setup (works by default). - Computers can belong to different subnets (e.g. several computers from LAN plus several connected via WiFi). - Messages from *Master* are received only by its *Slave* apps. - Easy to test on a single computer. - No restrictions except for an exactly defined port for *Master*. **Disadvantages:** - Significant number of *Slave* apps increases load on the network segment between *Master* and router, as a separate copy must be sent to each *Slave*. > **Notice:** Switching to *Multicast/Broadcast* modes helps reducing the network load in case of a growing number of Slaves. As in these modes the load is almost unaffected, unlike *Unicast*, where the load is proportional to the number os Slaves. |
| **Multicast** |
| *Master* sends a message to a unique multicast address, and the router redirects this message only to the computers that "listen" to this address (have joined the *multicast* group). > **Notice:** All computers must use the same port. *Master* should know the multicast address, while *Slave* apps should be connected to the same *multicast* group. **Advantages:** - Lowest possible load on *Master* and network. - *Master* sends the message only once, *Slave* apps receive the copies of the same message. - Copies of the message are received by *Slave* PCs only, other PCs in the network don't receive them. **Disadvantages:** - More settings to be configured. - Router's default settings may result in blocking *Syncker* packets. You might need to change these settings to avoid it. - Impossible to test on a single computer. |


### Network Load


Summarizing the information from the table above as related to the network traffic load:


- The **Multicast** mode generates the minimum network traffic, as compared to other modes, thus creating the least load on the router and wi-fi.
- The **Broadcast** mode can be more consuming, because the packets are sent to all network PCs, including those that are not *Slave* (if any). If you don't have any other PCs in your network except for *Slave* ones, then the traffic amount will be the same as in the *Multicast* mode.
- The **Unicast** mode generates amount of network traffic that can be calculated as ***Multicast* * number of *Slave* PCs**.


To further optimize the traffic load, you can increase the time intervals for packets sending:


```cpp
	//On the Master
	master->setSendRate(15.0f); // send packets 15 times per second

	//Both on the Master and all Slaves
	syncker->setInterpolationPeriod(0.1f); // 100 ms delay

```


In this example, packets will be sent only 15 times per second, thus the lag will make 100 ms.


> **Notice:** To avoid visual jittering, the following condition must be fulfilled:
>
>
> **interpolation period > (1 / send rate)**


Consequently, reducing the lag (interpolation period) requires increasing the [send rate](../../../api/library/plugins/syncker/class.syncker_master_cpp.md#setSendRate_float_void), which will affect the network load:


```cpp
	//On the Master
	master->setSendRate(30.0f); // send packets 30 times per second

	//Both on the Master and all Slaves
	syncker->setInterpolationPeriod(0.05f); // 50 ms delay

```


## Multiple Cameras and Multi-Monitor Slaves


*Syncker* allows synchronizing views from multiple cameras. There are two types of cameras:


- **Main master camera** � a single camera that corresponds to the main viewer's position. The [screen configuration](#screen_configs) determines viewports relative to this camera. *Example:* a camera in the plane's cockpit, corresponding the pilot's point of view.
- **Auxiliary camera** � an additional camera (static or dynamic) that can be set anywhere in the scene. You can have as many cameras of this type as necessary. *Example:* a ground-based surveillance camera or a thermal imaging camera mounted on the plane's wing.


By default, the main master camera is used. You can create auxiliary cameras and specify their viewports to be displayed by selected *Slave* apps. Such cameras are synchronized automatically.


*Syncker* offers you an extreme flexibility of viewport configuration. You can use up to 6 monitors on a single *Slave*, each having it own viewport assigned. For this purpose, you should use the *[Wall](../../../principles/render/output/multi_monitor/spidervision_plugin/presets.md)* preset of the *[SpiderVision Plugin](../../../principles/render/output/multi_monitor/spidervision_plugin/index.md)*.


## Screen Configurations


To configure screens/projections, the [*SpiderVision* plugin](../../../principles/render/output/multi_monitor/spidervision_plugin/index.md) should be added to your project for both master and slaves. The order of plugins in the list matters � *SpiderVision* must be specified before *Syncker*:


```bash
-extern_plugin UnigineSpiderVision,UnigineSyncker

```


The setup window opens on pressing the *F10* button on any PC (master or slave) to configure the rendering of all viewports.


Screen configuration for *Syncker* has to meet the following requirements:


- Each display in the configuration should correspond to one of the monitors/projectors.
- Position and orientation of each display/projector must be relative to the [main master camera](#main_camera). The closer the monitor is to the viewer, the higher is the FOV value.


Two types of configuration can be used:


- A multi-monitor setup formed by displays, where each *Slave* renders its viewport on the corresponding monitor (or several monitors). > **Notice:** Projection and modelview matrices are automatically calculated on the basis of the viewer's position. The following picture shows the screen configuration for the multi-monitor setup, where each *Slave* renders its viewport to a single monitor. ![](syncker_multi_monitor.png) *Screen Configuration (the left picture) for Multi-Monitor Setup (the right picture)*
- A multi-projector setup formed by projectors, where each *Slave* renders its viewport via the corresponding projector. By default, the projectors display images as seen from the viewer's position. ![](syncker_projection.png) *Projector Configuration (the left picture) for Multi-Projector Setup (the right picture)* > **Notice:** Projection and modelview matrices are automatically calculated on the basis of the viewer's position.


## Syncker Pipeline


Basically *Syncker* has 4 states:


- **Wait for connections** � waiting until all *Slave* PCs are connected.
- **Starting...** � *MTU* calculation and startup synchronization of all hosts.
- **Session Started** � the session is started.
- **Session Finished** � the session is over, all *Slave* PCs are disconnected.


Let us consider *Syncker* running using broadcast addressing with *Master* and a single *Slave*:


1. After being launched, *Master* opens the port (`-sync_port`), and starts listening to it. *Syncker* status is switched to *"Wait for connections"*.
2. *Slave* gets the list of all available network adapters *(Wifi, Ethernet)*, finds a broadcast address for each of them, and periodically sends *connection request* packets (*[broadcast](#addressing_broadcast)* mode). The *Syncker* status is *"Wait for connections"*.
3. *Master* receives the connection request packet, registers *Slave* and sends a *connection response* packet (*[unicast](#addressing_unicast)* mode), where it indicates the currently loaded world. When all *Slave* PCs are connected, the *Syncker* status is switched to *"Starting..."* and *Master* sends projection settings to all of them.
4. As soon as *Slave* receives the confirmation from *Master* the status is switched to *"Starting..."* and starts loading the world from *Master*.
5. While the *Syncker* status remains *"Starting..."*, both *Master* and *Slave* are trying to find the maximum possible *MTU* value (currently limited to 1432 bytes).
6. Upon completion *Slave* sends a message to *Master* that it is ready to continue. After receiving such messages from all *Slave* PCs (and finding an *MTU* for each *Slave*), *Master* changes the status to *"Session Started"* notifying all hosts.
7. The session has started, everything is ready for work.


## Using Syncker


To **add the plugin to a new project**, start by [creating a project](../../../sdk/projects/index_cpp.md#creation) from a template. In the project creation dialog, open *Advanced Settings > Plugins*, enable the *Syncker* plugin, click *Add*, then select *Create New Project*.


![](add_plugin.png)


For **existing projects**, in the SDK Browser, open the *My Projects* tab, and click the three-dot menu on the project card. Select *Configure*, then click *Plugins*, enable the required plugin, click *Add*, and finish with *Configure Project*.


![](../../../sdk/projects/other_actions.png)


### Simple Synchronized Demonstration


Suppose, you have prepared a "static" project (meaning that no new objects are created in it and no existing ones are deleted or moved) with some cinematics. This corresponds to the majority of archviz projects or various types of demonstrations.


Suppose, you'd like to demonstrate this project using the *Wall* system. *Syncker* should do the job here, but there is nothing in your project about it, not a single line of code! Well, you don't need it, simply use a special system script that launches *Syncker*! That's all you should do, as the only thing moving during the cinematic sequence is the camera (which is synchronized automatically) with all other objects being static (no need to sync them).


This is the simplest mode, you don't have to know IP addresses or ports neither do you have to write any code. All you need to know is:


- Who shall be *Master*.
- What is the number of *Slave* PCs.


Then you simply do the following:


- Run the *Master* application substituting the [System Runtime Script](../../../code/fundamentals/execution_sequence/app_logic_system.md#scripts) with the special one (`core/systems/syncker/unigine.cpp`) and providing necessary startup [command-line options](../../../code/plugins/syncker/options.md) to define it as *Master* and set the total number of host computers: ```bash <your_app> -sync_init 1 -extern_plugin "UnigineSyncker" -sync_master 1 -sync_count 2 ``` `-sync_count` here sets the total number of computers (*Slave* PCs + *Master*). In this simplest case `-sync_count 2` � means a single *Master* and a single *Slave*.
- Run each *Slave* application using the same system script and indicating that the host is *Slave* (not *Master*): ```bash <your_app> -sync_init 1 -extern_plugin "UnigineSyncker" -sync_master 0 ```


That's it! Run *Master* and *Slave*(s) in any order (it doesn't matter). *Slave* shall automatically find *Master* in the network and connect to it.


### Basic Workflow


The basic workflow is as follows:


1. [**Implement *Syncker* logic for your *Master* and *Slave* applications**](../../../code/plugins/syncker/customize.md) (you can use the same application on both *Master* and *Slave* sides).
2. **Prepare your environment**. It is recommended to use a 100 Mb LAN. Otherwise, you may experience network lags (see [Troubleshooting](#troubleshooting) section). All applications you use must have access to all Unigine files and project data. So, you should copy your project to all computers. If some nodes are missing in the world file on a local computer, they will not be rendered.
3. **Run the *Master* application.** To run a *Master* application provide necessary startup [command-line options](../../../code/plugins/syncker/options.md), e.g.: ```bash <your_app> -extern_plugin UnigineSpiderVision,UnigineSyncker -sync_init 1 -sync_master 1 -computer_name <computer_name> -sync_count <number_of_hosts> ``` > **Notice:** The order of launching *Master* and *Slave* applications does not matter.
4. **Run a *Slave* application.** To run a *Slave* application provide necessary startup [command-line options](../../../code/plugins/syncker/options.md), e.g.: ```bash <your_app> -extern_plugin UnigineSpiderVision,UnigineSyncker -sync_init 1 -sync_master 0 -computer_name <computer_name> ``` If you want to configure projections and displays, you should use the *[SpiderVision](../../../principles/render/output/multi_monitor/spidervision_plugin/index.md)* plugin. > **Notice:** The order of plugins in the list matters: *SpiderVision* must be specified before *Syncker*.
5. **Set up [screen/projection configuration](../../../principles/render/output/multi_monitor/spidervision_plugin/index.md).** This step is performed when all *Syncker* hosts are successfully connected and working.


## Debug Window


Syncker's **debug window** enables you to monitor the hierarchy of objects at run time. The whole hierarchy means all objects (not only the ones registered in the Editor) including objects in cache, internal structure of [node references](../../../objects/nodes/reference/index.md), etc. When a node is selected, all necessary debug information is displayed. This information is updated each frame.


The **Search** option allows you to find any node by its name or ID (on *Master* or *Slave*), so a faulty node can be found quickly.


To open the debug window, run the `syncker_debug` console command from *Master* or *Slave* as follows:


```text
syncker_debug 1

```


The debug window can also be opened via the *System Menu*:


1. Open the *System Menu* by pressing *Esc*.
2. Enable the *Show debug window* option: ![](syncker_show_debug.jpg)


The debug window will open:


![](syncker_debug_window.jpg)

*Debug Window*


## Wireshark Plugin for Syncker


The Wireshark dissector plugin has been added for UNIGINE Syncker, making it easier to inspect and debug multi-display synchronization traffic.


The plugin decodes Syncker UDP packets directly in Wireshark, including connection setup, time synchronization, MTU checks, reliable transport data, and internal synchronization messages. It also supports fragment reassembly, LZ4 decompression, dynamic slave port detection, protocol version selection, and double-precision builds.


The plugin is **installed into Wireshark**, not into the UNIGINE or Syncker plugin directory. After installation, Wireshark automatically uses the dissector for captured Syncker traffic that matches the supported protocol format.


To use the Syncker Wireshark plugin:


1. Install Wireshark.
2. Copy the Syncker dissector plugin file (`<UNIGINE SDK>source\plugins\Unigine\Syncker\wireshark\syncker.lua`) to the Wireshark personal plugins folder. You can find the exact Wireshark plugin folder in *Help -> About Wireshark -> Folders -> Personal Plugins*. Typical plugin folders are:

  - Windows: %APPDATA%\Wireshark\plugins
  - Linux: ~/.local/lib/wireshark/plugins
3. Restart Wireshark.
4. Start capturing traffic on the network interface used by Syncker.
5. Run the Syncker-based application.
6. Inspect the decoded Syncker packets in Wireshark.


After Wireshark is restarted, the Syncker protocol data becomes available in the packet details view. The dissector can decode connection setup, time synchronization, MTU checks, reliable transport data, and internal synchronization messages.


In Wireshark, open *Preferences -> Protocols -> Syncker* to configure the Syncker dissector. The settings must match the Syncker configuration and the UNIGINE build used by the captured application:


![](syncker_settings.png)


| Protocol Version | UNIGINE protocol version used by the project. Select the version that matches the application generating the captured traffic. |
|---|---|
| UDP Port | UDP port used by Syncker. Packets sent to or from this port are automatically decoded as Syncker traffic. |
| Double Precision (UNIGINE_DOUBLE) | Toggle that specifies whether the captured application uses a double-precision UNIGINE build. |


## Troubleshooting


### Slave Cannot Connect to Master


The console shall look like this:


![](console_1.png)


*Slave* periodically sends broadcast messages when trying to find *Master* that responds, but there's no reply. Messages do not reach *Master*.


**Solutions:**


- Make sure that the port used by *Slave* for sending/receiving messages (*[Slave UDP port](../../../code/plugins/syncker/options.md#sync_slave_port)*) is not blocked by the firewall on *Master*. Try disabling firewalls on *Master* and all *Slave* PCs.
- Make sure that broadcast/multicast messages are not blocked by the router/switch. It is unlikely, but still possible.
- Try to explicitly specify *Master*'s IP address via the `sync_master_address` command, for example: ```text -sync_master_address 192.168.0.1 ``` In this case *Slave* shall skip the phase of searching for *Master* via broadcast messages and use [unicast mode](#addressing_unicast) for direct connection.
- Make sure that *Master* really waits for new connections. Check the sync_count value, is it greater than 1?


### Master Cannot Reply to Slave


In this case the console shall look like this:


![](console_2.png)


Connection requests from *Slave* were received by *Master*, the connection was opened and the session was started, but connection response did not reach *Slave*.


**Solutions:**


- Make sure that the port used by *Slave* for sending/receiving messages (*[Slave UDP port](../../../code/plugins/syncker/options.md#sync_slave_port)*) is not blocked by the firewall. Try disabling firewalls on *Master* and all *Slave* PCs.
- Make sure that *broadcast/multicast* messages are not blocked by the router/switch. It is unlikely, but still possible.
- Try using a unicast connection: ```text -sync_method unicast ```
- Check that the broadcast address found is valid, try setting up a broadcast channel for all hosts: ```text -sync_broadcast_address 255.255.255.255 ```
- Try setting another multicast address on the *Master* and *Slave* PCs via the `sync_multicast_address` command.
- Check IP/port of the *Slave* connected to *Master*. Is this the right *Slave*, or maybe there is another instance of *Slave* looking for *Master* on the same port? Try changing port number on *Master* and *Slave* (e.g., `-sync_port 25100`) and restart applications.


### Network Latency


If the network latency is too large despite 1Gb bandwidth or higher, it can be caused by a 100 Mb or 10 Mb device connected to a network. Data exchange rate will drop down to the maximum rate supported by such device, slowing down *Syncker* connection speed.


- Some 100 Mb or 10 Mb devices can have a working network interface when they are turned off.
- It is also possible that when turned off, 1 Gb devices have a network interface working at 100 Mb rate, which slows down connection in the LAN.


> **Warning:** *Syncker* is **not intended for use in Wi-Fi networks**, wired connections are required for stable operation.


Integration with the *[Microprofile](../../../tools/profiling/microprofile/index_cpp.md)* tool enables you to monitor performance, detect bottlenecks, and eliminate them.


#### Useful Tool


If you have a source SDK, you can use a simple and useful tool to monitor the network messages exchange speed. It is `server.usc` found in `source/tools/Interpreter/scripts/network/`.


### Problem Devices


Testing and operation revealed that the *Syncker* plugin may have issues when used with the following equipment:


- 3COM OfficeConnect Switch 5
- D-Link DES-1005D


If any issues arise, try switching to other equipment.
