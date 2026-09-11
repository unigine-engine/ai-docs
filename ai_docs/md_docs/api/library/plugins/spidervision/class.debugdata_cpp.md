# Unigine::Plugins::SpiderVision::DebugData Class (CPP)

**Header:** #include <plugins/Unigine/SpiderVision/UnigineSpiderVision.h>


This object stores the debug data such as the [warp grid](../../../../principles/render/output/multi_monitor/spidervision_plugin/projection_setup.md#warp) state, [blend zone](../../../../principles/render/output/multi_monitor/spidervision_plugin/projection_setup.md#blend) adjustment points, viewport [debug color](../../../../principles/render/output/multi_monitor/spidervision_plugin/projection_setup.md#render_options) filling, etc.


> **Notice:** The debug data are **not** stored in the configuration file.


This object is accessible via the corresponding method of the [ViewportData](../../../../api/library/plugins/spidervision/class.viewportdata_cpp.md#getDebug_DebugData) class.


## DebugData Class

### Members

## void setShowBlendLines ( bool lines )

Sets a new value indicating if the visualization is enabled for blend area control lines and selected points on the screen.
### Arguments

- *bool* **lines** - Set **true** to enable visualization of blend area control lines and points; **false** - to disable it.

## bool isShowBlendLines () const

Returns the current value indicating if the visualization is enabled for blend area control lines and selected points on the screen.
### Return value

**true** if visualization of blend area control lines and points is enabled ; otherwise **false**.
## void setBlendPointPositions ( const Vector < Math:: vec2 >& positions )

Sets a new positions of blend area points displayed in the viewport.
### Arguments

- *const [Vector](../../../../api/library/containers/vector/class.vector_cpp.md)< Math::[vec2](../../../../api/library/math/class.vec2_cpp.md)>&* **positions** - The vector containing positions of blend area points displayed in the viewport.

## Vector < Math:: vec2 > getBlendPointPositions () const

Returns the current positions of blend area points displayed in the viewport.
### Return value

Current vector containing positions of blend area points displayed in the viewport.
## void setShowGrid ( bool grid )

Sets a new value indicating if the visualization of warping grid on the screen is enabled.
### Arguments

- *bool* **grid** - Set **true** to enable visualization of warping grid; **false** - to disable it.

## bool isShowGrid () const

Returns the current value indicating if the visualization of warping grid on the screen is enabled.
### Return value

**true** if visualization of warping grid is enabled ; otherwise **false**.
## void setWarpPointsEnabled ( bool enabled )

Sets a new value indicating if warping control points are displayed in the viewport.
### Arguments

- *bool* **enabled** - Set **true** to enable display of warping control points; **false** - to disable it.

## bool isWarpPointsEnabled () const

Returns the current value indicating if warping control points are displayed in the viewport.
### Return value

**true** if display of warping control points is enabled ; otherwise **false**.
## void setWarpPointPositions ( const Vector < Math:: vec2 >& positions )

Sets a new positions of warping grid control points displayed in the viewport.
### Arguments

- *const [Vector](../../../../api/library/containers/vector/class.vector_cpp.md)< Math::[vec2](../../../../api/library/math/class.vec2_cpp.md)>&* **positions** - The vector containing positions of warping grid points displayed in the viewport.

## Vector < Math:: vec2 > getWarpPointPositions () const

Returns the current positions of warping grid control points displayed in the viewport.
### Return value

Current vector containing positions of warping grid points displayed in the viewport.
## void setDebugColorIndex ( int index )

Sets a new indexed color used in debug mode.
> **Notice:** Setting individual colors for different viewports enables you to visualize overlapping regions for different viewports and facilitates the setup process.


### Arguments

- *int* **index** - The color used in debug mode, one of the following values:

  - **0** - no color
  - **1** - red
  - **2** - green
  - **3** - blue
  - **4** - cyan
  - **5** - magenta
  - **6** - yellow
  - **7** - white
  - **8** - black

## int getDebugColorIndex () const

Returns the current indexed color used in debug mode.
> **Notice:** Setting individual colors for different viewports enables you to visualize overlapping regions for different viewports and facilitates the setup process.


### Return value

Current color used in debug mode, one of the following values:
- **0** - no color
- **1** - red
- **2** - green
- **3** - blue
- **4** - cyan
- **5** - magenta
- **6** - yellow
- **7** - white
- **8** - black


## Math:: vec4 getDebugColor () const

Returns the current color used in debug mode.
> **Notice:** Setting individual colors for different viewports enables you to visualize overlapping regions for different viewports and facilitates the setup process.


### Return value

Current color used in debug mode.
## static Event<> getEventChanged () const

event triggered on changing debug data. You can subscribe to events via *connect()* � and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cpp.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cpp.md)* classes for convenience (see examples below).

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
DebugData::getEventChanged().connect(changed_event_connections, changed_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
DebugData::getEventChanged().connect(changed_event_connections, []() {
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
DebugData::getEventChanged().connect(changed_event_connection, changed_event_handler);

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
DebugData::getEventChanged().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
changed_handler_id = DebugData::getEventChanged().connect(e_connections, []() {
		Log::message("\Handling Changed event (lambda).\n");
	}
);

// remove the subscription later using the ID
DebugData::getEventChanged().disconnect(changed_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Changed events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
DebugData::getEventChanged().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
DebugData::getEventChanged().setEnabled(true);

```

</details>

### Return value

Event instance.
## void setDebugStereo ( bool stereo )

Sets a new value indicating if the real eye images are replaced by solid diagnostic colors in stereo rendering: the left eye receives a solid green image and the right eye a solid red one, so the operator can verify which physical output receives which eye. Disabled by default.
### Arguments

- *bool* **stereo** - Set **true** to enable diagnostic eye-color substitution in stereo mode; **false** - to disable it.

## bool isDebugStereo () const

Returns the current value indicating if the real eye images are replaced by solid diagnostic colors in stereo rendering: the left eye receives a solid green image and the right eye a solid red one, so the operator can verify which physical output receives which eye. Disabled by default.
### Return value

**true** if diagnostic eye-color substitution in stereo mode is enabled ; otherwise **false**.
---

## String getDebugColorName ( int index ) const

Returns the name of the debug color by its index.
### Arguments

- *int* **index** - Index of the color used in debug mode.

### Return value

Name of the indexed color.
## int getNumDebugColors ( ) const

Returns the total number of indexed debug colors.
### Return value

The total number of indexed debug colors.
## void save ( const Ptr < Stream > & stream )

Saves the debug data to the specified stream.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream to which the data is to be written.

## void restore ( const Ptr < Stream > & stream )

Loads the debug data from the specified stream.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream the data from which is to be loaded.
