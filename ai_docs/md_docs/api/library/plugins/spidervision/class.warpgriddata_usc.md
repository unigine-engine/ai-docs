# Unigine::Plugins::SpiderVision::WarpGridData Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


The object of this class stores the information on the warp grid � a set of points and their handles that create a mesh based on which the displayed image is reshaped.


Warping of the image is required to render the projected image on a distorted surface in such a way that it would look undistorted.


This object is accessible via the corresponding method of the [ViewportData](../../../../api/library/plugins/spidervision/class.viewportdata_usc.md#getWarpGrid_WarpGridData) class.


The mask data are stored in the [configuration file](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#config_file).


## WarpGridData Class

### Members

## void setEnabled ( int enabled )

Sets a new value indicating if the warp grid rendering is enabled.
### Arguments

- *int* **enabled** - The rendering of the warp grid

## int isEnabled () const

Returns the current value indicating if the warp grid rendering is enabled.
### Return value

Current rendering of the warp grid
## int getNumRows () const

Returns the current number of warping grid points vertically in the warp grid, which define the grid rows.
### Return value

Current number of warping grid points vertically in the warp grid.
## int getNumColumns () const

Returns the current number of warping grid points horizontally in the warp grid, which define the grid columns.
### Return value

Current number of warping grid points horizontally in the warp grid.
## int getWarpPointsCount () const

Returns the current total number of points in the warp grid.
### Return value

Current total number of points in the warp grid.
## void setCanvasFlipMask ( int mask )

Sets a new type of flipping the canvas mask for the viewport.
### Arguments

- *int* **mask** - The type of mask flipping.

## int getCanvasFlipMask () const

Returns the current type of flipping the canvas mask for the viewport.
### Return value

Current type of mask flipping.
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

## void setGridSize ( int row , int column )

Sets the number of columns and rows on the warping grid.
### Arguments

- *int* **row** - Number of grid rows.
- *int* **column** - Number of grid columns.

## void setPoint ( int x , int y , vec2 point )

Sets the coordinates of the warping control point on the grid.
### Arguments

- *int* **x** - Position of the warping control point in the row, starting from 0 on the left.
- *int* **y** - Position of the warping control point in the column, starting from 0 at the bottom.
- *vec2* **point** - Screen-space coordinates of the point.

## void setPoint ( int index , vec2 point )

Sets the coordinates of the warping control point on the grid.
### Arguments

- *int* **index** - Warping control point index. The point with the 0 index is in the bottom left corner with the progression going upwards, and then to the next column bottom point.
- *vec2* **point** - Screen-space coordinates of the point.

## vec2 getPoint ( int x , int y )

Returns the coordinates of the warping control point on the grid.
### Arguments

- *int* **x** - Position of the warping control point in the row, starting from 0 on the left.
- *int* **y** - Position of the warping control point in the column, starting from 0 at the bottom.

### Return value

Screen-space coordinates of the point.
## vec2 getPoint ( int index )

Returns the coordinates of the warping control point on the grid.
### Arguments

- *int* **index** - Warping control point index. The point with the 0 index is in the bottom left corner with the progression going upwards, and then to the next column bottom point.

### Return value

Screen-space coordinates of the point.
## void setPointHandle ( int x , int y , int type , vec2 point )

Sets the type and position of the handle point for the specified warp grid point.
### Arguments

- *int* **x** - Position of the warping control point in the row, starting from 0 on the left.
- *int* **y** - Position of the warping control point in the column, starting from 0 at the bottom.
- *int* **type** - Type of control handle of the warping control point.
- *vec2* **point** - Screen-space coordinates of the point.

## void setPointHandle ( int index , int type , vec2 point )

Sets the type and position of the handle point for the specified warp grid point.
### Arguments

- *int* **index** - Warping control point index. The point with the 0 index is in the bottom left corner with the progression going upwards, and then to the next column bottom point.
- *int* **type** - Type of control handle of the warping control point.
- *vec2* **point** - Screen-space coordinates of the point.

## vec2 getPointHandle ( int x , int y , int type )

Returns the type and position of the handle point for the specified warp grid point.
### Arguments

- *int* **x** - Position of the warping control point in the row, starting from 0 on the left.
- *int* **y** - Position of the warping control point in the column, starting from 0 at the bottom.
- *int* **type** - Type of control handle of the warping control point.

### Return value

Screen-space coordinates of the point.
## vec2 getPointHandle ( int index , int type )

Returns the type and position of the handle point for the specified warp grid point.
### Arguments

- *int* **index** - Warping control point index. The point with the 0 index is in the bottom left corner with the progression going upwards, and then to the next column bottom point.
- *int* **type** - Type of control handle of the warping control point.

### Return value

Screen-space coordinates of the point.
## void setPointHandleSmoothType ( int x , int y , int smooth_type )

Sets the type of line curving for the handle point of the specified warp grid point.
### Arguments

- *int* **x** - Position of the warping control point in the row, starting from 0 on the left.
- *int* **y** - Position of the warping control point in the column, starting from 0 at the bottom.
- *int* **smooth_type** - The type of line curving for the handle point.

## void setPointHandleSmoothType ( int index , int smooth_type )

Sets the type of line curving for the handle point of the specified warp grid point.
### Arguments

- *int* **index** - Warping control point index. The point with the 0 index is in the bottom left corner with the progression going upwards, and then to the next column bottom point.
- *int* **smooth_type** - The type of line curving for the handle point.

## int getPointHandleSmoothType ( int x , int y )

Returns the type of line curving for the handle point of the specified warp grid point.
### Arguments

- *int* **x** - Position of the warping control point in the row, starting from 0 on the left.
- *int* **y** - Position of the warping control point in the column, starting from 0 at the bottom.

### Return value

The type of line curving for the handle point.
## int getPointHandleSmoothType ( int index )

Returns the type of line curving for the handle point of the specified warp grid point.
### Arguments

- *int* **index** - Warping control point index. The point with the 0 index is in the bottom left corner with the progression going upwards, and then to the next column bottom point.

### Return value

The type of line curving for the handle point.
## void saveXml ( Xml xml )

Saves the warp grid data to the given instance of the Xml class.
### Arguments

- *[Xml](../../../../api/library/common/class.xml_usc.md)* **xml** - [Xml class](../../../../api/library/common/class.xml_usc.md) instance into which the data will be saved.

## int restoreXml ( Xml xml )

Loads the warp grid data from the specified instance of the Xml class.
### Arguments

- *[Xml](../../../../api/library/common/class.xml_usc.md)* **xml** - [Xml class](../../../../api/library/common/class.xml_usc.md) instance the data from which is to be loaded.

### Return value

**1** if the data has been loaded successfully, otherwise **0**.
## void save ( Stream stream )

Saves the warp grid data to the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_usc.md)* **stream** - Stream to which the data is to be written.

## void restore ( Stream stream )

Loads the warp grid data from the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_usc.md)* **stream** - Stream the data from which is to be loaded.
