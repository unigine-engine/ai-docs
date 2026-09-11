# Unigine::Plugins::SpiderVision::CalibrationGridData Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


[Calibration Grid](../../../../principles/render/output/multi_monitor/spidervision_plugin/calibration.md) stores the data on the calibration grid adjustments of the current configuration.


Calibration grid is in fact a grid of a certain shape (sphere or box) with a specified distance between the lines of this grid. The grid helps aligning the images rendered by projectors to obtain a seamless image.


> **Notice:** The calibration grid data are **not** stored in the configuration file.


This object is accessible via the corresponding method of the [DisplaysConfig](../../../../api/library/plugins/spidervision/class.displaysconfig_usc.md#getCalibrationGrid_CalibrationGridData) class.


## CalibrationGridData Class

### Members

## void setVisible ( int visible )

Sets a new value indicating if the calibration grid is rendered.
### Arguments

- *int* **visible** - The rendering of the calibration grid

## int isVisible () const

Returns the current value indicating if the calibration grid is rendered.
### Return value

Current rendering of the calibration grid
## void setDistance ( float distance )

Sets a new distance from the viewpoint to the grid. The difference is noticeable with the Box type of calibration pattern.
### Arguments

- *float* **distance** - The distance from the viewpoint to the grid.

## float getDistance () const

Returns the current distance from the viewpoint to the grid. The difference is noticeable with the Box type of calibration pattern.
### Return value

Current distance from the viewpoint to the grid.
## void setType ( int type )

Sets a new type of the calibration pattern.
### Arguments

- *int* **type** - The type of the calibration pattern.

## int getType () const

Returns the current type of the calibration pattern.
### Return value

Current type of the calibration pattern.
## void setSphereCut ( int cut )

Sets a new value indicating if the Sphere Cut option is enabled for the sperical calibration grid. This option allows hiding the top and bottom poles.
### Arguments

- *int* **cut** - The Sphere Cut option

## int isSphereCut () const

Returns the current value indicating if the Sphere Cut option is enabled for the sperical calibration grid. This option allows hiding the top and bottom poles.
### Return value

Current Sphere Cut option
## void setLinesVerticalStep ( float step )

Sets a new distance between major vertical lines.
### Arguments

- *float* **step** - The distance between major vertical lines.

## float getLinesVerticalStep () const

Returns the current distance between major vertical lines.
### Return value

Current distance between major vertical lines.
## void setLinesHorizontalStep ( float step )

Sets a new distance between major horizontal lines.
### Arguments

- *float* **step** - The distance between major horizontal lines.

## float getLinesHorizontalStep () const

Returns the current distance between major horizontal lines.
### Return value

Current distance between major horizontal lines.
## void setLinesVerticalMinorCount ( int count )

Sets a new number of secondary lines between the two neighboring major vertical lines.
### Arguments

- *int* **count** - The number of secondary lines between the two neighboring major vertical lines.

## int getLinesVerticalMinorCount () const

Returns the current number of secondary lines between the two neighboring major vertical lines.
### Return value

Current number of secondary lines between the two neighboring major vertical lines.
## void setLinesHorizontalMinorCount ( int count )

Sets a new number of secondary lines between the two neighboring major horizontal lines.
### Arguments

- *int* **count** - The number of secondary lines between the two neighboring major horizontal lines.

## int getLinesHorizontalMinorCount () const

Returns the current number of secondary lines between the two neighboring major horizontal lines.
### Return value

Current number of secondary lines between the two neighboring major horizontal lines.
## void setTextEnabled ( int enabled )

Sets a new value indicating if text on the calibration grid is rendered.
### Arguments

- *int* **enabled** - The text rendering on the calibration grid

## int isTextEnabled () const

Returns the current value indicating if text on the calibration grid is rendered.
### Return value

Current text rendering on the calibration grid
## void setTextFontSize ( int size )

Sets a new size of the text displayed on the calibration grid.
### Arguments

- *int* **size** - The size of the text displayed on the calibration grid.

## int getTextFontSize () const

Returns the current size of the text displayed on the calibration grid.
### Return value

Current size of the text displayed on the calibration grid.
## void setLineHighlightEnabled ( int enabled )

Sets a new highlighting of one horizontal and one vertical line.
### Arguments

- *int* **enabled** - The highlighting of one horizontal and one vertical line

## int isLineHighlightEnabled () const

Returns the current highlighting of one horizontal and one vertical line.
### Return value

Current highlighting of one horizontal and one vertical line
## void setLineHighlightHorizontalIndex ( int index )

Sets a new index of the horizontal highlight. Only one line can be highlighted. The line is invisible if its index is set to zero.
### Arguments

- *int* **index** - The index of the horizontal highlight.

## int getLineHighlightHorizontalIndex () const

Returns the current index of the horizontal highlight. Only one line can be highlighted. The line is invisible if its index is set to zero.
### Return value

Current index of the horizontal highlight.
## void setLineHighlightVerticalIndex ( int index )

Sets a new index of the vertical highlight. Only one line can be highlighted. The line is invisible if its index is set to zero.
### Arguments

- *int* **index** - The index of the vertical highlight.

## int getLineHighlightVerticalIndex () const

Returns the current index of the vertical highlight. Only one line can be highlighted. The line is invisible if its index is set to zero.
### Return value

Current index of the vertical highlight.
## void setTransformYaw ( float yaw )

Sets a new grid transform along the vertical axis. Only the grid is transformed, the projected image is not transformed.
### Arguments

- *float* **yaw** - The yaw angle, in degrees.

## float getTransformYaw () const

Returns the current grid transform along the vertical axis. Only the grid is transformed, the projected image is not transformed.
### Return value

Current yaw angle, in degrees.
## void setTransformPitch ( float pitch )

Sets a new grid transform along the transverse axis. Only the grid is transformed, the projected image is not transformed.
### Arguments

- *float* **pitch** - The pitch angle, in degrees.

## float getTransformPitch () const

Returns the current grid transform along the transverse axis. Only the grid is transformed, the projected image is not transformed.
### Return value

Current pitch angle, in degrees.
## void setTransformRoll ( float roll )

Sets a new grid transform along the longitudinal axis. Only the grid is transformed, the projected image is not transformed.
### Arguments

- *float* **roll** - The roll angle, in degrees.

## float getTransformRoll () const

Returns the current grid transform along the longitudinal axis. Only the grid is transformed, the projected image is not transformed.
### Return value

Current roll angle, in degrees.
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
## void setBackgroundColor ( )

Sets a new background color of the calibration grid.
### Arguments

- **color** - The background color of the calibration grid.

## getBackgroundColor () const

Returns the current background color of the calibration grid.
### Return value

Current background color of the calibration grid.
## void setHighlightedColor ( )

Sets a new color of the highlighted line.
### Arguments

- **color** - The color of the highlighted line.

## getHighlightedColor () const

Returns the current color of the highlighted line.
### Return value

Current color of the highlighted line.
## void setHorizontalMinorLinesColor ( )

Sets a new color of the minor horizontal lines in the calibration grid.
### Arguments

- **color** - The color of the minor horizontal lines in the calibration grid.

## getHorizontalMinorLinesColor () const

Returns the current color of the minor horizontal lines in the calibration grid.
### Return value

Current color of the minor horizontal lines in the calibration grid.
## void setHorizontalMajorLinesColor ( )

Sets a new color of the major horizontal lines in the calibration grid.
### Arguments

- **color** - The color of the major horizontal lines in the calibration grid.

## getHorizontalMajorLinesColor () const

Returns the current color of the major horizontal lines in the calibration grid.
### Return value

Current color of the major horizontal lines in the calibration grid.
## void setVerticalMinorLinesColor ( )

Sets a new color of the minor vertical lines in the calibration grid.
### Arguments

- **color** - The color of the minor vertical lines in the calibration grid.

## getVerticalMinorLinesColor () const

Returns the current color of the minor vertical lines in the calibration grid.
### Return value

Current color of the minor vertical lines in the calibration grid.
## void setVerticalMajorLinesColor ( )

Sets a new color of the major vertical lines in the calibration grid.
### Arguments

- **color** - The color of the major vertical lines in the calibration grid.

## getVerticalMajorLinesColor () const

Returns the current color of the major vertical lines in the calibration grid.
### Return value

Current color of the major vertical lines in the calibration grid.
## void setAxesColor ( )

Sets a new color of the central axes in the calibration grid.
### Arguments

- **color** - The color of the central axes in the calibration grid.

## getAxesColor () const

Returns the current color of the central axes in the calibration grid.
### Return value

Current color of the central axes in the calibration grid.
## void setTextColor ( )

Sets a new color of the text in the calibration grid.
### Arguments

- **color** - The color of the text in the calibration grid.

## getTextColor () const

Returns the current color of the text in the calibration grid.
### Return value

Current color of the text in the calibration grid.
---

## void save ( Stream stream )

Saves the calibration grid data to the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_usc.md)* **stream** - Stream to which the data is to be written.

## void restore ( Stream stream )

Loads the calibration grid data from the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_usc.md)* **stream** - Stream the data from which is to be loaded.
