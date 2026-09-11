# VRPN Client Plugin (CPP)


*[Virtual Reality Peripheral Network (VRPN)](http://www.cs.unc.edu/Research/vrpn/)* is a device-independent system for accessing virtual reality peripherals in VR applications. The *VRPN* system consists of programming interfaces for both the client application and the hardware drivers and a server application that communicates with the hardware devices. The *[DTrack](http://www.ar-tracking.com/home/)* application often goes as a server application.


The *Virtual Reality Peripheral Network (VRPN)* plugin represents the client application which is connected to the server and used for receiving input data from different input devices (joysticks, 3D motion and orientation tracking sensors and so on) via the Network.


For example, by using the *VRPN Client* plugin, you can implement an application that processes input data from *ART* controls.


### See Also


- *[VrpnAnalogDevice](../../../api/library/plugins/vrpn/vrpnanalogdevice.class_cpp.md)* class
- *[VrpnButtonDevice](../../../api/library/plugins/vrpn/vrpnbuttondevice.class_cpp.md)* class
- *[VrpnTackerDevice](../../../api/library/plugins/vrpn/vrpntrackerdevice.class_cpp.md)* class
- Samples on the plugin usage: > **Notice:** The samples are available if you add the *VRPN Client* plugin to your project via UNIGINE SDK Browser.

  - demonstrates receiving data from the *FlyStick* device and two sensors, tracking this device and a head. The data is presented as a text.
  - demonstrates receiving data from the virtual FlyStick device and two sensors, tracking this device and a head, inside the UNIGINE scene.


## Launching VRPN Client Plugin


To **add the plugin to a new project**, start by [creating a project](../../../sdk/projects/index_cpp.md#creation) from a template. In the project creation dialog, open *Advanced Settings > Plugins*, enable the *VRPN* plugin, click *Add*, then select *Create New Project*.


![](add_plugin.png)


For **existing projects**, in the SDK Browser, open the *My Projects* tab, and click the three-dot menu on the project card. Select *Configure*, then click *Plugins*, enable the required plugin, click *Add*, and finish with *Configure Project*.


![](../../../sdk/projects/other_actions.png)


> **Notice:** Before launching the plugin, you should run a server application (it is usually *DTrack*) that receives input data from an input device. The *VRPN Client* plugin will connect to this server and receive data from it.


To use the *VRPN Client* plugin, you should specify the `extern_plugin` command line option on the application start-up:


```bash
main_x64 -extern_plugin "UnigineVrpnClient"
```


## Implementing Application Using VRPN Client Plugin


When the *VRPN Client* plugin is loaded, the following classes are added to UnigineScript:


- *[VrpnAnalogDevice](../../../api/library/plugins/vrpn/vrpnanalogdevice.class_cpp.md)* that receives data about input devices sticks.
- *[VrpnButtonDevice](../../../api/library/plugins/vrpn/vrpnbuttondevice.class_cpp.md)* that receives data about input devices buttons states.
- *[VrpnTrackerDevice](../../../api/library/plugins/vrpn/vrpntrackerdevice.class_cpp.md)* that receives about position, orientation, velocity and acceleration of tracked objects from 3D tracking sensors.


> **Notice:** Each class can be instanced more than once.


When implementing an application using the plugin, instances of the classes listed above should be created on engine initialization.


> **Notice:** The server address and the device name should be passed to constructors of the UnigineScript classes (*VrpnAnalogDevice, VrpnButtonDevice, VrpnTrackerDevice*) as follows: *device_name@server_address*.


For example, if the VRPN server is set on the PC via the *DTrack* application, the following should be passed: *DTrack@localhost*. If the server is set on another PC, instead of the `localhost`, you should specify the PC's IP address. You should also call the *[update()](../../../api/library/plugins/vrpn/vrpnanalogdevice.class_cpp.md#update_void)* method for each initialized device on engine update.


```cpp
#ifdef HAS_VRPN_CLIENT

VrpnTrackerDevice tracker;
VrpnButtonDevice button;
VrpnAnalogDevice analog;

int init() {

	tracker = new VrpnTrackerDevice("DTrack@localhost");
	button = new VrpnButtonDevice("DTrack@localhost");
	analog = new VrpnAnalogDevice("DTrack@localhost");

	return 1;
}

int shutdown() {

	delete tracker;
	delete button;
	delete analog;

	return 1;
}

int update() {

	tracker->update();
	button->update();
	analog->update();

	return 1;
}

#else

int init() {
	Log::warning("No VRPN Client plugin detected\n");
	return 1;
}

int shutdown() {
	return 1;
}

#endif

```
