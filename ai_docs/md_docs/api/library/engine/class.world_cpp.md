# Unigine::World Class (CPP)

**Header:** #include <UnigineWorld.h>

> **Notice:** This class is a singleton.


This class provides functionality for the [world script](../../../code/fundamentals/execution_sequence/app_logic_system.md#world_logic). It contains methods required for loading the world with all its nodes, managing a spatial tree and handling nodes collisions and intersections.


Loading of nodes on demand is managed via the [AsyncQueue Class](../../../api/library/filesystem/class.asyncqueue_cpp.md).


> **Notice:** C++ methods running editor script functions are described in the [Engine class](../../../api/library/engine/class.engine_cpp.md) reference.


### See also


- [AsyncQueue Class](../../../api/library/filesystem/class.asyncqueue_cpp.md) to manage loading nodes and other resources on demand.
- The [Intersections](../../../code/usage/intersections/index_cpp.md) article demonstrating how to use intersection-related functions


## World Class

### Enums

## MOVING_IMMOVABLE_NODES_MODE

| Name | Description |
|---|---|
| **MOVING_IMMOVABLE_NODES_MODE_BAN** = 0 | Moving of the nodes having the Immovable flag is prohibited. |
| **MOVING_IMMOVABLE_NODES_MODE_WARNING** = 1 | Moving of the nodes having the Immovable flag is accompanied by a warning in the console. |
| **MOVING_IMMOVABLE_NODES_MODE_ALLOW** = 2 | Moving of the nodes having the Immovable flag is allowed. |

### Members

## void setUnpackNodeReferences ( bool references )

Sets a new value indicating if automatic unpacking of [node references](../../../api/library/nodes/class.nodereference_cpp.md) at run time is enabled.
This option can be used to simplify hierarchy management, as when it is enabled all nodes contained in node references will be present in the world hierarchy. When disabled you have to check the hierarchy of each node reference individually (e.g. to find the number of children or manage some of them). The content of *NodeReference* nodes is unpacked only at run time and does not affect your `*.world` and `*.node` files. So, you can use all advantages of node references when building worlds in the UnigineEditor and manage a clear and straightforward hierarchy at run time.


> **Notice:** - This option is available only via code, can be enabled in the [System Script](../../../code/fundamentals/execution_sequence/app_logic_system.md#system_logic) and works for all worlds used in your project.
> - **Auto-unpacking is enabled** in C# projects by default.


### Arguments

- *bool* **references** - Set **true** to enable automatic unpacking of *Node Reference* nodes at run time; **false** - to disable it.

## bool isUnpackNodeReferences () const

Returns the current value indicating if automatic unpacking of [node references](../../../api/library/nodes/class.nodereference_cpp.md) at run time is enabled.
This option can be used to simplify hierarchy management, as when it is enabled all nodes contained in node references will be present in the world hierarchy. When disabled you have to check the hierarchy of each node reference individually (e.g. to find the number of children or manage some of them). The content of *NodeReference* nodes is unpacked only at run time and does not affect your `*.world` and `*.node` files. So, you can use all advantages of node references when building worlds in the UnigineEditor and manage a clear and straightforward hierarchy at run time.


> **Notice:** - This option is available only via code, can be enabled in the [System Script](../../../code/fundamentals/execution_sequence/app_logic_system.md#system_logic) and works for all worlds used in your project.
> - **Auto-unpacking is enabled** in C# projects by default.


### Return value

**true** if automatic unpacking of *Node Reference* nodes at run time is enabled ; otherwise **false**.
## void setAutoReloadNodeReferences ( bool references )

Sets a new value indicating if automatic reloading of *Node Reference* nodes is enabled.
If enabled, all *[NodeReference](../../../api/library/nodes/class.nodereference_cpp.md)* nodes will reload their `*.node` files, when the *[saveNode()](#saveNode_cstr_Node_int_int)* method is called.


> **Notice:** This option can be used if you modify and save reference nodes at runtime. Otherwise you'll have to manually update pointers for all *[NodeReferences](../../../api/library/nodes/class.nodereference_cpp.md)* referring to the changed node.


### Arguments

- *bool* **references** - Set **true** to enable automatic reloading of *Node Reference* nodes; **false** - to disable it.

## bool isAutoReloadNodeReferences () const

Returns the current value indicating if automatic reloading of *Node Reference* nodes is enabled.
If enabled, all *[NodeReference](../../../api/library/nodes/class.nodereference_cpp.md)* nodes will reload their `*.node` files, when the *[saveNode()](#saveNode_cstr_Node_int_int)* method is called.


> **Notice:** This option can be used if you modify and save reference nodes at runtime. Otherwise you'll have to manually update pointers for all *[NodeReferences](../../../api/library/nodes/class.nodereference_cpp.md)* referring to the changed node.


### Return value

**true** if automatic reloading of *Node Reference* nodes is enabled ; otherwise **false**.
## void setUpdateGridSize ( float size )

Sets a new size of the grid to be used for spatial tree update. The default value is an average one, and can be adjusted when necessary depending on the scene.
### Arguments

- *float* **size** - The grid size, in units. The default value is 1000 units.

## float getUpdateGridSize () const

Returns the current size of the grid to be used for spatial tree update. The default value is an average one, and can be adjusted when necessary depending on the scene.
### Return value

Current grid size, in units. The default value is 1000 units.
## void setDistance ( float distance )

Sets a new distance at which (and farther) nothing will be rendered or simulated.
### Arguments

- *float* **distance** - The distance at which (and farther) nothing will be rendered or simulated, in units.

## float getDistance () const

Returns the current distance at which (and farther) nothing will be rendered or simulated.
### Return value

Current distance at which (and farther) nothing will be rendered or simulated, in units.
## void setBudget ( float budget )

Sets a new value of the world generation budget for grass and clutter objects. New objects are not created when time is out of the budget.
### Arguments

- *float* **budget** - The budget value in seconds. The default value is 1/60.

## float getBudget () const

Returns the current value of the world generation budget for grass and clutter objects. New objects are not created when time is out of the budget.
### Return value

Current budget value in seconds. The default value is 1/60.
## bool isLoaded () const

Returns the current value indicating if the current world is fully loaded.
### Return value

**true** if the world is fully loaded; otherwise **false**.
## void setScriptName ( const char * name )

Sets a new name of the [world script](../../../principles/world_structure/index.md) `*.usc` file.
### Arguments

- *const char ** **name** - The name of the [world script](../../../principles/world_structure/index.md) `*.usc` file.

## const char * getScriptName () const

Returns the current name of the [world script](../../../principles/world_structure/index.md) `*.usc` file.
### Return value

Current name of the [world script](../../../principles/world_structure/index.md) `*.usc` file.
## void setPath ( const char * path )

Sets a new path to the [`*.world`-file](../../../principles/world_structure/index.md) where the world is stored.
### Arguments

- *const char ** **path** - The path to the [`*.world`-file](../../../principles/world_structure/index.md) where the world is stored.

## const char * getPath () const

Returns the current path to the [`*.world`-file](../../../principles/world_structure/index.md) where the world is stored.
### Return value

Current path to the [`*.world`-file](../../../principles/world_structure/index.md) where the world is stored.
## void setScriptExecute ( bool execute )

Sets a new value indicating if the world script (`*.usc` file) associated with the world should be executed.
### Arguments

- *bool* **execute** - Set **true** to enable a logic script associated with the world is to be loaded with it; **false** - to disable it.

## bool isScriptExecute () const

Returns the current value indicating if the world script (`*.usc` file) associated with the world should be executed.
### Return value

**true** if a logic script associated with the world is to be loaded with it; otherwise **false**.
## void setPhysicsSettings ( const char * settings )

Sets a new name of the `*.physics` file containing default [physics settings](../../../editor2/settings/physics_global/index.md) used by the World.
### Arguments

- *const char ** **settings** - The name of the `*.physics` file containing default [physics settings](../../../editor2/settings/physics_global/index.md) used by the World.

## const char * getPhysicsSettings () const

Returns the current name of the `*.physics` file containing default [physics settings](../../../editor2/settings/physics_global/index.md) used by the World.
### Return value

Current name of the `*.physics` file containing default [physics settings](../../../editor2/settings/physics_global/index.md) used by the World.
## void setSoundSettings ( const char * settings )

Sets a new name of the `*.sound` file containing default [sound settings](../../../editor2/settings/sound_global/index.md) used by the World.
### Arguments

- *const char ** **settings** - The name of the `*.sound` file containing default [sound settings](../../../editor2/settings/sound_global/index.md) used by the World.

## const char * getSoundSettings () const

Returns the current name of the `*.sound` file containing default [sound settings](../../../editor2/settings/sound_global/index.md) used by the World.
### Return value

Current name of the `*.sound` file containing default [sound settings](../../../editor2/settings/sound_global/index.md) used by the World.
## void setRenderSettings ( const char * settings )

Sets a new name of the `*.render` file containing default [render settings](../../../editor2/settings/render_settings/index.md) used by the World.
### Arguments

- *const char ** **settings** - The name of the `*.render` file containing default [render settings](../../../editor2/settings/render_settings/index.md) used by the World.

## const char * getRenderSettings () const

Returns the current name of the `*.render` file containing default [render settings](../../../editor2/settings/render_settings/index.md) used by the World.
### Return value

Current name of the `*.render` file containing default [render settings](../../../editor2/settings/render_settings/index.md) used by the World.
## const char * getLoadWorldRequestPath () const

Returns the current path to the world to be loaded.
### Return value

Current path to the world to be loaded.
## bool isLoadWorldRequested () const

Returns the current value indicating if another world is going to be loaded in the next frame.
### Return value

**true** if another world is going to be loaded in the next frame; otherwise **false**.
## void setMovingImmovableNodeMode ( World::MOVING_IMMOVABLE_NODES_MODE mode )

***Console*:**`world_moving_immovable_node_mode`Sets a new  mode of handling attempts to move nodes having the *[Immovable](../../../editor2/node_parameters/transformation_common/index.md#clutter)* flag enabled.
> **Notice:** Please be aware that there are two cases when you may disable warnings and allow movement of *Immovable* nodes:
> - At run-time for procedural generation of levels. This may cause some freezing but won't affect performance much. Upon completion of the generation process you should enable warnings again.
> - On world initialization, this will change world loading time but won't affect overall performance.


### Arguments

- *[World::MOVING_IMMOVABLE_NODES_MODE](../../../api/library/engine/class.world_cpp.md#MOVING_IMMOVABLE_NODES_MODE)* **mode** - The handling mode for attempts to move nodes having the *[Immovable](../../../editor2/node_parameters/transformation_common/index.md#clutter)* flag enabled. One of the following values:

  - **0** - movement of nodes having the *[Immovable](../../../editor2/node_parameters/transformation_common/index.md#clutter)* flag is prohibited.
  - **1** - movement of nodes having the *[Immovable](../../../editor2/node_parameters/transformation_common/index.md#clutter)* flag is accompanied by a warning in the Console. (by default)
  - **2** - movement of nodes having the *[Immovable](../../../editor2/node_parameters/transformation_common/index.md#clutter)* flag is allowed (no warnings displayed).

## World::MOVING_IMMOVABLE_NODES_MODE getMovingImmovableNodeMode () const

***Console*:**`world_moving_immovable_node_mode`Returns the current  mode of handling attempts to move nodes having the *[Immovable](../../../editor2/node_parameters/transformation_common/index.md#clutter)* flag enabled.
> **Notice:** Please be aware that there are two cases when you may disable warnings and allow movement of *Immovable* nodes:
> - At run-time for procedural generation of levels. This may cause some freezing but won't affect performance much. Upon completion of the generation process you should enable warnings again.
> - On world initialization, this will change world loading time but won't affect overall performance.


### Return value

Current handling mode for attempts to move nodes having the *[Immovable](../../../editor2/node_parameters/transformation_common/index.md#clutter)* flag enabled. One of the following values:
- **0** - movement of nodes having the *[Immovable](../../../editor2/node_parameters/transformation_common/index.md#clutter)* flag is prohibited.
- **1** - movement of nodes having the *[Immovable](../../../editor2/node_parameters/transformation_common/index.md#clutter)* flag is accompanied by a warning in the Console. (by default)
- **2** - movement of nodes having the *[Immovable](../../../editor2/node_parameters/transformation_common/index.md#clutter)* flag is allowed (no warnings displayed).

## void setExperimentalNavigationSettings ( const char * settings )

Sets a new path to the file holding the navigation settings of the world � the registry of areas and flags that the [ExperimentalNavigation](../../../api/library/pathfinding/class.experimentalnavigation_cpp.md) singleton exposes. Keeping it in a file lets several worlds share one set of area definitions instead of each carrying its own copy.
### Arguments

- *const char ** **settings** - The path to the navigation settings file.

## String getExperimentalNavigationSettings () const

Returns the current path to the file holding the navigation settings of the world � the registry of areas and flags that the [ExperimentalNavigation](../../../api/library/pathfinding/class.experimentalnavigation_cpp.md) singleton exposes. Keeping it in a file lets several worlds share one set of area definitions instead of each carrying its own copy.
### Return value

Current path to the navigation settings file.
## void setAsyncLoadNodeReferences ( bool references )

Sets a new value indicating if asynchronous loading of Node References is enabled.
### Arguments

- *bool* **references** - Set **true** to enable asynchronous loading of Node References; **false** - to disable it.

## bool isAsyncLoadNodeReferences () const

Returns the current value indicating if asynchronous loading of Node References is enabled.
### Return value

**true** if asynchronous loading of Node References is enabled ; otherwise **false**.
## static Event<const Ptr < Node > &> getEventNodeRemoved () const

event triggered when a node is removed from the world. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Node> & **node**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the NodeRemoved event handler
void noderemoved_event_handler(const Ptr<Node> & node)
{
	Log::message("\Handling NodeRemoved event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections noderemoved_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
World::getEventNodeRemoved().connect(noderemoved_event_connections, noderemoved_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
World::getEventNodeRemoved().connect(noderemoved_event_connections, [](const Ptr<Node> & node) {
		Log::message("\Handling NodeRemoved event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
noderemoved_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection noderemoved_event_connection;

// subscribe to the NodeRemoved event with a handler function keeping the connection
World::getEventNodeRemoved().connect(noderemoved_event_connection, noderemoved_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
noderemoved_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
noderemoved_event_connection.setEnabled(true);

// ...

// remove subscription to the NodeRemoved event via the connection
noderemoved_event_connection.disconnect();

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

	// A NodeRemoved event handler implemented as a class member
	void event_handler(const Ptr<Node> & node)
	{
		Log::message("\Handling NodeRemoved event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
World::getEventNodeRemoved().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId noderemoved_handler_id;

// subscribe to the NodeRemoved event with a lambda handler function and keeping connection ID
noderemoved_handler_id = World::getEventNodeRemoved().connect(e_connections, [](const Ptr<Node> & node) {
		Log::message("\Handling NodeRemoved event (lambda).\n");
	}
);

// remove the subscription later using the ID
World::getEventNodeRemoved().disconnect(noderemoved_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all NodeRemoved events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
World::getEventNodeRemoved().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
World::getEventNodeRemoved().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const Ptr < Node > &> getEventNodeAdded () const

event triggered when a node is added into the world, including creation of a node from code. The event is also triggered when a the world is loaded from the xml file. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Node> & **node**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the NodeAdded event handler
void nodeadded_event_handler(const Ptr<Node> & node)
{
	Log::message("\Handling NodeAdded event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections nodeadded_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
World::getEventNodeAdded().connect(nodeadded_event_connections, nodeadded_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
World::getEventNodeAdded().connect(nodeadded_event_connections, [](const Ptr<Node> & node) {
		Log::message("\Handling NodeAdded event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
nodeadded_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection nodeadded_event_connection;

// subscribe to the NodeAdded event with a handler function keeping the connection
World::getEventNodeAdded().connect(nodeadded_event_connection, nodeadded_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
nodeadded_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
nodeadded_event_connection.setEnabled(true);

// ...

// remove subscription to the NodeAdded event via the connection
nodeadded_event_connection.disconnect();

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

	// A NodeAdded event handler implemented as a class member
	void event_handler(const Ptr<Node> & node)
	{
		Log::message("\Handling NodeAdded event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
World::getEventNodeAdded().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId nodeadded_handler_id;

// subscribe to the NodeAdded event with a lambda handler function and keeping connection ID
nodeadded_handler_id = World::getEventNodeAdded().connect(e_connections, [](const Ptr<Node> & node) {
		Log::message("\Handling NodeAdded event (lambda).\n");
	}
);

// remove the subscription later using the ID
World::getEventNodeAdded().disconnect(nodeadded_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all NodeAdded events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
World::getEventNodeAdded().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
World::getEventNodeAdded().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<> getEventPostWorldShutdown () const

event triggered after calling all WorldLogic::shutdown() methods. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the PostWorldShutdown event handler
void postworldshutdown_event_handler()
{
	Log::message("\Handling PostWorldShutdown event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections postworldshutdown_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
World::getEventPostWorldShutdown().connect(postworldshutdown_event_connections, postworldshutdown_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
World::getEventPostWorldShutdown().connect(postworldshutdown_event_connections, []() {
		Log::message("\Handling PostWorldShutdown event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
postworldshutdown_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection postworldshutdown_event_connection;

// subscribe to the PostWorldShutdown event with a handler function keeping the connection
World::getEventPostWorldShutdown().connect(postworldshutdown_event_connection, postworldshutdown_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
postworldshutdown_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
postworldshutdown_event_connection.setEnabled(true);

// ...

// remove subscription to the PostWorldShutdown event via the connection
postworldshutdown_event_connection.disconnect();

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

	// A PostWorldShutdown event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling PostWorldShutdown event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
World::getEventPostWorldShutdown().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId postworldshutdown_handler_id;

// subscribe to the PostWorldShutdown event with a lambda handler function and keeping connection ID
postworldshutdown_handler_id = World::getEventPostWorldShutdown().connect(e_connections, []() {
		Log::message("\Handling PostWorldShutdown event (lambda).\n");
	}
);

// remove the subscription later using the ID
World::getEventPostWorldShutdown().disconnect(postworldshutdown_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all PostWorldShutdown events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
World::getEventPostWorldShutdown().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
World::getEventPostWorldShutdown().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<> getEventPreWorldShutdown () const

event triggered before calling all WorldLogic::shutdown() methods. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the PreWorldShutdown event handler
void preworldshutdown_event_handler()
{
	Log::message("\Handling PreWorldShutdown event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections preworldshutdown_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
World::getEventPreWorldShutdown().connect(preworldshutdown_event_connections, preworldshutdown_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
World::getEventPreWorldShutdown().connect(preworldshutdown_event_connections, []() {
		Log::message("\Handling PreWorldShutdown event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
preworldshutdown_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection preworldshutdown_event_connection;

// subscribe to the PreWorldShutdown event with a handler function keeping the connection
World::getEventPreWorldShutdown().connect(preworldshutdown_event_connection, preworldshutdown_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
preworldshutdown_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
preworldshutdown_event_connection.setEnabled(true);

// ...

// remove subscription to the PreWorldShutdown event via the connection
preworldshutdown_event_connection.disconnect();

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

	// A PreWorldShutdown event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling PreWorldShutdown event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
World::getEventPreWorldShutdown().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId preworldshutdown_handler_id;

// subscribe to the PreWorldShutdown event with a lambda handler function and keeping connection ID
preworldshutdown_handler_id = World::getEventPreWorldShutdown().connect(e_connections, []() {
		Log::message("\Handling PreWorldShutdown event (lambda).\n");
	}
);

// remove the subscription later using the ID
World::getEventPreWorldShutdown().disconnect(preworldshutdown_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all PreWorldShutdown events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
World::getEventPreWorldShutdown().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
World::getEventPreWorldShutdown().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<> getEventPostWorldInit () const

event triggered after calling all WorldLogic::init() methods. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** Forced closing of the Engine should be disabled with the [`-auto_quit 0`](../../../code/command_line.md#auto_quit) command-line option.


> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the PostWorldInit event handler
void postworldinit_event_handler()
{
	Log::message("\Handling PostWorldInit event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections postworldinit_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
World::getEventPostWorldInit().connect(postworldinit_event_connections, postworldinit_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
World::getEventPostWorldInit().connect(postworldinit_event_connections, []() {
		Log::message("\Handling PostWorldInit event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
postworldinit_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection postworldinit_event_connection;

// subscribe to the PostWorldInit event with a handler function keeping the connection
World::getEventPostWorldInit().connect(postworldinit_event_connection, postworldinit_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
postworldinit_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
postworldinit_event_connection.setEnabled(true);

// ...

// remove subscription to the PostWorldInit event via the connection
postworldinit_event_connection.disconnect();

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

	// A PostWorldInit event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling PostWorldInit event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
World::getEventPostWorldInit().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId postworldinit_handler_id;

// subscribe to the PostWorldInit event with a lambda handler function and keeping connection ID
postworldinit_handler_id = World::getEventPostWorldInit().connect(e_connections, []() {
		Log::message("\Handling PostWorldInit event (lambda).\n");
	}
);

// remove the subscription later using the ID
World::getEventPostWorldInit().disconnect(postworldinit_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all PostWorldInit events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
World::getEventPostWorldInit().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
World::getEventPostWorldInit().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<> getEventPreWorldInit () const

event triggered before calling all WorldLogic::init() methods. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the PreWorldInit event handler
void preworldinit_event_handler()
{
	Log::message("\Handling PreWorldInit event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections preworldinit_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
World::getEventPreWorldInit().connect(preworldinit_event_connections, preworldinit_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
World::getEventPreWorldInit().connect(preworldinit_event_connections, []() {
		Log::message("\Handling PreWorldInit event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
preworldinit_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection preworldinit_event_connection;

// subscribe to the PreWorldInit event with a handler function keeping the connection
World::getEventPreWorldInit().connect(preworldinit_event_connection, preworldinit_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
preworldinit_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
preworldinit_event_connection.setEnabled(true);

// ...

// remove subscription to the PreWorldInit event via the connection
preworldinit_event_connection.disconnect();

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

	// A PreWorldInit event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling PreWorldInit event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
World::getEventPreWorldInit().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId preworldinit_handler_id;

// subscribe to the PreWorldInit event with a lambda handler function and keeping connection ID
preworldinit_handler_id = World::getEventPreWorldInit().connect(e_connections, []() {
		Log::message("\Handling PreWorldInit event (lambda).\n");
	}
);

// remove the subscription later using the ID
World::getEventPreWorldInit().disconnect(preworldinit_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all PreWorldInit events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
World::getEventPreWorldInit().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
World::getEventPreWorldInit().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const char *, const Ptr < Node > &> getEventPostNodeSave () const

event triggered after calling the World::saveNode() method. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const char * **world_file_path**, const Ptr<Node> & **node**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the PostNodeSave event handler
void postnodesave_event_handler(const char * world_file_path,  const Ptr<Node> & node)
{
	Log::message("\Handling PostNodeSave event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections postnodesave_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
World::getEventPostNodeSave().connect(postnodesave_event_connections, postnodesave_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
World::getEventPostNodeSave().connect(postnodesave_event_connections, [](const char * world_file_path,  const Ptr<Node> & node) {
		Log::message("\Handling PostNodeSave event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
postnodesave_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection postnodesave_event_connection;

// subscribe to the PostNodeSave event with a handler function keeping the connection
World::getEventPostNodeSave().connect(postnodesave_event_connection, postnodesave_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
postnodesave_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
postnodesave_event_connection.setEnabled(true);

// ...

// remove subscription to the PostNodeSave event via the connection
postnodesave_event_connection.disconnect();

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

	// A PostNodeSave event handler implemented as a class member
	void event_handler(const char * world_file_path,  const Ptr<Node> & node)
	{
		Log::message("\Handling PostNodeSave event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
World::getEventPostNodeSave().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId postnodesave_handler_id;

// subscribe to the PostNodeSave event with a lambda handler function and keeping connection ID
postnodesave_handler_id = World::getEventPostNodeSave().connect(e_connections, [](const char * world_file_path,  const Ptr<Node> & node) {
		Log::message("\Handling PostNodeSave event (lambda).\n");
	}
);

// remove the subscription later using the ID
World::getEventPostNodeSave().disconnect(postnodesave_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all PostNodeSave events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
World::getEventPostNodeSave().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
World::getEventPostNodeSave().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const char *, const Ptr < Node > &> getEventPreNodeSave () const

event triggered before calling the World::saveNode() method. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const char * **world_file_path**, const Ptr<Node> & **node**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the PreNodeSave event handler
void prenodesave_event_handler(const char * world_file_path,  const Ptr<Node> & node)
{
	Log::message("\Handling PreNodeSave event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections prenodesave_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
World::getEventPreNodeSave().connect(prenodesave_event_connections, prenodesave_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
World::getEventPreNodeSave().connect(prenodesave_event_connections, [](const char * world_file_path,  const Ptr<Node> & node) {
		Log::message("\Handling PreNodeSave event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
prenodesave_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection prenodesave_event_connection;

// subscribe to the PreNodeSave event with a handler function keeping the connection
World::getEventPreNodeSave().connect(prenodesave_event_connection, prenodesave_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
prenodesave_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
prenodesave_event_connection.setEnabled(true);

// ...

// remove subscription to the PreNodeSave event via the connection
prenodesave_event_connection.disconnect();

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

	// A PreNodeSave event handler implemented as a class member
	void event_handler(const char * world_file_path,  const Ptr<Node> & node)
	{
		Log::message("\Handling PreNodeSave event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
World::getEventPreNodeSave().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId prenodesave_handler_id;

// subscribe to the PreNodeSave event with a lambda handler function and keeping connection ID
prenodesave_handler_id = World::getEventPreNodeSave().connect(e_connections, [](const char * world_file_path,  const Ptr<Node> & node) {
		Log::message("\Handling PreNodeSave event (lambda).\n");
	}
);

// remove the subscription later using the ID
World::getEventPreNodeSave().disconnect(prenodesave_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all PreNodeSave events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
World::getEventPreNodeSave().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
World::getEventPreNodeSave().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const char *> getEventPostWorldClear () const

event triggered after clearing the World. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const char * **world_file_path**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the PostWorldClear event handler
void postworldclear_event_handler(const char * world_file_path)
{
	Log::message("\Handling PostWorldClear event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections postworldclear_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
World::getEventPostWorldClear().connect(postworldclear_event_connections, postworldclear_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
World::getEventPostWorldClear().connect(postworldclear_event_connections, [](const char * world_file_path) {
		Log::message("\Handling PostWorldClear event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
postworldclear_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection postworldclear_event_connection;

// subscribe to the PostWorldClear event with a handler function keeping the connection
World::getEventPostWorldClear().connect(postworldclear_event_connection, postworldclear_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
postworldclear_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
postworldclear_event_connection.setEnabled(true);

// ...

// remove subscription to the PostWorldClear event via the connection
postworldclear_event_connection.disconnect();

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

	// A PostWorldClear event handler implemented as a class member
	void event_handler(const char * world_file_path)
	{
		Log::message("\Handling PostWorldClear event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
World::getEventPostWorldClear().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId postworldclear_handler_id;

// subscribe to the PostWorldClear event with a lambda handler function and keeping connection ID
postworldclear_handler_id = World::getEventPostWorldClear().connect(e_connections, [](const char * world_file_path) {
		Log::message("\Handling PostWorldClear event (lambda).\n");
	}
);

// remove the subscription later using the ID
World::getEventPostWorldClear().disconnect(postworldclear_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all PostWorldClear events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
World::getEventPostWorldClear().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
World::getEventPostWorldClear().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const char *> getEventPreWorldClear () const

event triggered before clearing the world � either closing the current world or preparing to load the next World. This event always takes place in Engine::swap(), i.e. in the end of the frame. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const char * **world_file_path**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the PreWorldClear event handler
void preworldclear_event_handler(const char * world_file_path)
{
	Log::message("\Handling PreWorldClear event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections preworldclear_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
World::getEventPreWorldClear().connect(preworldclear_event_connections, preworldclear_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
World::getEventPreWorldClear().connect(preworldclear_event_connections, [](const char * world_file_path) {
		Log::message("\Handling PreWorldClear event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
preworldclear_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection preworldclear_event_connection;

// subscribe to the PreWorldClear event with a handler function keeping the connection
World::getEventPreWorldClear().connect(preworldclear_event_connection, preworldclear_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
preworldclear_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
preworldclear_event_connection.setEnabled(true);

// ...

// remove subscription to the PreWorldClear event via the connection
preworldclear_event_connection.disconnect();

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

	// A PreWorldClear event handler implemented as a class member
	void event_handler(const char * world_file_path)
	{
		Log::message("\Handling PreWorldClear event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
World::getEventPreWorldClear().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId preworldclear_handler_id;

// subscribe to the PreWorldClear event with a lambda handler function and keeping connection ID
preworldclear_handler_id = World::getEventPreWorldClear().connect(e_connections, [](const char * world_file_path) {
		Log::message("\Handling PreWorldClear event (lambda).\n");
	}
);

// remove the subscription later using the ID
World::getEventPreWorldClear().disconnect(preworldclear_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all PreWorldClear events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
World::getEventPreWorldClear().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
World::getEventPreWorldClear().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const char *> getEventPostWorldSave () const

event triggered after saving the World. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const char * **world_file_path**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the PostWorldSave event handler
void postworldsave_event_handler(const char * world_file_path)
{
	Log::message("\Handling PostWorldSave event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections postworldsave_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
World::getEventPostWorldSave().connect(postworldsave_event_connections, postworldsave_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
World::getEventPostWorldSave().connect(postworldsave_event_connections, [](const char * world_file_path) {
		Log::message("\Handling PostWorldSave event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
postworldsave_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection postworldsave_event_connection;

// subscribe to the PostWorldSave event with a handler function keeping the connection
World::getEventPostWorldSave().connect(postworldsave_event_connection, postworldsave_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
postworldsave_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
postworldsave_event_connection.setEnabled(true);

// ...

// remove subscription to the PostWorldSave event via the connection
postworldsave_event_connection.disconnect();

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

	// A PostWorldSave event handler implemented as a class member
	void event_handler(const char * world_file_path)
	{
		Log::message("\Handling PostWorldSave event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
World::getEventPostWorldSave().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId postworldsave_handler_id;

// subscribe to the PostWorldSave event with a lambda handler function and keeping connection ID
postworldsave_handler_id = World::getEventPostWorldSave().connect(e_connections, [](const char * world_file_path) {
		Log::message("\Handling PostWorldSave event (lambda).\n");
	}
);

// remove the subscription later using the ID
World::getEventPostWorldSave().disconnect(postworldsave_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all PostWorldSave events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
World::getEventPostWorldSave().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
World::getEventPostWorldSave().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const char *> getEventPreWorldSave () const

event triggered before saving the World. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const char * **world_file_path**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the PreWorldSave event handler
void preworldsave_event_handler(const char * world_file_path)
{
	Log::message("\Handling PreWorldSave event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections preworldsave_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
World::getEventPreWorldSave().connect(preworldsave_event_connections, preworldsave_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
World::getEventPreWorldSave().connect(preworldsave_event_connections, [](const char * world_file_path) {
		Log::message("\Handling PreWorldSave event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
preworldsave_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection preworldsave_event_connection;

// subscribe to the PreWorldSave event with a handler function keeping the connection
World::getEventPreWorldSave().connect(preworldsave_event_connection, preworldsave_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
preworldsave_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
preworldsave_event_connection.setEnabled(true);

// ...

// remove subscription to the PreWorldSave event via the connection
preworldsave_event_connection.disconnect();

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

	// A PreWorldSave event handler implemented as a class member
	void event_handler(const char * world_file_path)
	{
		Log::message("\Handling PreWorldSave event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
World::getEventPreWorldSave().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId preworldsave_handler_id;

// subscribe to the PreWorldSave event with a lambda handler function and keeping connection ID
preworldsave_handler_id = World::getEventPreWorldSave().connect(e_connections, [](const char * world_file_path) {
		Log::message("\Handling PreWorldSave event (lambda).\n");
	}
);

// remove the subscription later using the ID
World::getEventPreWorldSave().disconnect(preworldsave_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all PreWorldSave events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
World::getEventPreWorldSave().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
World::getEventPreWorldSave().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const char *> getEventPostWorldLoad () const

event triggered after loading the World. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const char * **world_file_path**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the PostWorldLoad event handler
void postworldload_event_handler(const char * world_file_path)
{
	Log::message("\Handling PostWorldLoad event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections postworldload_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
World::getEventPostWorldLoad().connect(postworldload_event_connections, postworldload_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
World::getEventPostWorldLoad().connect(postworldload_event_connections, [](const char * world_file_path) {
		Log::message("\Handling PostWorldLoad event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
postworldload_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection postworldload_event_connection;

// subscribe to the PostWorldLoad event with a handler function keeping the connection
World::getEventPostWorldLoad().connect(postworldload_event_connection, postworldload_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
postworldload_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
postworldload_event_connection.setEnabled(true);

// ...

// remove subscription to the PostWorldLoad event via the connection
postworldload_event_connection.disconnect();

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

	// A PostWorldLoad event handler implemented as a class member
	void event_handler(const char * world_file_path)
	{
		Log::message("\Handling PostWorldLoad event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
World::getEventPostWorldLoad().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId postworldload_handler_id;

// subscribe to the PostWorldLoad event with a lambda handler function and keeping connection ID
postworldload_handler_id = World::getEventPostWorldLoad().connect(e_connections, [](const char * world_file_path) {
		Log::message("\Handling PostWorldLoad event (lambda).\n");
	}
);

// remove the subscription later using the ID
World::getEventPostWorldLoad().disconnect(postworldload_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all PostWorldLoad events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
World::getEventPostWorldLoad().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
World::getEventPostWorldLoad().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const char *> getEventPreWorldLoad () const

event triggered before loading the World. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const char * **world_file_path**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the PreWorldLoad event handler
void preworldload_event_handler(const char * world_file_path)
{
	Log::message("\Handling PreWorldLoad event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections preworldload_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
World::getEventPreWorldLoad().connect(preworldload_event_connections, preworldload_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
World::getEventPreWorldLoad().connect(preworldload_event_connections, [](const char * world_file_path) {
		Log::message("\Handling PreWorldLoad event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
preworldload_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection preworldload_event_connection;

// subscribe to the PreWorldLoad event with a handler function keeping the connection
World::getEventPreWorldLoad().connect(preworldload_event_connection, preworldload_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
preworldload_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
preworldload_event_connection.setEnabled(true);

// ...

// remove subscription to the PreWorldLoad event via the connection
preworldload_event_connection.disconnect();

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

	// A PreWorldLoad event handler implemented as a class member
	void event_handler(const char * world_file_path)
	{
		Log::message("\Handling PreWorldLoad event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
World::getEventPreWorldLoad().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId preworldload_handler_id;

// subscribe to the PreWorldLoad event with a lambda handler function and keeping connection ID
preworldload_handler_id = World::getEventPreWorldLoad().connect(e_connections, [](const char * world_file_path) {
		Log::message("\Handling PreWorldLoad event (lambda).\n");
	}
);

// remove the subscription later using the ID
World::getEventPreWorldLoad().disconnect(preworldload_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all PreWorldLoad events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
World::getEventPreWorldLoad().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
World::getEventPreWorldLoad().setEnabled(true);

```

</details>

### Return value

Event instance.
---

## bool getCollision ( const Math:: WorldBoundBox & bb , Vector < Ptr < Object >> & OUT_objects )


Searches for all [collider objects](../../../principles/physics/collision/index.md#collider) within a given bounding box.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *const  Math::[WorldBoundBox](../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bb** - Bounding box.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Object](../../../api/library/objects/class.object_cpp.md)>> &* **OUT_objects** - Array with collider objects' smart pointers. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true if collider objects are found; otherwise, false.
## bool getCollision ( const Math:: WorldBoundSphere & bs , Vector < Ptr < Object >> & OUT_objects )


Searches for all [collider objects](../../../principles/physics/collision/index.md#collider) within a given bounding sphere.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *const  Math::[WorldBoundSphere](../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **bs** - Bounding sphere.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Object](../../../api/library/objects/class.object_cpp.md)>> &* **OUT_objects** - Array with collider objects' smart pointers. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true if collider objects are found; otherwise, false.
## bool getCollision ( const Math:: WorldBoundFrustum & bf , Vector < Ptr < Object >> & OUT_objects )


Searches for all [collider objects](../../../principles/physics/collision/index.md#collider) within a given bounding frustum.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *const  Math::[WorldBoundFrustum](../../../api/library/math/bounds/class.worldboundfrustum_cpp.md) &* **bf** - Bounding frustum.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Object](../../../api/library/objects/class.object_cpp.md)>> &* **OUT_objects** - Array with collider objects' smart pointers. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true if collider objects are found; otherwise, false.
## bool getCollision ( const Math:: Vec3 & p0 , const Math:: Vec3 & p1 , Vector < Ptr < Object >> & OUT_objects )


Performs tracing from the p0 point to the p1 point to find all [collider objects](../../../principles/physics/collision/index.md#collider) intersected by the line. This function detects intersection with surfaces (polygons) of mesh and terrain objects.


Collisions with the surface can be found only if the following conditions are fulfilled:


1. The surface is enabled.
2. Per-surface [Collision](../../../api/library/objects/class.object_cpp.md#setCollision_int_int_void) flag is enabled.
3. The surface has a material assigned.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - The start point coordinates.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - The end point coordinates.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Object](../../../api/library/objects/class.object_cpp.md)>> &* **OUT_objects** - Array with collider objects' smart pointers. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true if collider objects are found; otherwise, false.
## void setData ( const char * name , const char * data )

Sets user data associated with the world with the specified key. In the `*.world` file, the data is set in the data tag with the specified key.
### Arguments

- *const char ** **name** - String containing a key identifying user data to be stored in the `*.world` file. > **Notice:** The "editor_data" key is reserved for the UnigineEditor.
- *const char ** **data** - New user data.

## const char * getData ( const char * name )

Returns user string data associated with the world by the specified key. This string is written directly into the data tag of the `*.world` file with the specified key.
### Arguments

- *const char ** **name** - String containing a key identifying user data stored in the `*.world` file. > **Notice:** The "editor_data" key is reserved for the UnigineEditor.

### Return value

User string data.
## bool hasData ( const char * name ) const

Checks whether user string data associated with the world by the specified key is stored in the data tag of the `*.world` file.
### Arguments

- *const char ** **name** - String containing a key identifying user data stored in the `*.world` file. > **Notice:** The "editor_data" key is reserved for the UnigineEditor.

### Return value

true if user string data associated with the world by the specified key is stored in the data tag of the `*.world` file; otherwise, false.
## void removeData ( const char * name )

Removes user string data associated with the world by the specified key. This string is stored in the data tag of the `*.world` file with the specified key.
### Arguments

- *const char ** **name** - String containing a key identifying user data stored in the `*.world` file. > **Notice:** The "editor_data" key is reserved for the UnigineEditor.

## Ptr < Object > getIntersection ( const Math:: Vec3 & p0 , const Math:: Vec3 & p1 , int mask )


Performs tracing from the p0 point to the p1 point to find **the first object intersected by the line**. This function detects intersection with surfaces (polygons) of meshes. An intersection can be found only if an object has a matching intersection mask.


Intersections with the surface can be found only if the following conditions are fulfilled:


1. The surface is enabled.
2. Per-surface [Intersection](../../../api/library/objects/class.object_cpp.md#setIntersection_int_int_void) flag is enabled.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - Line start point coordinates.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - Line end point coordinates.
- *int* **mask** - Intersection mask. If 0 is passed, the function will return NULL.

### Return value

Pointer to the first intersected object.
## Ptr < Object > getIntersection ( const Math:: Vec3 & p0 , const Math:: Vec3 & p1 , int mask , const Vector < Ptr < Node >> & exclude )


Performs tracing from the p0 point to the p1 point to find **the first object intersected by the line** (except for the ones passed in the **exclude** list). This function detects intersection with surfaces (polygons) of meshes. An intersection can be found only if an object has a matching intersection mask.


Intersections with the surface can be found only if the following conditions are fulfilled:


1. The surface is enabled.
2. Per-surface [Intersection](../../../api/library/objects/class.object_cpp.md#setIntersection_int_int_void) flag is enabled.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - Line start point coordinates.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - Line end point coordinates.
- *int* **mask** - Intersection mask. If 0 is passed, the function will return NULL.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>> &* **exclude** - List of nodes to be ignored when searching for intersection by the traced line.

### Return value

The first intersected object found at the line (except for the ones passed in the **exclude** list); otherwise, NULL pointer.
## Ptr < Object > getIntersection ( const Math:: Vec3 & p0 , const Math:: Vec3 & p1 , int mask , const Ptr < WorldIntersection > & intersection )


Performs tracing from the p0 point to the p1 point to find **the first object intersecting the line**. This function detects intersection with surfaces (polygons) of meshes. An intersection can be found only if an object is matching the intersection mask.


Intersections with the surface can be found only if the following conditions are fulfilled:


1. The surface is enabled.
2. Per-surface [Intersection](../../../api/library/objects/class.object_cpp.md#setIntersection_int_int_void) flag is enabled.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - Coordinates of the line start point.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - Coordinates of the line end point.
- *int* **mask** - Intersection mask. If 0 is passed, the function will return NULL.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[WorldIntersection](../../../api/library/worlds/class.worldintersection_cpp.md)> &* **intersection** - Pointer to the WorldIntersection object to be filled.

### Return value

Pointer to the first intersected object.
## Ptr < Object > getIntersection ( const Math:: Vec3 & p0 , const Math:: Vec3 & p1 , int mask , const Ptr < WorldIntersectionNormal > & intersection )


Performs tracing from the p0 point to the p1 point to find **the first object intersecting the line**. This function detects intersection with surfaces (polygons) of meshes. An intersection can be found only if an object is matching the intersection mask.


Intersections with the surface can be found only if the following conditions are fulfilled:


1. The surface is enabled.
2. Per-surface [Intersection](../../../api/library/objects/class.object_cpp.md#setIntersection_int_int_void) flag is enabled.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - Coordinates of the line start point.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - Coordinates of the line end point.
- *int* **mask** - Intersection mask. If 0 is passed, the function will return NULL.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[WorldIntersectionNormal](../../../api/library/worlds/class.worldintersectionnormal_cpp.md)> &* **intersection** - Pointer to the WorldIntersectionNormal object to be filled.

### Return value

Pointer to the first intersected object.
## Ptr < Object > getIntersection ( const Math:: Vec3 & p0 , const Math:: Vec3 & p1 , int mask , const Ptr < WorldIntersectionTexCoord > & intersection )


Performs tracing from the p0 point to the p1 point to find **the first object intersecting the line**. This function detects intersection with surfaces (polygons) of meshes. An intersection can be found only if an object is matching the intersection mask.


Intersections with the surface can be found only if the following conditions are fulfilled:


1. The surface is enabled.
2. Per-surface [Intersection](../../../api/library/objects/class.object_cpp.md#setIntersection_int_int_void) flag is enabled.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - Coordinates of the line start point.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - Coordinates of the line end point.
- *int* **mask** - Intersection mask. If 0 is passed, the function will return NULL.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[WorldIntersectionTexCoord](../../../api/library/worlds/class.worldintersectiontexcoord_cpp.md)> &* **intersection** - Pointer to the WorldIntersectionTexCoord object to be filled.

### Return value

Pointer to the first intersected object.
## Ptr < Object > getIntersection ( const Math:: Vec3 & p0 , const Math:: Vec3 & p1 , int mask , const Vector < Ptr < Node >> & exclude , const Ptr < WorldIntersection > & intersection )


Performs tracing from the p0 point to the p1 point to find **the first object intersecting the line**. This function detects intersection with surfaces (polygons) of meshes. An intersection can be found only if an object is matching the intersection mask.


Intersections with the surface can be found only if the following conditions are fulfilled:


1. The surface is enabled.
2. Per-surface [Intersection](../../../api/library/objects/class.object_cpp.md#setIntersection_int_int_void) flag is enabled.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - Coordinates of the line start point.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - Coordinates of the line end point.
- *int* **mask** - Intersection mask. If 0 is passed, the function will return NULL.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>> &* **exclude** - The list of nodes to be excluded.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[WorldIntersection](../../../api/library/worlds/class.worldintersection_cpp.md)> &* **intersection** - Pointer to the WorldIntersection object to be filled.

### Return value

Pointer to the first intersected object.
## Ptr < Object > getIntersection ( const Math:: Vec3 & p0 , const Math:: Vec3 & p1 , int mask , const Vector < Ptr < Node >> & exclude , const Ptr < WorldIntersectionNormal > & intersection )


Performs tracing from the p0 point to the p1 point to find **the first object intersecting the line**. This function detects intersection with surfaces (polygons) of meshes. An intersection can be found only if an object is matching the intersection mask.


Intersections with the surface can be found only if the following conditions are fulfilled:


1. The surface is enabled.
2. Per-surface [Intersection](../../../api/library/objects/class.object_cpp.md#setIntersection_int_int_void) flag is enabled.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - Coordinates of the line start point.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - Coordinates of the line end point.
- *int* **mask** - Intersection mask. If 0 is passed, the function will return NULL.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>> &* **exclude** - The list of nodes to be excluded.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[WorldIntersectionNormal](../../../api/library/worlds/class.worldintersectionnormal_cpp.md)> &* **intersection** - Pointer to the WorldIntersectionNormal object to be filled.

### Return value

Pointer to the first intersected object.
## Ptr < Object > getIntersection ( const Math:: Vec3 & p0 , const Math:: Vec3 & p1 , int mask , const Vector < Ptr < Node >> & exclude , const Ptr < WorldIntersectionTexCoord > & intersection )


Performs tracing from the p0 point to the p1 point to find **the first object intersected by the line**. This function detects intersection with surfaces (polygons) of meshes. An intersection can be found only if an object is matching the intersection mask.


Intersections with the surface can be found only if the following conditions are fulfilled:


1. The surface is enabled.
2. Per-surface [Intersection](../../../api/library/objects/class.object_cpp.md#setIntersection_int_int_void) flag is enabled.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - Coordinates of the line start point.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - Coordinates of the line end point.
- *int* **mask** - Intersection mask. If 0 is passed, the function will return NULL.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>> &* **exclude** - The list of nodes to be excluded.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[WorldIntersectionTexCoord](../../../api/library/worlds/class.worldintersectiontexcoord_cpp.md)> &* **intersection** - Pointer to the WorldIntersectionTexCoord object to be filled.

### Return value

Pointer to the first intersected object.
## bool getIntersection ( const Math:: Vec3 & p0 , const Math:: Vec3 & p1 , Vector < Ptr < Object >> & OUT_objects , bool check_surface_flags = true )


Performs tracing from the p0 point to the p1 point to find **objects intersected by the line**. This function detects intersection with objects' bounds.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - Coordinates of the line start point.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - Coordinates of the line end point.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Object](../../../api/library/objects/class.object_cpp.md)>> &* **OUT_objects** - Array of intersected objects' smart pointers. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *bool* **check_surface_flags** - true if [surface*Intersection* flags](../../../api/library/objects/class.object_cpp.md#getIntersection_int_int) are to be taken into account when checking for intersections with objects; otherwise, false. When set to true objects with surface *Intersection* flags disabled (default setting) will be ignored as non-intersectable.

### Return value

true if intersections are found; otherwise, false.
## bool getIntersection ( const Math:: WorldBoundBox & bb , Vector < Ptr < Object >> & OUT_objects )


Searches for intersections **with objects** that are found in a given bounding box.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *const  Math::[WorldBoundBox](../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bb** - Bounding box where intersection search will be performed.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Object](../../../api/library/objects/class.object_cpp.md)>> &* **OUT_objects** - Array of intersected objects' smart pointers. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true if intersections are found; otherwise, false.
## bool getIntersection ( const Math:: WorldBoundBox & bb , Vector < Ptr < Node >> & OUT_nodes )


Searches for intersections **with nodes** that are found in a given bounding box.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *const  Math::[WorldBoundBox](../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bb** - Bounding box where intersection search will be performed.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>> &* **OUT_nodes** - Array of intersected nodes' smart pointers. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true if intersections are found; otherwise, false.
## bool getIntersection ( const Math:: WorldBoundBox & bb , Node::TYPE type , Vector < Ptr < Node >> & OUT_nodes )


Searches for intersections **with specified type of nodes** that are found in a given bounding box.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *const  Math::[WorldBoundBox](../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bb** - Bounding box where intersection search will be performed.
- *[Node::TYPE](../../../api/library/nodes/class.node_cpp.md#TYPE)* **type** - Node type filter. Only the nodes of the specified type will be checked.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>> &* **OUT_nodes** - Array of intersected nodes' smart pointers. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true if intersections are found; otherwise, false.
## bool getIntersection ( const Math:: WorldBoundSphere & bs , Vector < Ptr < Object >> & OUT_objects )


Searches for intersections **with objects** that are found in a given bounding sphere.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *const  Math::[WorldBoundSphere](../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **bs** - Bounding sphere where intersection search will be performed.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Object](../../../api/library/objects/class.object_cpp.md)>> &* **OUT_objects** - Array of intersected objects' smart pointers. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true if intersections are found; otherwise, false.
## bool getIntersection ( const Math:: WorldBoundSphere & bs , Vector < Ptr < Node >> & OUT_nodes )


Searches for intersections **with nodes** that are found in a given bounding sphere.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *const  Math::[WorldBoundSphere](../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **bs** - Bounding sphere where intersection search will be performed.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>> &* **OUT_nodes** - Array of intersected nodes' smart pointers. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true if intersections are found; otherwise, false.
## bool getIntersection ( const Math:: WorldBoundSphere & bs , Node::TYPE type , Vector < Ptr < Node >> & OUT_nodes )


Searches for intersections **with nodes of the specified type** that are found in a given bounding sphere.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *const  Math::[WorldBoundSphere](../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **bs** - Bounding sphere where intersection search will be performed.
- *[Node::TYPE](../../../api/library/nodes/class.node_cpp.md#TYPE)* **type** - Node type filter. Only the nodes of the specified type will be checked.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>> &* **OUT_nodes** - Array of intersected nodes' smart pointers. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true if intersections are found; otherwise, false.
## bool getIntersection ( const Math:: WorldBoundFrustum & bf , Vector < Ptr < Object >> & OUT_objects )


Searches for intersections **with Objects** that are found in a given bounding frustum. This method catches all objects independent of their visibility (i.e., if an object is disabled, any of its LODs are disabled, or it is out of the [visibility distance](../../../editor2/settings/render_settings/visibility_distances/index.md) range, but is located within the bounding frustum, the intersection shall be detected). To check for intersections while taking into account the visibility aspect, use *[getVisibleIntersection()](#getVisibleIntersection_Vec3_WorldBoundFrustum_VECObject_float_int)*. Check the [usage example](../../../code/usage/intersections/index_cpp.md#frustrum_search) applying this method.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *const  Math::[WorldBoundFrustum](../../../api/library/math/bounds/class.worldboundfrustum_cpp.md) &* **bf** - Bounding frustum where intersection search will be performed.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Object](../../../api/library/objects/class.object_cpp.md)>> &* **OUT_objects** - Array of intersected objects' smart pointers. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true if intersections are found; otherwise, false.
## bool getIntersection ( const Math:: WorldBoundFrustum & bf , Node::TYPE type , Vector < Ptr < Node >> & OUT_nodes )


Searches for intersections **with nodes of the specified type** that are found in a given bounding frustum. This method catches all nodes of the specified type independent of their visibility (i.e., if an object is disabled, any of its LODs are disabled, or it is out of the [visibility distance](../../../editor2/settings/render_settings/visibility_distances/index.md) range, but is located within the bounding frustum, the intersection shall be detected). To check for intersections while taking into account the visibility aspect, use *[getVisibleIntersection()](#getVisibleIntersection_Vec3_WorldBoundFrustum_int_VECNode_float_int)*.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *const  Math::[WorldBoundFrustum](../../../api/library/math/bounds/class.worldboundfrustum_cpp.md) &* **bf** - Bounding frustum where intersection search will be performed.
- *[Node::TYPE](../../../api/library/nodes/class.node_cpp.md#TYPE)* **type** - Node type filter. Only the nodes of the specified type will be checked.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>> &* **OUT_nodes** - Array of intersected nodes' smart pointers. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true if intersections are found; otherwise, false.
## bool getIntersection ( const Math:: WorldBoundFrustum & bf , Vector < Ptr < Node >> & OUT_nodes )


Searches for intersections **with nodes of the specified type** that are found in a given bounding frustum. This method catches all nodes independent of their visibility (i.e., if an object is disabled, any of its LODs are disabled, or it is out of the [visibility distance](../../../editor2/settings/render_settings/visibility_distances/index.md) range, but is located within the bounding frustum, the intersection shall be detected). To check for intersections while taking into account the visibility aspect, use *[getVisibleIntersection()](#getVisibleIntersection_Vec3_WorldBoundFrustum_int_VECNode_float_int)*.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *const  Math::[WorldBoundFrustum](../../../api/library/math/bounds/class.worldboundfrustum_cpp.md) &* **bf** - Bounding frustum where intersection search will be performed.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>> &* **OUT_nodes** - Array of intersected nodes' smart pointers. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true if intersections are found; otherwise, false.
## bool getVisibleIntersection ( const Math:: Vec3 & camera , const Math:: WorldBoundFrustum & bf , Vector < Ptr < Object >> & OUT_objects , float max_distance )

Searches for intersections with objects inside a given bounding frustum that are visible to the specified camera position, i.e. [either of its LODs](../../../api/library/objects/class.object_cpp.md#setMinVisibleDistance_float_int_void) is within the [visibility distance](../../../editor2/settings/render_settings/visibility_distances/index.md) distance. Unlike the *[getIntersection()](#getIntersection_WorldBoundFrustum_VECObject_int)* method, this one takes the "visibility" concept into account (hidden objects or the ones that are too far away won't be found). Check this [usage example](../../../code/usage/intersections/index_cpp.md#frustrum_search) for more details.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **camera** - Position of the camera from which the visibility distance to objects is checked.
- *const  Math::[WorldBoundFrustum](../../../api/library/math/bounds/class.worldboundfrustum_cpp.md) &* **bf** - Bounding frustum inside which intersection search is performed.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Object](../../../api/library/objects/class.object_cpp.md)>> &* **OUT_objects** - Array of intersected objects. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *float* **max_distance** - Maximum visibility distance for objects, in units. If the distance from the specified camera position to an object exceeds this limit, the intersection is not registered even if the node is within the specified bounding frustum.

### Return value

true if at least one intersection is found; otherwise, false.
## bool getVisibleIntersection ( const Math:: Vec3 & camera , const Math:: WorldBoundFrustum & bf , Node::TYPE type , Vector < Ptr < Node >> & OUT_nodes , float max_distance )


Searches for intersections with nodes inside a given bounding frustum that are visible to the specified camera position, i.e. [either of its LODs](../../../api/library/objects/class.object_cpp.md#setMinVisibleDistance_float_int_void) is within the [visibility distance](../../../editor2/settings/render_settings/visibility_distances/index.md) distance. Unlike the *[getIntersection()](#getIntersection_WorldBoundFrustum_int_VECNode_int)* method, this one takes the "visibility" concept into account (hidden nodes or the ones that are too far away won't be found). Check this [usage example](../../../code/usage/intersections/index_cpp.md#frustrum_search) for more details.


> **Notice:** This method can be used only for nodes inherited from the [Object](../../../api/library/objects/class.object_cpp.md) class, i.e. they have sufraces that store LOD and [visibility distance](../../../editor2/settings/render_settings/visibility_distances/index.md) data.


### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **camera** - Position of the camera from which the visibility distance to nodes is checked.
- *const  Math::[WorldBoundFrustum](../../../api/library/math/bounds/class.worldboundfrustum_cpp.md) &* **bf** - Bounding frustum inside which intersection search is performed.
- *[Node::TYPE](../../../api/library/nodes/class.node_cpp.md#TYPE)* **type** - Node type (one of the [NODE_*](../../../api/library/nodes/class.node_cpp.md#DECAL_BEGIN) variables); set it to -1 if you won't use this filter.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>> &* **OUT_nodes** - Array of intersected nodes. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *float* **max_distance** - Maximum visibility distance for nodes, in units. If the distance from the specified camera position to a node exceeds this limit, the intersection is not registered even if the node is within the specified bounding frustum.

### Return value

true if at least one intersection is found; otherwise, false.
## bool loadWorld ( const char * path )

Loads a world from the specified file path and replaces the current world with it. The world is not loaded immediately � loading starts at the [beginning](../../../code/fundamentals/execution_sequence/main_loop.md#update) of the next frame, while the current world is unloaded at the [end](../../../code/fundamentals/execution_sequence/main_loop.md#swap) of the current frame.
### Arguments

- *const char ** **path** - Path to the [file describing the world](../../../principles/world_structure/index.md).

### Return value

true if the world is loaded successfully; otherwise, false.
## bool loadWorld ( const char * path , bool partial_path )

Loads a world from the specified file path and replaces the current world with it. The world is not loaded immediately � loading starts at the [beginning](../../../code/fundamentals/execution_sequence/main_loop.md#update) of the next frame, while the current world is unloaded at the [end](../../../code/fundamentals/execution_sequence/main_loop.md#swap) of the current frame.
### Arguments

- *const char ** **path** - Path to the [file describing the world](../../../principles/world_structure/index.md).
- *bool* **partial_path** - true if the path to the world file is partial; or false if it is a full path.

### Return value

true if the world is loaded successfully; otherwise, false.
## bool loadWorldForce ( const char * path )

Loads a world from the specified file path and replaces the current world with it. The world is loaded immediately, breaking the Execution Sequence, therefore should be used either before [Engine::update()](../../../code/fundamentals/execution_sequence/main_loop.md#update) or after [Engine::swap()](../../../code/fundamentals/execution_sequence/main_loop.md#swap). If called in Engine::update(), the Execution Sequence will be as follows: update() before calling loadWorldForce(), loadWorldForce(), shutdown(), continuation of update() from the place of interruption, postUpdate(), swap(), init(), etc. This function is recommended for the Editor-related use.
### Arguments

- *const char ** **path** - Path to the [file describing the world](../../../principles/world_structure/index.md).

### Return value

true if the world is loaded successfully; otherwise, false.
## bool loadWorldForce ( const char * path , bool partial_path )

Loads a world from the specified file path and replaces the current world with it. The world is loaded immediately, breaking the Execution Sequence, therefore should be used either before [Engine::update()](../../../code/fundamentals/execution_sequence/main_loop.md#update) or after [Engine::swap()](../../../code/fundamentals/execution_sequence/main_loop.md#swap). If called in *Engine::update()*, the Execution Sequence will be as follows: *update()* before calling *loadWorldForce(), loadWorldForce(), shutdown()*, continuation of *update()* from the place of interruption, *postUpdate(), swap(), init()*, etc. This function is recommended for the Editor-related use.
### Arguments

- *const char ** **path** - Path to the [file describing the world](../../../principles/world_structure/index.md).
- *bool* **partial_path** - true if the path to the world file is partial; or false if it is a full path.

### Return value

true if the world is loaded successfully; otherwise, false.
## bool saveWorld ( )

Saves the World.
### Return value

true, if the world has been saved successfully; otherwise false.
## bool saveWorld ( const char * path )

Saves the world to the specified location.
### Arguments

- *const char ** **path** - Path to where the world is going to be saved.

### Return value

true, if the world has been saved successfully; otherwise false.
## bool reloadWorld ( )

Reloads the World.
### Return value

true, if the world has been reloaded successfully; otherwise false.
## bool quitWorld ( )

Closes the World.
### Return value

true, if the world has been quit successfully; otherwise false.
## bool addWorld ( const char * name )

Loads a world from a file and adds it to the current World.
### Arguments

- *const char ** **name** - Name of the [file describing the world](../../../principles/world_structure/index.md).

### Return value

true if the world is loaded and added successfully; otherwise, false.
## bool isNode ( int id ) const

Checks if a node with a given ID exists in the World.
### Arguments

- *int* **id** - Node ID.

### Return value

true if the node with the given ID exists; otherwise, false.
## void getNodes ( Vector < Ptr < Node >> & OUT_nodes , bool expand_node_reference = true , bool expand_world_clutter = true ) const

 Collects all instances of all nodes (either loaded from the `*.world` file or created dynamically at run time), including [cache](../../../principles/world_management/index.md#node_cache), [Node Reference internals](../../../api/library/nodes/class.nodereference_cpp.md#unpacking), World Clutters contents (if the corresponding flags are set) and puts them to the specified output list.
> **Notice:** If you need only root nodes to be returned, use [getRootNodes()](#getRootNodes_VECNode_void) instead


### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>> &* **OUT_nodes** - Array with node smart pointers. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *bool* **expand_node_reference** - true to get nodes contained in *NodeReferences*; otherwise, false.
- *bool* **expand_world_clutter** - true to get nodes contained in *WorldClutters*; otherwise, false.

## Ptr < Node > loadNode ( const char * file_path , bool cache = true )

Loads a node (or a hierarchy of nodes) from a `.node / .fbx` file. If the node is loaded successfully, it is managed by the current world (its *[Lifetime](../../../api/library/nodes/class.node_cpp.md#getLifetime_int)* is *[World](../../../api/library/nodes/class.node_cpp.md#LIFETIME)*).
[Cached nodes](../../../principles/world_management/index.md#node_cache) remain in the memory. If you don't intend to load more node references from a certain `*.node` asset, set the **cache** argument to 0 or you can delete cached nodes from the list of world nodes afterwards by using the *[destroyCacheNode()](#destroyCacheNode_cstr_int)* method.


### Arguments

- *const char ** **file_path** - Path to the `*.node` file to be loaded.
- *bool* **cache** - true to use caching of nodes, false not to use.

### Return value

Loaded node; NULL if the node cannot be loaded.
## Ptr < Node > loadNode ( const UGUID & file_guid , bool cache = true )

Loads a node (or a hierarchy of nodes) from a `.node / .fbx` file with the specified file GUID. If the node is loaded successfully, it is managed by the current world (its *[Lifetime](../../../api/library/nodes/class.node_cpp.md#getLifetime_int)* is *[World](../../../api/library/nodes/class.node_cpp.md#LIFETIME)*).
[Cached nodes](../../../principles/world_management/index.md#node_cache) remain in the memory. If you don't intend to load more node references from a certain `*.node` asset, set the **cache** argument to 0 or you can delete cached nodes from the list of world nodes afterwards by using the *[destroyCacheNode()](#destroyCacheNode_cstr_int)* method.


### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **file_guid** - GUID of the `*.node` file to be loaded.
- *bool* **cache** - true to use caching of nodes, false not to use.

### Return value

Loaded node; NULL if the node cannot be loaded.
## bool loadNodes ( const char * file_path , Vector < Ptr < Node >> & OUT_nodes ) const

Loads nodes from a file.
### Arguments

- *const char ** **file_path** - Path to the `*.node` file.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>> &* **OUT_nodes** - Array of nodes' smart pointers to which the loaded nodes are appended. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true if the nodes are loaded successfully; otherwise, false.
## bool saveNode ( const char * file_path , const Ptr < Node > & node , bool binary = 0 )

Saves a given node to a file with due regard for its [local transformation](../../../api/library/nodes/class.node_cpp.md#getTransform_Mat4).
### Arguments

- *const char ** **file_path** - Path to the `*.node` file.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)> &* **node** - Pointer to the node to save.
- *bool* **binary** - If set to true, the node is saved to the binary `*.xml`. This file cannot be read, but using it speeds up the saving of the node and requires less disk space.

### Return value

true if the node is saved successfully; otherwise, false.
## bool saveNodes ( const char * file_path , const Vector < Ptr < Node >> & nodes , bool binary = 0 ) const

Saves nodes to a file.
### Arguments

- *const char ** **file_path** - Path to the `*.node` file.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>> &* **nodes** - Array of nodes' smart pointers to be saved.
- *bool* **binary** - If set to true, the node is saved to the binary `*.xml`. This file cannot be read, but using it speeds up the saving of the node and requires less disk space.

### Return value

true if the nodes are saved successfully; otherwise, false.
## void updateSpatial ( )


Updates the node [BSP (binary space partitioning) tree](../../../principles/world_management/index.md#outdoor).


The engine calls this method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed. As a new node becomes a part of the BSP tree only after this method is called, all engine subsystems (renderer, physics, sound, pathfinding, collisions, intersections, etc.) can process this node only in the next frame. If you need the subsystem to process the node in the very first frame, you can call the *updateSpatial()* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


## Ptr < Node > getNodeByID ( int node_id ) const

Returns a node by its identifier if it exists.
### Arguments

- *int* **node_id** - Node ID.

### Return value

Node, if it exists in the world; otherwise, **nullptr**.
## Ptr < Node > getNodeByName ( const char * name ) const


Returns a node by its name if it exists. If the world contains multiple nodes having the same name, only the first one found shall be returned. To get all nodes having the same name, use the [*getNodesByName()*](#getNodesByName_cstr_VECNode_void) method.


> **Notice:** method filters out isolated node hierarchies and cache nodes, so it does not return nodes having a possessor (*NodeReference / Clutter / Cluster*) among its predecessors or nodes from cache.


### Arguments

- *const char ** **name** - Node name.

### Return value

Node, if it exists in the world; otherwise, **nullptr**.
## void getNodesByName ( const char * name , Vector < Ptr < Node >> & OUT_nodes ) const

Generates a list of nodes in the world with a given name and puts it to **nodes**.
### Arguments

- *const char ** **name** - Node name.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>> &* **OUT_nodes** - List of nodes with the given name (if any); otherwise, **nullptr**. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## Ptr < Node > getNodeByType ( int type ) const

Returns the first node of the specified type in the World. Hidden and system nodes are ignored.
### Arguments

- *int* **type** - Node type identifier, one of the [NODE_*](../../../api/library/nodes/class.node_cpp.md#NODE_BEGIN) values.

### Return value

First node of the specified type, if it exists in the world; otherwise, **nullptr**.
## void getNodesByType ( int type , Vector < Ptr < Node >> & OUT_nodes ) const

Generates a list of nodes of the specified type in the world and puts it to **nodes**. Hidden and system nodes are ignored.
### Arguments

- *int* **type** - Node type identifier, one of the [NODE_*](../../../api/library/nodes/class.node_cpp.md#NODE_BEGIN) values.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>> &* **OUT_nodes** - List of nodes of the given type (if any); otherwise, **nullptr**. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## bool isNode ( const char * name ) const

Checks if a node with a given name exists in the World.
### Arguments

- *const char ** **name** - Node name.

### Return value

true if a node with the specified name exists in the world; otherwise, false.
## void clearBindings ( )

Clears internal buffers with pointers and instances. This function is used for proper cloning of objects with hierarchies, for example, bodies and joints. Should be called before cloning.
## void getRootNodes ( Vector < Ptr < Node >> & OUT_nodes )

Gets all root nodes in the world hierarchy and puts them to nodes. Doesn't include [cached](../../../principles/world_management/index.md#node_cache) nodes.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>> &* **OUT_nodes** - Vector, to which all root nodes of the world hierarchy are to be put. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## int getRootNodeIndex ( const Ptr < Node > & node ) const

Returns the index for the specified root node, that belongs to the world hierarchy.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)> &* **node** - Root node, for which an index is to be obtained.

### Return value

Index of the specified root node if it exists; otherwise, -1.
## void setRootNodeIndex ( const Ptr < Node > & node , int index )

Sets a new index for the specified root node, that belongs to the world hierarchy.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)> &* **node** - Root node, for which a new index is to be set.
- *int* **index** - New index to be set for the specified root node.

## void setNodeIdSeed ( unsigned int seed )

Sets a seed value for random generation of a node ID. This method is used for deterministic generation.
### Arguments

- *unsigned int* **seed** - A seed value.

## void setNodeIdRange ( int from , int to )

Sets a range for random generation of a node ID. This method can be used, for example, to generate IDs for nodes divided in several groups: within a group, IDs will be generated in a separate range.
### Arguments

- *int* **from** - Beginning of the range.
- *int* **to** - End of the range.

## void findNodes ( CallbackBase2 < Ptr < Node >, bool *> * find_node_callback ) const

Traverses the whole world hierarchy and calls the specified callback function for each node found. The traversal starts from the root nodes and goes down the hierarchy, also entering [Node Reference internals](../../../api/library/nodes/class.nodereference_cpp.md#unpacking) and the nodes referenced by World Clutters. Each node is reported only once, the nodes scheduled for deletion are skipped. Unlike the *[getNodes()](#getNodes_VECNode_int_int_void)* method, this one doesn't collect all nodes into a list: the nodes are reported one by one and the callback can cut off the whole hierarchy of the current node, which is faster when you are looking for specific nodes in a large world.
```cpp
CallbackBase2<Ptr<Node>, bool *> *find_nodes_cb = MakeCallback(find_nodes);
World::findNodes(find_nodes_cb);
delete find_nodes_cb;

```


### Arguments

- *[CallbackBase2](../../../api/library/common/callbacks/class.callbackbase2_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>, bool *> ** **find_node_callback** - Callback function to be called for each node found during the traversal. The second argument of the callback is an output flag: set it to true to skip the hierarchy of the current node (its children and the content it references), or leave it false to continue traversing this branch. The callback function must have the following signature: *find_node_callback(**NodePtr** node, **bool *** skip_hierarchy)*

## bool removeNodeFile ( const char * file_path )

Clears [cached](../../../principles/world_management/index.md#node_cache) nodes for the given `*.node` file and removes all related *Node References* from the scene.
When trying to access cached nodes, keep in mind the following:


- if the node was loaded by the name � the node gets stored in the cache by its **name**;
- if the node was loaded from the parent *Node Reference* � the node is stored in the cache by its **GUID**.


Here is an example on how to clear cached nodes and reload them in both cases:


<details>
<summary>Example | Close</summary>

```cpp
NodePtr node = World::loadNode(file_name);
// change something in the node...
World::saveNode(file_name, node);

// clear cache by the name and remove all node references associated with this source from the scene
World::removeNodeFile(file_name);
// clear cache by the GUID (if this node is inside another Node Reference) and remove all node references associated with this source from the scene
World::removeNodeFile(FileSystem::guidToPath(FileSystem::getGUID(file_name)));

```

</details>


### Arguments

- *const char ** **file_path** - Path to the `*.node` file.

### Return value

true if nodes for the given `*.node` file were successfully removed from cache with related *Node References* removed from the scene; otherwise, false.
## bool removeNodeFile ( const UGUID & file_guid )

Clears [cached](../../../principles/world_management/index.md#node_cache) nodes for the given `*.node` file and removes all related *Node References* from the scene.
When trying to access cached nodes, keep in mind the following:


- if the node was loaded by the name � the node gets stored in the cache by its **name**;
- if the node was loaded from the parent *Node Reference* � the node is stored in the cache by its **GUID**.


Here is an example on how to clear cached nodes and reload them in both cases:


<details>
<summary>Example | Close</summary>

```cpp
NodePtr node = World::loadNode(file_name);
// change something in the node...
World::saveNode(file_name, node);

// clear cache by the name and remove all node references associated with this source from the scene
World::removeNodeFile(file_name);
// clear cache by the GUID (if this node is inside another Node Reference) and remove all node references associated with this source from the scene
World::removeNodeFile(FileSystem::guidToPath(FileSystem::getGUID(file_name)));

```

</details>


### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **file_guid** - GUID of the `*.node` file.

### Return value

true if nodes for the given `*.node` file were successfully removed from cache with related *Node References* removed from the scene; otherwise, false.
## bool reloadNodeFile ( const char * file_path )

Clears [cached](../../../principles/world_management/index.md#node_cache) nodes for the given `*.node` file and reloads all related *Node References* in the scene.
When trying to access cached nodes, keep in mind the following:


- if the node was loaded by the name � the node gets stored in the cache by its **name**;
- if the node was loaded from the parent *Node Reference* � the node is stored in the cache by its **GUID**.


Here is an example on how to clear cached nodes and reload them in both cases:


<details>
<summary>Example | Close</summary>

```cpp
NodePtr node = World::loadNode(file_name);
// change something in the node...
World::saveNode(file_name, node);

// clear cache by the name and reload all node references associated with this source
World::reloadNodeFile(file_name);
// clear cache by the GUID (if this node is inside another Node Reference) and reload all node references associated with this source
World::reloadNodeFile(FileSystem::guidToPath(FileSystem::getGUID(file_name)));

```

</details>


### Arguments

- *const char ** **file_path** - Path to the `*.node` file.

### Return value

true if nodes for the given `*.node` file were successfully removed from cache and reloaded from the source file; otherwise, false.
## bool reloadNodeFile ( const UGUID & file_guid )

Clears [cached](../../../principles/world_management/index.md#node_cache) nodes for the given `*.node` file and reloads all related *Node References* in the scene.
When trying to access cached nodes, keep in mind the following:


- if the node was loaded by the name � the node gets stored in the cache by its **name**;
- if the node was loaded from the parent *Node Reference* � the node is stored in the cache by its **GUID**.


Here is an example on how to clear cached nodes and reload them in both cases:


<details>
<summary>Example | Close</summary>

```cpp
NodePtr node = World::loadNode(file_name);
// change something in the node...
World::saveNode(file_name, node);

// clear cache by the name and reload all node references associated with this source
World::reloadNodeFile(file_name);
// clear cache by the GUID (if this node is inside another Node Reference) and reload all node references associated with this source
World::reloadNodeFile(FileSystem::guidToPath(FileSystem::getGUID(file_name)));

```

</details>


### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **file_guid** - GUID of the `*.node` file.

### Return value

true if nodes for the given `*.node` file were successfully removed from cache and reloaded from the source file; otherwise, false.
## bool destroyCacheNode ( const char * file_path )

Clears [cached](../../../principles/world_management/index.md#node_cache) nodes for the given `*.node` file.
When trying to access cached nodes, keep in mind the following:


- if the node was loaded by the name � the node gets stored in the cache by its **name**;
- if the node was loaded from the parent *Node Reference* � the node is stored in the cache by its **GUID**.


Here is an example on how to clear cached nodes in both cases:


<details>
<summary>Example | Close</summary>

```cpp
NodePtr node = World::loadNode(file_name);
// change something in the node...
World::saveNode(file_name, node);

// clear cache by the name
World::destroyCacheNode(file_name);
// clear cache by the GUID (if this node is inside another Node Reference)
World::destroyCacheNode(FileSystem::guidToPath(FileSystem::getGUID(file_name)));

// reload the node
node.deleteForce();
node = World::loadNode(file_name);

```

</details>


### Arguments

- *const char ** **file_path** - Path to the `*.node` file.

### Return value

true if nodes for the given `*.node` file were successfully removed from cache; otherwise, false.
## bool destroyCacheNode ( const UGUID & file_guid )

Clears [cached](../../../principles/world_management/index.md#node_cache) nodes for the given `*.node` file.
When trying to access cached nodes, keep in mind the following:


- if the node was loaded by the name � the node gets stored in the cache by its **name**;
- if the node was loaded from the parent *Node Reference* � the node is stored in the cache by its **GUID**.


Here is an example on how to clear cached nodes in both cases:


<details>
<summary>Example | Close</summary>

```cpp
NodePtr node = World::loadNode(file_name);
// change something in the node...
World::saveNode(file_name, node);

// clear cache by the name
World::destroyCacheNode(file_name);
// clear cache by the GUID (if this node is inside another Node Reference)
World::destroyCacheNode(FileSystem::guidToPath(FileSystem::getGUID(file_name)));

// reload the node
node.deleteForce();
node = World::loadNode(file_name);

```

</details>


### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **file_guid** - GUID of the `*.node` file.

### Return value

true if nodes for a `*.node` file with the given GUID were successfully removed from cache; otherwise, false.
