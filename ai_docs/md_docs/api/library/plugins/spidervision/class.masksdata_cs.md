# Unigine::Plugins::SpiderVision::MasksData Class (CS)


This class stores data on all [masks](../../../../principles/render/output/multi_monitor/spidervision_plugin/projection_setup.md#masks) created for the viewport and provides the interface for configuring each mask.


The mask is an arbitrary shape filled by a selected color that allows cutting out selected areas on the image rendered in the viewport.


This object is accessible via the corresponding method of the [ViewportData](../../../../api/library/plugins/spidervision/class.viewportdata_cs.md#getMasks_MasksData) class.


The mask data are stored in the [configuration file](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#config_file).


## MasksData Class

### Properties

## bool Enabled

The value indicating if masks rendering is enabled.
## 🔒︎ int NumMasks

The total number of masks in the configuration.
## 🔒︎ Event EventChanged

The event triggered on changing masks data. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

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
MasksData.EventChanged.Connect(changed_event_connections, changed_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
MasksData.EventChanged.Connect(changed_event_connections, () => {
		Log.Message("Handling Changed event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
changed_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Changed event with a handler function
MasksData.EventChanged.Connect(changed_event_handler);

// remove subscription to the Changed event later by the handler function
MasksData.EventChanged.Disconnect(changed_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection changed_event_connection;

// subscribe to the Changed event with a lambda handler function and keeping the connection
changed_event_connection = MasksData.EventChanged.Connect(() => {
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
MasksData.EventChanged.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
MasksData.EventChanged.Enabled = true;

```

</details>

### Members

---

## void Clear ( )

Clears all masks.
## int AddMask ( )

Adds a new mask.
### Return value

Mask index.
## void RemoveMask ( int index )

Removes the mask with the specified index.
### Arguments

- *int* **index** - Mask index.

## void SetMaskName ( int mask , string name )

Sets the name for the specified mask.
### Arguments

- *int* **mask** - Mask index.
- *string* **name** - Mask name.

## string GetMaskName ( int mask )

Returns the name for the specified mask.
### Arguments

- *int* **mask** - Mask index.

### Return value

Mask name.
## void SetMaskEnabled ( int mask , bool enabled )

Sets the value indicating if rendering of the specified mask is enabled.
### Arguments

- *int* **mask** - Mask index.
- *bool* **enabled** - true to enable rendering of the mask, false to disable it.

## bool IsMaskEnabled ( int mask )

Returns the value indicating if rendering of the specified mask is enabled.
### Arguments

- *int* **mask** - Mask index.

### Return value

true if rendering of the mask is enabled, otherwise false.
## void SetMaskSmoothStep ( int mask , int smooth_step )

Sets smoothing of edges for the specified mask.
### Arguments

- *int* **mask** - Mask index.
- *int* **smooth_step** - Smoothing value, the number of additional points to be inserted between the control points of the mask.

## int GetMaskSmoothStep ( int mask )

Returns the smoothing value for the specified mask.
### Arguments

- *int* **mask** - Mask index.

### Return value

Smoothing value, the number of additional points inserted between the control points of the mask.
## int AddPoint ( int mask )

Adds the point to the mask as the last point in the list of points.
### Arguments

- *int* **mask** - Mask index.

### Return value

Index of the added point.
## int AddPoint ( int mask , int insert_index )

Adds the point to the mask.
### Arguments

- *int* **mask** - Mask index.
- *int* **insert_index** - Point index.

### Return value

Total count of points in the mask.
## void RemovePoint ( int mask , int index )

Removes the point from the mask.
### Arguments

- *int* **mask** - Mask index.
- *int* **index** - Point index.

## int GetNumPoints ( int mask )

Returns the total number of points in the mask.
### Arguments

- *int* **mask** - Mask index.

### Return value

Total number of points.
## void SetPoint ( int mask , int index , vec2 point )

Sets the coordinates for the specified point in the mask.
### Arguments

- *int* **mask** - Mask index.
- *int* **index** - Point index.
- *vec2* **point** - Point coordinates.

## vec2 GetPoint ( int mask , int index )

Returns the coordinates for the specified point in the mask.
### Arguments

- *int* **mask** - Mask index.
- *int* **index** - Point index.

### Return value

Point coordinates.
## void SetPointHandleLeft ( int mask , int index , vec2 point )

Sets the left control handle point for the specified point in the mask.
### Arguments

- *int* **mask** - Mask index.
- *int* **index** - Point index.
- *vec2* **point** - Coordinates of left control handle point.

## vec2 GetHandleLeft ( int mask , int index )

Returns the left control handle point for the specified point in the mask.
### Arguments

- *int* **mask** - Mask index.
- *int* **index** - Point index.

### Return value

Coordinates of left control handle point.
## void SetPointHandleRight ( int mask , int index , vec2 point )

Sets the right control handle point for the specified point in the mask.
### Arguments

- *int* **mask** - Mask index.
- *int* **index** - Point index.
- *vec2* **point** - Coordinates of right control handle point.

## vec2 GetHandleRight ( int mask , int index )

Returns the right control handle point for the specified point in the mask.
### Arguments

- *int* **mask** - Mask index.
- *int* **index** - Point index.

### Return value

Coordinates of right control handle point.
## void SetPointSmoothType ( int mask , int index , ViewportData.POINT_SMOOTH_TYPE type )

Sets the line curving behavior for the point.
### Arguments

- *int* **mask** - Mask index.
- *int* **index** - Point index.
- *[ViewportData.POINT_SMOOTH_TYPE](../../../../api/library/plugins/spidervision/class.viewportdata_cs.md#POINT_SMOOTH_TYPE)* **type** - Type of the line curving behavior in the point.

## ViewportData.POINT_SMOOTH_TYPE GetPointSmoothType ( int mask , int index )

Returns the line curving behavior for the point.
### Arguments

- *int* **mask** - Mask index.
- *int* **index** - Point index.

### Return value

Type of the line curving behavior in the point.
## void SaveXml ( Xml xml )

Saves the masks data to the given instance of the Xml class.
### Arguments

- *[Xml](../../../../api/library/common/class.xml_cs.md)* **xml** - [Xml class](../../../../api/library/common/class.xml_cs.md) instance into which the data will be saved.

## bool RestoreXml ( Xml xml )

Loads the masks data from the specified instance of the Xml class.
### Arguments

- *[Xml](../../../../api/library/common/class.xml_cs.md)* **xml** - [Xml class](../../../../api/library/common/class.xml_cs.md) instance the data from which is to be loaded.

### Return value

true if the data has been loaded successfully, otherwise false.
## void Save ( Stream stream )

Saves the masks data to the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_cs.md)* **stream** - Stream to which the data is to be written.

## void Restore ( Stream stream )

Loads the masks data from the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_cs.md)* **stream** - Stream the data from which is to be loaded.
