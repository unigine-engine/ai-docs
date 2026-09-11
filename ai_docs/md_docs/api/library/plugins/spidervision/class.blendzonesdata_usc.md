# Unigine::Plugins::SpiderVision::BlendZonesData Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class stores data on all [blend zones](../../../../principles/render/output/multi_monitor/spidervision_plugin/projection_setup.md#blend) created for the viewport and provides the interface for configuring each blend zone.


The blend zone is an arbitrary shape formed by three vertical lines so that it has two parts � one part is a mask (from blue to green line), and the other one (from green to red line) is a gradient zone.


![](../../../../principles/render/output/multi_monitor/spidervision_plugin/blend_zone.jpg)


The blend zone data are stored in the [configuration file](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#config_file).


To configure parameters of a specific blend zone of a viewport, the methods of this class are to be used. However, the instance of the *BlendZonesData* class doesn't store any information on which viewport it is assigned to � the information is stored in the *[ViewportData](../../../../api/library/plugins/spidervision/class.viewportdata_usc.md#getBlendZones_BlendZonesData)* class instance.


## BlendZonesData Class

### Members

## void setEnabled ( int enabled )

Sets a new value indicating if blend zones rendering is enabled.
### Arguments

- *int* **enabled** - The rendering of blend zones

## int isEnabled () const

Returns the current value indicating if blend zones rendering is enabled.
### Return value

Current rendering of blend zones
## int getNumZones () const

Returns the current total number of blend zones.
### Return value

Current total number of blend zones.
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

## int addZone ( )

Adds a new blend zone for the viewport.
### Return value

Index of the added blend zone.
## void removeZone ( int index )

Removes the specified blend zone.
### Arguments

- *int* **index** - Index of the blend zone.

## void clear ( )

Clears all blend zones.
## void changeZoneResolution ( int zone , int count )

Defines the number of lines between the start and the end point that help configuring the contour. This method corresponds to the *Resolution* parameter in blend zone settings in UI.
### Arguments

- *int* **zone** - Index of the blend zone.
- *int* **count** - Number of lines in the area from the start to the end point of the blend zone.

## void setZoneEnabled ( int zone , int in_enabled )

Enables or disables the specified blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.
- *int* **in_enabled** - **1** to enable the specified blend zone, **0** to disable it.

## int isZoneEnabled ( int zone )

Returns the value indicating if the specified blend zone is enabled.
### Arguments

- *int* **zone** - Index of the blend zone.

### Return value

**1** if the specified blend zone is enabled, otherwise **0**.
## void setZoneAlpha ( int zone , float in_alpha )

Sets the alpha value for the specified blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.
- *float* **in_alpha** - Alpha value.

## float getZoneAlpha ( int zone )

Returns the alpha value for the specified blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.

### Return value

Alpha value.
## void setZoneContrast ( int zone , float in_contrast )

Sets the contrast value for the specified blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.
- *float* **in_contrast** - Contrast value.

## float getZoneContrast ( int zone )

Returns the contrast value for the specified blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.

### Return value

Contrast value.
## void setZoneGamma ( int zone , float in_gamma )

Sets the gamma value for the specified blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.
- *float* **in_gamma** - Gamma value.

## float getZoneGamma ( int zone )

Returns the gamma value for the specified blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.

### Return value

Gamma value.
## void setZoneLinked ( int zone , int linked )

Sets the value specifying if linking of the zone is enabled. If enabled, allows adjusting Alpha, Contrast, and Gamma for two blends simultaneously for better neighboring of two viewports.
### Arguments

- *int* **zone** - Index of the blend zone.
- *int* **linked** - **1** to enable linking of the zone, **0** to disable it.

## int isZoneLinked ( int zone )

Returns the value specifying if linking of the zone is enabled. If enabled, allows adjusting Alpha, Contrast, and Gamma for two blends simultaneously for better neighboring of two viewports.
### Arguments

- *int* **zone** - Index of the blend zone.

### Return value

**1** if linking of the zone is enabled, otherwise **0**.
## void setZoneLink ( int zone , ivec2 link )

Links two blendzones to configure their parameters sinchronously.
### Arguments

- *int* **zone** - Index of the blend zone.
- *ivec2* **link** - Vector containing two values:

  1. Index of the vieport the blend zone of which is to be linked
  2. Index of the blend zone in the list of blend zones of that viewport

## ivec2 getZoneLink ( int zone )

Returns the information on the blend zone linked to this blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.

### Return value

Vector containing two values:
1. Index of the vieport the blend zone of which is to be linked
2. Index of the blend zone in the list of blend zones of that viewport


## int addLine ( int zone )

Adds the line to the specified blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.

### Return value

Index of the line.
## void removeLine ( int zone , int index )

Removes the specified line from the specified blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.
- *int* **index** - Index of the line.

## int getNumLines ( int zone )

Returns the total number of lines for the specified blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.

### Return value

Total number of lines.
## void setLinePoint ( int zone , int line , int type , vec2 point )

Sets the point with the specified coordinates and type on the specified line of the specified blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.
- *int* **line** - Index of the line.
- *int* **type** - Type of the point.
- *vec2* **point** - Coordinates of the point.

## vec2 getLinePoint ( int zone , int line , int type )

Returns the coordinates of the point with the specified type on the specified line of the specified blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.
- *int* **line** - Index of the line.
- *int* **type** - Type of the point.

### Return value

Coordinates of the point.
## void setLinePointHandleLeft ( int zone , int line , int type , vec2 handle_left )

Sets the coordinates of the left handle for the specified point.
### Arguments

- *int* **zone** - Index of the blend zone.
- *int* **line** - Index of the line.
- *int* **type** - Type of the point.
- *vec2* **handle_left** - Coordinates of the handle.

## vec2 getLinePointHandleLeft ( int zone , int line , int type )

Returns the coordinates of the left handle for the specified point.
### Arguments

- *int* **zone** - Index of the blend zone.
- *int* **line** - Index of the line.
- *int* **type** - Type of the point.

### Return value

Coordinates of the handle.
## void setLinePointHandleRight ( int zone , int line , int type , vec2 handle_right )

Sets the coordinates of the right handle for the specified point.
### Arguments

- *int* **zone** - Index of the blend zone.
- *int* **line** - Index of the line.
- *int* **type** - Type of the point.
- *vec2* **handle_right** - Coordinates of the handle.

## vec2 getLinePointHandleRight ( int zone , int line , int type )

Returns the coordinates of the right handle for the specified point.
### Arguments

- *int* **zone** - Index of the blend zone.
- *int* **line** - Index of the line.
- *int* **type** - Type of the point.

### Return value

Coordinates of the handle.
## void setLinePointSmoothType ( int zone , int line , int type , int smooth_type )

Sets the line curving behavior for the point.
### Arguments

- *int* **zone** - Index of the blend zone.
- *int* **line** - Index of the line.
- *int* **type** - Type of the point.
- *int* **smooth_type** - Type of the line curving behavior in the point.

## int getLinePointSmoothType ( int zone , int line , int type )

Returns the line curving behavior for the point.
### Arguments

- *int* **zone** - Index of the blend zone.
- *int* **line** - Index of the line.
- *int* **type** - Type of the point.

### Return value

Type of the line curving behavior in the point.
## void setZoneName ( int zone , String name )

Sets the name for the blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.
- *String* **name** - Name of the blend zone.

## String getZoneName ( int zone )

Returns the name of the blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.

### Return value

Name of the blend zone.
## void setZoneSmooth ( int zone , int value )

Sets the smooth value that defines the roundness of the blend zone edges.
### Arguments

- *int* **zone** - Index of the blend zone.
- *int* **value** - Smooth value, the number of additional points creating the Bezier spline between two blend zone points.

## int getZoneSmooth ( int zone )

Returns the smooth value that defines the roundness of the blend zone edges.
### Arguments

- *int* **zone** - Index of the blend zone.

### Return value

Smooth value.
## void saveXml ( Xml xml )

Saves the blend zones data to the given instance of the Xml class.
### Arguments

- *[Xml](../../../../api/library/common/class.xml_usc.md)* **xml** - [Xml class](../../../../api/library/common/class.xml_usc.md) instance into which the data will be saved.

## int restoreXml ( Xml xml )

Loads the blend zones data from the specified instance of the Xml class.
### Arguments

- *[Xml](../../../../api/library/common/class.xml_usc.md)* **xml** - [Xml class](../../../../api/library/common/class.xml_usc.md) instance the data from which is to be loaded.

### Return value

**1** if the data has been loaded successfully, otherwise **0**.
## void save ( Stream stream )

Saves the blend zones data to the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_usc.md)* **stream** - Stream to which the data is to be written.

## void restore ( Stream stream )

Loads the blend zones data from the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_usc.md)* **stream** - Stream the data from which is to be loaded.
