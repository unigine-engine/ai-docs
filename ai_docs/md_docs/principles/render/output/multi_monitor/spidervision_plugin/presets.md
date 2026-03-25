# Multi-Monitor and Multi-Projection Presets


The plugin has presets that help to automatically create the *Wall* configuration of displays.


## Wall Preset


The *Wall* generator is designed to configure rendering the UNIGINE world into the configurable number of windows. They can fit any display configuration and can be rendered both in the windowed and the full screen mode.


The *Wall* preset is useful to generate a multi-monitor setup of viewports formed as an array.


To open the *Wall* generator select *Generate -> Wall* in the menu:


![](open_wall_generator.png)


The following window will open:


![](wall_generator_window.png)


Configurable settings are available depending on the viewport type.


| Name | Name of the group that is displayed in the left panel of the SpiderVision Setup window. |
|---|---|
| Size | Number of rows and columns in the wall grid. |
| Type | Image [type](../../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#render_type) rendered in the viewport. |
| Offset | Vertical and horizontal distance between edges of neighboring viewports, in meters. This value represents a distance between matrices of neighboring monitors, from the edge of one screen to the edge of the other screen. |
| Display Size | Physical size of each display in the group. The value is set in meters (for *Display* image type). |
| Distance To Viewer | Distance between the viewer and the center of the wall grid, in meters (for *Display* image type). |
| Aspect | Width-to-height ratio of the projected image (for *Projector* image type). |
| Vertical FOV | Vertical field of view, in degrees (for *Projector* image type). |
| Offset | Offset of the projected image relative to the viewer (for *Display* image type). The value is set in meters. |
| Angle | External angle between two neighboring columns of displays, in degrees. ![](wall_angle_30.png) *Wall Angle set to 30* |
| Window Size | Window size of each viewport in the group, in pixels. |
| Auto Arrange | Automatic positioning of windows on the displays. If disabled, all windows are created with the position (0, 0) at the same place and are to be positioned manually. |


All these settings, except *Size*, may be reconfigured later as you select the *Wall* group parent item in the viewports tab.


You can **ungroup** the *Wall* group: select the root item and press the **U** hotkey. After the *Wall* is ungrouped, you can modify each viewport individually. **Ctrl + Z** undoes all changes and restores the *Wall* group.


![](hotkey_u.gif)
