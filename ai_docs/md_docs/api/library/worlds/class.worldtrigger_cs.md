# Unigine::WorldTrigger Class (CS)

**Inherits from:** Node


World triggers trigger events when any nodes (colliders or not) get inside or outside of them. The trigger can detect a node of any type by its bounding box. The trigger reacts to all nodes (default behavior).


> **Notice:** **[World Triggers](../../../objects/worlds/world_trigger/index.md)** detect only the nodes with *Triggers Interaction* enabled - either in the Editor or via API using *[TriggerInteractionEnabled](../../../api/library/nodes/class.node_cs.md#setTriggerInteractionEnabled_int_void)*.


The handler function of *World Trigger* is actually executed only when the next engine function is called: that is, before *[UpdatePhysics()](../../../code/fundamentals/execution_sequence/main_loop.md#physics_updatePhysics)* (in the current frame) or before *[Update()](../../../code/fundamentals/execution_sequence/main_loop.md#world_update)* (in the next frame) � whatever comes first.


> **Notice:** If you have moved some nodes and want to execute event handlers based on changed positions in the same frame, you need to call *[UpdateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* first.


### Example


The example below allows creating a line of boxes moving in and out of the World Trigger area and triggering the events. Getting inside the World Trigger enables emission for the boxes, and getting out of it disables the emission.


```csharp
private static void set_state(Node n, string name, int val)
	{
		Unigine.Object node = n as Unigine.Object;
		if (node == null)
			return;

		for (int i = 0; i < node.NumSurfaces; i++)
		{
			Material material = node.GetMaterialInherit(i);
			if (material == null)
				continue;
			int id = material.FindState(name);
			if (id != -1)
				material.SetState(id, val);
		}
	}

	private static void trigger_enter(Node node)
	{
		set_state(node, "emission", 1);
	}

	private static void trigger_leave(Node node)
	{
		set_state(node, "emission", 0);
	}

	private const int MAX_OBJECTS = 10;
	private List<ObjectMeshStatic> objects = new List<ObjectMeshStatic>();

	WorldTrigger trigger;

	private void Init()
	{

		// create trigger
		trigger = new WorldTrigger(new vec3(3.0f));
		trigger.EventEnter.Connect(trigger_enter);
		trigger.EventLeave.Connect(trigger_leave);

		// create objects
		for (int i = 0; i < MAX_OBJECTS; i++)
		{
			ObjectMeshStatic mesh = new ObjectMeshStatic("cbox.mesh");
			mesh.TriggerInteractionEnabled = true;
			mesh.SetMaterialParameterFloat4("albedo_color", new vec4(1.0f, 0.0f, 0.0f, 1.0f), 0);
			objects.Add(mesh);
		}

		// enable the visualizer
		Visualizer.Enabled = true;

	}

	private void Update()
	{

		trigger.RenderVisualizer();
		float time = Game.Time;

		float hsize = objects.Count / 2.0f;

		for (int i = 0; i < objects.Count; i++)
		{
			float x = (float)Math.Sin(time) * hsize - hsize + i;
			objects[i].WorldTransform = MathLib.Translate(new Vec3(x, -x, 0.0f));
		}

	}


```


### See Also


- Video tutorial on [How To Use World Triggers to Detect Nodes by Their Bounds](../../../videotutorials/how_to/how_to_cs/world_trigger.md)
- Article on [Event Handling](../../../code/fundamentals/events/index_cs.md#triggers)
- C++ sample
- C# Component sample
- UnigineScript samples:

  -
  -
  -


## WorldTrigger Class

### Properties

## string LeaveCallbackName

The name of the handler function name to be executed on leaving the world trigger. This handler function is set via [EventLeave()](#getEventLeave_Event).
## string EnterCallbackName

The name of handler function to be executed on entering the world trigger. This handler function is set via [getEventEnter()](#getEventEnter_Event).
## 🔒︎ int NumNodes

The number of nodes contained in the world trigger.
## vec3 Size

The current dimensions of the world trigger.
## bool Touch

The value indicating if a touch mode is enabled for the trigger. With this mode on, the trigger will react to the node by partial contact. When set to off, the trigger reacts only if the whole bounding sphere/box gets inside or outside of it.
## 🔒︎ Event< Node > EventLeave

The event triggered when a node leaves the world trigger. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Node **node**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Leave event handler
void leave_event_handler(Node node)
{
	Log.Message("\Handling Leave event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections leave_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventLeave.Connect(leave_event_connections, leave_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventLeave.Connect(leave_event_connections, (Node node) => {
		Log.Message("Handling Leave event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
leave_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Leave event with a handler function
publisher.EventLeave.Connect(leave_event_handler);

// remove subscription to the Leave event later by the handler function
publisher.EventLeave.Disconnect(leave_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection leave_event_connection;

// subscribe to the Leave event with a lambda handler function and keeping the connection
leave_event_connection = publisher.EventLeave.Connect((Node node) => {
		Log.Message("Handling Leave event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
leave_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
leave_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
leave_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Leave events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventLeave.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventLeave.Enabled = true;

```

</details>

## 🔒︎ Event< Node > EventEnter

The event triggered when a node enters the world trigger. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Node **node**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Enter event handler
void enter_event_handler(Node node)
{
	Log.Message("\Handling Enter event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections enter_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEnter.Connect(enter_event_connections, enter_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEnter.Connect(enter_event_connections, (Node node) => {
		Log.Message("Handling Enter event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
enter_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Enter event with a handler function
publisher.EventEnter.Connect(enter_event_handler);

// remove subscription to the Enter event later by the handler function
publisher.EventEnter.Disconnect(enter_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection enter_event_connection;

// subscribe to the Enter event with a lambda handler function and keeping the connection
enter_event_connection = publisher.EventEnter.Connect((Node node) => {
		Log.Message("Handling Enter event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
enter_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
enter_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
enter_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Enter events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEnter.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEnter.Enabled = true;

```

</details>

### Members

---

## WorldTrigger ( vec3 size )

Constructor. Creates a new world trigger with given dimensions.
### Arguments

- *vec3* **size** - Dimensions of the new world trigger. If negative values are provided, **0** will be used instead of them.

## Node GetNode ( int num )

Returns a specified node contained in the world trigger.
```csharp
WorldTrigger trigger;

private void Init()
{

	// create a world trigger
	trigger = new WorldTrigger(new vec3(3.0f));
}

private void Update()
{

	// press the i key to get the info about nodes inside the trigger
	if (trigger != null && Input.IsKeyDown(Input.KEY.I))
	{
		//get the number of nodes inside the trigger
		int numNodes = trigger.NumNodes;
		Unigine.Log.Message("The number of nodes inside the trigger is " + numNodes + "\n");

		//loop through all nodes to print their names and types
		for (int i = 0; i < numNodes; i++)
		{
			Node node = trigger.GetNode(i);
			Unigine.Log.Message("The type of the " + node.Name + " node is " + node.Type + "\n");
		}
	}
}


```


### Arguments

- *int* **num** - Node number in range from 0 to the total number of nodes.

### Return value

Node pointer.
## Node [] GetNodes ( )

Gets nodes contained in the trigger.
### Arguments

## static int type ( )

Returns the type of the node.
### Return value

[World](../../../api/library/engine/class.world_cs.md) type identifier.
