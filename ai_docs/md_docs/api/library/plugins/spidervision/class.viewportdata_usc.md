# Unigine::Plugins::SpiderVision::ViewportData Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


The object of this class stores all data on the viewport: transformations, viewport type settings, physical size of the display, VFOV, aspect, vertical and horizontal offsets, warping effect details, etc.


This object is accessible via the corresponding methods of the [DisplaysConfig](../../../../api/library/plugins/spidervision/class.displaysconfig_usc.md#getViewportByIndex_int_ViewportData) class.


The mask data are stored in the [configuration file](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#config_file).


## ViewportData Class

### Members

## int getID () const

Returns the current viewport ID.
### Return value

Current viewport ID.
## void setName ( String name )

Sets a new [viewport name](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#viewport_name).
### Arguments

- *String* **name** - The viewport name.

## String getName () const

Returns the current [viewport name](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#viewport_name).
### Return value

Current viewport name.
## void setComputerName ( String name )

Sets a new [name of the computer](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#computer_name), on which this viewport is to be rendered.
### Arguments

- *String* **name** - The name of the computer, on which this viewport is to be rendered. If not set, the viewport is rendered on any PC.

## String getComputerName () const

Returns the current [name of the computer](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#computer_name), on which this viewport is to be rendered.
### Return value

Current name of the computer, on which this viewport is to be rendered. If not set, the viewport is rendered on any PC.
## void setDisplayIndex ( int index )

Sets a new [display index](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#display_index).
### Arguments

- *int* **index** - The display index.

## int getDisplayIndex () const

Returns the current [display index](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#display_index).
### Return value

Current display index.
## void setWindowSize ( ivec2 size )

Sets a new [size of the window](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#window_size), if it is in the [Window mode](#WINDOW_MODE_WINDOWED).
### Arguments

- *ivec2* **size** - The window size.

## ivec2 getWindowSize () const

Returns the current [size of the window](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#window_size), if it is in the [Window mode](#WINDOW_MODE_WINDOWED).
### Return value

Current window size.
## void setWindowPosition ( ivec2 position )

Sets a new [window position](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#window_position) on the screen.
### Arguments

- *ivec2* **position** - The coordinates of the top left corner of the window on the screen.

## ivec2 getWindowPosition () const

Returns the current [window position](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#window_position) on the screen.
### Return value

Current coordinates of the top left corner of the window on the screen.
## void setWindowMode ( int mode )

Sets a new [window mode](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#window_mode) for the rendered viewport: fullscreen imitation (frameless window adapted to the full window area) or window.
### Arguments

- *int* **mode** - The window mode for the rendered viewport.

## int getWindowMode () const

Returns the current [window mode](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#window_mode) for the rendered viewport: fullscreen imitation (frameless window adapted to the full window area) or window.
### Return value

Current window mode for the rendered viewport.
## void setProjectionEnabled ( int enabled )

Sets a new value indicating if the [projection rendering](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#projection_enabled) in viewport is enabled.
### Arguments

- *int* **enabled** - The projection rendering

## int isProjectionEnabled () const

Returns the current value indicating if the [projection rendering](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#projection_enabled) in viewport is enabled.
### Return value

Current projection rendering
## void setPosition ( vec3 position )

Sets a new [viewport position](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#transform_position) relative to the viewpoint in the setup.
### Arguments

- *vec3* **position** - The viewport position relative to the viewpoint in the setup.

## vec3 getPosition () const

Returns the current [viewport position](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#transform_position) relative to the viewpoint in the setup.
### Return value

Current viewport position relative to the viewpoint in the setup.
## void setRotation ( vec3 rotation )

Sets a new [viewport rotation](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#transform_rotation) relative to its own center in the setup.
### Arguments

- *vec3* **rotation** - The viewport rotation relative to its own center in the setup.

## vec3 getRotation () const

Returns the current [viewport rotation](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#transform_rotation) relative to its own center in the setup.
### Return value

Current viewport rotation relative to its own center in the setup.
## void setOffset ( vec2 offset )

Sets a new offset of the FOV.
### Arguments

- *vec2* **offset** - The FOV offset.

## vec2 getOffset () const

Returns the current offset of the FOV.
### Return value

Current FOV offset.
## void setType ( int type )

Sets a new type of the projection matrix distortion applied to the viewport: display or projector.
### Arguments

- *int* **type** - The projection matrix distortion type applied to the viewport.

## int getType () const

Returns the current type of the projection matrix distortion applied to the viewport: display or projector.
### Return value

Current projection matrix distortion type applied to the viewport.
## void setSize ( vec2 size )

Sets a new physical size of the display.
### Arguments

- *vec2* **size** - The physical size of the display.

## vec2 getSize () const

Returns the current physical size of the display.
### Return value

Current physical size of the display.
## void setAspect ( float aspect )

Sets a new aspect ratio for the projector.
### Arguments

- *float* **aspect** - The aspect ratio for the projector.

## float getAspect () const

Returns the current aspect ratio for the projector.
### Return value

Current aspect ratio for the projector.
## void setVFov ( float vfov )

Sets a new vertical field of view for the projector.
### Arguments

- *float* **vfov** - The vertical field of view for the projector, in degrees.

## float getVFov () const

Returns the current vertical field of view for the projector.
### Return value

Current vertical field of view for the projector, in degrees.
## void setGroupID ( int id )

Sets a new ID of the group of viewports.
### Arguments

- *int* **id** - The ID of the group of viewports.

## int getGroupID () const

Returns the current ID of the group of viewports.
### Return value

Current ID of the group of viewports.
## static getEventBaseChanged () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventWarpChanged () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventEasyblendChanged () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventBlendChanged () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventMaskChanged () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventColorChanged () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventDebugChanged () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventSomethingChanged () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## void setViewportRendering ( int rendering )

Sets a new value indicating whether the viewport rendering is enabled.
### Arguments

- *int* **rendering** - The viewport rendering

## int isViewportRendering () const

Returns the current value indicating whether the viewport rendering is enabled.
### Return value

Current viewport rendering
## void setPixelDensity ( float density )

Sets a new rendering resolution of the viewport in pixels per meter, used for display-type viewports: the render texture size is calculated automatically from the physical screen dimensions and the specified pixel density, preserving the correct aspect ratio. The default value is 1200.
### Arguments

- *float* **density** - The rendering resolution of the viewport, in pixels per meter

## float getPixelDensity () const

Returns the current rendering resolution of the viewport in pixels per meter, used for display-type viewports: the render texture size is calculated automatically from the physical screen dimensions and the specified pixel density, preserving the correct aspect ratio. The default value is 1200.
### Return value

Current rendering resolution of the viewport, in pixels per meter
## void setRenderMode ( int mode )

Sets a new rendering mode of the viewport, one of the *RENDER_MODE_** values: a single (mono) image or a side-by-side stereo pair. The default is the mono mode.
### Arguments

- *int* **mode** - The rendering mode of the viewport

## int getRenderMode () const

Returns the current rendering mode of the viewport, one of the *RENDER_MODE_** values: a single (mono) image or a side-by-side stereo pair. The default is the mono mode.
### Return value

Current rendering mode of the viewport
## void setSwapEyesInStereoMode ( int mode )

Sets a new value indicating if the left and right eye images are exchanged in stereo mode. Use this option if the stereo signal is reversed due to the display or projection hardware configuration. Has no effect in the mono mode.
### Arguments

- *int* **mode** - The swapping of the eye images in stereo mode

## int isSwapEyesInStereoMode () const

Returns the current value indicating if the left and right eye images are exchanged in stereo mode. Use this option if the stereo signal is reversed due to the display or projection hardware configuration. Has no effect in the mono mode.
### Return value

Current swapping of the eye images in stereo mode
---

## void update ( )

Updates the data displayed in the viewport.
## void grabWindowParameters ( )

Updates the viewport data according to the [current window parameters](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#grab): display index, window size and position.
## int isGrouped ( )

Returns the value specifying if the viewport is in the group.
### Return value

**1** if the viewport is a part of a group, otherwise **0**.
## void loadEasyBlendSettings ( String filepath )

Loads the settings from the EasyBlend setup file.
### Arguments

- *String* **filepath** - Path to the EasyBlend setup file.

## void removeEasyblendSetup ( )

Removes the EasyBlend setup.
## WarpGridData getWarpGrid ( )

Returns the warp grid data.
### Return value

[WarpGridData class](../../../../api/library/plugins/spidervision/class.warpgriddata_usc.md) instance that stores the warp grid data.
## BlendZonesData getBlendZones ( )

Returns the blend zones data.
### Return value

[BlendZonesData class](../../../../api/library/plugins/spidervision/class.blendzonesdata_usc.md) instance that stores the blend zones data.
## MasksData getMasks ( )

Returns the masks data.
### Return value

[MasksData class](../../../../api/library/plugins/spidervision/class.masksdata_usc.md) instance that stores the masks data.
## ColorCorrectionData getColorCorrection ( )

Returns the color correction data.
### Return value

[ColorCorrectionData class](../../../../api/library/plugins/spidervision/class.colorcorrectiondata_usc.md) instance that stores the color correction data.
## DebugData getDebug ( )

Returns the debug data.
### Return value

[DebugData class](../../../../api/library/plugins/spidervision/class.debugdata_usc.md) instance that stores the debug data.
## EasyBlendData getEasyblendData ( )

Returns the EasyBlend data.
### Return value

[EasyBlendData class](../../../../api/library/plugins/spidervision/class.easyblenddata_usc.md) instance that stores the EasyBlend data.
## void saveXml ( Xml xml )

Saves the viewport data to the given instance of the Xml class.
### Arguments

- *[Xml](../../../../api/library/common/class.xml_usc.md)* **xml** - [Xml class](../../../../api/library/common/class.xml_usc.md) instance into which the data will be saved.

## int restoreXml ( Xml xml )

Loads the viewport data from the specified instance of the Xml class.
### Arguments

- *[Xml](../../../../api/library/common/class.xml_usc.md)* **xml** - [Xml class](../../../../api/library/common/class.xml_usc.md) instance the data from which is to be loaded.

### Return value

**1** if the data has been loaded successfully, otherwise **0**.
## void save ( Stream stream )

Saves the viewport data to the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_usc.md)* **stream** - Stream to which the data is to be written.

## void restore ( Stream stream )

Loads the viewport data from the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_usc.md)* **stream** - Stream the data from which is to be loaded.

## void saveBase ( Stream stream )

Saves the viewport data to the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_usc.md)* **stream** - Stream to which the data is to be written.

## void restoreBase ( Stream stream )

Loads the viewport data from the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_usc.md)* **stream** - Stream the data from which is to be loaded.

## void copy ( ViewportData data )

Copies the current viewport data to the specified instance of the ViewportData class.
### Arguments

- *[ViewportData](../../../../api/library/plugins/spidervision/class.viewportdata_usc.md)* **data** - Viewport data.
