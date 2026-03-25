# Unigine::Plugins::SpiderVision::WarpGridData Class (CPP)

**Header:** #include <plugins/Unigine/SpiderVision/UnigineSpiderVision.h>


The object of this class stores the information on the warp grid — a set of points and their handles that create a mesh based on which the displayed image is reshaped.


Warping of the image is required to render the projected image on a distorted surface in such a way that it would look undistorted.


This object is accessible via the corresponding method of the [ViewportData](../../../../api/library/plugins/spidervision/class.viewportdata_cpp.md#getWarpGrid_WarpGridData) class.


The mask data are stored in the [configuration file](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#config_file).


## WarpGridData Class

### Enums

## VIEWPORT_FLIP_TYPE

| Name | Description |
|---|---|
| **VIEWPORT_FLIP_TYPE_NONE** = 0 | The canvas mask is not flipped. |
| **VIEWPORT_FLIP_TYPE_VERTICAL** = 1 | The canvas mask is flipped vertically. |
| **VIEWPORT_FLIP_TYPE_HORIZONTAL** = 2 | The canvas mask is flipped horizontally. |
| **VIEWPORT_FLIP_TYPE_BOTH** = 3 | The canvas mask is flipped both vertically and horizontally. |

## WARP_HANDLE_ROLE

| Name | Description |
|---|---|
| **WARP_HANDLE_ROLE_LEFT** = 0 | Left-side control handle of the warping control point on the grid. |
| **WARP_HANDLE_ROLE_RIGHT** = 1 | Right-side control handle of the warping control point on the grid. |
| **WARP_HANDLE_ROLE_UP** = 2 | Top-side control handle of the warping control point on the grid. |
| **WARP_HANDLE_ROLE_DOWN** = 3 | Bottom-side control handle of the warping control point on the grid. |
| **WARP_HANDLE_ROLE_NUM** = 4 | Total number of control handles of the warping control point. |

### Members

---

## void setGridSize ( int row , int column )

Sets the number of columns and rows on the warping grid.
### Arguments

- *int* **row** - Number of grid rows.
- *int* **column** - Number of grid columns.

## void setPoint ( int x , int y , const Math:: vec2 & point )

Sets the coordinates of the warping control point on the grid.
### Arguments

- *int* **x** - Position of the warping control point in the row, starting from 0 on the left.
- *int* **y** - Position of the warping control point in the column, starting from 0 at the bottom.
- *const  Math::[vec2](../../../../api/library/math/class.vec2_cpp.md) &* **point** - Screen-space coordinates of the point.

## void setPoint ( int index , const Math:: vec2 & point )

Sets the coordinates of the warping control point on the grid.
### Arguments

- *int* **index** - Warping control point index. The point with the 0 index is in the bottom left corner with the progression going upwards, and then to the next column bottom point.
- *const  Math::[vec2](../../../../api/library/math/class.vec2_cpp.md) &* **point** - Screen-space coordinates of the point.

## Math:: vec2 getPoint ( int x , int y ) const

Returns the coordinates of the warping control point on the grid.
### Arguments

- *int* **x** - Position of the warping control point in the row, starting from 0 on the left.
- *int* **y** - Position of the warping control point in the column, starting from 0 at the bottom.

### Return value

Screen-space coordinates of the point.
## Math:: vec2 getPoint ( int index ) const

Returns the coordinates of the warping control point on the grid.
### Arguments

- *int* **index** - Warping control point index. The point with the 0 index is in the bottom left corner with the progression going upwards, and then to the next column bottom point.

### Return value

Screen-space coordinates of the point.
## void setPointHandle ( int x , int y , WarpGridData::WARP_HANDLE_ROLE type , const Math:: vec2 & point )

Sets the type and position of the handle point for the specified warp grid point.
### Arguments

- *int* **x** - Position of the warping control point in the row, starting from 0 on the left.
- *int* **y** - Position of the warping control point in the column, starting from 0 at the bottom.
- *[WarpGridData::WARP_HANDLE_ROLE](../../../../api/library/plugins/spidervision/class.warpgriddata_cpp.md#WARP_HANDLE_ROLE)* **type** - Type of control handle of the warping control point.
- *const  Math::[vec2](../../../../api/library/math/class.vec2_cpp.md) &* **point** - Screen-space coordinates of the point.

## void setPointHandle ( int index , WarpGridData::WARP_HANDLE_ROLE type , const Math:: vec2 & point )

Sets the type and position of the handle point for the specified warp grid point.
### Arguments

- *int* **index** - Warping control point index. The point with the 0 index is in the bottom left corner with the progression going upwards, and then to the next column bottom point.
- *[WarpGridData::WARP_HANDLE_ROLE](../../../../api/library/plugins/spidervision/class.warpgriddata_cpp.md#WARP_HANDLE_ROLE)* **type** - Type of control handle of the warping control point.
- *const  Math::[vec2](../../../../api/library/math/class.vec2_cpp.md) &* **point** - Screen-space coordinates of the point.

## Math:: vec2 getPointHandle ( int x , int y , WarpGridData::WARP_HANDLE_ROLE type ) const

Returns the type and position of the handle point for the specified warp grid point.
### Arguments

- *int* **x** - Position of the warping control point in the row, starting from 0 on the left.
- *int* **y** - Position of the warping control point in the column, starting from 0 at the bottom.
- *[WarpGridData::WARP_HANDLE_ROLE](../../../../api/library/plugins/spidervision/class.warpgriddata_cpp.md#WARP_HANDLE_ROLE)* **type** - Type of control handle of the warping control point.

### Return value

Screen-space coordinates of the point.
## Math:: vec2 getPointHandle ( int index , WarpGridData::WARP_HANDLE_ROLE type ) const

Returns the type and position of the handle point for the specified warp grid point.
### Arguments

- *int* **index** - Warping control point index. The point with the 0 index is in the bottom left corner with the progression going upwards, and then to the next column bottom point.
- *[WarpGridData::WARP_HANDLE_ROLE](../../../../api/library/plugins/spidervision/class.warpgriddata_cpp.md#WARP_HANDLE_ROLE)* **type** - Type of control handle of the warping control point.

### Return value

Screen-space coordinates of the point.
## void setPointHandleSmoothType ( int x , int y , ViewportData::POINT_SMOOTH_TYPE smooth_type )

Sets the type of line curving for the handle point of the specified warp grid point.
### Arguments

- *int* **x** - Position of the warping control point in the row, starting from 0 on the left.
- *int* **y** - Position of the warping control point in the column, starting from 0 at the bottom.
- *[ViewportData::POINT_SMOOTH_TYPE](../../../../api/library/plugins/spidervision/class.viewportdata_cpp.md#POINT_SMOOTH_TYPE)* **smooth_type** - The type of line curving for the handle point.

## void setPointHandleSmoothType ( int index , ViewportData::POINT_SMOOTH_TYPE smooth_type )

Sets the type of line curving for the handle point of the specified warp grid point.
### Arguments

- *int* **index** - Warping control point index. The point with the 0 index is in the bottom left corner with the progression going upwards, and then to the next column bottom point.
- *[ViewportData::POINT_SMOOTH_TYPE](../../../../api/library/plugins/spidervision/class.viewportdata_cpp.md#POINT_SMOOTH_TYPE)* **smooth_type** - The type of line curving for the handle point.

## ViewportData::POINT_SMOOTH_TYPE getPointHandleSmoothType ( int x , int y ) const

Returns the type of line curving for the handle point of the specified warp grid point.
### Arguments

- *int* **x** - Position of the warping control point in the row, starting from 0 on the left.
- *int* **y** - Position of the warping control point in the column, starting from 0 at the bottom.

### Return value

The type of line curving for the handle point.
## ViewportData::POINT_SMOOTH_TYPE getPointHandleSmoothType ( int index ) const

Returns the type of line curving for the handle point of the specified warp grid point.
### Arguments

- *int* **index** - Warping control point index. The point with the 0 index is in the bottom left corner with the progression going upwards, and then to the next column bottom point.

### Return value

The type of line curving for the handle point.
## void saveXml ( const Ptr < Xml > & xml )

Saves the warp grid data to the given instance of the Xml class.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Xml](../../../../api/library/common/class.xml_cpp.md)> &* **xml** - [Xml class](../../../../api/library/common/class.xml_cpp.md) instance into which the data will be saved.

## bool restoreXml ( const Ptr < Xml > & xml )

Loads the warp grid data from the specified instance of the Xml class.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Xml](../../../../api/library/common/class.xml_cpp.md)> &* **xml** - [Xml class](../../../../api/library/common/class.xml_cpp.md) instance the data from which is to be loaded.

### Return value

true if the data has been loaded successfully, otherwise false.
## void save ( const Ptr < Stream > & stream )

Saves the warp grid data to the specified stream.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream to which the data is to be written.

## void restore ( const Ptr < Stream > & stream )

Loads the warp grid data from the specified stream.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream the data from which is to be loaded.
