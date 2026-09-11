# Unigine::Plugins::SpiderVision::DisplaysConfig Class (CPP)

**Header:** #include <plugins/Unigine/SpiderVision/UnigineSpiderVision.h>


The object of this class describes the current configuration, stores information about all viewports and groups of the current configuration and provides an interface to interact with them.


## DisplaysConfig Class

### Members

## String getPath () const

Returns the current path to the displays configuration file.
### Return value

Current path to the displays configuration file.
## unsigned int getNumViewports () const

Returns the current total number of viewports in the configuration.
### Return value

Current total number of viewports in the configuration.
## unsigned int getNumGroups () const

Returns the current total number of projection groups in the configuration.
### Return value

Current total number of projection groups in the configuration.
## void setShowHotkey ( Input::KEY hotkey )

Sets a new hotkey that opens the displays configuration window.
### Arguments

- *[Input::KEY](../../../../api/library/controls/class.input_cpp.md#KEY)* **hotkey** - The hotkey that opens the displays configuration window.

## Input::KEY getShowHotkey () const

Returns the current hotkey that opens the displays configuration window.
### Return value

Current hotkey that opens the displays configuration window.
## static Event<ViewportData*> getEventViewportCreated () const

event triggered when a viewport is created. You can subscribe to events via *connect()* � and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cpp.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cpp.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(ViewportData ***viewport_data**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the ViewportCreated event handler
void viewportcreated_event_handler(ViewportData *viewport_data)
{
	Log::message("\Handling ViewportCreated event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections viewportcreated_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
DisplaysConfig::getEventViewportCreated().connect(viewportcreated_event_connections, viewportcreated_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
DisplaysConfig::getEventViewportCreated().connect(viewportcreated_event_connections, [](ViewportData *viewport_data) {
		Log::message("\Handling ViewportCreated event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
viewportcreated_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection viewportcreated_event_connection;

// subscribe to the ViewportCreated event with a handler function keeping the connection
DisplaysConfig::getEventViewportCreated().connect(viewportcreated_event_connection, viewportcreated_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
viewportcreated_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
viewportcreated_event_connection.setEnabled(true);

// ...

// remove subscription to the ViewportCreated event via the connection
viewportcreated_event_connection.disconnect();

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

	// A ViewportCreated event handler implemented as a class member
	void event_handler(ViewportData *viewport_data)
	{
		Log::message("\Handling ViewportCreated event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
DisplaysConfig::getEventViewportCreated().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId viewportcreated_handler_id;

// subscribe to the ViewportCreated event with a lambda handler function and keeping connection ID
viewportcreated_handler_id = DisplaysConfig::getEventViewportCreated().connect(e_connections, [](ViewportData *viewport_data) {
		Log::message("\Handling ViewportCreated event (lambda).\n");
	}
);

// remove the subscription later using the ID
DisplaysConfig::getEventViewportCreated().disconnect(viewportcreated_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all ViewportCreated events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
DisplaysConfig::getEventViewportCreated().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
DisplaysConfig::getEventViewportCreated().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<ViewportData*> getEventViewportRemoved () const

event triggered when a viewport is removed. You can subscribe to events via *connect()* � and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cpp.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cpp.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(ViewportData ***viewport_data**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the ViewportRemoved event handler
void viewportremoved_event_handler(ViewportData *viewport_data)
{
	Log::message("\Handling ViewportRemoved event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections viewportremoved_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
DisplaysConfig::getEventViewportRemoved().connect(viewportremoved_event_connections, viewportremoved_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
DisplaysConfig::getEventViewportRemoved().connect(viewportremoved_event_connections, [](ViewportData *viewport_data) {
		Log::message("\Handling ViewportRemoved event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
viewportremoved_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection viewportremoved_event_connection;

// subscribe to the ViewportRemoved event with a handler function keeping the connection
DisplaysConfig::getEventViewportRemoved().connect(viewportremoved_event_connection, viewportremoved_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
viewportremoved_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
viewportremoved_event_connection.setEnabled(true);

// ...

// remove subscription to the ViewportRemoved event via the connection
viewportremoved_event_connection.disconnect();

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

	// A ViewportRemoved event handler implemented as a class member
	void event_handler(ViewportData *viewport_data)
	{
		Log::message("\Handling ViewportRemoved event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
DisplaysConfig::getEventViewportRemoved().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId viewportremoved_handler_id;

// subscribe to the ViewportRemoved event with a lambda handler function and keeping connection ID
viewportremoved_handler_id = DisplaysConfig::getEventViewportRemoved().connect(e_connections, [](ViewportData *viewport_data) {
		Log::message("\Handling ViewportRemoved event (lambda).\n");
	}
);

// remove the subscription later using the ID
DisplaysConfig::getEventViewportRemoved().disconnect(viewportremoved_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all ViewportRemoved events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
DisplaysConfig::getEventViewportRemoved().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
DisplaysConfig::getEventViewportRemoved().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<> getEventLoad () const

event triggered on a displays configuration from a file. You can subscribe to events via *connect()* � and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cpp.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cpp.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Load event handler
void load_event_handler()
{
	Log::message("\Handling Load event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections load_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
DisplaysConfig::getEventLoad().connect(load_event_connections, load_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
DisplaysConfig::getEventLoad().connect(load_event_connections, []() {
		Log::message("\Handling Load event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
load_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection load_event_connection;

// subscribe to the Load event with a handler function keeping the connection
DisplaysConfig::getEventLoad().connect(load_event_connection, load_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
load_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
load_event_connection.setEnabled(true);

// ...

// remove subscription to the Load event via the connection
load_event_connection.disconnect();

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

	// A Load event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling Load event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
DisplaysConfig::getEventLoad().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId load_handler_id;

// subscribe to the Load event with a lambda handler function and keeping connection ID
load_handler_id = DisplaysConfig::getEventLoad().connect(e_connections, []() {
		Log::message("\Handling Load event (lambda).\n");
	}
);

// remove the subscription later using the ID
DisplaysConfig::getEventLoad().disconnect(load_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Load events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
DisplaysConfig::getEventLoad().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
DisplaysConfig::getEventLoad().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<> getEventClear () const

event triggered on clearing displays configuration. You can subscribe to events via *connect()* � and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cpp.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cpp.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Clear event handler
void clear_event_handler()
{
	Log::message("\Handling Clear event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections clear_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
DisplaysConfig::getEventClear().connect(clear_event_connections, clear_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
DisplaysConfig::getEventClear().connect(clear_event_connections, []() {
		Log::message("\Handling Clear event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
clear_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection clear_event_connection;

// subscribe to the Clear event with a handler function keeping the connection
DisplaysConfig::getEventClear().connect(clear_event_connection, clear_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
clear_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
clear_event_connection.setEnabled(true);

// ...

// remove subscription to the Clear event via the connection
clear_event_connection.disconnect();

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

	// A Clear event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling Clear event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
DisplaysConfig::getEventClear().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId clear_handler_id;

// subscribe to the Clear event with a lambda handler function and keeping connection ID
clear_handler_id = DisplaysConfig::getEventClear().connect(e_connections, []() {
		Log::message("\Handling Clear event (lambda).\n");
	}
);

// remove the subscription later using the ID
DisplaysConfig::getEventClear().disconnect(clear_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Clear events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
DisplaysConfig::getEventClear().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
DisplaysConfig::getEventClear().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<CalibrationGridData*> getEventCalibrationGridChanged () const

event triggered on making changes to the calibration grid. You can subscribe to events via *connect()* � and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cpp.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cpp.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(CalibrationGridData ***calibration_data**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the CalibrationGridChanged event handler
void calibrationgridchanged_event_handler(CalibrationGridData *calibration_data)
{
	Log::message("\Handling CalibrationGridChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections calibrationgridchanged_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
DisplaysConfig::getEventCalibrationGridChanged().connect(calibrationgridchanged_event_connections, calibrationgridchanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
DisplaysConfig::getEventCalibrationGridChanged().connect(calibrationgridchanged_event_connections, [](CalibrationGridData *calibration_data) {
		Log::message("\Handling CalibrationGridChanged event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
calibrationgridchanged_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection calibrationgridchanged_event_connection;

// subscribe to the CalibrationGridChanged event with a handler function keeping the connection
DisplaysConfig::getEventCalibrationGridChanged().connect(calibrationgridchanged_event_connection, calibrationgridchanged_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
calibrationgridchanged_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
calibrationgridchanged_event_connection.setEnabled(true);

// ...

// remove subscription to the CalibrationGridChanged event via the connection
calibrationgridchanged_event_connection.disconnect();

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

	// A CalibrationGridChanged event handler implemented as a class member
	void event_handler(CalibrationGridData *calibration_data)
	{
		Log::message("\Handling CalibrationGridChanged event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
DisplaysConfig::getEventCalibrationGridChanged().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId calibrationgridchanged_handler_id;

// subscribe to the CalibrationGridChanged event with a lambda handler function and keeping connection ID
calibrationgridchanged_handler_id = DisplaysConfig::getEventCalibrationGridChanged().connect(e_connections, [](CalibrationGridData *calibration_data) {
		Log::message("\Handling CalibrationGridChanged event (lambda).\n");
	}
);

// remove the subscription later using the ID
DisplaysConfig::getEventCalibrationGridChanged().disconnect(calibrationgridchanged_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all CalibrationGridChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
DisplaysConfig::getEventCalibrationGridChanged().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
DisplaysConfig::getEventCalibrationGridChanged().setEnabled(true);

```

</details>

### Return value

Event instance.
## void setHeadPosition ( const Math:: vec3 & position )

Sets a new position of the viewer's head (the eye origin) in the projection coordinate space, in meters: the camera position from which the off-axis view and projection of each display viewport are computed. In stereo mode the two eyes are offset from it along the head's horizontal axis. Head tracking is injected by writing this value every frame.
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md)&* **position** - The position of the viewer's head

## Math:: vec3 getHeadPosition () const

Returns the current position of the viewer's head (the eye origin) in the projection coordinate space, in meters: the camera position from which the off-axis view and projection of each display viewport are computed. In stereo mode the two eyes are offset from it along the head's horizontal axis. Head tracking is injected by writing this value every frame.
### Return value

Current position of the viewer's head
## void setHeadRotation ( const Math:: quat & rotation )

Sets a new orientation of the viewer's head in the projection coordinate space. It defines the inter-eye axis along which the eyes are separated in stereo mode.
### Arguments

- *const  Math::[quat](../../../../api/library/math/class.quat_cpp.md)&* **rotation** - The orientation of the viewer's head

## Math:: quat getHeadRotation () const

Returns the current orientation of the viewer's head in the projection coordinate space. It defines the inter-eye axis along which the eyes are separated in stereo mode.
### Return value

Current orientation of the viewer's head
## Event<const Math:: mat4 &> getEventHeadTransformChanged () const

event triggered when the head position or the head rotation changes, carrying the resulting head transformation. You can subscribe to events via *connect()* � and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cpp.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cpp.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Math::mat4 &**head_transform**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the HeadTransformChanged event handler
void headtransformchanged_event_handler(const Math::mat4 &head_transform)
{
	Log::message("\Handling HeadTransformChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections headtransformchanged_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventHeadTransformChanged().connect(headtransformchanged_event_connections, headtransformchanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventHeadTransformChanged().connect(headtransformchanged_event_connections, [](const Math::mat4 &head_transform) {
		Log::message("\Handling HeadTransformChanged event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
headtransformchanged_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection headtransformchanged_event_connection;

// subscribe to the HeadTransformChanged event with a handler function keeping the connection
publisher->getEventHeadTransformChanged().connect(headtransformchanged_event_connection, headtransformchanged_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
headtransformchanged_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
headtransformchanged_event_connection.setEnabled(true);

// ...

// remove subscription to the HeadTransformChanged event via the connection
headtransformchanged_event_connection.disconnect();

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

	// A HeadTransformChanged event handler implemented as a class member
	void event_handler(const Math::mat4 &head_transform)
	{
		Log::message("\Handling HeadTransformChanged event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventHeadTransformChanged().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId headtransformchanged_handler_id;

// subscribe to the HeadTransformChanged event with a lambda handler function and keeping connection ID
headtransformchanged_handler_id = publisher->getEventHeadTransformChanged().connect(e_connections, [](const Math::mat4 &head_transform) {
		Log::message("\Handling HeadTransformChanged event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventHeadTransformChanged().disconnect(headtransformchanged_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all HeadTransformChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventHeadTransformChanged().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventHeadTransformChanged().setEnabled(true);

```

</details>

### Return value

Event instance.
---

## ViewportData * getViewportByIndex ( int index ) const

Returns the data for the specified viewport by the index (a value from 0 to the [total number of viewports](#getNumViewports_uint)). Index has a temporary correlation with the viewport ID, which may change as the number of viewports is updated. Addressing to a viewport by index implies that the index refers to the viewport ID, which in turn refers to the ViewportData corresponding to that ID.
This method may be applied as follows:


```cpp
for(int i = 0; i < config->getNumViewports(); ++i)
{
	auto viewport = config->getViewportByIndex(i);
	// ... required actions with viewport
}

```


### Arguments

- *int* **index** - Index of the viewport, a value from 0 to the [total number of viewports](#getNumViewports_uint). Index has a temporary correlation with the viewport ID, which may change as the number of viewports is updated. Addressing to a viewport by index implies that the index refers to the viewport ID, which in turn refers to the ViewportData corresponding to that ID.

### Return value

[ViewportData class](../../../../api/library/plugins/spidervision/class.viewportdata_cpp.md) instance that stores the viewport data.
## ViewportData * getViewport ( int id ) const

Returns the viewport by the specified ID.
### Arguments

- *int* **id** - Viewport ID.

### Return value

[ViewportData class](../../../../api/library/plugins/spidervision/class.viewportdata_cpp.md) instance that stores the viewport data.
## ViewportData * createViewport ( int group_id = -1 )

Creates a viewport for the specified viewport group. If no group is set, an individual viewport is created.
### Arguments

- *int* **group_id** - ID of the group. The default value of -1 means that the viewport is not related to any group.

### Return value

[ViewportData class](../../../../api/library/plugins/spidervision/class.viewportdata_cpp.md) instance that stores the viewport data.
## void removeViewport ( int id )

Removes the specified viewport.
### Arguments

- *int* **id** - ID of the viewport.

## GroupData * getGroupByIndex ( int index ) const

Returns the group with the specified index.
### Arguments

- *int* **index** - Index of the group, a value from 0 to the [total number of viewport groups](#getNumGroups_uint).

### Return value

[GroupData class](../../../../api/library/plugins/spidervision/class.groupdata_cpp.md) instance that stores the group data.
## GroupData * getGroup ( int id ) const

Returns the viewport group by the specified ID.
### Arguments

- *int* **id** - ID of the group.

### Return value

[GroupData class](../../../../api/library/plugins/spidervision/class.groupdata_cpp.md) instance that stores the group data.
## GroupData * createGroup ( GroupData::GROUP_TYPE type )

Creates the group of the specified type.
### Arguments

- *[GroupData::GROUP_TYPE](../../../../api/library/plugins/spidervision/class.groupdata_cpp.md#GROUP_TYPE)* **type** - Type of the group.

### Return value

[GroupData class](../../../../api/library/plugins/spidervision/class.groupdata_cpp.md) instance that stores the group data.
## void removeGroup ( int id )

Removes the group with the specified ID.
### Arguments

- *int* **id** - ID of the group.

## CalibrationGridData * getCalibrationGrid ( )

Returns the calibration grid for the configuration.
### Return value

[CalibrationGridData class](../../../../api/library/plugins/spidervision/class.calibrationgriddata_cpp.md) instance that stores the calibration grid data.
## bool hasUnsavedChanges ( ) const

Returns the value indicating if the displays configuration has any unsaved changes.
### Return value

true if the displays configuration has any unsaved changes, otherwise false.
## bool loadConfig ( const char * filepath )

Loads the configuration from the specified source.
### Arguments

- *const char ** **filepath** - Path to the displays configuration file.

### Return value

true if the configuration file is loaded successfully, otherwise false.
## void loadConfig ( const Ptr < Stream > & stream )

Loads the configuration data from the specified source.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../../api/library/common/class.stream_cpp.md)> &* **stream** - Source stream pointer.

## bool saveConfig ( const char * filepath )

Saves the configuration the specified displays configuration file.
### Arguments

- *const char ** **filepath** - Path to the displays configuration file.

### Return value

true if the configuration file is saved successfully, otherwise false.
## void clear ( )

Clears the displays configuration.
## void saveXml ( const Ptr < Xml > & xml )

Saves the displays configuration data to the given instance of the Xml class.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Xml](../../../../api/library/common/class.xml_cpp.md)> &* **xml** - [Xml class](../../../../api/library/common/class.xml_cpp.md) instance into which the data will be saved.

## bool restoreXml ( const Ptr < Xml > & xml )

Loads the displays configuration data from the specified instance of the Xml class.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Xml](../../../../api/library/common/class.xml_cpp.md)> &* **xml** - [Xml class](../../../../api/library/common/class.xml_cpp.md) instance the data from which is to be loaded.

### Return value

true if the data has been loaded successfully, otherwise false.
## void save ( const Ptr < Stream > & stream )

Saves the displays configuration data to the specified stream.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream to which the data is to be written.

## void restore ( const Ptr < Stream > & stream )

Loads the displays configuration data from the specified stream.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream the data from which is to be loaded.

## void loadConfig ( const Ptr < Xml > & stream )

Loads the configuration from the XML file.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Xml](../../../../api/library/common/class.xml_cpp.md)> &* **stream** - [Xml class](../../../../api/library/common/class.xml_cpp.md) instance the data from which is to be loaded.
