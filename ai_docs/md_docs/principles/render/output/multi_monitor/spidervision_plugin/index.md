# Multi-Monitor & Projection Rendering With SpiderVision Plugin


The *SpiderVision* plugin allows creating various display and projection configurations including the following:


- **Projections and multi-projector setups** ![](../../appprojection/projection_setup.png)
- Configurable number of windows that can be arranged into **[multi-screen walls](../../../../../principles/render/output/multi_monitor/spidervision_plugin/presets.md#wall)** and **[CAVE systems](../../../../../principles/render/output/multi_monitor/spidervision_plugin/presets.md#cave)** | ![Four monitors in 2x2 configuration](../appwall/2x2.jpg) *2�2 configuration* | ![Four monitors in 4x1 configuration](../appwall/4x1.jpg) *4�1 configuration* | |---|---|
- [Syncker](../../../../../code/plugins/syncker/index.md) projections
- Multi-projector setups that are stored in the [EasyBlend](../../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#easyblend) calibration files created via Scalable Display Manager and set up via EasyBlend SDK


> **Warning:** *SpiderVision* currently doesn't support:
>
>
> - [Panoramic rendering](../../../../../principles/render/output/apppanorama/index.md)


The plugin provides:


- [Tools](../../../../../principles/render/output/multi_monitor/spidervision_plugin/projection_setup.md) for edge blending, non-linear image mapping, and color correction for each projection
- Full [customization](../../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md) of each viewport by using a required view frustum
- Compensation for display borders by setting a [custom offset](../../../../../principles/render/output/multi_monitor/spidervision_plugin/presets.md#wall) view frustum for monitors
- Unlimited number of monitors and projections (limited by performance only)


## Hardware and Software Requirements


- The plugin runs on *Windows* and *Linux* and supports *DirectX 12* and *Vulkan* graphic API.
- The supported version of *EasyBlend* is ***Scalable 7.0***.
- Microsoft Visual C++ 2008 Redistributable Package x64 is required.
- DPI scaling is not supported.
- This plugin cannot be used in a Qt-based application.


## Launching the Project with SpiderVision Plugin


1. Add the plugin to your project by configuring it in SDK Browser (*Configure -> Plugins -> SpiderVision*): ![](add_plugin.png)
2. Run the project runtime.
3. [Launch](#startup_commands) the plugin.
4. Open the plugin interface with a hotkey (*F10* by default, or as reconfigured via the config file).
5. Create and save a new configuration.The projection/display rendering is initiated after you load a configuration (select *File -> Load* in the *SpiderVision* setup window). The subsequent changes in the configuration will be applied on the fly. > **Notice:** You can import [configuration files from outdated plugins](../../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#migration) (*Projection* plugin, *Wall* plugin) to continue using them.
6. Now you can [configure viewports and projections](../../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#configure), adjust the projection [colors](../../../../../principles/render/output/multi_monitor/spidervision_plugin/projection_setup.md#color), [warping](../../../../../principles/render/output/multi_monitor/spidervision_plugin/projection_setup.md#warp), and other rendering features, as well as align the projected images using the [calibration grid](../../../../../principles/render/output/multi_monitor/spidervision_plugin/calibration.md).


### Start-Up Commands


To launch the application with the plugin via the command line, use the following:


```bash
main_x64.exe -extern_plugin UnigineSpiderVision
```


You can also use the [`plugin_load`](../../../../../code/console/index.md#plugin_load) console command in the runtime to initialize the plugin:


```bash
-extern_plugin UnigineSpiderVision
```


Then in the runtime console, use the `world_load` console command to run the project world, and press the *F10* hotkey to open the *SpiderVision* plugin interface.


## See Also


- [Set of samples](../../../../../sdk/api_samples/sim_cpp/spider_vision.md) demonstrating the possibilities of configuring the multi-monitor [SpiderVision setup](../../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md) parameters via code
- [*SpiderVision* Plugin API](../../../../../api/library/plugins/spidervision/index.md)
