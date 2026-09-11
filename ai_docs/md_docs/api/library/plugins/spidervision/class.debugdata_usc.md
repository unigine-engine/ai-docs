# Unigine::Plugins::SpiderVision::DebugData Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This object stores the debug data such as the [warp grid](../../../../principles/render/output/multi_monitor/spidervision_plugin/projection_setup.md#warp) state, [blend zone](../../../../principles/render/output/multi_monitor/spidervision_plugin/projection_setup.md#blend) adjustment points, viewport [debug color](../../../../principles/render/output/multi_monitor/spidervision_plugin/projection_setup.md#render_options) filling, etc.


> **Notice:** The debug data are **not** stored in the configuration file.


This object is accessible via the corresponding method of the [ViewportData](../../../../api/library/plugins/spidervision/class.viewportdata_usc.md#getDebug_DebugData) class.


## DebugData Class

### Members

## void setShowBlendLines ( int lines )

Sets a new value indicating if the visualization is enabled for blend area control lines and selected points on the screen.
### Arguments

- *int* **lines** - The visualization of blend area control lines and points

## int isShowBlendLines () const

Returns the current value indicating if the visualization is enabled for blend area control lines and selected points on the screen.
### Return value

Current visualization of blend area control lines and points
## void setBlendPointPositions ( Vector<vec2> positions )

Sets a new positions of blend area points displayed in the viewport.
### Arguments

- *Vector<vec2>* **positions** - The array containing positions of blend area points displayed in the viewport.

## Vector<vec2> getBlendPointPositions () const

Returns the current positions of blend area points displayed in the viewport.
### Return value

Current array containing positions of blend area points displayed in the viewport.
## void setShowGrid ( int grid )

Sets a new value indicating if the visualization of warping grid on the screen is enabled.
### Arguments

- *int* **grid** - The visualization of warping grid

## int isShowGrid () const

Returns the current value indicating if the visualization of warping grid on the screen is enabled.
### Return value

Current visualization of warping grid
## void setWarpPointsEnabled ( int enabled )

Sets a new value indicating if warping control points are displayed in the viewport.
### Arguments

- *int* **enabled** - The display of warping control points

## int isWarpPointsEnabled () const

Returns the current value indicating if warping control points are displayed in the viewport.
### Return value

Current display of warping control points
## void setWarpPointPositions ( Vector<vec2> positions )

Sets a new positions of warping grid control points displayed in the viewport.
### Arguments

- *Vector<vec2>* **positions** - The array containing positions of warping grid points displayed in the viewport.

## Vector<vec2> getWarpPointPositions () const

Returns the current positions of warping grid control points displayed in the viewport.
### Return value

Current array containing positions of warping grid points displayed in the viewport.
## void setDebugColorIndex ( int index )

Sets a new indexed color used in debug mode.
> **Notice:** Setting individual colors for different viewports enables you to visualize overlapping regions for different viewports and facilitates the setup process.


### Arguments

- *int* **index** - The color used in debug mode, one of the following values:

  - **0** - no color
  - **1** - red
  - **2** - green
  - **3** - blue
  - **4** - cyan
  - **5** - magenta
  - **6** - yellow
  - **7** - white
  - **8** - black

## int getDebugColorIndex () const

Returns the current indexed color used in debug mode.
> **Notice:** Setting individual colors for different viewports enables you to visualize overlapping regions for different viewports and facilitates the setup process.


### Return value

Current color used in debug mode, one of the following values:
- **0** - no color
- **1** - red
- **2** - green
- **3** - blue
- **4** - cyan
- **5** - magenta
- **6** - yellow
- **7** - white
- **8** - black


## vec4 getDebugColor () const

Returns the current color used in debug mode.
> **Notice:** Setting individual colors for different viewports enables you to visualize overlapping regions for different viewports and facilitates the setup process.


### Return value

Current color used in debug mode.
## static getEventChanged () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## void setDebugStereo ( int stereo )

Sets a new value indicating if the real eye images are replaced by solid diagnostic colors in stereo rendering: the left eye receives a solid green image and the right eye a solid red one, so the operator can verify which physical output receives which eye. Disabled by default.
### Arguments

- *int* **stereo** - The diagnostic eye-color substitution in stereo mode

## int isDebugStereo () const

Returns the current value indicating if the real eye images are replaced by solid diagnostic colors in stereo rendering: the left eye receives a solid green image and the right eye a solid red one, so the operator can verify which physical output receives which eye. Disabled by default.
### Return value

Current diagnostic eye-color substitution in stereo mode
---

## String getDebugColorName ( int index )

Returns the name of the debug color by its index.
### Arguments

- *int* **index** - Index of the color used in debug mode.

### Return value

Name of the indexed color.
## int getNumDebugColors ( )

Returns the total number of indexed debug colors.
### Return value

The total number of indexed debug colors.
## void save ( Stream stream )

Saves the debug data to the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_usc.md)* **stream** - Stream to which the data is to be written.

## void restore ( Stream stream )

Loads the debug data from the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_usc.md)* **stream** - Stream the data from which is to be loaded.
