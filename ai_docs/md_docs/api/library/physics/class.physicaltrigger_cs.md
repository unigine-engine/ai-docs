# Unigine.PhysicalTrigger Class (CS)

**Inherits from:** Physical


***Physical Trigger*** triggers events when a physical object gets inside or outside it. To be detected by the trigger, physical objects are required to have at the same time both:


1. [Bodies](../../../api/library/physics/class.body_cs.md) (with matching [Physical Mask](../../../api/library/physics/class.body_cs.md#setPhysicalMask_int_void)) > **Notice:** For [BodyDummy](../../../api/library/physics/class.bodydummy_cs.md) to trigger PhysicalTrigger, you need to call [updateContacts()](#updateContacts_void) first.
2. [Shapes](../../../api/library/physics/class.shape_cs.md) (with matching [Collision mask](../../../api/library/physics/class.shape_cs.md#setCollisionMask_int_void))


To force update of the physical trigger, [updateContacts()](#updateContacts_void) can be called. After that, you can access all updated data about the contacts in the same frame. However, handler functions will still be executed only when the next engine function is called: that is, before *[updatePhysics()](../../../code/fundamentals/execution_sequence/main_loop.md#physics)* (in the current frame), or before the *[update()](../../../code/fundamentals/execution_sequence/main_loop.md#update)* (in the next frame) � whatever comes first.


> **Notice:** If you have moved some nodes and want to execute event handlers based on changed positions in the same frame, you need to call [updateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void) first.


### See Also


- Video tutorial on [How To Use Physical Triggers to Catch Physical Objects](../../../videotutorials/how_to/how_to_cs/physical_trigger.md)
- Article on [Event Handling](../../../code/fundamentals/events/index_cs.md)
- UnigineScript samples:

  -
  -
  -


### Usage Example


In this example a physical trigger and two boxes, each with a body and a shape, are created. When a box with matching physical mask enters the physical trigger the **trigger_enter()** function is called, when it leaves the trigger - the **trigger_leave()** function is called.


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;
using System.Linq;
using System.Text;

#region Math Variables
#if UNIGINE_DOUBLE
using Scalar = System.Double;
using Vec2 = Unigine.dvec2;
using Vec3 = Unigine.dvec3;
using Vec4 = Unigine.dvec4;
using Mat4 = Unigine.dmat4;
#else
using Scalar = System.Single;
using Vec2 = Unigine.vec2;
using Vec3 = Unigine.vec3;
using Vec4 = Unigine.vec4;
using Mat4 = Unigine.mat4;
using WorldBoundBox = Unigine.BoundBox;
using WorldBoundSphere = Unigine.BoundSphere;
using WorldBoundFrustum = Unigine.BoundFrustum;
#endif
#endregion

public partial class name : Component
{
	PhysicalTrigger trigger;
	EventConnections trigger_event_connections = new EventConnections();
	ObjectMeshDynamic box1;
	ObjectMeshDynamic box2;

	// function to be executed when a physical object enters the trigger
	private void trigger_enter(Body body)
	{
		// trying to get an object from the body
		Unigine.Object obj = body.Object;
		if (!obj)
			return;

		// enabling material emission for all object's surfaces
		for (int i = 0; i < obj.NumSurfaces; i++)
			obj.SetMaterialState("emission", 1, i);

		// displaying the name of the object entering trigger area
		Log.Message("\n {0} has entered the trigger area!", body.Object.Name);
	}

	// function to be executed when a physical object leaves the trigger
	private void trigger_leave(Body body)
	{
		// trying to get an object from the body
		Unigine.Object obj = body.Object;
		if (!obj)
			return;

		// disabling material emission for all object's surfaces
		for (int i = 0; i < obj.NumSurfaces; i++)
			obj.SetMaterialState("emission", 0, i);

		// displaying the name of the object leaving trigger area
		Log.Message("\n {0} has left the trigger area!", body.Object.Name);
	}

	/// function, creating a named box having a specified size, color and transformation with a body and a shape
	ObjectMeshDynamic createBodyBox(String name, vec3 size, float mass, vec4 color, Mat4 transform, int physical_mask)
	{
		// creating geometry and setting up its parameters (name, material and transformation)
		ObjectMeshDynamic OMD = Primitives.CreateBox(size);
		OMD.WorldTransform = transform;
		OMD.SetMaterialParameterFloat4("albedo_color", color, 0);
		OMD.Name = name;

		// adding physics, i.e. a rigid body and a box shape with specified mass
		BodyRigid body = new BodyRigid(OMD);

		body.AddShape(new ShapeBox(size), MathLib.Translate(new vec3(0.0f)));
		body.PhysicalMask = physical_mask;
		body.Mass = mass;

		return OMD;
	}

	private void Init()
	{
			// enabling visualizer to render bounds of the physical trigger
			Unigine.Console.Run("show_visualizer 1");

			// creating a physical trigger
			trigger = new PhysicalTrigger(Shape.TYPE.SHAPE_BOX,new vec3(2.0f, 2.0f, 1.0f));

			// setting trigger's position
			trigger.Position = new Vec3(0.0f, 0.0f, 1.0f);

			// setting trigger's physical mask equal to 1
			trigger.PhysicalMask = 1;

			// retrieving trigger size
			vec3 size = trigger.Size;

			// displaying trigger size and shape type
			Log.Message("\n Trigger parameters size({0}, {1} , {2}) type: {3}", size.x, size.y, size.z, trigger.ShapeType);

			// subscribing for the Enter event
			trigger.EventEnter.Connect(trigger_event_connections, body => trigger_enter(body));

			// subscribing for the Leave event
			trigger.EventLeave.Connect(trigger_event_connections, body => trigger_leave(body));

			// creating a box with a body and physical mask value equal to 2 to be ignored by the trigger
			box1 = createBodyBox("Box1", new vec3(0.2f), 5.0f, new vec4(1.0f, 0.0f, 0.0f, 1.0f), MathLib.Translate(new Vec3(0.0f, 0.0f, 2.22f)),2);

			// creating a box with a body and physical mask value equal to 1 to affect the trigger
			box2 = createBodyBox("Box2", new vec3(0.2f), 0.0f, new vec4(1.0f, 1.0f, 0.0f, 1.0f), MathLib.Translate(new Vec3(3.5f, 0.0f, 1.2f)),1);

			// displaying physical masks of both boxes and the trigger
			Log.Message("\n Box1 Physical mask: {0}", box1.Body.PhysicalMask);
			Log.Message("\n Box2 Physical mask: {0}", box2.Body.PhysicalMask);
			Log.Message("\n Trigger Physical mask: {0}", trigger.PhysicalMask);
	}

	private void Update()
	{
		// showing the bounds of the physical trigger
		trigger.RenderVisualizer();

		// changing the position of the second box
		box2.WorldPosition = box2.WorldPosition - new vec3(0.5f * Game.IFps, 0.0f, 0.0f);

	}

	private void UpdatePhysics()
	{

		// updating information on trigger contacts
		trigger.UpdateContacts();

	}

	private void Shutdown()
	{

		// unsubscribing from all events
		trigger_event_connections.DisconnectAll();
	}
}

```


## PhysicalTrigger Class

### Properties

## vec3 Size

The size of the physical trigger.
## int ShapeType

The shape type of the physical trigger.
## 🔒︎ int NumContacts

The total number of contacts with bodies, shapes, and colliding surfaces in which a physical trigger participated.
## 🔒︎ int NumBodies

The total number of bodies intersecting with the physical trigger.
## string LeaveCallbackName

The name of the callback function fired on leaving the physical trigger. This callback function is set via [setLeaveCallbackName()](#setLeaveCallbackName_cstr_void) .
## int ExclusionMask

The bit mask that prevents detecting collisions with shapes and bodies. This mask is independent of the collision mask. To avoid detecting collisions by a physical trigger for bodies and shapes with matching collision masks, at least one bit in exclusion masks should match.
## string EnterCallbackName

The name of the callback function fired on entering the physical trigger.
## int CollisionMask

The collision bit mask for the trigger:
- the trigger will be activated if the entered body will have a matching [physical mask](../../../api/library/physics/class.body_cs.md#setPhysicalMask_int_void) and at the same time its shape will have a matching [collision mask](../../../api/library/physics/class.shape_cs.md#setCollisionMask_int_void).


## 🔒︎ Event< Body > EventLeave

The Event triggered when a body leaves the physical trigger. The event handler must receive a [*Body*](../../../api/library/physics/class.body_cs.md) as its first argument. In addition, it can also take **2** arguments of any type. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Body **body**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Leave event handler
void leave_event_handler(Body body)
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
publisher.EventLeave.Connect(leave_event_connections, (Body body) => {
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
leave_event_connection = publisher.EventLeave.Connect((Body body) => {
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

## 🔒︎ Event< Body > EventEnter

The Event triggered when a body enters the physical trigger. The callback function must receive a [*Body*](../../../api/library/physics/class.body_cs.md) as its first argument. In addition, it can also take 2 arguments of any type. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Body **body**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Enter event handler
void enter_event_handler(Body body)
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
publisher.EventEnter.Connect(enter_event_connections, (Body body) => {
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
enter_event_connection = publisher.EventEnter.Connect((Body body) => {
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

## PhysicalTrigger ( Shape.TYPE type , vec3 size )

Constructor. Creates a physical trigger of the specified shape and size.
### Arguments

- *[Shape.TYPE](../../../api/library/physics/class.shape_cs.md#TYPE)* **type** - Shape of the physical trigger:

  - 0 = *Sphere*
  - 1 = *Capsule*
  - 2 = *Cylinder*
  - 3 = *Box*
- *vec3* **size** - Size of the physical trigger:

  - *Radius*, in case of a sphere
  - *Radius* and *height*, in case of a capsule or a cylinder
  - *Dimensions*, in case of the box

## Body GetBody ( int num )

Returns the specified body that intersects the physical trigger.
### Arguments

- *int* **num** - Body number.

### Return value

Intersected body.
## float GetContactDepth ( int contact )

Returns penetration depth by the given contact.
### Arguments

- *int* **contact** - Contact number.

### Return value

Penetration depth.
## vec3 GetContactNormal ( int contact )

Returns a normal of the contact point, in world coordinates.
### Arguments

- *int* **contact** - Contact number.

### Return value

Normal of the contact point.
## Object GetContactObject ( int contact )

Returns an object participating in the contact with a physical trigger .
### Arguments

- *int* **contact** - Contact number.

### Return value

Object in contact.
## vec3 GetContactPoint ( int contact )

Returns world coordinates of the contact point.
### Arguments

- *int* **contact** - Contact number.

### Return value

Contact point.
## Shape GetContactShape ( int contact )

Returns a shape that collided with a physical trigger.
### Arguments

- *int* **contact** - Contact number.

### Return value

Shape in contact.
## int GetContactSurface ( int contact )

Returns the surface of the current object, which is in contact .
### Arguments

- *int* **contact** - Contact number.

### Return value

Surface number.
## static int type ( )

Returns the type of the node.
### Return value

[Physical trigger](../../../api/library/nodes/class.node_cs.md#PHYSICAL_TRIGGER) type identifier.
## void UpdateContacts ( )

Forces a physical trigger to be updated, i.e. to recalculate its intersections with physical objects and colliders. After that, you can access all updated data; however, event handler functions themselves will be executed only when physics flush is over.
