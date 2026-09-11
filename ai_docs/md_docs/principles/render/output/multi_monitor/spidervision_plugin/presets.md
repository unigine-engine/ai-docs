# Multi-Monitor and Multi-Projection Presets


The plugin has presets that help to automatically create such configurations as *Wall* and *CAVE*.


| ![](display_wall.png) *Display Wall* | ![](cave_projection.png) *CAVE projection* |
|---|---|


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


## CAVE Preset


The *CAVE* (Cave Automatic Virtual Environment) generator creates a CAVE room made of *Display*-type viewports. The **left**, **back**, and **right** walls and the **bottom** (floor) are always created, while the **front** wall and the **top** (ceiling) are optional.


To open the *CAVE* generator, select *Generate -> CAVE* in the menu. The *Generate CAVE* window will open with the following parameters:


![](cave_generator_window.png)


| Name | Name of the group that is displayed in the left panel of the SpiderVision Setup window. |
|---|---|
| Center Offset | Offsets the center of the generated CAVE group relative to its default position. The value is set in meters. |
| Wall Size | Specifies the dimensions (width and height) of the generated CAVE walls. The value is set in meters. |
| Floor Size | Specifies the dimensions (width and depth) of the generated CAVE floor and ceiling. The value is set in meters. |
| Pixel Density | Specifies the pixel density that will be assigned to the generated CAVE group. The value is set in pixels per meter: the render texture size is calculated automatically from the physical screen dimensions and the specified pixel density, preserving the correct aspect ratio. |
| Window Size | Specifies the size of the generated application windows, in pixels. |
| Exclusive Fullscreen | Enables [exclusive fullscreen](../../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#window_mode) mode for all generated windows. If disabled, the windows are created in the *Borderless Windowed* mode. |
| Stereo | Specifies whether the generated viewports use *Mono* (single image) or *Stereo* (side-by-side stereo image) [rendering](../../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#render_mode). |
| Inverse | Generates viewports configured for rear-projection systems (the walls are flipped). Enable this option when the image is projected onto the back side of the screen. |
| Use Front Side | Adds the front wall when generating the CAVE. |
| Use Top Side | Adds the ceiling when generating the CAVE. |


Click *Generate* to create the group. All parameters, except *Use Front Side* and *Use Top Side*, may be reconfigured later as you select the *CAVE* group parent item in the viewports tab.


To synchronize the project and launch the application across the CAVE machines, use the [IG Control Panel](../../../../../ig/ig_control_panel.md) tool.
