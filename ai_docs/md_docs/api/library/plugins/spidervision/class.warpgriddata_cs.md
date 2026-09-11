# Unigine::Plugins::SpiderVision::WarpGridData Class (CS)


The object of this class stores the information on the warp grid � a set of points and their handles that create a mesh based on which the displayed image is reshaped.


Warping of the image is required to render the projected image on a distorted surface in such a way that it would look undistorted.


This object is accessible via the corresponding method of the [ViewportData](../../../../api/library/plugins/spidervision/class.viewportdata_cs.md#getWarpGrid_WarpGridData) class.


The mask data are stored in the [configuration file](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#config_file).


## WarpGridData Class

### Enums

## VIEWPORT_FLIP_TYPE

| Name | Description |
|---|---|
| **NONE** = 0 | The canvas mask is not flipped. |
| **VERTICAL** = 1 | The canvas mask is flipped vertically. |
| **HORIZONTAL** = 2 | The canvas mask is flipped horizontally. |
| **BOTH** = 3 | The canvas mask is flipped both vertically and horizontally. |

## WARP_HANDLE_ROLE

| Name | Description |
|---|---|
| **LEFT** = 0 | Left-side control handle of the warping control point on the grid. |
| **RIGHT** = 1 | Right-side control handle of the warping control point on the grid. |
| **UP** = 2 | Top-side control handle of the warping control point on the grid. |
| **DOWN** = 3 | Bottom-side control handle of the warping control point on the grid. |
| **NUM** = 4 | Total number of control handles of the warping control point. |

### Properties

## bool Enabled

The value indicating if the warp grid rendering is enabled.
## 🔒︎ int NumRows

The number of warping grid points vertically in the warp grid, which define the grid rows.
## 🔒︎ int NumColumns

The number of warping grid points horizontally in the warp grid, which define the grid columns.
## 🔒︎ int WarpPointsCount

The total number of points in the warp grid.
## WarpGridData.VIEWPORT_FLIP_TYPE CanvasFlipMask

The type of flipping the canvas mask for the viewport.
## 🔒︎ Event EventChanged

The event triggered on changing warp grid data. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Changed event handler
void changed_event_handler()
{
	Log.Message("\Handling Changed event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections changed_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
WarpGridData.EventChanged.Connect(changed_event_connections, changed_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
WarpGridData.EventChanged.Connect(changed_event_connections, () => {
		Log.Message("Handling Changed event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
changed_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Changed event with a handler function
WarpGridData.EventChanged.Connect(changed_event_handler);

// remove subscription to the Changed event later by the handler function
WarpGridData.EventChanged.Disconnect(changed_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection changed_event_connection;

// subscribe to the Changed event with a lambda handler function and keeping the connection
changed_event_connection = WarpGridData.EventChanged.Connect(() => {
		Log.Message("Handling Changed event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
changed_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
changed_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
changed_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Changed events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
WarpGridData.EventChanged.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
WarpGridData.EventChanged.Enabled = true;

```

</details>

### Members

---

## void SetGridSize ( int row , int column )

Sets the number of columns and rows on the warping grid.
### Arguments

- *int* **row** - Number of grid rows.
- *int* **column** - Number of grid columns.

## void SetPoint ( int x , int y , vec2 point )

Sets the coordinates of the warping control point on the grid.
### Arguments

- *int* **x** - Position of the warping control point in the row, starting from 0 on the left.
- *int* **y** - Position of the warping control point in the column, starting from 0 at the bottom.
- *vec2* **point** - Screen-space coordinates of the point.

## void SetPoint ( int index , vec2 point )

Sets the coordinates of the warping control point on the grid.
### Arguments

- *int* **index** - Warping control point index. The point with the 0 index is in the bottom left corner with the progression going upwards, and then to the next column bottom point.
- *vec2* **point** - Screen-space coordinates of the point.

## vec2 GetPoint ( int x , int y )

Returns the coordinates of the warping control point on the grid.
### Arguments

- *int* **x** - Position of the warping control point in the row, starting from 0 on the left.
- *int* **y** - Position of the warping control point in the column, starting from 0 at the bottom.

### Return value

Screen-space coordinates of the point.
## vec2 GetPoint ( int index )

Returns the coordinates of the warping control point on the grid.
### Arguments

- *int* **index** - Warping control point index. The point with the 0 index is in the bottom left corner with the progression going upwards, and then to the next column bottom point.

### Return value

Screen-space coordinates of the point.
## void SetPointHandle ( int x , int y , WarpGridData.WARP_HANDLE_ROLE type , vec2 point )

Sets the type and position of the handle point for the specified warp grid point.
### Arguments

- *int* **x** - Position of the warping control point in the row, starting from 0 on the left.
- *int* **y** - Position of the warping control point in the column, starting from 0 at the bottom.
- *[WarpGridData.WARP_HANDLE_ROLE](../../../../api/library/plugins/spidervision/class.warpgriddata_cs.md#WARP_HANDLE_ROLE)* **type** - Type of control handle of the warping control point.
- *vec2* **point** - Screen-space coordinates of the point.

## void SetPointHandle ( int index , WarpGridData.WARP_HANDLE_ROLE type , vec2 point )

Sets the type and position of the handle point for the specified warp grid point.
### Arguments

- *int* **index** - Warping control point index. The point with the 0 index is in the bottom left corner with the progression going upwards, and then to the next column bottom point.
- *[WarpGridData.WARP_HANDLE_ROLE](../../../../api/library/plugins/spidervision/class.warpgriddata_cs.md#WARP_HANDLE_ROLE)* **type** - Type of control handle of the warping control point.
- *vec2* **point** - Screen-space coordinates of the point.

## vec2 GetPointHandle ( int x , int y , WarpGridData.WARP_HANDLE_ROLE type )

Returns the type and position of the handle point for the specified warp grid point.
### Arguments

- *int* **x** - Position of the warping control point in the row, starting from 0 on the left.
- *int* **y** - Position of the warping control point in the column, starting from 0 at the bottom.
- *[WarpGridData.WARP_HANDLE_ROLE](../../../../api/library/plugins/spidervision/class.warpgriddata_cs.md#WARP_HANDLE_ROLE)* **type** - Type of control handle of the warping control point.

### Return value

Screen-space coordinates of the point.
## vec2 GetPointHandle ( int index , WarpGridData.WARP_HANDLE_ROLE type )

Returns the type and position of the handle point for the specified warp grid point.
### Arguments

- *int* **index** - Warping control point index. The point with the 0 index is in the bottom left corner with the progression going upwards, and then to the next column bottom point.
- *[WarpGridData.WARP_HANDLE_ROLE](../../../../api/library/plugins/spidervision/class.warpgriddata_cs.md#WARP_HANDLE_ROLE)* **type** - Type of control handle of the warping control point.

### Return value

Screen-space coordinates of the point.
## void SetPointHandleSmoothType ( int x , int y , ViewportData.POINT_SMOOTH_TYPE smooth_type )

Sets the type of line curving for the handle point of the specified warp grid point.
### Arguments

- *int* **x** - Position of the warping control point in the row, starting from 0 on the left.
- *int* **y** - Position of the warping control point in the column, starting from 0 at the bottom.
- *[ViewportData.POINT_SMOOTH_TYPE](../../../../api/library/plugins/spidervision/class.viewportdata_cs.md#POINT_SMOOTH_TYPE)* **smooth_type** - The type of line curving for the handle point.

## void SetPointHandleSmoothType ( int index , ViewportData.POINT_SMOOTH_TYPE smooth_type )

Sets the type of line curving for the handle point of the specified warp grid point.
### Arguments

- *int* **index** - Warping control point index. The point with the 0 index is in the bottom left corner with the progression going upwards, and then to the next column bottom point.
- *[ViewportData.POINT_SMOOTH_TYPE](../../../../api/library/plugins/spidervision/class.viewportdata_cs.md#POINT_SMOOTH_TYPE)* **smooth_type** - The type of line curving for the handle point.

## ViewportData.POINT_SMOOTH_TYPE GetPointHandleSmoothType ( int x , int y )

Returns the type of line curving for the handle point of the specified warp grid point.
### Arguments

- *int* **x** - Position of the warping control point in the row, starting from 0 on the left.
- *int* **y** - Position of the warping control point in the column, starting from 0 at the bottom.

### Return value

The type of line curving for the handle point.
## ViewportData.POINT_SMOOTH_TYPE GetPointHandleSmoothType ( int index )

Returns the type of line curving for the handle point of the specified warp grid point.
### Arguments

- *int* **index** - Warping control point index. The point with the 0 index is in the bottom left corner with the progression going upwards, and then to the next column bottom point.

### Return value

The type of line curving for the handle point.
## void SaveXml ( Xml xml )

Saves the warp grid data to the given instance of the Xml class.
### Arguments

- *[Xml](../../../../api/library/common/class.xml_cs.md)* **xml** - [Xml class](../../../../api/library/common/class.xml_cs.md) instance into which the data will be saved.

## bool RestoreXml ( Xml xml )

Loads the warp grid data from the specified instance of the Xml class.
### Arguments

- *[Xml](../../../../api/library/common/class.xml_cs.md)* **xml** - [Xml class](../../../../api/library/common/class.xml_cs.md) instance the data from which is to be loaded.

### Return value

true if the data has been loaded successfully, otherwise false.
## void Save ( Stream stream )

Saves the warp grid data to the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_cs.md)* **stream** - Stream to which the data is to be written.

## void Restore ( Stream stream )

Loads the warp grid data from the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_cs.md)* **stream** - Stream the data from which is to be loaded.
