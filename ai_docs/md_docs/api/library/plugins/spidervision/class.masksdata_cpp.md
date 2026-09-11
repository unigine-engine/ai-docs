# Unigine::Plugins::SpiderVision::MasksData Class (CPP)

**Header:** #include <plugins/Unigine/SpiderVision/UnigineSpiderVision.h>


This class stores data on all [masks](../../../../principles/render/output/multi_monitor/spidervision_plugin/projection_setup.md#masks) created for the viewport and provides the interface for configuring each mask.


The mask is an arbitrary shape filled by a selected color that allows cutting out selected areas on the image rendered in the viewport.


This object is accessible via the corresponding method of the [ViewportData](../../../../api/library/plugins/spidervision/class.viewportdata_cpp.md#getMasks_MasksData) class.


The mask data are stored in the [configuration file](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#config_file).


## MasksData Class

### Members

## void setEnabled ( bool enabled )

Sets a new value indicating if masks rendering is enabled.
### Arguments

- *bool* **enabled** - Set **true** to enable rendering of masks; **false** - to disable it.

## bool isEnabled () const

Returns the current value indicating if masks rendering is enabled.
### Return value

**true** if rendering of masks is enabled ; otherwise **false**.
## int getNumMasks () const

Returns the current total number of masks in the configuration.
### Return value

Current total number of masks in the configuration.
## static Event<> getEventChanged () const

event triggered on changing masks data. You can subscribe to events via *connect()* � and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cpp.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cpp.md)* classes for convenience (see examples below).

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
MasksData::getEventChanged().connect(changed_event_connections, changed_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
MasksData::getEventChanged().connect(changed_event_connections, []() {
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
MasksData::getEventChanged().connect(changed_event_connection, changed_event_handler);

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
MasksData::getEventChanged().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
changed_handler_id = MasksData::getEventChanged().connect(e_connections, []() {
		Log::message("\Handling Changed event (lambda).\n");
	}
);

// remove the subscription later using the ID
MasksData::getEventChanged().disconnect(changed_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Changed events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
MasksData::getEventChanged().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
MasksData::getEventChanged().setEnabled(true);

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

## void setMaskName ( int mask , const char * name )

Sets the name for the specified mask.
### Arguments

- *int* **mask** - Mask index.
- *const char ** **name** - Mask name.

## String getMaskName ( int mask ) const

Returns the name for the specified mask.
### Arguments

- *int* **mask** - Mask index.

### Return value

Mask name.
## void setMaskEnabled ( int mask , bool enabled )

Sets the value indicating if rendering of the specified mask is enabled.
### Arguments

- *int* **mask** - Mask index.
- *bool* **enabled** - true to enable rendering of the mask, false to disable it.

## bool isMaskEnabled ( int mask ) const

Returns the value indicating if rendering of the specified mask is enabled.
### Arguments

- *int* **mask** - Mask index.

### Return value

true if rendering of the mask is enabled, otherwise false.
## void setMaskSmoothStep ( int mask , int smooth_step )

Sets smoothing of edges for the specified mask.
### Arguments

- *int* **mask** - Mask index.
- *int* **smooth_step** - Smoothing value, the number of additional points to be inserted between the control points of the mask.

## int getMaskSmoothStep ( int mask ) const

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

## int getNumPoints ( int mask ) const

Returns the total number of points in the mask.
### Arguments

- *int* **mask** - Mask index.

### Return value

Total number of points.
## void setPoint ( int mask , int index , const Math:: vec2 & point )

Sets the coordinates for the specified point in the mask.
### Arguments

- *int* **mask** - Mask index.
- *int* **index** - Point index.
- *const  Math::[vec2](../../../../api/library/math/class.vec2_cpp.md) &* **point** - Point coordinates.

## Math:: vec2 getPoint ( int mask , int index ) const

Returns the coordinates for the specified point in the mask.
### Arguments

- *int* **mask** - Mask index.
- *int* **index** - Point index.

### Return value

Point coordinates.
## void setPointHandleLeft ( int mask , int index , const Math:: vec2 & point )

Sets the left control handle point for the specified point in the mask.
### Arguments

- *int* **mask** - Mask index.
- *int* **index** - Point index.
- *const  Math::[vec2](../../../../api/library/math/class.vec2_cpp.md) &* **point** - Coordinates of left control handle point.

## Math:: vec2 getHandleLeft ( int mask , int index ) const

Returns the left control handle point for the specified point in the mask.
### Arguments

- *int* **mask** - Mask index.
- *int* **index** - Point index.

### Return value

Coordinates of left control handle point.
## void setPointHandleRight ( int mask , int index , const Math:: vec2 & point )

Sets the right control handle point for the specified point in the mask.
### Arguments

- *int* **mask** - Mask index.
- *int* **index** - Point index.
- *const  Math::[vec2](../../../../api/library/math/class.vec2_cpp.md) &* **point** - Coordinates of right control handle point.

## Math:: vec2 getHandleRight ( int mask , int index ) const

Returns the right control handle point for the specified point in the mask.
### Arguments

- *int* **mask** - Mask index.
- *int* **index** - Point index.

### Return value

Coordinates of right control handle point.
## void setPointSmoothType ( int mask , int index , ViewportData::POINT_SMOOTH_TYPE type )

Sets the line curving behavior for the point.
### Arguments

- *int* **mask** - Mask index.
- *int* **index** - Point index.
- *[ViewportData::POINT_SMOOTH_TYPE](../../../../api/library/plugins/spidervision/class.viewportdata_cpp.md#POINT_SMOOTH_TYPE)* **type** - Type of the line curving behavior in the point.

## ViewportData::POINT_SMOOTH_TYPE getPointSmoothType ( int mask , int index ) const

Returns the line curving behavior for the point.
### Arguments

- *int* **mask** - Mask index.
- *int* **index** - Point index.

### Return value

Type of the line curving behavior in the point.
## void saveXml ( const Ptr < Xml > & xml )

Saves the masks data to the given instance of the Xml class.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Xml](../../../../api/library/common/class.xml_cpp.md)> &* **xml** - [Xml class](../../../../api/library/common/class.xml_cpp.md) instance into which the data will be saved.

## bool restoreXml ( const Ptr < Xml > & xml )

Loads the masks data from the specified instance of the Xml class.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Xml](../../../../api/library/common/class.xml_cpp.md)> &* **xml** - [Xml class](../../../../api/library/common/class.xml_cpp.md) instance the data from which is to be loaded.

### Return value

true if the data has been loaded successfully, otherwise false.
## void save ( const Ptr < Stream > & stream )

Saves the masks data to the specified stream.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream to which the data is to be written.

## void restore ( const Ptr < Stream > & stream )

Loads the masks data from the specified stream.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream the data from which is to be loaded.
