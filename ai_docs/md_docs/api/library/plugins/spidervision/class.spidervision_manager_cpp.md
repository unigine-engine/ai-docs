# Unigine::Plugins::SpiderVision::Manager Class (CPP)

**Header:** #include <plugins/Unigine/SpiderVision/UnigineSpiderVision.h>

> **Notice:** This class is a singleton.


This class provides auxiliary functions for configuring the plugin, as well as access to an object of [DisplaysConfig](../../../../api/library/plugins/spidervision/class.displaysconfig_cpp.md) class.


## Manager Class

### Members

## DisplaysConfig * getConfig () const

Returns the current *[DisplaysConfig](../../../../api/library/plugins/spidervision/class.displaysconfig_cpp.md)* class instance that stores the complete configuration data.
### Return value

Current *[DisplaysConfig](../../../../api/library/plugins/spidervision/class.displaysconfig_cpp.md)* class instance that stores the complete configuration data.
## void setComputerName ( const char * name )

Sets a new name of the computer on which the viewport is to be displayed. If this parameter is not set, the viewport can be displayed on any PC. If set, the viewport is only displayed on the PC that has a matching name.
### Arguments

- *const char ** **name** - The name of the computer on which the viewport is to be displayed.

## String getComputerName () const

Returns the current name of the computer on which the viewport is to be displayed. If this parameter is not set, the viewport can be displayed on any PC. If set, the viewport is only displayed on the PC that has a matching name.
### Return value

Current name of the computer on which the viewport is to be displayed.
## void setConfiguratorEnabled ( bool enabled )

Sets a new value indicating if the configurator window is open.
### Arguments

- *bool* **enabled** - Set **true** to enable the configurator interface; **false** - to disable it.

## bool isConfiguratorEnabled () const

Returns the current value indicating if the configurator window is open.
### Return value

**true** if the configurator interface is enabled ; otherwise **false**.
## static Event<> getEventComputerNameChanged () const

event triggered on changing a computer name. You can subscribe to events via *connect()* � and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cpp.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cpp.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the ComputerNameChanged event handler
void computernamechanged_event_handler()
{
	Log::message("\Handling ComputerNameChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections computernamechanged_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Manager::getEventComputerNameChanged().connect(computernamechanged_event_connections, computernamechanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Manager::getEventComputerNameChanged().connect(computernamechanged_event_connections, []() {
		Log::message("\Handling ComputerNameChanged event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
computernamechanged_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection computernamechanged_event_connection;

// subscribe to the ComputerNameChanged event with a handler function keeping the connection
Manager::getEventComputerNameChanged().connect(computernamechanged_event_connection, computernamechanged_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
computernamechanged_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
computernamechanged_event_connection.setEnabled(true);

// ...

// remove subscription to the ComputerNameChanged event via the connection
computernamechanged_event_connection.disconnect();

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

	// A ComputerNameChanged event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling ComputerNameChanged event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Manager::getEventComputerNameChanged().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId computernamechanged_handler_id;

// subscribe to the ComputerNameChanged event with a lambda handler function and keeping connection ID
computernamechanged_handler_id = Manager::getEventComputerNameChanged().connect(e_connections, []() {
		Log::message("\Handling ComputerNameChanged event (lambda).\n");
	}
);

// remove the subscription later using the ID
Manager::getEventComputerNameChanged().disconnect(computernamechanged_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all ComputerNameChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Manager::getEventComputerNameChanged().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Manager::getEventComputerNameChanged().setEnabled(true);

```

</details>

### Return value

Event instance.
---

## int findViewportID ( const char * viewport_name )

Returns the of the viewport window with the specified name.
### Arguments

- *const char ** **viewport_name** - Name of the viewport.

### Return value

ID of the viewport window with the specified name if it exists, otherwise -1.
## int findGroupID ( const char * group_name )

Returns the of the viewport group with the specified name.
### Arguments

- *const char ** **group_name** - Name of the viewport group.

### Return value

ID of the viewport group with the specified name if it exists, otherwise -1.
## void setProjectionEnabled ( int viewport_id , bool enabled )

Sets a value indicating if the projection for the specified viewport (correction of the image according to projection) is enabled. If disabled, the image is rendered as seen from the point of view without any distortions (i.e. regardless of the viewport plane position in the configuration space). If enabled, the image takes into account the projection angle (i.e. the viewport plane position relative to the point of view in the configuration space) and distorts the rendered image accordingly.
### Arguments

- *int* **viewport_id** - ID of the viewport window.
- *bool* **enabled** - true to enable [projection for the specified viewport](../../../../ig/index.md#interpolation); false - to disable.

## void setViewportCustomPlayer ( int viewport_id , const Ptr < Player > & player )

Assigns a player to the specified viewport.
### Arguments

- *int* **viewport_id** - ID of the viewport window.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Player](../../../../api/library/players/class.player_cpp.md)> &* **player** - The player camera.

## void setGroupCustomPlayer ( int group_id , const Ptr < Player > & player )

Assigns a player to the specified group of viewports.
### Arguments

- *int* **group_id** - ID of the viewport group.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Player](../../../../api/library/players/class.player_cpp.md)> &* **player** - The player camera.

## Ptr < EngineWindowViewport > getEngineWindow ( int viewport_id ) const

Returns the engine window viewport for the specified viewport.
### Arguments

- *int* **viewport_id** - ID of the viewport window.

### Return value

The engine window viewport.
## Ptr < Player > getViewportCustomPlayer ( int viewport_id )

Returns the custom player previously assigned to the given viewport's window via **[setViewportCustomPlayer()](../../../...md#setViewportCustomPlayer_int_Player_void)**.
### Arguments

- *int* **viewport_id** - ID of the viewport.

### Return value

Custom player assigned to the viewport's window, or null if the viewport does not exist or no custom player is set (rendering then falls back to the game player).
