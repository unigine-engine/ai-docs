# 3-Monitor Output with Surround Plugin


*Surround* is designed to span the UNIGINE-based project across three monitors. It allows expanding the borders of the virtual world while keeping the full control over the rendered viewports.


> **Notice:** This plugin cannot be used in a Qt-based application.


## Hardware Requirements


Both hardware requirements should be met to launch *Surround*:


1. At least 3 video simultaneous outputs on a one video card or *NVIDIA SLI* system.
2. *AMD Radeon HD 6000* Series or *NVIDIA GeForce 600* Series GPU.


### See Also


- *[engine.surround](../../../../../api/library/plugins/engine.surround_cpp.md)* functions
- sample for additional details. To run the first sample from the *UNIGINE SDK Browser*, press the ***Surround plugin*** button on the *Plugin Samples* tab.


## Launching Surround


*Surround* can be rendered both in the windowed and in the full screen mode.


![Surround on three monitors](appsurround.png)

*Surroundoutput onto three monitors*


Launch the application together with a plugin library (`bin/plugins/Unigine/Surround/UnigineSurround_*`) with the usually required [start-up arguments](../../../../../code/command_line.md) (such as rendering API, window size, etc.).


```bash
main_x64 -extern_plugin UnigineSurround
```


You can use 64-bit debug or release versions of the library. (The engine automatically loads the appropriate version of the library depending on the specified main application.)


> **Notice:** It is not possible to use *Surround* with:
>
>
> - Multi-monitor plugins (*[SpiderVision](../../../../../principles/render/output/multi_monitor/spidervision_plugin/index.md)*)
> - [Panoramic rendering](../../../../../principles/render/output/apppanorama/index.md)
> - [Stereo 3D](../../../../../principles/render/output/stereo/index.md)


## Customizing Surround


*Surround* can be customized to support any custom viewing frustums (symmetric or asymmetric ones) when rendering onto three monitors.


> **Notice:** To prevent modifying camera settings from system script, specify the `-extern_define "PROJECTION_USER"` definition in the project's launcher.


### Surround Cameras


*Surround* has one **primary** viewport in the center, while all others are rendered as **auxiliary** ones. By default, the primary display is the UNIGINE engine viewport used for one-monitor configuration. It uses matrices of the *Player* used by the engine to view the scene. Other displays are arbitrary cameras with any perspective and facing whatever direction needed. Each display has its own modelview and projection matrices. Both the primary monitor and auxiliary ones can be enabled or disabled, if necessary.


- The central monitor is a primary one. Two side monitors are auxiliary monitors that can be arbitrary cameras with any perspective and facing whatever direction needed.
- Each display, including the primary one, has its own modelview and projection matrices.
- By default, only a primary one has an interface (render system GUI, editor widgets, wireframe, or the profiler). However, separate [GUIs](../../../../../api/library/plugins/engine.surround_cpp.md#engine.surround.getGui_void) can be drawn on all monitors.
- All viewports have their own [viewport](../../../../../principles/bit_masking/index.md#viewport) and *Reflection* mask to selectively render nodes and reflections from them.


### How to Customize Cameras Configuration


Just like in case with *Wall*, rendering of *Surround* viewports is controlled by the `wall.h` script (found in `<UnigineSDK>/data/core/scripts/system`).


To implement a custom camera configuration, comment `wall.h` out in the `unigine.usc` system script and wrap your custom code around with `#ifdef HAS_SURROUND ... #endif` in the *render()* function of the system script:


```cpp
int render() {
	#ifdef HAS_SURROUND
		// place an implementation of a
		// custom camera configuration here
		// ...
	#endif
	return 1;
}

```


There are two possible setups depending on how the central monitor is rendered. It can be drawn by:


- The default engine [renderer](../../../../../api/library/rendering/class.render_cpp.md) (the same as when a usual one-monitor application is rendered).
- The *Surround* renderer itself (which is safer if you are going to use asymmetric frustum for the central monitor and modify its modelview matrix).


> **Notice:** Only one of two renderers should be enabled at the same time.


The following example demonstrates how to tweak cameras configuration and choose the renderer for the central monitor.


#### 1. Using default engine renderer


The first variant is to render the central (primary) monitor by the default engine renderer.


1. Enable two side (auxiliary) monitors via *[engine.surround.setEnabled()](../../../../../api/library/plugins/engine.surround_cpp.md#engine.surround.setEnabled_void)*. All *Surround* monitors are disabled by default. The central one should be disabled, as it is drawn by the default engine renderer. ```cpp // Enable the 1-st and the 3-rd monitors. // The third argument of the function sets the "enabled" flag. engine.surround.setEnabled(0,1); engine.surround.setEnabled(2,1); ```
2. Set projection and modelview matrices for side monitors via *[engine.surround.setProjection()](../../../../../api/library/plugins/engine.surround_cpp.md#engine.surround.setProjection_void)* and *[engine.surround.setModelview()](../../../../../api/library/plugins/engine.surround_cpp.md#engine.surround.setModelview_void)*. ```cpp // Settings for the 1-st monitor engine.surround.setProjection(0,projection_0); engine.surround.setModelview(0,modelview_0); // Settings for the 3-rd monitor engine.surround.setProjection(2,projection_1); engine.surround.setModelview(2,modelview_1); ```


#### 2. Using Surround renderer


Another variant is to render the central monitor by the *Surround* renderer. This variant can be used, for example, if you want to set up symmetric frustums for all monitors.


1. Disable rendering into the default UNIGINE viewport via *[engine.render.setEnabled()](../../../../../api/library/rendering/class.render_cpp.md#setEnabled_int_void)*: ```cpp engine.render.setEnabled(0); ```
2. Enable all three *Surround* monitors including the primary one. As a result, all three viewports will be rendered by *Surround* renderer itself: ```cpp // Enable all three monitors: engine.surround.setEnabled(0,1); engine.surround.setEnabled(1,1); engine.surround.setEnabled(2,1); ```
3. Set modelview and projection matrices for all three monitors. ```cpp // Settings for the 1-st monitor engine.surround.setProjection(0,projection_0); engine.surround.setModelview(0,modelview_0); // Settings for the 2-nd (primary) monitor engine.surround.setProjection(1,projection_1); engine.surround.setModelview(1,modelview_1); // Settings for the 3-rd monitor engine.surround.setProjection(2,projection_2); engine.surround.setModelview(2,modelview_2); ```
