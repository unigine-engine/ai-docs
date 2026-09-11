# Unigine::NodeTrigger Class (CS)

**Inherits from:** Node


A *[Trigger](../../../objects/nodes/trigger/index.md)* node is a zero-sized node that has no visual representation and triggers events when:


- It is enabled/disabled (the *Enabled* event is triggered).
- Its transformation is changed (the *Position* event is triggered).


The *Trigger* node is usually added as a child node to another node, so that the handler functions were executed on the parent node enabling/disabling or transforming.


For example, to detect if some node has been enabled (for example, a world clutter node that renders nodes only around the camera that has enabled it), the *Trigger* node is added as a child to this node and executes the corresponding function.


### Creating a Trigger Node


To create a *Trigger* node, simply call the NodeTrigger [constructor](#NodeTrigger) and then add the node as a child to another node, for which handlers should be executed.


```csharp
private NodeTrigger trigger;
private ObjectMeshStatic obj;

private void Init()
{

	// create a mesh
	Mesh mesh = new Mesh();
	mesh.AddBoxSurface("box_0", new vec3(1.0f));
	// create a node (e.g. an instance of the ObjectMeshStatic class)
	obj = new ObjectMeshStatic("core/meshes/box.mesh");
	// change material albedo color
	obj.SetMaterialParameterFloat4("albedo_color", new vec4(1.0f, 0.0f, 0.0f, 1.0f), 0);
	// create a trigger node
	trigger = new NodeTrigger();

	// add it as a child to the static mesh
	obj.AddWorldChild(trigger);

}


```


### Editing a Trigger Node


Editing a trigger node includes implementing and specifying the *Enabled* and *Position* event handlers that are executed on enabling or positioning the *Trigger* node correspondingly.


The event handler function must receive at least **1** argument of the NodeTrigger type. In addition, it can also take another 2 arguments of any type.


The event handlers are set via pointers specified when subscribing to the following events: *[EventEnabled](#getEventEnabled_Event)* and *[EventPosition](#getEventPosition_Event)*.


```csharp
private NodeTrigger trigger;
private ObjectMeshStatic obj;

// the position event handler
void position_event_handler(NodeTrigger trigger)
{
	Log.Message("Object position has been changed. New position is: {0}\n", trigger.WorldPosition.ToString());
}
// the enabled event handler
void enabled_event_handler(NodeTrigger trigger)
{
	Log.Message("The enabled event handler is {0}\n", trigger.Enabled);
}

private void Init()
{

	// create a mesh
	Mesh mesh = new Mesh();
	mesh.AddBoxSurface("box_0", new vec3(1.0f));
	// create a node (e.g. an instance of the ObjectMeshStatic class)
	obj = new ObjectMeshStatic("core/meshes/box.mesh");
	// change material albedo color
	obj.SetMaterialParameterFloat4("albedo_color", new vec4(1.0f, 0.0f, 0.0f, 1.0f), 0);
	// create a trigger node
	trigger = new NodeTrigger();

	// add it as a child to the static mesh
	obj.AddWorldChild(trigger);

	// add the enabled event handler to be executed when the node is enabled/disabled
	trigger.EventEnabled.Connect(enabled_event_handler);
	// add the position event handler to be executed when the node position is changed
        trigger.EventPosition.Connect(position_event_handler);

}

private void Update()
{

	float time = Game.Time;
	Vec3 pos = new Vec3(MathLib.Sin(time) * 2.0f, MathLib.Cos(time) * 2.0f, 0.0f);
	// change the enabled flag of the node
	obj.Enabled = pos.x > 0.0f || pos.y > 0.0f;
	// change the node position
	obj.WorldPosition = pos;

}


```


### See Also


- Video tutorial on [How To Use Node Triggers to Detect Changes in Node States](../../../videotutorials/how_to/how_to_cs/node_trigger.md)
- Article on [Event Handling](../../../code/fundamentals/events/index_cs.md#triggers)
- C++ sample
- C# Component sample


## NodeTrigger Class

### Properties

## 🔒︎ Event< NodeTrigger > EventPosition

The Event triggered when the trigger node position has changed. The event handler must receive a *NodeTrigger* as its first argument. In addition, it can also take **2** arguments of any type. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(NodeTrigger **trigger**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Position event handler
void position_event_handler(NodeTrigger trigger)
{
	Log.Message("\Handling Position event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections position_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventPosition.Connect(position_event_connections, position_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventPosition.Connect(position_event_connections, (NodeTrigger trigger) => {
		Log.Message("Handling Position event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
position_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Position event with a handler function
publisher.EventPosition.Connect(position_event_handler);

// remove subscription to the Position event later by the handler function
publisher.EventPosition.Disconnect(position_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection position_event_connection;

// subscribe to the Position event with a lambda handler function and keeping the connection
position_event_connection = publisher.EventPosition.Connect((NodeTrigger trigger) => {
		Log.Message("Handling Position event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
position_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
position_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
position_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Position events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventPosition.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventPosition.Enabled = true;

```

</details>

## 🔒︎ Event< NodeTrigger > EventEnabled

The Event triggered when the trigger node is enabled or disabled. The event handler must receive a *NodeTrigger* as its first argument. In addition, it can also take **2** arguments of any type. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(NodeTrigger **trigger**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Enabled event handler
void enabled_event_handler(NodeTrigger trigger)
{
	Log.Message("\Handling Enabled event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections enabled_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEnabled.Connect(enabled_event_connections, enabled_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEnabled.Connect(enabled_event_connections, (NodeTrigger trigger) => {
		Log.Message("Handling Enabled event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
enabled_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Enabled event with a handler function
publisher.EventEnabled.Connect(enabled_event_handler);

// remove subscription to the Enabled event later by the handler function
publisher.EventEnabled.Disconnect(enabled_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection enabled_event_connection;

// subscribe to the Enabled event with a lambda handler function and keeping the connection
enabled_event_connection = publisher.EventEnabled.Connect((NodeTrigger trigger) => {
		Log.Message("Handling Enabled event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
enabled_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
enabled_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
enabled_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Enabled events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEnabled.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEnabled.Enabled = true;

```

</details>

### Members

---

## NodeTrigger ( )

Constructor. Creates a new trigger node.
## void SetEnabledCallbackName ( string name )

Sets a callback function to be fired when the trigger node is enabled. The callback function must be implemented in the world script (on the UnigineScript side). The callback function can take no arguments, a *[Node](../../../api/library/nodes/class.node_cs.md)*or a *NodeTrigger*.
> **Notice:** The method allows for setting a callback with **0** or **1** argument only.

On UnigineScript side:
```cpp
// implement the enabled callback
void enabled_callback(Node node) {
	log.message("The enabled flag is %d\n", node.isEnabled());
}

```

 On C# side:
```csharp
private void Init()
{

	// create a trigger node
	trigger = new NodeTrigger();


	// set the enabled event handler to be executed when the node is enabled/disabled
        trigger.SetEnabledCallbackName("enabled_event_handler");

}


```


### Arguments

- *string* **name** - Name of the callback function implemented in the world script (UnigineScript side).

## string GetEnabledCallbackName ( )

Returns the name of callback function to be fired on enabling the trigger node. This callback function is set via *[setEnabledCallbackName()](#setEnabledCallbackName_cstr_void)*.
### Return value

Name of the callback function implemented in the world script (UnigineScript side).
## void SetPositionCallbackName ( string name )

Sets a callback function to be fired when the trigger node position has changed. The callback function must be implemented in the world script (on the UnigineScript side). The callback function can take no arguments, a *[Node](../../../api/library/nodes/class.node_cs.md)*or a *NodeTrigger*.
> **Notice:** The method allows for setting a callback with **0** or **1** argument only.

On UnigineScript side:
```cpp
// implement the position callback
void position_callback(Node node) {
	log.message("A new position of the node is %s\n", typeinfo(node.getWorldPosition()));
}

```

 On C# side:
```csharp
private void Init()
{

	// create a trigger node
	trigger = new NodeTrigger();


	// set the position event handler to be executed when the node position is changed
        trigger.SetPositionCallbackName("position_event_handler");

}


```


### Arguments

- *string* **name** - Name of the callback function implemented in the world script (UnigineScript side).

## string GetPositionCallbackName ( )

Returns the name of callback function to be fired on changing the trigger node position. This function is set by using the *[setPositionCallbackName()](#setPositionCallbackName_cstr_void)*function.
### Return value

Name of the callback function implemented in the world script (UnigineScript side).
