# Event Handling (CS)


When writing your application logic, one of the biggest challenges you're likely to face is connecting the various changing elements in a way that works. For example, making a character move, jump, or adding up the score can be relatively easy to do on its own. But connecting all things that happen in your game or application without making it confusing to work with can be very challenging.


The ***Event System*** enables you to create application logic that is executed when an **event** is triggered during the application execution. It allows objects to subscribe one or more of their own functions to a subject's event. Then, when the subject triggers the event, the objects' functions are called in response. Such functions are also known as **event handlers**.


The Event System features the following:


- *Strict type checking for signatures*: you can see how many and which exactly arguments an event handler function requires.
- *Compile-time checking*: it ensures that argument types match event types, preventing runtime errors.
- *Simple subscription/unsubscription to events with [lambda functions](#lambda_functions)* with no need to perform internal type conversions.
- *Automatic event unsubscription*.
- *Temporary event deactivation*: particular events can be temporarily disabled to perform specific actions without triggering them.
- *Batch management*: you can unsubscribe from several subscriptions in a single function call.


## Events


An **event** is represented by the abstract *Event* class. It serves as an interface for interaction with the event. Typically, you get this interface via a reference as **Event<args...>**, where *args* represents a list of arguments the event will pass to a handler function.


For example, **[Body.EventPosition](../../../api/library/physics/class.body_cs.md#getEventPosition_Event)** returns the event with the following signature:


```csharp
Event<Body>

```


It means the handler function must receive an argument of the same type when connected with the event.


### Emulating Events


Sometimes, it is necessary to emulate events. For custom events, you can use the ***EventInvoker.Run()*** function that receives the same arguments as the event and invokes its handler functions.


The following example shows how to create your event and then run it when necessary:


```csharp
class MyEventClass
{
	public Event<int> MyEvent { get { return my_event; } }

	public void RunEvent()
	{
		num_runs++;
		my_event.Run(num_runs);
	}

	private int num_runs = 0;
	private EventInvoker<int> my_event = new EventInvoker<int>();
};

static void Main(string[] args)
{
	MyEventClass my_class = new MyEventClass();

	my_class.MyEvent.Connect(
		(int n) =>
		{
			System.Console.WriteLine("n = {0}", n);
		}
	);

	my_class.RunEvent();
	my_class.RunEvent();
}

```


The existing events that are implemented for built-in objects and available through API can be emulated using the corresponding ***RunEvent*()*** methods (without having to use ***EventInvoker.Run()***). For example, to emulate the *Show* event for a [widget](../../../api/library/gui/class.widget_cs.md), call **[Widget.RunEventShow()](../../../api/library/gui/class.widget_cs.md#runEventShow_void)**.


```csharp
widget.RunEventShow();

```


## Event Handlers


The event handler functions can receive **no more than 5** arguments.


In addition, the Event System performs strict type checking for handler function signatures: you can subscribe to the event only if the types of the function arguments match the event types. For example, in the case of the event with a single *int* argument, you are only able to link it with a handler that also accepts a single integer argument. Even if the types can be implicitly converted (as in the example), subscribing is not permitted.


```csharp
Event<int> event; // event signature
void on_event(int a); 	// types match, subscription is allowed
void on_event(long a); 	// type mismatch, no subscription

```


This restriction also applies to the *in, out*, and *ref* modifiers. For instance, when the event type is a user class with no modifiers:


```csharp
Event<MyClass> event;
void on_event(MyClass a);		// types match, subscription is allowed
void on_event(out MyClass a);	// type mismatch
void on_event(in MyClass a);	// type mismatch

```


### Discarding Arguments


In most cases, not all arguments passed to the handler function by the event are necessary. So, events allow for **discarding unnecessary arguments** when functions subscribe to them. You can only discard one argument at a time, starting with the last one. For example, the following handler functions can subscribe to the event:


```csharp
// the event
Event<int, float, string, vec3, MyClass> event;

// the event handlers with discarded arguments
on_event(int a, float b, string s, vec3 v, MyClass c);
on_event(int a, float b, string s, vec3 v);
on_event(int a, float b, string s);
on_event(int a, float b);
on_event(int a);
on_event();

```


### Receiving Additional Arguments


To receive an additional user argument in the handler function, you need to add the required argument to the end of the handler arguments list and pass its value to the **Connect()** function.


```csharp
class UserClass
{
	{ /* ... */ }
};

static EventInvoker<int, float> my_event = new EventInvoker<int, float>();

void on_event_0(int a, float b, int my_var) { /* ... */ }

void on_event_1(int a, float b, UserClass c) { /* ... */ }

void on_event(float f, string str) { /* ... */ }

static MyClass my_class = new MyClass();

static void Main(string[] args)
{
	// pass the value of the additional "my_var" argument to the handler function
	my_event.Connect(on_event_0, 33);
	// pass the value of the additional "c" argument to the handler function
	my_event.Connect(on_event_1, my_class);
	// discard the int and float handler arguments, add the custom float and const char* and pass them to connect()
	my_event.Connect(on_event, 33.3f, "test");

	return 0;
}

```


## Subscribing to Events


For convenience, the Event System provides the *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes that allow simple event subscription/unsubscription. Let's go through them in detail.


### Single Subscription with EventConnection


The *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* class keeps a connection between an event and its handler. You can subscribe to events via the *Event.Connect()* function and unsubscribe via *Event.Disconnect()*:


- The *Connect()* function receives the handler function as an argument. It returns *EventConnection* that can be used to unsubscribe from the event. The number of the *Connect()* function arguments may vary.
- The *Disconnect()* function receives the handler function as an argument.


For example, to set the connection between the event and the *static handler function*, you can implement the following:


```csharp
static EventInvoker<int, float> my_event = new EventInvoker<int, float>();

// a static handler function
static void on_event(int a, float b) { /*...*/ }

static void Main(string[] args)
{
	// connect the handler function with the event
	EventConnection connection = my_event.Connect(on_event);
}

```


You can temporarily **turn the event off** to perform specific actions without triggering it.


```csharp
// disable the event
my_event.Enabled = false;

/* perform some actions */

// and enable it again
my_event.Enabled = true;

```


Moreover, you can **toggle individual connections on and off**, providing flexibility when working with events.


```csharp
EventConnection connection = my_event.Connect(on_event);
/* ... */

// disable the connection
connection.Enabled = false;

/* perform some actions */

// and enable it back when necessary
connection.Enabled = true;

```


Later, you can unsubscribe from the event in one of the following ways:


- By using the handler function: ```csharp // break the connection by using the handler function my_event.Disconnect(on_event); ```
- By using *EventConnection*: ```csharp // break the connection by using EventConnection connection.Disconnect() ```


If the handler function is a *class method*, you should create a class instance, subscribe to the event, and unsubscribe later as follows:


```csharp
class MyClass
{
	public void on_event(int a, float b) { /*...*/ }
}

static EventInvoker<int, float> my_event = new EventInvoker<int, float>();

static void Main(string[] args)
{
    MyClass obj = new MyClass();

	// connect the handler function with the event
	EventConnection connection = my_event.Connect(obj.on_event);

	/* ... */

	// break the connection by using the handler function later
	my_event.Disconnect(obj.on_event);
}

```


### Multiple Subscriptions with EventConnections


The *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* class is a container for the *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* instances. Multiple subscriptions to a single event or **different events** can be linked to a single *EventConnections* instance.


For example, you can create multiple subscriptions to a single event as follows:


```csharp
EventConnections connections = new EventConnections();

static EventInvoker my_event = new EventInvoker();

// event handlers
void on_some_event_0() { Log.Message("\Handling the 1st event\n"); }
void on_some_event_1() { Log.Message("\Handling the 2nd event\n"); }

void init()
{
	// add two handlers for the event
	// and link it to an EventConnections instance to remove a pack of subscriptions later
	my_event.Connect(connections, on_some_event_0);
	my_event.Connect(connections, on_some_event_1);
}

```


Also, you can create multiple subscriptions to different events:


```csharp
EventConnections connections = new EventConnections();

static EventInvoker my_event_0 = new EventInvoker();
static EventInvoker my_event_1 = new EventInvoker();

// event handlers
void on_some_event_0() { Log.Message("\Handling the 1st event\n"); }
void on_some_event_1() { Log.Message("\Handling the 2nd event\n"); }

void init()
{
	// subscribe for events with handlers to be executed when the events are triggered;
	// here multiple subscriptions are linked to a single EventConnections class instance
	my_event_0.Connect(connections, on_some_event_0);
	my_event_1.Connect(connections, on_some_event_1);
}

```


Later all of these linked subscriptions can be removed with a single line:


```csharp
// break the connection by using EventConnections
// all instances of EventConnection will be removed from the EventConnections container
connections.DisconnectAll();

```


### Using Lambda Functions


You can pass a lambda function as an argument to the **Connect()** function to handle the event: there is no need to perform internal type conversions. All features available for the handler functions are also applicable to lambda functions, except additional arguments.


```csharp
class MyClass
{
};

static EventInvoker<int, float> my_event = new EventInvokerlt;int, float>();

static void Main(string[] args)
{
	EventConnection connection = my_event.Connect(
		(int a, float b) =>
		{
			System.Console.WriteLine("a = {0}, b = {1}", a, b);
		},
	);

	connection = my_event.Connect(
		(int a) =>
		{
			System.Console.WriteLine("a = {0}", a);
		},
	);

	connection = my_event.Connect(
		(int a, string s) =>
		{
			System.Console.WriteLine("a = {0}, s = {1}", a, s);
		},
		"my string"
	);

	connection = my_event.Connect(
		(int a, float b, string s) =>
		{
			System.Console.WriteLine("a = {0}, b = {1}, s = {2}", a, b, s);
		},
		"test"
	);

	my_event.Run(3, 33.0f);
}

```


See more [examples of practical use of lambda functions](#physics) below.


## Using Predefined Events


Some Unigine API members have several predefined events that can be handled in specific cases. The following chapters showcase the practical use of the concepts described above.


### Triggers


Triggers are used to detect changes in nodes position or state. Unigine offers three types of built-in triggers:


- *[**NodeTrigger**](../../../api/library/nodes/class.nodetrigger_cs.md)* triggers events when the trigger node is [enabled](../../../api/library/nodes/class.nodetrigger_cs.md#getEventEnabled_Event) or its [position](../../../api/library/nodes/class.nodetrigger_cs.md#getEventPosition_Event) has changed.
- *[**WorldTrigger**](../../../api/library/worlds/class.worldtrigger_cs.md)* triggers events when any node (collider or not) gets [inside](../../../api/library/worlds/class.worldtrigger_cs.md#getEventEnter_Event) or [outside](../../../api/library/worlds/class.worldtrigger_cs.md#getEventLeave_Event) it. > **Notice:** **World Triggers** detect only the nodes with *Triggers Interaction* enabled - either in the Editor or via API using *[TriggerInteractionEnabled](../../../api/library/nodes/class.node_cs.md#setTriggerInteractionEnabled_int_void)*.
- *[**PhysicalTrigger**](../../../api/library/physics/class.physicaltrigger_cs.md)* triggers events when physical objects get [inside](../../../api/library/physics/class.physicaltrigger_cs.md#getEventEnter_Event) or [outside](../../../api/library/physics/class.physicaltrigger_cs.md#getEventLeave_Event) it.


Here is a simple *NodeTrigger* usage example. The event handlers are set via pointers specified when subscribing to the following events: *[EventEnabled](../../../api/library/nodes/class.nodetrigger_cs.md#getEventEnabled_Event)* and *[EventPosition](../../../api/library/nodes/class.nodetrigger_cs.md#getEventPosition_Event)*.


<details>
<summary>NodeTriggerEvents.cs | Close</summary>

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

</details>


And here is an example of *WorldTrigger* that demonstrates how to subscribe to the *Enter* event with a corresponding handler and keep this connection to unsubscribe later.


<details>
<summary>WorldTriggerEvents.cs | Close</summary>

```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

#if UNIGINE_DOUBLE
using Vec3 = Unigine.dvec3;
using Vec4 = Unigine.dvec4;
using Mat4 = Unigine.dmat4;
#else
using Vec3 = Unigine.vec3;
using Vec4 = Unigine.vec4;
using Mat4 = Unigine.mat4;
#endif

public partial class EventHandlers : Component
{
		// implement the Enter event handler
		void enter_event_handler(Node node)
		{
			Log.Message("\nA node named {0} has entered the trigger\n", node.Name);
		}
		// implement the Leave event handler
		void leave_event_handler(Node node)
		{
			Log.Message("\nA node named {0} has left the trigger\n", node.Name);
		}
		WorldTrigger trigger;
		EventConnection enter_event_connection;

	private void Init()
	{
		// create a world trigger
		trigger = new WorldTrigger(new vec3(3.0f));
		// subscribe for the enter event with a handler to be executed when a node enters the world trigger
		// and keep its connection to be used to unsubscribe when necessary
		enter_event_connection = trigger.EventEnter.Connect(enter_event_handler);
		// add the leave event handler to be executed when a node leaves the world trigger
		trigger.EventLeave.Connect(leave_event_handler);
	}

	private void Update()
	{
	}

	private void Shutdown()
	{
		// removing the subscription for the Enter event by using the connection (enter_event_connection)
		enter_event_connection.Disconnect();
	}
}

```

</details>


### Widgets


The widgets base class *[**Widget**](../../../api/library/gui/class.widget_cs.md)* allows subscribing to events.


The example below demonstrates how to set a lambda function to handle the widget's *Clicked* event.


<details>
<summary>WidgetEvents.cs | Close</summary>

```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

#if UNIGINE_DOUBLE
using Vec3 = Unigine.dvec3;
using Vec4 = Unigine.dvec4;
using Mat4 = Unigine.dmat4;
#else
using Vec3 = Unigine.vec3;
using Vec4 = Unigine.vec4;
using Mat4 = Unigine.mat4;
#endif

public partial class EventHandlers : Component
{

	private void Init()
	{
		// get the system GUI
		Gui gui = Gui.GetCurrent();

		// create a button widget and set its caption
		WidgetButton widget_button = new WidgetButton(gui, "Press me");

		// rearrange a button size
		widget_button.Arrange();

		// set a button position
		widget_button.SetPosition(10,10);

		// set a lambda function to handle the CLICKED event
		widget_button.EventClicked.Connect(() => Log.Message("Button pressed\n"));

		// add the created button widget to the system GUI
		gui.AddChild(widget_button, Gui.ALIGN_OVERLAP | Gui.ALIGN_FIXED);
	}
}

```

</details>


### Physics


You can track certain events of the physics-related [Bodies](../../../api/library/physics/class.body_cs.md) and [Joints](../../../api/library/physics/class.joint_cs.md):


- ****[Body.EventFrozen](../../../api/library/physics/class.body_cs.md#getEventFrozen_Event)**** to track an event when a body freezes.
- ****[Body.EventPosition](../../../api/library/physics/class.body_cs.md#getEventPosition_Event)**** to track an event when a body changes its position.
- ****[Body.EventContactEnter](../../../api/library/physics/class.body_cs.md#getEventContactEnter_Event)**** to track an event when a contact emerges (body starts touching another body or collidable surface).
- ****[Body.EventContactLeave](../../../api/library/physics/class.body_cs.md#getEventContactLeave_Event)**** to track an event when a contact ends (body stops touching another body or collidable surface).
- ****[Body.EventContacts](../../../api/library/physics/class.body_cs.md#getEventContacts_Event)**** to get **all contacts** of the body including new ones (*enter*) and the ending ones (*leave*). Leave contacts are removed after the callback execution stage, so this is the only point where you can still get them.
- ****[Joint.EventBroken](../../../api/library/physics/class.joint_cs.md#getEventBroken_Event)**** to track an event when a joint breaks.


The following example demostrates how to subscribe to the Body events by using lambda functions and then remove all the event subscriptions for the Body.


<details>
<summary>PhysicsEvents.cs | Close</summary>

```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

#if UNIGINE_DOUBLE
using Vec3 = Unigine.dvec3;
using Vec4 = Unigine.dvec4;
using Mat4 = Unigine.dmat4;
#else
using Vec3 = Unigine.vec3;
using Vec4 = Unigine.vec4;
using Mat4 = Unigine.mat4;
#endif

public partial class EventHandlers : Component
{
		EventConnections body_event_connections = new EventConnections();

	private void Init()
	{
		// create a box
		ObjectMeshStatic meshStatic = new ObjectMeshStatic("core/meshes/box.mesh");
		meshStatic.Position = new Vec3(0, 0, 5.0f);

		// add a rigid body to the box
		BodyRigid body = new BodyRigid(meshStatic);

		// subscribe for body events by using lambda functions and storing connections to remove them later
		body.EventFrozen.Connect(body_event_connections, b => b.Object.SetMaterialParameterFloat4("albedo_color", new vec4(1.0f, 0.0f, 0.0f, 1.0f), 0));
		body.EventPosition.Connect(body_event_connections, b => b.Object.SetMaterialParameterFloat4("albedo_color", new vec4(0.0f, 0.0f, 1.0f, 1.0f), 0));
		body.EventContactEnter.Connect(body_event_connections, (b, num) => b.Object.SetMaterialParameterFloat4("albedo_color", new vec4(1.0f, 1.0f, 0.0f, 1.0f), 0));

		// add a shape to the body
		ShapeBox shape = new ShapeBox(body, new vec3(1.0f));
	}
	private void Shutdown()
	{
		// removing all previously stored event subscriptions for the body
		body_event_connections.DisconnectAll();
	}
}

```

</details>


> **Notice:** Physics-based events are executed in the main thread, as they are mainly used for creation, destruction or modification of other objects.


### Properties


Events can be used to determine actions to be performed when adding or removing node and surface properties as well as when swapping node properties. Here is an example demonstrating how to track adding a node property via events.


<details>
<summary>PropertyEvents.cs | Close</summary>

```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

#if UNIGINE_DOUBLE
using Vec3 = Unigine.dvec3;
using Vec4 = Unigine.dvec4;
using Mat4 = Unigine.dmat4;
#else
using Vec3 = Unigine.vec3;
using Vec4 = Unigine.vec4;
using Mat4 = Unigine.mat4;
#endif

public partial class EventHandlers : Component
{
		void node_property_added(Node n, Property property)
		{
			Log.Message("Property \"{0}\" was added to the node named \"{1}\".\n", property.Name, n.Name);
		}
		void parameter_changed(Property property, int num)
		{
			Log.Message("Parameter \"{0}\" of the property \"{1}\" has changed its value.\n", property.GetParameterPtr(num).Name, property.Name);
		}
		public void property_removed(Property property)
		{
			Log.Message("Property \"{0}\" was removed.\n", property.Name);
		}

	private void Init()
	{
		NodeDummy node = new NodeDummy();

		// search for a property named "new_property_0"
		Property property = Properties.FindProperty("new_property_0");

		// subscribing for the PropertyNodeAdd event to handle adding a property to a node
		Node.EventPropertyNodeAdd.Connect(node_property_added);

		// add the property named "new_property_0" to the node
		node.AddProperty("new_property_0");
		// subscribing for the ParameterChange event to handle changing property parameter
		property.EventParameterChanged.Connect(parameter_changed);

		// change the value of the "my_int_param" parameter
		property.GetParameterPtr("my_int_param").SetValue(3);
		// inherit a new property named "new_property_1" from the base property "surface_base"
		Properties.FindManualProperty("surface_base").Inherit("new_property_1");

		// subscribing for property removal event
		Properties.EventRemoved.Connect(property_removed);

		// remove the property named "new_property_1"
		Properties.RemoveProperty(Properties.FindProperty("new_property_1").GUID);
	}
}

```

</details>
