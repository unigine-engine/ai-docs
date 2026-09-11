# Unigine::Plugins::SpiderVision::WarpGridData Class (CPP)

**Header:** #include <plugins/Unigine/SpiderVision/UnigineSpiderVision.h>


The object of this class stores the information on the warp grid � a set of points and their handles that create a mesh based on which the displayed image is reshaped.


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

## void setEnabled ( bool enabled )

Sets a new value indicating if the warp grid rendering is enabled.
### Arguments

- *bool* **enabled** - Set **true** to enable rendering of the warp grid; **false** - to disable it.

## bool isEnabled () const

Returns the current value indicating if the warp grid rendering is enabled.
### Return value

**true** if rendering of the warp grid is enabled ; otherwise **false**.
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
## void setCanvasFlipMask ( WarpGridData::VIEWPORT_FLIP_TYPE mask )

Sets a new type of flipping the canvas mask for the viewport.
### Arguments

- *[WarpGridData::VIEWPORT_FLIP_TYPE](../../../../api/library/plugins/spidervision/class.warpgriddata_cpp.md#VIEWPORT_FLIP_TYPE)* **mask** - The type of mask flipping.

## WarpGridData::VIEWPORT_FLIP_TYPE getCanvasFlipMask () const

Returns the current type of flipping the canvas mask for the viewport.
### Return value

Current type of mask flipping.
## static Event<> getEventChanged () const

event triggered on changing warp grid data. You can subscribe to events via *connect()* � and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cpp.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cpp.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Changed event handler
void changed_event_handler()
{
	Log::message("\Handling Changed event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections changed_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
WarpGridData::getEventChanged().connect(changed_event_connections, changed_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
WarpGridData::getEventChanged().connect(changed_event_connections, []() {
		Log::message("\Handling Changed event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
changed_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection changed_event_connection;

// subscribe to the Changed event with a handler function keeping the connection
WarpGridData::getEventChanged().connect(changed_event_connection, changed_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
changed_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
changed_event_connection.setEnabled(true);

// ...

// remove subscription to the Changed event via the connection
changed_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A Changed event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling Changed event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
WarpGridData::getEventChanged().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId changed_handler_id;

// subscribe to the Changed event with a lambda handler function and keeping connection ID
changed_handler_id = WarpGridData::getEventChanged().connect(e_connections, []() {
		Log::message("\Handling Changed event (lambda).\n");
	}
);

// remove the subscription later using the ID
WarpGridData::getEventChanged().disconnect(changed_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Changed events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
WarpGridData::getEventChanged().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
WarpGridData::getEventChanged().setEnabled(true);

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
