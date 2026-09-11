# Unigine::Plugins::SpiderVision::DebugData Class (CS)


This object stores the debug data such as the [warp grid](../../../../principles/render/output/multi_monitor/spidervision_plugin/projection_setup.md#warp) state, [blend zone](../../../../principles/render/output/multi_monitor/spidervision_plugin/projection_setup.md#blend) adjustment points, viewport [debug color](../../../../principles/render/output/multi_monitor/spidervision_plugin/projection_setup.md#render_options) filling, etc.


> **Notice:** The debug data are **not** stored in the configuration file.


This object is accessible via the corresponding method of the [ViewportData](../../../../api/library/plugins/spidervision/class.viewportdata_cs.md#getDebug_DebugData) class.


## DebugData Class

### Properties

## bool ShowBlendLines

The value indicating if the visualization is enabled for blend area control lines and selected points on the screen.
## vec2[] BlendPointPositions

The positions of blend area points displayed in the viewport.
## bool ShowGrid

The value indicating if the visualization of warping grid on the screen is enabled.
## bool WarpPointsEnabled

The value indicating if warping control points are displayed in the viewport.
## vec2[] WarpPointPositions

The positions of warping grid control points displayed in the viewport.
## int DebugColorIndex

The indexed color used in debug mode.
> **Notice:** Setting individual colors for different viewports enables you to visualize overlapping regions for different viewports and facilitates the setup process.


## 🔒︎ vec4 DebugColor

The color used in debug mode.
> **Notice:** Setting individual colors for different viewports enables you to visualize overlapping regions for different viewports and facilitates the setup process.


## 🔒︎ Event EventChanged

The event triggered on changing debug data. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

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
DebugData.EventChanged.Connect(changed_event_connections, changed_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
DebugData.EventChanged.Connect(changed_event_connections, () => {
		Log.Message("Handling Changed event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
changed_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Changed event with a handler function
DebugData.EventChanged.Connect(changed_event_handler);

// remove subscription to the Changed event later by the handler function
DebugData.EventChanged.Disconnect(changed_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection changed_event_connection;

// subscribe to the Changed event with a lambda handler function and keeping the connection
changed_event_connection = DebugData.EventChanged.Connect(() => {
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
DebugData.EventChanged.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
DebugData.EventChanged.Enabled = true;

```

</details>

## bool DebugStereo

The value indicating if the real eye images are replaced by solid diagnostic colors in stereo rendering: the left eye receives a solid green image and the right eye a solid red one, so the operator can verify which physical output receives which eye. Disabled by default.
### Members

---

## string GetDebugColorName ( int index )

Returns the name of the debug color by its index.
### Arguments

- *int* **index** - Index of the color used in debug mode.

### Return value

Name of the indexed color.
## int GetNumDebugColors ( )

Returns the total number of indexed debug colors.
### Return value

The total number of indexed debug colors.
## void Save ( Stream stream )

Saves the debug data to the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_cs.md)* **stream** - Stream to which the data is to be written.

## void Restore ( Stream stream )

Loads the debug data from the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_cs.md)* **stream** - Stream the data from which is to be loaded.
