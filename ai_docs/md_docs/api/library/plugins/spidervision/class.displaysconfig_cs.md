# Unigine::Plugins::SpiderVision::DisplaysConfig Class (CS)


The object of this class describes the current configuration, stores information about all viewports and groups of the current configuration and provides an interface to interact with them.


## DisplaysConfig Class

### Properties

## 🔒︎ string Path

The path to the displays configuration file.
## 🔒︎ uint NumViewports

The total number of viewports in the configuration.
## 🔒︎ uint NumGroups

The total number of projection groups in the configuration.
## Input.KEY ShowHotkey

The hotkey that opens the displays configuration window.
## 🔒︎ Event< ViewportData > EventViewportCreated

The event triggered when a viewport is created. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(ViewportData **viewport_data**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the ViewportCreated event handler
void viewportcreated_event_handler(ViewportData viewport_data)
{
	Log.Message("\Handling ViewportCreated event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections viewportcreated_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
DisplaysConfig.EventViewportCreated.Connect(viewportcreated_event_connections, viewportcreated_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
DisplaysConfig.EventViewportCreated.Connect(viewportcreated_event_connections, (ViewportData viewport_data) => {
		Log.Message("Handling ViewportCreated event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
viewportcreated_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the ViewportCreated event with a handler function
DisplaysConfig.EventViewportCreated.Connect(viewportcreated_event_handler);

// remove subscription to the ViewportCreated event later by the handler function
DisplaysConfig.EventViewportCreated.Disconnect(viewportcreated_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection viewportcreated_event_connection;

// subscribe to the ViewportCreated event with a lambda handler function and keeping the connection
viewportcreated_event_connection = DisplaysConfig.EventViewportCreated.Connect((ViewportData viewport_data) => {
		Log.Message("Handling ViewportCreated event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
viewportcreated_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
viewportcreated_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
viewportcreated_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring ViewportCreated events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
DisplaysConfig.EventViewportCreated.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
DisplaysConfig.EventViewportCreated.Enabled = true;

```

</details>

## 🔒︎ Event< ViewportData > EventViewportRemoved

The event triggered when a viewport is removed. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(ViewportData **viewport_data**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the ViewportRemoved event handler
void viewportremoved_event_handler(ViewportData viewport_data)
{
	Log.Message("\Handling ViewportRemoved event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections viewportremoved_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
DisplaysConfig.EventViewportRemoved.Connect(viewportremoved_event_connections, viewportremoved_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
DisplaysConfig.EventViewportRemoved.Connect(viewportremoved_event_connections, (ViewportData viewport_data) => {
		Log.Message("Handling ViewportRemoved event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
viewportremoved_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the ViewportRemoved event with a handler function
DisplaysConfig.EventViewportRemoved.Connect(viewportremoved_event_handler);

// remove subscription to the ViewportRemoved event later by the handler function
DisplaysConfig.EventViewportRemoved.Disconnect(viewportremoved_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection viewportremoved_event_connection;

// subscribe to the ViewportRemoved event with a lambda handler function and keeping the connection
viewportremoved_event_connection = DisplaysConfig.EventViewportRemoved.Connect((ViewportData viewport_data) => {
		Log.Message("Handling ViewportRemoved event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
viewportremoved_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
viewportremoved_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
viewportremoved_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring ViewportRemoved events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
DisplaysConfig.EventViewportRemoved.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
DisplaysConfig.EventViewportRemoved.Enabled = true;

```

</details>

## 🔒︎ Event EventLoad

The event triggered on loading a displays configuration from a file. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Load event handler
void load_event_handler()
{
	Log.Message("\Handling Load event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections load_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
DisplaysConfig.EventLoad.Connect(load_event_connections, load_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
DisplaysConfig.EventLoad.Connect(load_event_connections, () => {
		Log.Message("Handling Load event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
load_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Load event with a handler function
DisplaysConfig.EventLoad.Connect(load_event_handler);

// remove subscription to the Load event later by the handler function
DisplaysConfig.EventLoad.Disconnect(load_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection load_event_connection;

// subscribe to the Load event with a lambda handler function and keeping the connection
load_event_connection = DisplaysConfig.EventLoad.Connect(() => {
		Log.Message("Handling Load event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
load_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
load_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
load_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Load events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
DisplaysConfig.EventLoad.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
DisplaysConfig.EventLoad.Enabled = true;

```

</details>

## 🔒︎ Event EventClear

The event triggered on clearing displays configuration. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Clear event handler
void clear_event_handler()
{
	Log.Message("\Handling Clear event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections clear_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
DisplaysConfig.EventClear.Connect(clear_event_connections, clear_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
DisplaysConfig.EventClear.Connect(clear_event_connections, () => {
		Log.Message("Handling Clear event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
clear_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Clear event with a handler function
DisplaysConfig.EventClear.Connect(clear_event_handler);

// remove subscription to the Clear event later by the handler function
DisplaysConfig.EventClear.Disconnect(clear_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection clear_event_connection;

// subscribe to the Clear event with a lambda handler function and keeping the connection
clear_event_connection = DisplaysConfig.EventClear.Connect(() => {
		Log.Message("Handling Clear event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
clear_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
clear_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
clear_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Clear events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
DisplaysConfig.EventClear.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
DisplaysConfig.EventClear.Enabled = true;

```

</details>

## 🔒︎ Event< CalibrationGridData > EventCalibrationGridChanged

The event triggered on making changes to the calibration grid. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(CalibrationGridData **calibration_data**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the CalibrationGridChanged event handler
void calibrationgridchanged_event_handler(CalibrationGridData calibration_data)
{
	Log.Message("\Handling CalibrationGridChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections calibrationgridchanged_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
DisplaysConfig.EventCalibrationGridChanged.Connect(calibrationgridchanged_event_connections, calibrationgridchanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
DisplaysConfig.EventCalibrationGridChanged.Connect(calibrationgridchanged_event_connections, (CalibrationGridData calibration_data) => {
		Log.Message("Handling CalibrationGridChanged event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
calibrationgridchanged_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the CalibrationGridChanged event with a handler function
DisplaysConfig.EventCalibrationGridChanged.Connect(calibrationgridchanged_event_handler);

// remove subscription to the CalibrationGridChanged event later by the handler function
DisplaysConfig.EventCalibrationGridChanged.Disconnect(calibrationgridchanged_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection calibrationgridchanged_event_connection;

// subscribe to the CalibrationGridChanged event with a lambda handler function and keeping the connection
calibrationgridchanged_event_connection = DisplaysConfig.EventCalibrationGridChanged.Connect((CalibrationGridData calibration_data) => {
		Log.Message("Handling CalibrationGridChanged event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
calibrationgridchanged_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
calibrationgridchanged_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
calibrationgridchanged_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring CalibrationGridChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
DisplaysConfig.EventCalibrationGridChanged.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
DisplaysConfig.EventCalibrationGridChanged.Enabled = true;

```

</details>

## vec3 HeadPosition

The position of the viewer's head (the eye origin) in the projection coordinate space, in meters: the camera position from which the off-axis view and projection of each display viewport are computed. In stereo mode the two eyes are offset from it along the head's horizontal axis. Head tracking is injected by writing this value every frame.
## quat HeadRotation

The orientation of the viewer's head in the projection coordinate space. It defines the inter-eye axis along which the eyes are separated in stereo mode.
## 🔒︎ Event< Math::mat4> EventHeadTransformChanged

The The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the HeadTransformChanged event handler
void headtransformchanged_event_handler()
{
	Log.Message("\Handling HeadTransformChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections headtransformchanged_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventHeadTransformChanged.Connect(headtransformchanged_event_connections, headtransformchanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventHeadTransformChanged.Connect(headtransformchanged_event_connections, () => {
		Log.Message("Handling HeadTransformChanged event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
headtransformchanged_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the HeadTransformChanged event with a handler function
publisher.EventHeadTransformChanged.Connect(headtransformchanged_event_handler);

// remove subscription to the HeadTransformChanged event later by the handler function
publisher.EventHeadTransformChanged.Disconnect(headtransformchanged_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection headtransformchanged_event_connection;

// subscribe to the HeadTransformChanged event with a lambda handler function and keeping the connection
headtransformchanged_event_connection = publisher.EventHeadTransformChanged.Connect(() => {
		Log.Message("Handling HeadTransformChanged event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
headtransformchanged_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
headtransformchanged_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
headtransformchanged_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring HeadTransformChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventHeadTransformChanged.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventHeadTransformChanged.Enabled = true;

```

</details>

### Members

---

## ViewportData GetViewportByIndex ( int index )

Returns the data for the specified viewport by the index (a value from 0 to the [total number of viewports](#getNumViewports_uint)). Index has a temporary correlation with the viewport ID, which may change as the number of viewports is updated. Addressing to a viewport by index implies that the index refers to the viewport ID, which in turn refers to the ViewportData corresponding to that ID.
This method may be applied as follows:


```csharp
for(int i =0; i < config.NumViewports; ++i)
{
	var viewport = config.GetViewportByIndex(i);
	// ... required actions with viewport
}

```


### Arguments

- *int* **index** - Index of the viewport, a value from 0 to the [total number of viewports](#getNumViewports_uint). Index has a temporary correlation with the viewport ID, which may change as the number of viewports is updated. Addressing to a viewport by index implies that the index refers to the viewport ID, which in turn refers to the ViewportData corresponding to that ID.

### Return value

[ViewportData class](../../../../api/library/plugins/spidervision/class.viewportdata_cs.md) instance that stores the viewport data.
## ViewportData GetViewport ( int id )

Returns the viewport by the specified ID.
### Arguments

- *int* **id** - Viewport ID.

### Return value

[ViewportData class](../../../../api/library/plugins/spidervision/class.viewportdata_cs.md) instance that stores the viewport data.
## ViewportData CreateViewport ( int group_id = -1 )

Creates a viewport for the specified viewport group. If no group is set, an individual viewport is created.
### Arguments

- *int* **group_id** - ID of the group. The default value of -1 means that the viewport is not related to any group.

### Return value

[ViewportData class](../../../../api/library/plugins/spidervision/class.viewportdata_cs.md) instance that stores the viewport data.
## void RemoveViewport ( int id )

Removes the specified viewport.
### Arguments

- *int* **id** - ID of the viewport.

## GroupData GetGroupByIndex ( int index )

Returns the group with the specified index.
### Arguments

- *int* **index** - Index of the group, a value from 0 to the [total number of viewport groups](#getNumGroups_uint).

### Return value

[GroupData class](../../../../api/library/plugins/spidervision/class.groupdata_cs.md) instance that stores the group data.
## GroupData GetGroup ( int id )

Returns the viewport group by the specified ID.
### Arguments

- *int* **id** - ID of the group.

### Return value

[GroupData class](../../../../api/library/plugins/spidervision/class.groupdata_cs.md) instance that stores the group data.
## GroupData CreateGroup ( GroupData.GROUP_TYPE type )

Creates the group of the specified type.
### Arguments

- *[GroupData.GROUP_TYPE](../../../../api/library/plugins/spidervision/class.groupdata_cs.md#GROUP_TYPE)* **type** - Type of the group.

### Return value

[GroupData class](../../../../api/library/plugins/spidervision/class.groupdata_cs.md) instance that stores the group data.
## void RemoveGroup ( int id )

Removes the group with the specified ID.
### Arguments

- *int* **id** - ID of the group.

## CalibrationGridData GetCalibrationGrid ( )

Returns the calibration grid for the configuration.
### Return value

[CalibrationGridData class](../../../../api/library/plugins/spidervision/class.calibrationgriddata_cs.md) instance that stores the calibration grid data.
## bool HasUnsavedChanges ( )

Returns the value indicating if the displays configuration has any unsaved changes.
### Return value

true if the displays configuration has any unsaved changes, otherwise false.
## bool LoadConfig ( string filepath )

Loads the configuration from the specified source.
### Arguments

- *string* **filepath** - Path to the displays configuration file.

### Return value

true if the configuration file is loaded successfully, otherwise false.
## void LoadConfig ( Stream stream )

Loads the configuration data from the specified source.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_cs.md)* **stream** - Stream to read data from.

## bool SaveConfig ( string filepath )

Saves the configuration the specified displays configuration file.
### Arguments

- *string* **filepath** - Path to the displays configuration file.

### Return value

true if the configuration file is saved successfully, otherwise false.
## void Clear ( )

Clears the displays configuration.
## void SaveXml ( Xml xml )

Saves the displays configuration data to the given instance of the Xml class.
### Arguments

- *[Xml](../../../../api/library/common/class.xml_cs.md)* **xml** - [Xml class](../../../../api/library/common/class.xml_cs.md) instance into which the data will be saved.

## bool RestoreXml ( Xml xml )

Loads the displays configuration data from the specified instance of the Xml class.
### Arguments

- *[Xml](../../../../api/library/common/class.xml_cs.md)* **xml** - [Xml class](../../../../api/library/common/class.xml_cs.md) instance the data from which is to be loaded.

### Return value

true if the data has been loaded successfully, otherwise false.
## void Save ( Stream stream )

Saves the displays configuration data to the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_cs.md)* **stream** - Stream to which the data is to be written.

## void Restore ( Stream stream )

Loads the displays configuration data from the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_cs.md)* **stream** - Stream the data from which is to be loaded.

## void LoadConfig ( Xml stream )

Loads the configuration from the XML file.
### Arguments

- *[Xml](../../../../api/library/common/class.xml_cs.md)* **stream** - [Xml class](../../../../api/library/common/class.xml_cs.md) instance the data from which is to be loaded.
