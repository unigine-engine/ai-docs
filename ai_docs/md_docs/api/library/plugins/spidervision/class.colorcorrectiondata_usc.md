# Unigine::Plugins::SpiderVision::ColorCorrectionData Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


The instance of this class stores the viewport color correction data. Color correction may be required to compensate for the difference in color rendition of different projectors.


You can also adjust the brightness of the image to make the parts of the image that are farther away from the viewer lighter and vice versa, so that the brightness of the resulting image is uniform.


The color correction data are stored in the [configuration file](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#config_file).


This object is accessible via the corresponding method of the [ViewportData](../../../../api/library/plugins/spidervision/class.viewportdata_usc.md#getColorCorrection_ColorCorrectionData) class.


## ColorCorrectionData Class

### Members

## void setEnabled ( int enabled )

Sets a new value indicating if the color correction is applied.
### Arguments

- *int* **enabled** - The color correction

## int isEnabled () const

Returns the current value indicating if the color correction is applied.
### Return value

Current color correction
## void setColorScale ( vec4 scale )

Sets a new color multiplier for the rendered image.
### Arguments

- *vec4* **scale** - The color multiplier

## vec4 getColorScale () const

Returns the current color multiplier for the rendered image.
### Return value

Current color multiplier
## void setColorBias ( vec4 bias )

Sets a new color bias for the rendered image.
### Arguments

- *vec4* **bias** - The per-channel color bias.

## vec4 getColorBias () const

Returns the current color bias for the rendered image.
### Return value

Current per-channel color bias.
## void setCornerBrightness ( vec4 brightness )

Sets a new brightness correction values for the corners of the rendered image.
### Arguments

- *vec4* **brightness** - The four-component vector containing brightness values, in the **[0.0f, 1.0f]** range, for the corners of the rendered image (upper left, upper right, lower left, lower right).

## vec4 getCornerBrightness () const

Returns the current brightness correction values for the corners of the rendered image.
### Return value

Current four-component vector containing brightness values, in the **[0.0f, 1.0f]** range, for the corners of the rendered image (upper left, upper right, lower left, lower right).
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
---

## void saveXml ( Xml xml )

Saves the color correction data to the given instance of the Xml class.
### Arguments

- *[Xml](../../../../api/library/common/class.xml_usc.md)* **xml** - [Xml class](../../../../api/library/common/class.xml_usc.md) instance into which the data will be saved.

## int restoreXml ( Xml xml )

Loads the color correction data from the specified instance of the Xml class.
### Arguments

- *[Xml](../../../../api/library/common/class.xml_usc.md)* **xml** - [Xml class](../../../../api/library/common/class.xml_usc.md) instance the data from which is to be loaded.

### Return value

**1** if the data has been loaded successfully, otherwise **0**.
## void save ( Stream stream )

Saves the color correction data to the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_usc.md)* **stream** - Stream to which the data is to be written.

## void restore ( Stream stream )

Loads the color correction data from the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_usc.md)* **stream** - Stream the data from which is to be loaded.
