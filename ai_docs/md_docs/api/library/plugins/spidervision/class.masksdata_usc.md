# Unigine::Plugins::SpiderVision::MasksData Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class stores data on all [masks](../../../../principles/render/output/multi_monitor/spidervision_plugin/projection_setup.md#masks) created for the viewport and provides the interface for configuring each mask.


The mask is an arbitrary shape filled by a selected color that allows cutting out selected areas on the image rendered in the viewport.


This object is accessible via the corresponding method of the [ViewportData](../../../../api/library/plugins/spidervision/class.viewportdata_usc.md#getMasks_MasksData) class.


The mask data are stored in the [configuration file](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#config_file).


## MasksData Class

### Members

## void setEnabled ( int enabled )

Sets a new value indicating if masks rendering is enabled.
### Arguments

- *int* **enabled** - The rendering of masks

## int isEnabled () const

Returns the current value indicating if masks rendering is enabled.
### Return value

Current rendering of masks
## int getNumMasks () const

Returns the current total number of masks in the configuration.
### Return value

Current total number of masks in the configuration.
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

## void clear ( )

Clears all masks.
## int addMask ( )

Adds a new mask.
### Return value

Mask index.
## void removeMask ( int index )

Removes the mask with the specified index.
### Arguments

- *int* **index** - Mask index.

## void setMaskName ( int mask , String name )

Sets the name for the specified mask.
### Arguments

- *int* **mask** - Mask index.
- *String* **name** - Mask name.

## String getMaskName ( int mask )

Returns the name for the specified mask.
### Arguments

- *int* **mask** - Mask index.

### Return value

Mask name.
## void setMaskEnabled ( int mask , int enabled )

Sets the value indicating if rendering of the specified mask is enabled.
### Arguments

- *int* **mask** - Mask index.
- *int* **enabled** - **1** to enable rendering of the mask, **0** to disable it.

## int isMaskEnabled ( int mask )

Returns the value indicating if rendering of the specified mask is enabled.
### Arguments

- *int* **mask** - Mask index.

### Return value

**1** if rendering of the mask is enabled, otherwise **0**.
## void setMaskSmoothStep ( int mask , int smooth_step )

Sets smoothing of edges for the specified mask.
### Arguments

- *int* **mask** - Mask index.
- *int* **smooth_step** - Smoothing value, the number of additional points to be inserted between the control points of the mask.

## int getMaskSmoothStep ( int mask )

Returns the smoothing value for the specified mask.
### Arguments

- *int* **mask** - Mask index.

### Return value

Smoothing value, the number of additional points inserted between the control points of the mask.
## int addPoint ( int mask )

Adds the point to the mask as the last point in the list of points.
### Arguments

- *int* **mask** - Mask index.

### Return value

Index of the added point.
## int addPoint ( int mask , int insert_index )

Adds the point to the mask.
### Arguments

- *int* **mask** - Mask index.
- *int* **insert_index** - Point index.

### Return value

Total count of points in the mask.
## void removePoint ( int mask , int index )

Removes the point from the mask.
### Arguments

- *int* **mask** - Mask index.
- *int* **index** - Point index.

## int getNumPoints ( int mask )

Returns the total number of points in the mask.
### Arguments

- *int* **mask** - Mask index.

### Return value

Total number of points.
## void setPoint ( int mask , int index , vec2 point )

Sets the coordinates for the specified point in the mask.
### Arguments

- *int* **mask** - Mask index.
- *int* **index** - Point index.
- *vec2* **point** - Point coordinates.

## vec2 getPoint ( int mask , int index )

Returns the coordinates for the specified point in the mask.
### Arguments

- *int* **mask** - Mask index.
- *int* **index** - Point index.

### Return value

Point coordinates.
## void setPointHandleLeft ( int mask , int index , vec2 point )

Sets the left control handle point for the specified point in the mask.
### Arguments

- *int* **mask** - Mask index.
- *int* **index** - Point index.
- *vec2* **point** - Coordinates of left control handle point.

## vec2 getHandleLeft ( int mask , int index )

Returns the left control handle point for the specified point in the mask.
### Arguments

- *int* **mask** - Mask index.
- *int* **index** - Point index.

### Return value

Coordinates of left control handle point.
## void setPointHandleRight ( int mask , int index , vec2 point )

Sets the right control handle point for the specified point in the mask.
### Arguments

- *int* **mask** - Mask index.
- *int* **index** - Point index.
- *vec2* **point** - Coordinates of right control handle point.

## vec2 getHandleRight ( int mask , int index )

Returns the right control handle point for the specified point in the mask.
### Arguments

- *int* **mask** - Mask index.
- *int* **index** - Point index.

### Return value

Coordinates of right control handle point.
## void setPointSmoothType ( int mask , int index , int type )

Sets the line curving behavior for the point.
### Arguments

- *int* **mask** - Mask index.
- *int* **index** - Point index.
- *int* **type** - Type of the line curving behavior in the point.

## int getPointSmoothType ( int mask , int index )

Returns the line curving behavior for the point.
### Arguments

- *int* **mask** - Mask index.
- *int* **index** - Point index.

### Return value

Type of the line curving behavior in the point.
## void saveXml ( Xml xml )

Saves the masks data to the given instance of the Xml class.
### Arguments

- *[Xml](../../../../api/library/common/class.xml_usc.md)* **xml** - [Xml class](../../../../api/library/common/class.xml_usc.md) instance into which the data will be saved.

## int restoreXml ( Xml xml )

Loads the masks data from the specified instance of the Xml class.
### Arguments

- *[Xml](../../../../api/library/common/class.xml_usc.md)* **xml** - [Xml class](../../../../api/library/common/class.xml_usc.md) instance the data from which is to be loaded.

### Return value

**1** if the data has been loaded successfully, otherwise **0**.
## void save ( Stream stream )

Saves the masks data to the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_usc.md)* **stream** - Stream to which the data is to be written.

## void restore ( Stream stream )

Loads the masks data from the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_usc.md)* **stream** - Stream the data from which is to be loaded.
