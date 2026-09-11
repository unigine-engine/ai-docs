# Unigine::Plugins::SpiderVision::WallGroupData Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


The object of this class represents a group of viewports arranged in a defined number of rows and columns with a specified distance between the viewports and orientation of viewports thus creating a [wall](../../../../principles/render/output/multi_monitor/spidervision_plugin/presets.md#wall).


## WallGroupData Class

### Members

## void setSize ( ivec2 size )

Sets a new size of the wall, number of columns and rows.
### Arguments

- *ivec2* **size** - The number of columns and rows in the wall.

## ivec2 getSize () const

Returns the current size of the wall, number of columns and rows.
### Return value

Current number of columns and rows in the wall.
## void setOffset ( vec2 offset )

Sets a new horizontal and vertical distances between the edges of the neighboring viewports in the wall.
### Arguments

- *vec2* **offset** - The horizontal and vertical distances between neighboring viewports.

## vec2 getOffset () const

Returns the current horizontal and vertical distances between the edges of the neighboring viewports in the wall.
### Return value

Current horizontal and vertical distances between neighboring viewports.
## void setDisplaySize ( vec2 size )

Sets a new actual width and height of the display in the Wall group. It is assumed that the wall consists of identical displays. If sizes of displays differ, you may consider creating a configuration with several Wall groups.
### Arguments

- *vec2* **size** - The display width and height.

## vec2 getDisplaySize () const

Returns the current actual width and height of the display in the Wall group. It is assumed that the wall consists of identical displays. If sizes of displays differ, you may consider creating a configuration with several Wall groups.
### Return value

Current display width and height.
## void setWindowSize ( ivec2 size )

Sets a new width and height of the window on the display screen.
### Arguments

- *ivec2* **size** - The width and height of the window on the screen, in pixels.

## ivec2 getWindowSize () const

Returns the current width and height of the window on the display screen.
### Return value

Current width and height of the window on the screen, in pixels.
## void setDistanceToViewer ( float viewer )

Sets a new distance from the viewer point to the center of the group.
### Arguments

- *float* **viewer** - The distance from the viewer point to the center of the group, in units.

## float getDistanceToViewer () const

Returns the current distance from the viewer point to the center of the group.
### Return value

Current distance from the viewer point to the center of the group, in units.
## void setAngle ( float angle )

Sets a new angle between the neighboring displays in the XY plane (i.e. around the Z axis).
### Arguments

- *float* **angle** - The angle between the neighboring displays in the XY plane.

## float getAngle () const

Returns the current angle between the neighboring displays in the XY plane (i.e. around the Z axis).
### Return value

Current angle between the neighboring displays in the XY plane.
## void setAutoArrange ( bool arrange )

Sets a new value indicating if automatic positioning of windows on the displays is enabled. If disabled, all windows are created with the position (0, 0) at the same place and are to be positioned manually.
### Arguments

- *bool* **arrange** - Set **true** to enable automatic positioning of windows on the displays; **false** - to disable it.

## bool isAutoArrange () const

Returns the current value indicating if automatic positioning of windows on the displays is enabled. If disabled, all windows are created with the position (0, 0) at the same place and are to be positioned manually.
### Return value

**true** if automatic positioning of windows on the displays is enabled ; otherwise **false**.
## void setAspect ( float aspect )

Sets a new
### Arguments

- *float* **aspect** - The

## float getAspect () const

Returns the current
### Return value

Current
## void setVFov ( float vfov )

Sets a new
### Arguments

- *float* **vfov** - The

## float getVFov () const

Returns the current
### Return value

Current
## void setTransformType ( int type )

Sets a new
### Arguments

- *int* **type** - The

## int getTransformType () const

Returns the current
### Return value

Current
## void setPixelDensity ( float density )

Sets a new pixel density assigned to the viewports of the generated group, in pixels per meter: the render texture size is calculated automatically from the physical screen dimensions and the specified pixel density, preserving the correct aspect ratio. The default value is 1200.
### Arguments

- *float* **density** - The pixel density of the generated group, in pixels per meter

## float getPixelDensity () const

Returns the current pixel density assigned to the viewports of the generated group, in pixels per meter: the render texture size is calculated automatically from the physical screen dimensions and the specified pixel density, preserving the correct aspect ratio. The default value is 1200.
### Return value

Current pixel density of the generated group, in pixels per meter
