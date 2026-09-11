# Unigine::Plugins::SpiderVision::Manager Class (CS)

> **Notice:** This class is a singleton.


This class provides auxiliary functions for configuring the plugin, as well as access to an object of [DisplaysConfig](../../../../api/library/plugins/spidervision/class.displaysconfig_cs.md) class.


## Manager Class

### Properties

## 🔒︎ DisplaysConfig Config

The *[DisplaysConfig](../../../../api/library/plugins/spidervision/class.displaysconfig_cs.md)* class instance that stores the complete configuration data.
## string ComputerName

The name of the computer on which the viewport is to be displayed. If this parameter is not set, the viewport can be displayed on any PC. If set, the viewport is only displayed on the PC that has a matching name.
## bool ConfiguratorEnabled

The value indicating if the configurator window is open.
## 🔒︎ Event EventComputerNameChanged

The event triggered on changing a computer name. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the ComputerNameChanged event handler
void computernamechanged_event_handler()
{
	Log.Message("\Handling ComputerNameChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections computernamechanged_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Manager.EventComputerNameChanged.Connect(computernamechanged_event_connections, computernamechanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Manager.EventComputerNameChanged.Connect(computernamechanged_event_connections, () => {
		Log.Message("Handling ComputerNameChanged event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
computernamechanged_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the ComputerNameChanged event with a handler function
Manager.EventComputerNameChanged.Connect(computernamechanged_event_handler);

// remove subscription to the ComputerNameChanged event later by the handler function
Manager.EventComputerNameChanged.Disconnect(computernamechanged_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection computernamechanged_event_connection;

// subscribe to the ComputerNameChanged event with a lambda handler function and keeping the connection
computernamechanged_event_connection = Manager.EventComputerNameChanged.Connect(() => {
		Log.Message("Handling ComputerNameChanged event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
computernamechanged_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
computernamechanged_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
computernamechanged_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring ComputerNameChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Manager.EventComputerNameChanged.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Manager.EventComputerNameChanged.Enabled = true;

```

</details>

### Members

---

## int FindViewportID ( string viewport_name )

Returns the of the viewport window with the specified name.
### Arguments

- *string* **viewport_name** - Name of the viewport.

### Return value

ID of the viewport window with the specified name if it exists, otherwise -1.
## int FindGroupID ( string group_name )

Returns the of the viewport group with the specified name.
### Arguments

- *string* **group_name** - Name of the viewport group.

### Return value

ID of the viewport group with the specified name if it exists, otherwise -1.
## void SetProjectionEnabled ( int viewport_id , bool enabled )

Sets a value indicating if the projection for the specified viewport (correction of the image according to projection) is enabled. If disabled, the image is rendered as seen from the point of view without any distortions (i.e. regardless of the viewport plane position in the configuration space). If enabled, the image takes into account the projection angle (i.e. the viewport plane position relative to the point of view in the configuration space) and distorts the rendered image accordingly.
### Arguments

- *int* **viewport_id** - ID of the viewport window.
- *bool* **enabled** - true to enable [projection for the specified viewport](../../../../ig/index.md#interpolation); false - to disable.

## void SetViewportCustomPlayer ( int viewport_id , Player player )

Assigns a player to the specified viewport.
### Arguments

- *int* **viewport_id** - ID of the viewport window.
- *[Player](../../../../api/library/players/class.player_cs.md)* **player** - The player camera.

## void SetGroupCustomPlayer ( int group_id , Player player )

Assigns a player to the specified group of viewports.
### Arguments

- *int* **group_id** - ID of the viewport group.
- *[Player](../../../../api/library/players/class.player_cs.md)* **player** - The player camera.

## EngineWindowViewport GetEngineWindow ( int viewport_id )

Returns the engine window viewport for the specified viewport.
### Arguments

- *int* **viewport_id** - ID of the viewport window.

### Return value

The engine window viewport.
## Player GetViewportCustomPlayer ( int viewport_id )

Returns the custom player previously assigned to the given viewport's window via **[SetViewportCustomPlayer()](../../../...md#setViewportCustomPlayer_int_Player_void)**.
### Arguments

- *int* **viewport_id** - ID of the viewport.

### Return value

Custom player assigned to the viewport's window, or null if the viewport does not exist or no custom player is set (rendering then falls back to the game player).
