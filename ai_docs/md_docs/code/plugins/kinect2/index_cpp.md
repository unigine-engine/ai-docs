# Kinect2 Plugin (CPP)


**Kinect 2.0** is a motion sensing input device that tracks the human body motions and translates this data to 3D worlds. The sensor detects joints therefore building a virtual 3D skeleton.


The *Kinect2* plugin is used for receiving already detected data from a *Kinect2* sensor. The plugin is provided as an add-on.


![](kinect_buffers.png)

*kinect_00Sample that showsKinectbuffers: color, depth, and IR range*


Minimum capabilities:


- 64-bit (x64) processor
- Physical dual-core 3.1 GHz (2 logical cores per physical) or faster processor
- USB 3.0 controller dedicated to the *Kinect* for Windows v2 sensor or the *Kinect* Adapter for Windows for use with the *Kinect* for *Xbox One* sensor
- 4 GB of RAM
- Graphics card that supports *DirectX 12* or *Vulkan*
- *Windows* 10/11
- Kinect SDK 2.0


### See Also


- *[Kinect Class (engine.kinect)](../../../api/library/plugins/engine.kinect_cpp.md)* functions
- Samples on the plugin usage:

  - shows all 3 buffers (color, depth, IR range)
  - shows all detected virtual skeletons
  - shows all detected faces


## Launching Kinect2 Plugin


To **add the plugin to a new project**, start by [creating a project](../../../sdk/projects/index_cpp.md#creation) from a template. In the project creation dialog, open *Advanced Settings > Plugins*, enable the *Kinect2* plugin, click *Add*, then select *Create New Project*.


![](add_plugin.png)


For **existing projects**, in the SDK Browser, open the *My Projects* tab, and click the three-dot menu on the project card. Select *Configure*, then click *Plugins*, enable the required plugin, click *Add*, and finish with *Configure Project*.


![](../../../sdk/projects/other_actions.png)


To use the plugin, you should perform the following:


- Specify the `extern_plugin` command line option on the application start-up: ```bash main_x64 -extern_plugin "UnigineKinect" ```


## Implementing Application Using Kinect2 Plugin


The plugin can receive the following types of data:


- Buffers: [color](../../../api/library/plugins/engine.kinect_cpp.md#STREAM_COLOR), [depth](../../../api/library/plugins/engine.kinect_cpp.md#STREAM_DEPTH), [IR range](../../../api/library/plugins/engine.kinect_cpp.md#STREAM_INFRARED).
- Virtual skeletons (up to 6 skeletons can be detected): position and orientation of bones in a 3D world, position of hands, accuracy of each bone detection.
- Faces (up to 6 faces can be detected): face [boundaries](../../../api/library/plugins/engine.kinect_cpp.md#getFaceBoundsInColorSpace_int_ivec4) and facial key [points](../../../api/library/plugins/engine.kinect_cpp.md#getFacePointInColorSpace_int_int_vec3) (eyes, mouth, nose) in coordinates of color and IR buffers, features (eye glasses, smile, closed eyes).


> **Notice:** When the plugin is loaded, the *[engine.kinect](../../../api/library/plugins/engine.kinect_cpp.md)* library with a bunch of functions is added to UnigineScript.


When implementing an application using the plugin, it is necessary to call the *[init()](../../../api/library/plugins/engine.kinect_cpp.md#init_uint_int)* function with the required arguments on engine initialization and the *[shutdown()](../../../api/library/plugins/engine.kinect_cpp.md#shutdown_void)* function on engine shutdown. For example:

```cpp
#ifdef HAS_KINECT

int init () {
	kinect::init(KINECT_STREAM_INFRARED | KINECT_STREAM_DEPTH | KINECT_STREAM_COLOR);
	return 1;
}

int update() {
	// update logic
	// here you can, for example, show the contents of the required buffers
	return 1;
}

void shutdown() {
	kinect::shutdown();
	return;
}

#else

int init() {
	Log::warning("No kinect plugin detected");
	return 1;
}

int shutdown() {
	return 1;
}

#endif

```
