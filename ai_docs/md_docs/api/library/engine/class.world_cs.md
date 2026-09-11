# Unigine::World Class (CS)

> **Notice:** This class is a singleton.


This class provides functionality for the [world script](../../../code/fundamentals/execution_sequence/app_logic_system.md#world_logic). It contains methods required for loading the world with all its nodes, managing a spatial tree and handling nodes collisions and intersections.


Loading of nodes on demand is managed via the [AsyncQueue Class](../../../api/library/filesystem/class.asyncqueue_cs.md).


> **Notice:** C++ methods running editor script functions are described in the [Engine class](../../../api/library/engine/class.engine_cs.md) reference.


### See also


- [AsyncQueue Class](../../../api/library/filesystem/class.asyncqueue_cs.md) to manage loading nodes and other resources on demand.
- The [Intersections](../../../code/usage/intersections/index_cs.md) article demonstrating how to use intersection-related functions


## World Class

### Enums

## MOVING_IMMOVABLE_NODES_MODE

| Name | Description |
|---|---|
| **BAN** = 0 | Moving of the nodes having the Immovable flag is prohibited. |
| **WARNING** = 1 | Moving of the nodes having the Immovable flag is accompanied by a warning in the console. |
| **ALLOW** = 2 | Moving of the nodes having the Immovable flag is allowed. |

### Properties

## bool UnpackNodeReferences

The value indicating if automatic unpacking of [node references](../../../api/library/nodes/class.nodereference_cs.md) at run time is enabled.
This option can be used to simplify hierarchy management, as when it is enabled all nodes contained in node references will be present in the world hierarchy. When disabled you have to check the hierarchy of each node reference individually (e.g. to find the number of children or manage some of them). The content of *NodeReference* nodes is unpacked only at run time and does not affect your `*.world` and `*.node` files. So, you can use all advantages of node references when building worlds in the UnigineEditor and manage a clear and straightforward hierarchy at run time.


> **Notice:** - This option is available only via code, can be enabled in the [System Script](../../../code/fundamentals/execution_sequence/app_logic_system.md#system_logic) and works for all worlds used in your project.
> - **Auto-unpacking is enabled** in C# projects by default.


## bool AutoReloadNodeReferences

The value indicating if automatic reloading of *Node Reference* nodes is enabled.
If enabled, all *[NodeReference](../../../api/library/nodes/class.nodereference_cs.md)* nodes will reload their `*.node` files, when the *[saveNode()](#saveNode_cstr_Node_int_int)* method is called.


> **Notice:** This option can be used if you modify and save reference nodes at runtime. Otherwise you'll have to manually update pointers for all *[NodeReferences](../../../api/library/nodes/class.nodereference_cs.md)* referring to the changed node.


## float UpdateGridSize

The size of the grid to be used for spatial tree update. The default value is an average one, and can be adjusted when necessary depending on the scene.
## float Distance

The distance at which (and farther) nothing will be rendered or simulated.
## float Budget

The value of the world generation budget for grass and clutter objects. New objects are not created when time is out of the budget.
## 🔒︎ bool IsLoaded

The value indicating if the current world is fully loaded.
## string ScriptName

The name of the [world script](../../../principles/world_structure/index.md) `*.usc` file.
## string Path

The path to the [`*.world`-file](../../../principles/world_structure/index.md) where the world is stored.
## bool ScriptExecute

The value indicating if the world script (`*.usc` file) associated with the world should be executed.
## string PhysicsSettings

The name of the `*.physics` file containing default [physics settings](../../../editor2/settings/physics_global/index.md) used by the World.
## string SoundSettings

The name of the `*.sound` file containing default [sound settings](../../../editor2/settings/sound_global/index.md) used by the World.
## string RenderSettings

The name of the `*.render` file containing default [render settings](../../../editor2/settings/render_settings/index.md) used by the World.
## 🔒︎ string LoadWorldRequestPath

The path to the world to be loaded.
## 🔒︎ bool IsLoadWorldRequested

The value indicating if another world is going to be loaded in the next frame.
## World.MOVING_IMMOVABLE_NODES_MODE MovingImmovableNodeMode

***Console*:**`world_moving_immovable_node_mode`The  mode of handling attempts to move nodes having the *[Immovable](../../../editor2/node_parameters/transformation_common/index.md#clutter)* flag enabled.
> **Notice:** Please be aware that there are two cases when you may disable warnings and allow movement of *Immovable* nodes:
> - At run-time for procedural generation of levels. This may cause some freezing but won't affect performance much. Upon completion of the generation process you should enable warnings again.
> - On world initialization, this will change world loading time but won't affect overall performance.


## string ExperimentalNavigationSettings

The path to the file holding the navigation settings of the world � the registry of areas and flags that the [ExperimentalNavigation](../../../api/library/pathfinding/class.experimentalnavigation_cs.md) singleton exposes. Keeping it in a file lets several worlds share one set of area definitions instead of each carrying its own copy.
## bool AsyncLoadNodeReferences

The value indicating if asynchronous loading of Node References is enabled.
## 🔒︎ Event< Node > EventNodeRemoved

The event triggered when a node is removed from the world. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Node **node**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the NodeRemoved event handler
void noderemoved_event_handler(Node node)
{
	Log.Message("\Handling NodeRemoved event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections noderemoved_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
World.EventNodeRemoved.Connect(noderemoved_event_connections, noderemoved_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
World.EventNodeRemoved.Connect(noderemoved_event_connections, (Node node) => {
		Log.Message("Handling NodeRemoved event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
noderemoved_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the NodeRemoved event with a handler function
World.EventNodeRemoved.Connect(noderemoved_event_handler);

// remove subscription to the NodeRemoved event later by the handler function
World.EventNodeRemoved.Disconnect(noderemoved_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection noderemoved_event_connection;

// subscribe to the NodeRemoved event with a lambda handler function and keeping the connection
noderemoved_event_connection = World.EventNodeRemoved.Connect((Node node) => {
		Log.Message("Handling NodeRemoved event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
noderemoved_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
noderemoved_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
noderemoved_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring NodeRemoved events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
World.EventNodeRemoved.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
World.EventNodeRemoved.Enabled = true;

```

</details>

## 🔒︎ Event< Node > EventNodeAdded

The event triggered when a node is added into the world, including creation of a node from code. The event is also triggered when a the world is loaded from the xml file. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Node **node**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the NodeAdded event handler
void nodeadded_event_handler(Node node)
{
	Log.Message("\Handling NodeAdded event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections nodeadded_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
World.EventNodeAdded.Connect(nodeadded_event_connections, nodeadded_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
World.EventNodeAdded.Connect(nodeadded_event_connections, (Node node) => {
		Log.Message("Handling NodeAdded event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
nodeadded_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the NodeAdded event with a handler function
World.EventNodeAdded.Connect(nodeadded_event_handler);

// remove subscription to the NodeAdded event later by the handler function
World.EventNodeAdded.Disconnect(nodeadded_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection nodeadded_event_connection;

// subscribe to the NodeAdded event with a lambda handler function and keeping the connection
nodeadded_event_connection = World.EventNodeAdded.Connect((Node node) => {
		Log.Message("Handling NodeAdded event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
nodeadded_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
nodeadded_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
nodeadded_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring NodeAdded events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
World.EventNodeAdded.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
World.EventNodeAdded.Enabled = true;

```

</details>

## 🔒︎ Event EventPostWorldShutdown

The event triggered after calling all WorldLogic::shutdown() methods. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the PostWorldShutdown event handler
void postworldshutdown_event_handler()
{
	Log.Message("\Handling PostWorldShutdown event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections postworldshutdown_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
World.EventPostWorldShutdown.Connect(postworldshutdown_event_connections, postworldshutdown_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
World.EventPostWorldShutdown.Connect(postworldshutdown_event_connections, () => {
		Log.Message("Handling PostWorldShutdown event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
postworldshutdown_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the PostWorldShutdown event with a handler function
World.EventPostWorldShutdown.Connect(postworldshutdown_event_handler);

// remove subscription to the PostWorldShutdown event later by the handler function
World.EventPostWorldShutdown.Disconnect(postworldshutdown_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection postworldshutdown_event_connection;

// subscribe to the PostWorldShutdown event with a lambda handler function and keeping the connection
postworldshutdown_event_connection = World.EventPostWorldShutdown.Connect(() => {
		Log.Message("Handling PostWorldShutdown event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
postworldshutdown_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
postworldshutdown_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
postworldshutdown_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring PostWorldShutdown events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
World.EventPostWorldShutdown.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
World.EventPostWorldShutdown.Enabled = true;

```

</details>

## 🔒︎ Event EventPreWorldShutdown

The event triggered before calling all WorldLogic::shutdown() methods. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the PreWorldShutdown event handler
void preworldshutdown_event_handler()
{
	Log.Message("\Handling PreWorldShutdown event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections preworldshutdown_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
World.EventPreWorldShutdown.Connect(preworldshutdown_event_connections, preworldshutdown_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
World.EventPreWorldShutdown.Connect(preworldshutdown_event_connections, () => {
		Log.Message("Handling PreWorldShutdown event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
preworldshutdown_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the PreWorldShutdown event with a handler function
World.EventPreWorldShutdown.Connect(preworldshutdown_event_handler);

// remove subscription to the PreWorldShutdown event later by the handler function
World.EventPreWorldShutdown.Disconnect(preworldshutdown_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection preworldshutdown_event_connection;

// subscribe to the PreWorldShutdown event with a lambda handler function and keeping the connection
preworldshutdown_event_connection = World.EventPreWorldShutdown.Connect(() => {
		Log.Message("Handling PreWorldShutdown event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
preworldshutdown_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
preworldshutdown_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
preworldshutdown_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring PreWorldShutdown events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
World.EventPreWorldShutdown.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
World.EventPreWorldShutdown.Enabled = true;

```

</details>

## 🔒︎ Event EventPostWorldInit

The event triggered after calling all WorldLogic::init() methods. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** Forced closing of the Engine should be disabled with the [`-auto_quit 0`](../../../code/command_line.md#auto_quit) command-line option.


> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the PostWorldInit event handler
void postworldinit_event_handler()
{
	Log.Message("\Handling PostWorldInit event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections postworldinit_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
World.EventPostWorldInit.Connect(postworldinit_event_connections, postworldinit_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
World.EventPostWorldInit.Connect(postworldinit_event_connections, () => {
		Log.Message("Handling PostWorldInit event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
postworldinit_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the PostWorldInit event with a handler function
World.EventPostWorldInit.Connect(postworldinit_event_handler);

// remove subscription to the PostWorldInit event later by the handler function
World.EventPostWorldInit.Disconnect(postworldinit_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection postworldinit_event_connection;

// subscribe to the PostWorldInit event with a lambda handler function and keeping the connection
postworldinit_event_connection = World.EventPostWorldInit.Connect(() => {
		Log.Message("Handling PostWorldInit event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
postworldinit_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
postworldinit_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
postworldinit_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring PostWorldInit events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
World.EventPostWorldInit.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
World.EventPostWorldInit.Enabled = true;

```

</details>

## 🔒︎ Event EventPreWorldInit

The event triggered before calling all WorldLogic::init() methods. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the PreWorldInit event handler
void preworldinit_event_handler()
{
	Log.Message("\Handling PreWorldInit event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections preworldinit_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
World.EventPreWorldInit.Connect(preworldinit_event_connections, preworldinit_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
World.EventPreWorldInit.Connect(preworldinit_event_connections, () => {
		Log.Message("Handling PreWorldInit event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
preworldinit_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the PreWorldInit event with a handler function
World.EventPreWorldInit.Connect(preworldinit_event_handler);

// remove subscription to the PreWorldInit event later by the handler function
World.EventPreWorldInit.Disconnect(preworldinit_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection preworldinit_event_connection;

// subscribe to the PreWorldInit event with a lambda handler function and keeping the connection
preworldinit_event_connection = World.EventPreWorldInit.Connect(() => {
		Log.Message("Handling PreWorldInit event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
preworldinit_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
preworldinit_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
preworldinit_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring PreWorldInit events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
World.EventPreWorldInit.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
World.EventPreWorldInit.Enabled = true;

```

</details>

## 🔒︎ Event<string, Node > EventPostNodeSave

The event triggered after calling the World::saveNode() method. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(string **world_file_path**, Node **node**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the PostNodeSave event handler
void postnodesave_event_handler(string world_file_path,  Node node)
{
	Log.Message("\Handling PostNodeSave event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections postnodesave_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
World.EventPostNodeSave.Connect(postnodesave_event_connections, postnodesave_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
World.EventPostNodeSave.Connect(postnodesave_event_connections, (string world_file_path,  Node node) => {
		Log.Message("Handling PostNodeSave event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
postnodesave_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the PostNodeSave event with a handler function
World.EventPostNodeSave.Connect(postnodesave_event_handler);

// remove subscription to the PostNodeSave event later by the handler function
World.EventPostNodeSave.Disconnect(postnodesave_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection postnodesave_event_connection;

// subscribe to the PostNodeSave event with a lambda handler function and keeping the connection
postnodesave_event_connection = World.EventPostNodeSave.Connect((string world_file_path,  Node node) => {
		Log.Message("Handling PostNodeSave event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
postnodesave_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
postnodesave_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
postnodesave_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring PostNodeSave events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
World.EventPostNodeSave.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
World.EventPostNodeSave.Enabled = true;

```

</details>

## 🔒︎ Event<string, Node > EventPreNodeSave

The event triggered before calling the World::saveNode() method. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(string **world_file_path**, Node **node**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the PreNodeSave event handler
void prenodesave_event_handler(string world_file_path,  Node node)
{
	Log.Message("\Handling PreNodeSave event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections prenodesave_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
World.EventPreNodeSave.Connect(prenodesave_event_connections, prenodesave_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
World.EventPreNodeSave.Connect(prenodesave_event_connections, (string world_file_path,  Node node) => {
		Log.Message("Handling PreNodeSave event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
prenodesave_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the PreNodeSave event with a handler function
World.EventPreNodeSave.Connect(prenodesave_event_handler);

// remove subscription to the PreNodeSave event later by the handler function
World.EventPreNodeSave.Disconnect(prenodesave_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection prenodesave_event_connection;

// subscribe to the PreNodeSave event with a lambda handler function and keeping the connection
prenodesave_event_connection = World.EventPreNodeSave.Connect((string world_file_path,  Node node) => {
		Log.Message("Handling PreNodeSave event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
prenodesave_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
prenodesave_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
prenodesave_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring PreNodeSave events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
World.EventPreNodeSave.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
World.EventPreNodeSave.Enabled = true;

```

</details>

## 🔒︎ Event<string> EventPostWorldClear

The event triggered after clearing the World. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(string **world_file_path**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the PostWorldClear event handler
void postworldclear_event_handler(string world_file_path)
{
	Log.Message("\Handling PostWorldClear event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections postworldclear_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
World.EventPostWorldClear.Connect(postworldclear_event_connections, postworldclear_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
World.EventPostWorldClear.Connect(postworldclear_event_connections, (string world_file_path) => {
		Log.Message("Handling PostWorldClear event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
postworldclear_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the PostWorldClear event with a handler function
World.EventPostWorldClear.Connect(postworldclear_event_handler);

// remove subscription to the PostWorldClear event later by the handler function
World.EventPostWorldClear.Disconnect(postworldclear_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection postworldclear_event_connection;

// subscribe to the PostWorldClear event with a lambda handler function and keeping the connection
postworldclear_event_connection = World.EventPostWorldClear.Connect((string world_file_path) => {
		Log.Message("Handling PostWorldClear event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
postworldclear_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
postworldclear_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
postworldclear_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring PostWorldClear events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
World.EventPostWorldClear.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
World.EventPostWorldClear.Enabled = true;

```

</details>

## 🔒︎ Event<string> EventPreWorldClear

The event triggered before clearing the world � either closing the current world or preparing to load the next World. This event always takes place in Engine::swap(), i.e. in the end of the frame. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(string **world_file_path**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the PreWorldClear event handler
void preworldclear_event_handler(string world_file_path)
{
	Log.Message("\Handling PreWorldClear event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections preworldclear_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
World.EventPreWorldClear.Connect(preworldclear_event_connections, preworldclear_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
World.EventPreWorldClear.Connect(preworldclear_event_connections, (string world_file_path) => {
		Log.Message("Handling PreWorldClear event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
preworldclear_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the PreWorldClear event with a handler function
World.EventPreWorldClear.Connect(preworldclear_event_handler);

// remove subscription to the PreWorldClear event later by the handler function
World.EventPreWorldClear.Disconnect(preworldclear_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection preworldclear_event_connection;

// subscribe to the PreWorldClear event with a lambda handler function and keeping the connection
preworldclear_event_connection = World.EventPreWorldClear.Connect((string world_file_path) => {
		Log.Message("Handling PreWorldClear event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
preworldclear_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
preworldclear_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
preworldclear_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring PreWorldClear events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
World.EventPreWorldClear.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
World.EventPreWorldClear.Enabled = true;

```

</details>

## 🔒︎ Event<string> EventPostWorldSave

The event triggered after saving the World. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(string **world_file_path**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the PostWorldSave event handler
void postworldsave_event_handler(string world_file_path)
{
	Log.Message("\Handling PostWorldSave event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections postworldsave_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
World.EventPostWorldSave.Connect(postworldsave_event_connections, postworldsave_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
World.EventPostWorldSave.Connect(postworldsave_event_connections, (string world_file_path) => {
		Log.Message("Handling PostWorldSave event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
postworldsave_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the PostWorldSave event with a handler function
World.EventPostWorldSave.Connect(postworldsave_event_handler);

// remove subscription to the PostWorldSave event later by the handler function
World.EventPostWorldSave.Disconnect(postworldsave_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection postworldsave_event_connection;

// subscribe to the PostWorldSave event with a lambda handler function and keeping the connection
postworldsave_event_connection = World.EventPostWorldSave.Connect((string world_file_path) => {
		Log.Message("Handling PostWorldSave event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
postworldsave_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
postworldsave_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
postworldsave_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring PostWorldSave events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
World.EventPostWorldSave.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
World.EventPostWorldSave.Enabled = true;

```

</details>

## 🔒︎ Event<string> EventPreWorldSave

The event triggered before saving the World. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(string **world_file_path**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the PreWorldSave event handler
void preworldsave_event_handler(string world_file_path)
{
	Log.Message("\Handling PreWorldSave event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections preworldsave_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
World.EventPreWorldSave.Connect(preworldsave_event_connections, preworldsave_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
World.EventPreWorldSave.Connect(preworldsave_event_connections, (string world_file_path) => {
		Log.Message("Handling PreWorldSave event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
preworldsave_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the PreWorldSave event with a handler function
World.EventPreWorldSave.Connect(preworldsave_event_handler);

// remove subscription to the PreWorldSave event later by the handler function
World.EventPreWorldSave.Disconnect(preworldsave_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection preworldsave_event_connection;

// subscribe to the PreWorldSave event with a lambda handler function and keeping the connection
preworldsave_event_connection = World.EventPreWorldSave.Connect((string world_file_path) => {
		Log.Message("Handling PreWorldSave event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
preworldsave_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
preworldsave_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
preworldsave_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring PreWorldSave events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
World.EventPreWorldSave.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
World.EventPreWorldSave.Enabled = true;

```

</details>

## 🔒︎ Event<string> EventPostWorldLoad

The event triggered after loading the World. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(string **world_file_path**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the PostWorldLoad event handler
void postworldload_event_handler(string world_file_path)
{
	Log.Message("\Handling PostWorldLoad event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections postworldload_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
World.EventPostWorldLoad.Connect(postworldload_event_connections, postworldload_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
World.EventPostWorldLoad.Connect(postworldload_event_connections, (string world_file_path) => {
		Log.Message("Handling PostWorldLoad event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
postworldload_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the PostWorldLoad event with a handler function
World.EventPostWorldLoad.Connect(postworldload_event_handler);

// remove subscription to the PostWorldLoad event later by the handler function
World.EventPostWorldLoad.Disconnect(postworldload_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection postworldload_event_connection;

// subscribe to the PostWorldLoad event with a lambda handler function and keeping the connection
postworldload_event_connection = World.EventPostWorldLoad.Connect((string world_file_path) => {
		Log.Message("Handling PostWorldLoad event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
postworldload_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
postworldload_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
postworldload_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring PostWorldLoad events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
World.EventPostWorldLoad.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
World.EventPostWorldLoad.Enabled = true;

```

</details>

## 🔒︎ Event<string> EventPreWorldLoad

The event triggered before loading the World. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(string **world_file_path**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the PreWorldLoad event handler
void preworldload_event_handler(string world_file_path)
{
	Log.Message("\Handling PreWorldLoad event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections preworldload_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
World.EventPreWorldLoad.Connect(preworldload_event_connections, preworldload_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
World.EventPreWorldLoad.Connect(preworldload_event_connections, (string world_file_path) => {
		Log.Message("Handling PreWorldLoad event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
preworldload_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the PreWorldLoad event with a handler function
World.EventPreWorldLoad.Connect(preworldload_event_handler);

// remove subscription to the PreWorldLoad event later by the handler function
World.EventPreWorldLoad.Disconnect(preworldload_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection preworldload_event_connection;

// subscribe to the PreWorldLoad event with a lambda handler function and keeping the connection
preworldload_event_connection = World.EventPreWorldLoad.Connect((string world_file_path) => {
		Log.Message("Handling PreWorldLoad event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
preworldload_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
preworldload_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
preworldload_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring PreWorldLoad events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
World.EventPreWorldLoad.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
World.EventPreWorldLoad.Enabled = true;

```

</details>

### Members

---

## bool GetCollision ( WorldBoundBox bb , Object [] OUT_objects )


Searches for all [collider objects](../../../principles/physics/collision/index.md#collider) within a given bounding box.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *[WorldBoundBox](../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bb** - Bounding box.
- *[Object](../../../api/library/objects/class.object_cs.md)[]* **OUT_objects** - Array with collider objects' smart pointers. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true if collider objects are found; otherwise, false.
## bool GetCollision ( WorldBoundSphere bs , Object [] OUT_objects )


Searches for all [collider objects](../../../principles/physics/collision/index.md#collider) within a given bounding sphere.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *[WorldBoundSphere](../../../api/library/math/cs/bounds/worldboundsphere_cs.md)* **bs** - Bounding sphere.
- *[Object](../../../api/library/objects/class.object_cs.md)[]* **OUT_objects** - Array with collider objects' smart pointers. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true if collider objects are found; otherwise, false.
## bool GetCollision ( WorldBoundFrustum bf , Object [] OUT_objects )


Searches for all [collider objects](../../../principles/physics/collision/index.md#collider) within a given bounding frustum.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *[WorldBoundFrustum](../../../api/library/math/cs/bounds/worldboundfrustum_cs.md)* **bf** - Bounding frustum.
- *[Object](../../../api/library/objects/class.object_cs.md)[]* **OUT_objects** - Array with collider objects' smart pointers. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true if collider objects are found; otherwise, false.
## bool GetCollision ( vec3 p0 , vec3 p1 , Object [] OUT_objects )


Performs tracing from the p0 point to the p1 point to find all [collider objects](../../../principles/physics/collision/index.md#collider) intersected by the line. This function detects intersection with surfaces (polygons) of mesh and terrain objects.


Collisions with the surface can be found only if the following conditions are fulfilled:


1. The surface is enabled.
2. Per-surface [Collision](../../../api/library/objects/class.object_cs.md#setCollision_int_int_void) flag is enabled.
3. The surface has a material assigned.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *vec3* **p0** - The start point coordinates.
- *vec3* **p1** - The end point coordinates.
- *[Object](../../../api/library/objects/class.object_cs.md)[]* **OUT_objects** - Array with collider objects' smart pointers. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true if collider objects are found; otherwise, false.
## void SetData ( string name , string data )

Sets user data associated with the world with the specified key. In the `*.world` file, the data is set in the data tag with the specified key.
### Arguments

- *string* **name** - String containing a key identifying user data to be stored in the `*.world` file. > **Notice:** The "editor_data" key is reserved for the UnigineEditor.
- *string* **data** - New user data.

## string GetData ( string name )

Returns user string data associated with the world by the specified key. This string is written directly into the data tag of the `*.world` file with the specified key.
### Arguments

- *string* **name** - String containing a key identifying user data stored in the `*.world` file. > **Notice:** The "editor_data" key is reserved for the UnigineEditor.

### Return value

User string data.
## bool HasData ( string name )

Checks whether user string data associated with the world by the specified key is stored in the data tag of the `*.world` file.
### Arguments

- *string* **name** - String containing a key identifying user data stored in the `*.world` file. > **Notice:** The "editor_data" key is reserved for the UnigineEditor.

### Return value

true if user string data associated with the world by the specified key is stored in the data tag of the `*.world` file; otherwise, false.
## void RemoveData ( string name )

Removes user string data associated with the world by the specified key. This string is stored in the data tag of the `*.world` file with the specified key.
### Arguments

- *string* **name** - String containing a key identifying user data stored in the `*.world` file. > **Notice:** The "editor_data" key is reserved for the UnigineEditor.

## Object GetIntersection ( vec3 p0 , vec3 p1 , int mask )


Performs tracing from the p0 point to the p1 point to find **the first object intersected by the line**. This function detects intersection with surfaces (polygons) of meshes. An intersection can be found only if an object has a matching intersection mask.


Intersections with the surface can be found only if the following conditions are fulfilled:


1. The surface is enabled.
2. Per-surface [Intersection](../../../api/library/objects/class.object_cs.md#setIntersection_int_int_void) flag is enabled.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *vec3* **p0** - Line start point coordinates.
- *vec3* **p1** - Line end point coordinates.
- *int* **mask** - Intersection mask. If 0 is passed, the function will return NULL.

### Return value

Intersected object.
## Object GetIntersection ( vec3 p0 , vec3 p1 , int mask , Node [] exclude )


Performs tracing from the p0 point to the p1 point to find **the first object intersected by the line** (except for the ones passed in the **exclude** list). This function detects intersection with surfaces (polygons) of meshes. An intersection can be found only if an object has a matching intersection mask.


Intersections with the surface can be found only if the following conditions are fulfilled:


1. The surface is enabled.
2. Per-surface [Intersection](../../../api/library/objects/class.object_cs.md#setIntersection_int_int_void) flag is enabled.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *vec3* **p0** - Line start point coordinates.
- *vec3* **p1** - Line end point coordinates.
- *int* **mask** - Intersection mask. If 0 is passed, the function will return NULL.
- *[Node](../../../api/library/nodes/class.node_cs.md)[]* **exclude** - List of nodes to be ignored when searching for intersection by the traced line.

### Return value

The first intersected object found at the line (except for the ones passed in the **exclude** list); nullptr if there was no intersection.
## Object GetIntersection ( vec3 p0 , vec3 p1 , int mask , WorldIntersection intersection )


Performs tracing from the p0 point to the p1 point to find **the first object intersecting the line**. This function detects intersection with surfaces (polygons) of meshes. An intersection can be found only if an object is matching the intersection mask.


Intersections with the surface can be found only if the following conditions are fulfilled:


1. The surface is enabled.
2. Per-surface [Intersection](../../../api/library/objects/class.object_cs.md#setIntersection_int_int_void) flag is enabled.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *vec3* **p0** - Coordinates of the line start point.
- *vec3* **p1** - Coordinates of the line end point.
- *int* **mask** - Intersection mask. If 0 is passed, the function will return NULL.
- *[WorldIntersection](../../../api/library/worlds/class.worldintersection_cs.md)* **intersection** - WorldIntersection object to be filled.

### Return value

First intersected object.
## Object GetIntersection ( vec3 p0 , vec3 p1 , int mask , WorldIntersectionNormal intersection )


Performs tracing from the p0 point to the p1 point to find **the first object intersecting the line**. This function detects intersection with surfaces (polygons) of meshes. An intersection can be found only if an object is matching the intersection mask.


Intersections with the surface can be found only if the following conditions are fulfilled:


1. The surface is enabled.
2. Per-surface [Intersection](../../../api/library/objects/class.object_cs.md#setIntersection_int_int_void) flag is enabled.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *vec3* **p0** - Coordinates of the line start point.
- *vec3* **p1** - Coordinates of the line end point.
- *int* **mask** - Intersection mask. If 0 is passed, the function will return NULL.
- *[WorldIntersectionNormal](../../../api/library/worlds/class.worldintersectionnormal_cs.md)* **intersection** - WorldIntersectionNormal object to be filled.

### Return value

First intersected object.
## Object GetIntersection ( vec3 p0 , vec3 p1 , int mask , WorldIntersectionTexCoord intersection )


Performs tracing from the p0 point to the p1 point to find **the first object intersecting the line**. This function detects intersection with surfaces (polygons) of meshes. An intersection can be found only if an object is matching the intersection mask.


Intersections with the surface can be found only if the following conditions are fulfilled:


1. The surface is enabled.
2. Per-surface [Intersection](../../../api/library/objects/class.object_cs.md#setIntersection_int_int_void) flag is enabled.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *vec3* **p0** - Coordinates of the line start point.
- *vec3* **p1** - Coordinates of the line end point.
- *int* **mask** - Intersection mask. If 0 is passed, the function will return NULL.
- *[WorldIntersectionTexCoord](../../../api/library/worlds/class.worldintersectiontexcoord_cs.md)* **intersection** - WorldIntersectionTexCoord object to be filled.

### Return value

First intersected object.
## Object GetIntersection ( vec3 p0 , vec3 p1 , int mask , Node [] exclude , WorldIntersection intersection )


Performs tracing from the p0 point to the p1 point to find **the first object intersecting the line**. This function detects intersection with surfaces (polygons) of meshes. An intersection can be found only if an object is matching the intersection mask.


Intersections with the surface can be found only if the following conditions are fulfilled:


1. The surface is enabled.
2. Per-surface [Intersection](../../../api/library/objects/class.object_cs.md#setIntersection_int_int_void) flag is enabled.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *vec3* **p0** - Coordinates of the line start point.
- *vec3* **p1** - Coordinates of the line end point.
- *int* **mask** - Intersection mask. If 0 is passed, the function will return NULL.
- *[Node](../../../api/library/nodes/class.node_cs.md)[]* **exclude** - The list of nodes to be excluded.
- *[WorldIntersection](../../../api/library/worlds/class.worldintersection_cs.md)* **intersection** - WorldIntersection object to be filled.

### Return value

First intersected object.
## Object GetIntersection ( vec3 p0 , vec3 p1 , int mask , Node [] exclude , WorldIntersectionNormal intersection )


Performs tracing from the p0 point to the p1 point to find **the first object intersecting the line**. This function detects intersection with surfaces (polygons) of meshes. An intersection can be found only if an object is matching the intersection mask.


Intersections with the surface can be found only if the following conditions are fulfilled:


1. The surface is enabled.
2. Per-surface [Intersection](../../../api/library/objects/class.object_cs.md#setIntersection_int_int_void) flag is enabled.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *vec3* **p0** - Coordinates of the line start point.
- *vec3* **p1** - Coordinates of the line end point.
- *int* **mask** - Intersection mask. If 0 is passed, the function will return NULL.
- *[Node](../../../api/library/nodes/class.node_cs.md)[]* **exclude** - The list of nodes to be excluded.
- *[WorldIntersectionNormal](../../../api/library/worlds/class.worldintersectionnormal_cs.md)* **intersection** - WorldIntersectionNormal object to be filled.

### Return value

First intersected object.
## Object GetIntersection ( vec3 p0 , vec3 p1 , int mask , Node [] exclude , WorldIntersectionTexCoord intersection )


Performs tracing from the p0 point to the p1 point to find **the first object intersected by the line**. This function detects intersection with surfaces (polygons) of meshes. An intersection can be found only if an object is matching the intersection mask.


Intersections with the surface can be found only if the following conditions are fulfilled:


1. The surface is enabled.
2. Per-surface [Intersection](../../../api/library/objects/class.object_cs.md#setIntersection_int_int_void) flag is enabled.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *vec3* **p0** - Coordinates of the line start point.
- *vec3* **p1** - Coordinates of the line end point.
- *int* **mask** - Intersection mask. If 0 is passed, the function will return NULL.
- *[Node](../../../api/library/nodes/class.node_cs.md)[]* **exclude** - The list of nodes to be excluded.
- *[WorldIntersectionTexCoord](../../../api/library/worlds/class.worldintersectiontexcoord_cs.md)* **intersection** - WorldIntersectionTexCoord object to be filled.

### Return value

First intersected object.
## bool GetIntersection ( vec3 p0 , vec3 p1 , Object [] OUT_objects , bool check_surface_flags = true )


Performs tracing from the p0 point to the p1 point to find **objects intersected by the line**. This function detects intersection with objects' bounds.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *vec3* **p0** - Coordinates of the line start point.
- *vec3* **p1** - Coordinates of the line end point.
- *[Object](../../../api/library/objects/class.object_cs.md)[]* **OUT_objects** - Array of intersected objects. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *bool* **check_surface_flags** - true if [surface*Intersection* flags](../../../api/library/objects/class.object_cs.md#getIntersection_int_int) are to be taken into account when checking for intersections with objects; otherwise, false. When set to true objects with surface *Intersection* flags disabled (default setting) will be ignored as non-intersectable.

### Return value

true if intersections are found; otherwise, false.
## bool GetIntersection ( WorldBoundBox bb , Object [] OUT_objects )


Searches for intersections **with objects** that are found in a given bounding box.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *[WorldBoundBox](../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bb** - Bounding box where intersection search will be performed.
- *[Object](../../../api/library/objects/class.object_cs.md)[]* **OUT_objects** - Array of intersected objects. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true if intersections are found; otherwise, false.
## bool GetIntersection ( WorldBoundBox bb , Node [] OUT_nodes )


Searches for intersections **with nodes** that are found in a given bounding box.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *[WorldBoundBox](../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bb** - Bounding box where intersection search will be performed.
- *[Node](../../../api/library/nodes/class.node_cs.md)[]* **OUT_nodes** - Array of intersected nodes. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true if intersections are found; otherwise, false.
## bool GetIntersection ( WorldBoundBox bb , Node.TYPE type , Node [] OUT_nodes )


Searches for intersections **with specified type of nodes** that are found in a given bounding box.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *[WorldBoundBox](../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bb** - Bounding box where intersection search will be performed.
- *[Node.TYPE](../../../api/library/nodes/class.node_cs.md#TYPE)* **type** - Node type filter. Only the nodes of the specified type will be checked.
- *[Node](../../../api/library/nodes/class.node_cs.md)[]* **OUT_nodes** - Array of intersected nodes. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true if intersections are found; otherwise, false.
## bool GetIntersection ( WorldBoundSphere bs , Object [] OUT_objects )


Searches for intersections **with objects** that are found in a given bounding sphere.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *[WorldBoundSphere](../../../api/library/math/cs/bounds/worldboundsphere_cs.md)* **bs** - Bounding sphere where intersection search will be performed.
- *[Object](../../../api/library/objects/class.object_cs.md)[]* **OUT_objects** - Array of intersected objects. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true if intersections are found; otherwise, false.
## bool GetIntersection ( WorldBoundSphere bs , Node [] OUT_nodes )


Searches for intersections **with nodes** that are found in a given bounding sphere.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *[WorldBoundSphere](../../../api/library/math/cs/bounds/worldboundsphere_cs.md)* **bs** - Bounding sphere where intersection search will be performed.
- *[Node](../../../api/library/nodes/class.node_cs.md)[]* **OUT_nodes** - Array of intersected nodes. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true if intersections are found; otherwise, false.
## bool GetIntersection ( WorldBoundSphere bs , Node.TYPE type , Node [] OUT_nodes )


Searches for intersections **with nodes of the specified type** that are found in a given bounding sphere.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *[WorldBoundSphere](../../../api/library/math/cs/bounds/worldboundsphere_cs.md)* **bs** - Bounding sphere where intersection search will be performed.
- *[Node.TYPE](../../../api/library/nodes/class.node_cs.md#TYPE)* **type** - Node type filter. Only the nodes of the specified type will be checked.
- *[Node](../../../api/library/nodes/class.node_cs.md)[]* **OUT_nodes** - Array of intersected nodes. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true if intersections are found; otherwise, false.
## bool GetIntersection ( WorldBoundFrustum bf , Object [] OUT_objects )


Searches for intersections **with Objects** that are found in a given bounding frustum. This method catches all objects independent of their visibility (i.e., if an object is disabled, any of its LODs are disabled, or it is out of the [visibility distance](../../../editor2/settings/render_settings/visibility_distances/index.md) range, but is located within the bounding frustum, the intersection shall be detected). To check for intersections while taking into account the visibility aspect, use *[getVisibleIntersection()](#getVisibleIntersection_Vec3_WorldBoundFrustum_VECObject_float_int)*. Check the [usage example](../../../code/usage/intersections/index_cs.md#frustrum_search) applying this method.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *[WorldBoundFrustum](../../../api/library/math/cs/bounds/worldboundfrustum_cs.md)* **bf** - Bounding frustum where intersection search will be performed.
- *[Object](../../../api/library/objects/class.object_cs.md)[]* **OUT_objects** - Array of intersected objects. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true if intersections are found; otherwise, false.
## bool GetIntersection ( WorldBoundFrustum bf , Node.TYPE type , Node [] OUT_nodes )


Searches for intersections **with nodes of the specified type** that are found in a given bounding frustum. This method catches all nodes of the specified type independent of their visibility (i.e., if an object is disabled, any of its LODs are disabled, or it is out of the [visibility distance](../../../editor2/settings/render_settings/visibility_distances/index.md) range, but is located within the bounding frustum, the intersection shall be detected). To check for intersections while taking into account the visibility aspect, use *[getVisibleIntersection()](#getVisibleIntersection_Vec3_WorldBoundFrustum_int_VECNode_float_int)*.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *[WorldBoundFrustum](../../../api/library/math/cs/bounds/worldboundfrustum_cs.md)* **bf** - Bounding frustum where intersection search will be performed.
- *[Node.TYPE](../../../api/library/nodes/class.node_cs.md#TYPE)* **type** - Node type filter. Only the nodes of the specified type will be checked.
- *[Node](../../../api/library/nodes/class.node_cs.md)[]* **OUT_nodes** - Array of intersected nodes. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true if intersections are found; otherwise, false.
## bool GetIntersection ( WorldBoundFrustum bf , Node [] OUT_nodes )


Searches for intersections **with nodes of the specified type** that are found in a given bounding frustum. This method catches all nodes independent of their visibility (i.e., if an object is disabled, any of its LODs are disabled, or it is out of the [visibility distance](../../../editor2/settings/render_settings/visibility_distances/index.md) range, but is located within the bounding frustum, the intersection shall be detected). To check for intersections while taking into account the visibility aspect, use *[getVisibleIntersection()](#getVisibleIntersection_Vec3_WorldBoundFrustum_int_VECNode_float_int)*.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *[WorldBoundFrustum](../../../api/library/math/cs/bounds/worldboundfrustum_cs.md)* **bf** - Bounding frustum where intersection search will be performed.
- *[Node](../../../api/library/nodes/class.node_cs.md)[]* **OUT_nodes** - Array of intersected nodes. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true if intersections are found; otherwise, false.
## bool GetVisibleIntersection ( vec3 camera , WorldBoundFrustum bf , Object [] OUT_objects , float max_distance )

Searches for intersections with objects inside a given bounding frustum that are visible to the specified camera position, i.e. [either of its LODs](../../../api/library/objects/class.object_cs.md#setMinVisibleDistance_float_int_void) is within the [visibility distance](../../../editor2/settings/render_settings/visibility_distances/index.md) distance. Unlike the *[getIntersection()](#getIntersection_WorldBoundFrustum_VECObject_int)* method, this one takes the "visibility" concept into account (hidden objects or the ones that are too far away won't be found). Check this [usage example](../../../code/usage/intersections/index_cs.md#frustrum_search) for more details.
### Arguments

- *vec3* **camera** - Position of the camera from which the visibility distance to objects is checked.
- *[WorldBoundFrustum](../../../api/library/math/cs/bounds/worldboundfrustum_cs.md)* **bf** - Bounding frustum inside which intersection search is performed.
- *[Object](../../../api/library/objects/class.object_cs.md)[]* **OUT_objects** - Array of intersected objects. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *float* **max_distance** - Maximum visibility distance for objects, in units. If the distance from the specified camera position to an object exceeds this limit, the intersection is not registered even if the node is within the specified bounding frustum.

### Return value

true if at least one intersection is found; otherwise, false.
## bool GetVisibleIntersection ( vec3 camera , WorldBoundFrustum bf , Node.TYPE type , Node [] OUT_nodes , float max_distance )


Searches for intersections with nodes inside a given bounding frustum that are visible to the specified camera position, i.e. [either of its LODs](../../../api/library/objects/class.object_cs.md#setMinVisibleDistance_float_int_void) is within the [visibility distance](../../../editor2/settings/render_settings/visibility_distances/index.md) distance. Unlike the *[getIntersection()](#getIntersection_WorldBoundFrustum_int_VECNode_int)* method, this one takes the "visibility" concept into account (hidden nodes or the ones that are too far away won't be found). Check this [usage example](../../../code/usage/intersections/index_cs.md#frustrum_search) for more details.


> **Notice:** This method can be used only for nodes inherited from the [Object](../../../api/library/objects/class.object_cs.md) class, i.e. they have sufraces that store LOD and [visibility distance](../../../editor2/settings/render_settings/visibility_distances/index.md) data.


### Arguments

- *vec3* **camera** - Position of the camera from which the visibility distance to nodes is checked.
- *[WorldBoundFrustum](../../../api/library/math/cs/bounds/worldboundfrustum_cs.md)* **bf** - Bounding frustum inside which intersection search is performed.
- *[Node.TYPE](../../../api/library/nodes/class.node_cs.md#TYPE)* **type** - Node type (one of the [NODE_*](../../../api/library/nodes/class.node_cs.md#DECAL_BEGIN) variables); set it to -1 if you won't use this filter.
- *[Node](../../../api/library/nodes/class.node_cs.md)[]* **OUT_nodes** - Array of intersected nodes. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *float* **max_distance** - Maximum visibility distance for nodes, in units. If the distance from the specified camera position to a node exceeds this limit, the intersection is not registered even if the node is within the specified bounding frustum.

### Return value

true if at least one intersection is found; otherwise, false.
## bool LoadWorld ( string path )

Loads a world from the specified file path and replaces the current world with it. The world is not loaded immediately � loading starts at the [beginning](../../../code/fundamentals/execution_sequence/main_loop.md#update) of the next frame, while the current world is unloaded at the [end](../../../code/fundamentals/execution_sequence/main_loop.md#swap) of the current frame.
### Arguments

- *string* **path** - Path to the [file describing the world](../../../principles/world_structure/index.md).

### Return value

true if the world is loaded successfully; otherwise, false.
## bool LoadWorld ( string path , bool partial_path )

Loads a world from the specified file path and replaces the current world with it. The world is not loaded immediately � loading starts at the [beginning](../../../code/fundamentals/execution_sequence/main_loop.md#update) of the next frame, while the current world is unloaded at the [end](../../../code/fundamentals/execution_sequence/main_loop.md#swap) of the current frame.
### Arguments

- *string* **path** - Path to the [file describing the world](../../../principles/world_structure/index.md).
- *bool* **partial_path** - true if the path to the world file is partial; or false if it is a full path.

### Return value

true if the world is loaded successfully; otherwise, false.
## bool LoadWorldForce ( string path )

Loads a world from the specified file path and replaces the current world with it. The world is loaded immediately, breaking the Execution Sequence, therefore should be used either before [Engine::update()](../../../code/fundamentals/execution_sequence/main_loop.md#update) or after [Engine::swap()](../../../code/fundamentals/execution_sequence/main_loop.md#swap). If called in Engine::update(), the Execution Sequence will be as follows: update() before calling loadWorldForce(), loadWorldForce(), shutdown(), continuation of update() from the place of interruption, postUpdate(), swap(), init(), etc. This function is recommended for the Editor-related use.
### Arguments

- *string* **path** - Path to the [file describing the world](../../../principles/world_structure/index.md).

### Return value

true if the world is loaded successfully; otherwise, false.
## bool LoadWorldForce ( string path , bool partial_path )

Loads a world from the specified file path and replaces the current world with it. The world is loaded immediately, breaking the Execution Sequence, therefore should be used either before [Engine::update()](../../../code/fundamentals/execution_sequence/main_loop.md#update) or after [Engine::swap()](../../../code/fundamentals/execution_sequence/main_loop.md#swap). If called in *Engine::update()*, the Execution Sequence will be as follows: *update()* before calling *loadWorldForce(), loadWorldForce(), shutdown()*, continuation of *update()* from the place of interruption, *postUpdate(), swap(), init()*, etc. This function is recommended for the Editor-related use.
### Arguments

- *string* **path** - Path to the [file describing the world](../../../principles/world_structure/index.md).
- *bool* **partial_path** - true if the path to the world file is partial; or false if it is a full path.

### Return value

true if the world is loaded successfully; otherwise, false.
## bool SaveWorld ( )

Saves the World.
### Return value

true, if the world has been saved successfully; otherwise false.
## bool SaveWorld ( string path )

Saves the world to the specified location.
### Arguments

- *string* **path** - Path to where the world is going to be saved.

### Return value

true, if the world has been saved successfully; otherwise false.
## bool ReloadWorld ( )

Reloads the World.
### Return value

true, if the world has been reloaded successfully; otherwise false.
## bool QuitWorld ( )

Closes the World.
### Return value

true, if the world has been quit successfully; otherwise false.
## bool AddWorld ( string name )

Loads a world from a file and adds it to the current World.
### Arguments

- *string* **name** - Name of the [file describing the world](../../../principles/world_structure/index.md).

### Return value

true if the world is loaded and added successfully; otherwise, false.
## bool IsNode ( int id )

Checks if a node with a given ID exists in the World.
### Arguments

- *int* **id** - Node ID.

### Return value

true if the node with the given ID exists; otherwise, false.
## void GetNodes ( Node [] OUT_nodes , bool expand_node_reference = true , bool expand_world_clutter = true )

 Collects all instances of all nodes (either loaded from the `*.world` file or created dynamically at run time), including [cache](../../../principles/world_management/index.md#node_cache), [Node Reference internals](../../../api/library/nodes/class.nodereference_cs.md#unpacking), World Clutters contents (if the corresponding flags are set) and puts them to the specified output list.
> **Notice:** If you need only root nodes to be returned, use [getRootNodes()](#getRootNodes_VECNode_void) instead


### Arguments

- *[Node](../../../api/library/nodes/class.node_cs.md)[]* **OUT_nodes** - Array with node smart pointers. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *bool* **expand_node_reference** - true to get nodes contained in *NodeReferences*; otherwise, false.
- *bool* **expand_world_clutter** - true to get nodes contained in *WorldClutters*; otherwise, false.

## Node LoadNode ( string file_path , bool cache = true )

Loads a node (or a hierarchy of nodes) from a `.node / .fbx` file. If the node is loaded successfully, it is managed by the current world (its *[Lifetime](../../../api/library/nodes/class.node_cs.md#getLifetime_int)* is *[World](../../../api/library/nodes/class.node_cs.md#LIFETIME)*).
[Cached nodes](../../../principles/world_management/index.md#node_cache) remain in the memory. If you don't intend to load more node references from a certain `*.node` asset, set the **cache** argument to 0 or you can delete cached nodes from the list of world nodes afterwards by using the *[destroyCacheNode()](#destroyCacheNode_cstr_int)* method.


### Arguments

- *string* **file_path** - Path to the `*.node` file to be loaded.
- *bool* **cache** - true to use caching of nodes, false not to use.

### Return value

Loaded node; NULL if the node cannot be loaded.
## Node LoadNode ( UGUID file_guid , bool cache = true )

Loads a node (or a hierarchy of nodes) from a `.node / .fbx` file with the specified file GUID. If the node is loaded successfully, it is managed by the current world (its *[Lifetime](../../../api/library/nodes/class.node_cs.md#getLifetime_int)* is *[World](../../../api/library/nodes/class.node_cs.md#LIFETIME)*).
[Cached nodes](../../../principles/world_management/index.md#node_cache) remain in the memory. If you don't intend to load more node references from a certain `*.node` asset, set the **cache** argument to 0 or you can delete cached nodes from the list of world nodes afterwards by using the *[destroyCacheNode()](#destroyCacheNode_cstr_int)* method.


### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **file_guid** - GUID of the `*.node` file to be loaded.
- *bool* **cache** - true to use caching of nodes, false not to use.

### Return value

Loaded node; NULL if the node cannot be loaded.
## bool LoadNodes ( string file_path , Node [] OUT_nodes )

Loads nodes from a file.
### Arguments

- *string* **file_path** - Path to the `*.node` file.
- *[Node](../../../api/library/nodes/class.node_cs.md)[]* **OUT_nodes** - Array of nodes' smart pointers to which the loaded nodes are appended. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true if the nodes are loaded successfully; otherwise, false.
## bool SaveNode ( string file_path , Node node , bool binary = 0 )

Saves a given node to a file with due regard for its [local transformation](../../../api/library/nodes/class.node_cs.md#getTransform_Mat4).
### Arguments

- *string* **file_path** - Path to the `*.node` file.
- *[Node](../../../api/library/nodes/class.node_cs.md)* **node** - Pointer to the node to save.
- *bool* **binary** - If set to true, the node is saved to the binary `*.xml`. This file cannot be read, but using it speeds up the saving of the node and requires less disk space.

### Return value

true if the node is saved successfully; otherwise, false.
## bool SaveNodes ( string file_path , Node [] nodes , bool binary = 0 )

Saves nodes to a file.
### Arguments

- *string* **file_path** - Path to the `*.node` file.
- *[Node](../../../api/library/nodes/class.node_cs.md)[]* **nodes** - Array of nodes' smart pointers to be saved.
- *bool* **binary** - If set to true, the node is saved to the binary `*.xml`. This file cannot be read, but using it speeds up the saving of the node and requires less disk space.

### Return value

true if the nodes are saved successfully; otherwise, false.
## void UpdateSpatial ( )


Updates the node [BSP (binary space partitioning) tree](../../../principles/world_management/index.md#outdoor).


The engine calls this method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed. As a new node becomes a part of the BSP tree only after this method is called, all engine subsystems (renderer, physics, sound, pathfinding, collisions, intersections, etc.) can process this node only in the next frame. If you need the subsystem to process the node in the very first frame, you can call the *updateSpatial()* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


## Node GetNodeByID ( int node_id )

Returns a node by its identifier if it exists.
### Arguments

- *int* **node_id** - Node ID.

### Return value

Node, if it exists in the world; otherwise, **null**.
## Node GetNodeByName ( string name )


Returns a node by its name if it exists. If the world contains multiple nodes having the same name, only the first one found shall be returned. To get all nodes having the same name, use the [*getNodesByName()*](#getNodesByName_cstr_VECNode_void) method.


> **Notice:** method filters out isolated node hierarchies and cache nodes, so it does not return nodes having a possessor (*NodeReference / Clutter / Cluster*) among its predecessors or nodes from cache.


### Arguments

- *string* **name** - Node name.

### Return value

Node, if it exists in the world; otherwise, **null**.
## void GetNodesByName ( string name , Node [] OUT_nodes )

Generates a list of nodes in the world with a given name and puts it to **nodes**.
### Arguments

- *string* **name** - Node name.
- *[Node](../../../api/library/nodes/class.node_cs.md)[]* **OUT_nodes** - List of nodes with the given name (if any); otherwise, **null**. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## Node GetNodeByType ( int type )

Returns the first node of the specified type in the World. Hidden and system nodes are ignored.
### Arguments

- *int* **type** - Node type identifier, one of the [NODE_*](../../../api/library/nodes/class.node_cs.md#NODE_BEGIN) values.

### Return value

First node of the specified type, if it exists in the world; otherwise, **null**.
## void GetNodesByType ( int type , Node [] OUT_nodes )

Generates a list of nodes of the specified type in the world and puts it to **nodes**. Hidden and system nodes are ignored.
### Arguments

- *int* **type** - Node type identifier, one of the [NODE_*](../../../api/library/nodes/class.node_cs.md#NODE_BEGIN) values.
- *[Node](../../../api/library/nodes/class.node_cs.md)[]* **OUT_nodes** - List of nodes of the given type (if any); otherwise, **null**. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## bool IsNode ( string name )

Checks if a node with a given name exists in the World.
### Arguments

- *string* **name** - Node name.

### Return value

true if a node with the specified name exists in the world; otherwise, false.
## void ClearBindings ( )

Clears internal buffers with pointers and instances. This function is used for proper cloning of objects with hierarchies, for example, bodies and joints. Should be called before cloning.
## void GetRootNodes ( Node [] OUT_nodes )

Gets all root nodes in the world hierarchy and puts them to nodes. Doesn't include [cached](../../../principles/world_management/index.md#node_cache) nodes.
### Arguments

- *[Node](../../../api/library/nodes/class.node_cs.md)[]* **OUT_nodes** - Array, to which all root nodes of the world hierarchy are to be put. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## int GetRootNodeIndex ( Node node )

Returns the index for the specified root node, that belongs to the world hierarchy.
### Arguments

- *[Node](../../../api/library/nodes/class.node_cs.md)* **node** - Root node, for which an index is to be obtained.

### Return value

Index of the specified root node if it exists; otherwise, -1.
## void SetRootNodeIndex ( Node node , int index )

Sets a new index for the specified root node, that belongs to the world hierarchy.
### Arguments

- *[Node](../../../api/library/nodes/class.node_cs.md)* **node** - Root node, for which a new index is to be set.
- *int* **index** - New index to be set for the specified root node.

## void SetNodeIdSeed ( uint seed )

Sets a seed value for random generation of a node ID. This method is used for deterministic generation.
### Arguments

- *uint* **seed** - A seed value.

## void SetNodeIdRange ( int from , int to )

Sets a range for random generation of a node ID. This method can be used, for example, to generate IDs for nodes divided in several groups: within a group, IDs will be generated in a separate range.
### Arguments

- *int* **from** - Beginning of the range.
- *int* **to** - End of the range.

## void FindNodes ( FindNodeCallback find_node_callback )

Traverses the whole world hierarchy and calls the specified callback function for each node found. The traversal starts from the root nodes and goes down the hierarchy, also entering [Node Reference internals](../../../api/library/nodes/class.nodereference_cs.md#unpacking) and the nodes referenced by World Clutters. Each node is reported only once, the nodes scheduled for deletion are skipped. Unlike the *[getNodes()](#getNodes_VECNode_int_int_void)* method, this one doesn't collect all nodes into a list: the nodes are reported one by one and the callback can cut off the whole hierarchy of the current node, which is faster when you are looking for specific nodes in a large world.
```csharp
FindNodeCallback find_nodes_cb = new FindNodeCallback(find_nodes);
World.FindNodes(find_nodes_cb);

```


### Arguments

- *FindNodeCallback* **find_node_callback** - Callback function to be called for each node found during the traversal. The second argument of the callback is an output flag: set it to true to skip the hierarchy of the current node (its children and the content it references), or leave it false to continue traversing this branch. The callback function must have the following signature: *FindNodeCallback(**Node** node, **bool[]** skip_hierarchy)*

## bool RemoveNodeFile ( string file_path )

Clears [cached](../../../principles/world_management/index.md#node_cache) nodes for the given `*.node` file and removes all related *Node References* from the scene.
When trying to access cached nodes, keep in mind the following:


- if the node was loaded by the name � the node gets stored in the cache by its **name**;
- if the node was loaded from the parent *Node Reference* � the node is stored in the cache by its **GUID**.


Here is an example on how to clear cached nodes and reload them in both cases:


<details>
<summary>Example | Close</summary>

```csharp
Node node = World.LoadNode(file_name);
// change something in the node...
World.SaveNode(file_name, node);

// clear cache by the name and reload all node references associated with this source
World.RemoveNodeFile(file_name);
// clear cache by the GUID (if this node is inside another Node Reference) and reload all node references associated with this source
World.RemoveNodeFile("guid://" + FileSystem.GetGUID("file_name").GetString());

```

</details>


### Arguments

- *string* **file_path** - Path to the `*.node` file.

### Return value

true if nodes for the given `*.node` file were successfully removed from cache with related *Node References* removed from the scene; otherwise, false.
## bool RemoveNodeFile ( UGUID file_guid )

Clears [cached](../../../principles/world_management/index.md#node_cache) nodes for the given `*.node` file and removes all related *Node References* from the scene.
When trying to access cached nodes, keep in mind the following:


- if the node was loaded by the name � the node gets stored in the cache by its **name**;
- if the node was loaded from the parent *Node Reference* � the node is stored in the cache by its **GUID**.


Here is an example on how to clear cached nodes and reload them in both cases:


<details>
<summary>Example | Close</summary>

```csharp
Node node = World.LoadNode(file_name);
// change something in the node...
World.SaveNode(file_name, node);

// clear cache by the name and reload all node references associated with this source
World.RemoveNodeFile(file_name);
// clear cache by the GUID (if this node is inside another Node Reference) and reload all node references associated with this source
World.RemoveNodeFile("guid://" + FileSystem.GetGUID("file_name").GetString());

```

</details>


### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **file_guid** - GUID of the `*.node` file.

### Return value

true if nodes for the given `*.node` file were successfully removed from cache with related *Node References* removed from the scene; otherwise, false.
## bool ReloadNodeFile ( string file_path )

Clears [cached](../../../principles/world_management/index.md#node_cache) nodes for the given `*.node` file and reloads all related *Node References* in the scene.
When trying to access cached nodes, keep in mind the following:


- if the node was loaded by the name � the node gets stored in the cache by its **name**;
- if the node was loaded from the parent *Node Reference* � the node is stored in the cache by its **GUID**.


Here is an example on how to clear cached nodes and reload them in both cases:


<details>
<summary>Example | Close</summary>

```csharp
Node node = World.LoadNode(file_name);
// change something in the node...
World.SaveNode(file_name, node);

// clear cache by the name and reload all node references associated with this source
World.ReloadNodeFile(file_name);
// clear cache by the GUID (if this node is inside another Node Reference) and reload all node references associated with this source
World.ReloadNodeFile("guid://" + FileSystem.GetGUID("file_name").GetString());

```

</details>


### Arguments

- *string* **file_path** - Path to the `*.node` file.

### Return value

true if nodes for the given `*.node` file were successfully removed from cache and reloaded from the source file; otherwise, false.
## bool ReloadNodeFile ( UGUID file_guid )

Clears [cached](../../../principles/world_management/index.md#node_cache) nodes for the given `*.node` file and reloads all related *Node References* in the scene.
When trying to access cached nodes, keep in mind the following:


- if the node was loaded by the name � the node gets stored in the cache by its **name**;
- if the node was loaded from the parent *Node Reference* � the node is stored in the cache by its **GUID**.


Here is an example on how to clear cached nodes and reload them in both cases:


<details>
<summary>Example | Close</summary>

```csharp
Node node = World.LoadNode(file_name);
// change something in the node...
World.SaveNode(file_name, node);

// clear cache by the name and reload all node references associated with this source
World.ReloadNodeFile(file_name);
// clear cache by the GUID (if this node is inside another Node Reference) and reload all node references associated with this source
World.ReloadNodeFile("guid://" + FileSystem.GetGUID("file_name").GetString());

```

</details>


### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **file_guid** - GUID of the `*.node` file.

### Return value

true if nodes for the given `*.node` file were successfully removed from cache and reloaded from the source file; otherwise, false.
## bool DestroyCacheNode ( string file_path )

Clears [cached](../../../principles/world_management/index.md#node_cache) nodes of the given node file.
When trying to access cached nodes, keep in mind the following:


- if the node was loaded by the name � the node gets stored in the cache by its **name**;
- if the node was loaded from the parent *Node Reference* � the node is stored in the cache by its **GUID**.


Here is an example on how to clear cached nodes in both cases:


<details>
<summary>Example | Close</summary>

```csharp
Node node = World.LoadNode(file_name);
// change something in the node...
World.SaveNode(file_name, node);

// clear cache by the name
World.DestroyCacheNode(file_name);
// clear cache by the GUID (if this node is inside another node reference)
World.DestroyCacheNode("guid://" + FileSystem.GetGUID("file_name").GetString());

// reload the node
node.DeleteForce();
node = World.LoadNode(file_name);

```

</details>


### Arguments

- *string* **file_path** - Path to the `*.node` file.

### Return value

true if nodes for the given `*.node` file were successfully removed from cache; otherwise, false.
## bool DestroyCacheNode ( UGUID file_guid )

Clears [cached](../../../principles/world_management/index.md#node_cache) nodes of the given node file.
When trying to access cached nodes, keep in mind the following:


- if the node was loaded by the name � the node gets stored in the cache by its **name**;
- if the node was loaded from the parent *Node Reference* � the node is stored in the cache by its **GUID**.


Here is an example on how to clear cached nodes in both cases:


<details>
<summary>Example | Close</summary>

```csharp
Node node = World.LoadNode(file_name);
// change something in the node...
World.SaveNode(file_name, node);

// clear cache by the name
World.DestroyCacheNode(file_name);
// clear cache by the GUID (if this node is inside another node reference)
World.DestroyCacheNode("guid://" + FileSystem.GetGUID("file_name").GetString());

// reload the node
node.DeleteForce();
node = World.LoadNode(file_name);

```

</details>


### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **file_guid** - GUID of the `*.node` file.

### Return value

true if nodes for a `*.node` file with the given GUID were successfully removed from cache; otherwise, false.
