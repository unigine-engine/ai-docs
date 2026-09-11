# Unigine.PhysicalTrigger Class (CPP)

**Header:** #include <UniginePhysicals.h>

**Inherits from:** Physical


***Physical Trigger*** triggers events when a physical object gets inside or outside it. To be detected by the trigger, physical objects are required to have at the same time both:


1. [Bodies](../../../api/library/physics/class.body_cpp.md) (with matching [Physical Mask](../../../api/library/physics/class.body_cpp.md#setPhysicalMask_int_void)) > **Notice:** For [BodyDummy](../../../api/library/physics/class.bodydummy_cpp.md) to trigger PhysicalTrigger, you need to call [updateContacts()](#updateContacts_void) first.
2. [Shapes](../../../api/library/physics/class.shape_cpp.md) (with matching [Collision mask](../../../api/library/physics/class.shape_cpp.md#setCollisionMask_int_void))


To force update of the physical trigger, [updateContacts()](#updateContacts_void) can be called. After that, you can access all updated data about the contacts in the same frame. However, handler functions will still be executed only when the next engine function is called: that is, before *[updatePhysics()](../../../code/fundamentals/execution_sequence/main_loop.md#physics)* (in the current frame), or before the *[update()](../../../code/fundamentals/execution_sequence/main_loop.md#update)* (in the next frame) � whatever comes first.


> **Notice:** If you have moved some nodes and want to execute event handlers based on changed positions in the same frame, you need to call [updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void) first.


### See Also


- Video tutorial on [How To Use Physical Triggers to Catch Physical Objects](../../../videotutorials/how_to/how_to_cs/physical_trigger.md)
- Article on [Event Handling](../../../code/fundamentals/events/index_cpp.md)
- UnigineScript samples:

  -
  -
  -


### Usage Example


In this example a physical trigger and two boxes, each with a body and a shape, are created. When a box with matching physical mask enters the physical trigger the **trigger_enter()** function is called, when it leaves the trigger - the **trigger_leave()** function is called.


In the **AppWorldLogic.h** file let us add the following code:


```cpp
#include <UniginePhysics.h>
#include <UniginePhysicals.h>
#include <UnigineConsole.h>
#include <UnigineGame.h>

class AppWorldLogic : public Unigine::WorldLogic
{

public:

private:

	// pointer to the physical trigger
	Unigine::PhysicalTriggerPtr trigger;

	// buffer to store subscriptions for trigger events
	Unigine::EventConnections connections;

	// pointers to physical objects
	Unigine::ObjectMeshDynamicPtr box1;
	Unigine::ObjectMeshDynamicPtr box2;
};


```


In the **AppWorldLogic.cpp** file let us add the following code:


```cpp
#include "AppWorldLogic.h"

using namespace Unigine;
using namespace Math;

// handler function to be executed when a physical object enters the trigger
void trigger_enter(const BodyPtr &body)
{
	// trying to get an object from the body
	ObjectPtr obj = body->getObject();
	if (!obj)
		return;

	// enabling material emission for all object's surfaces
	for (int i = 0; i < obj->getNumSurfaces(); i++)
		obj->setMaterialState("emission", 1, i);

	// displaying the name of the object entering trigger area
	Log::message("\n %s has entered the trigger area!", body->getObject()->getName());
}

// handler function to be executed when a physical object leaves the trigger
void trigger_leave(const BodyPtr &body)
{
	// trying to get an object from the body
	ObjectPtr obj = body->getObject();
	if (!obj)
		return;

	// disabling material emission for all object's surfaces
	for (int i = 0; i < obj->getNumSurfaces(); i++)
		obj->setMaterialState("emission", 0, i);

	// displaying the name of the object leaving trigger area
	Log::message("\n %s has left the trigger area!", body->getObject()->getName());
}

/// function, creating a named box having a specified size, color and transformation with a body and a shape
ObjectMeshDynamicPtr createBodyBox(const char* name, vec3 size, float mass, vec4 color, Mat4 transform, int physical_mask)
{
	// creating geometry and setting up its parameters (name, material and transformation)
	ObjectMeshDynamicPtr OMD = Primitives::createBox(size);
	OMD->setWorldTransform(transform);
	OMD->setMaterialParameterFloat4("albedo_color", color, 0);
	OMD->setName(name);

	// adding physics, i.e. a rigid body and a box shape with specified mass
	BodyRigidPtr body = BodyRigid::create(OMD);
	body->addShape(ShapeBox::create(size), translate(vec3(0.0f)));
	OMD->getBody()->getShape(0)->setMass(mass);
	// setting the physical mask of the body
	body->setPhysicalMask(physical_mask);

	return OMD;
}

int AppWorldLogic::init()
{
	//enabling visualizer to render bounds of the physical trigger
	Console::run("show_visualizer 1");

	// creating a physical trigger
	trigger = PhysicalTrigger::create(Shape::SHAPE_BOX, vec3(2.0f, 2.0f, 1.0f));

	// setting trigger's position
	trigger->setPosition(Vec3(0.0f, 0.0f, 1.0f));

	// setting trigger's physical mask equal to 1
	trigger->setPhysicalMask(1);

	// retrieving trigger size
	vec3 size = trigger->getSize();

	// displaying trigger size and shape type
	Log::message("\n Trigger parameters size(%f, %f ,%f) type: %d", size.x, size.y, size.z, trigger->getShapeType());

	// subscribing for the trigger enter event
	trigger->getEventEnter().connect(connections, trigger_enter);

	// subscribing for the trigger leave event
	trigger->getEventLeave().connect(connections, trigger_leave);

	// creating a box with a body and physical mask value equal to 2 to be ignored by the trigger
	box1 = createBodyBox("Box1", vec3(0.2f), 5.0f, vec4(1.0f, 0.0f, 0.0f, 1.0f), translate(Vec3(0.0f, 0.0f, 2.22f)), 2);

	// creating a box with a body and physical mask value equal to 1 to affect the trigger
	box2 = createBodyBox("Box2", vec3(0.2f), 0.0f, vec4(1.0f, 1.0f, 0.0f, 1.0f), translate(Vec3(3.5f, 0.0f, 1.2f)), 1);

	// displaying physical masks of both boxes and the trigger
	Log::message("\n Box1 Physical mask: %d", box1->getBody()->getPhysicalMask());
	Log::message("\n Box2 Physical mask: %d", box2->getBody()->getPhysicalMask());
	Log::message("\n Trigger Physical mask: %d", trigger->getPhysicalMask());

	return 1;
}

int AppWorldLogic::update()
{
	// showing the bounds of the physical trigger
	trigger->renderVisualizer();

	// changing the position of the second box
	box2->setWorldPosition(box2->getWorldPosition() - Vec3(0.5f * Game::getIFps(), 0.0f, 0.0f));

	return 1;
}

int AppWorldLogic::updatePhysics()
{
	// updating information on trigger contacts
	trigger->updateContacts();

	return 1;
}

int AppWorldLogic::shutdown()
{
	// removing subscriptions to all trigger events
	connections.disconnectAll();

	return 1;
}


```


## PhysicalTrigger Class

### Members

## void setSize ( const Math:: vec3 & size )

Sets a new size of the physical trigger.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **size** - The size of the physical trigger:

  - Radius, in case of a sphere (pass the radius in the first element of the vector).
  - Radius and height, in case of a capsule or a cylinder (pass the radius as the first vector element and the height as the second element).
  - Dimensions along the X, Y and Z axes, in case of the box.

## Math:: vec3 getSize () const

Returns the current size of the physical trigger.
### Return value

Current size of the physical trigger:
- Radius, in case of a sphere (pass the radius in the first element of the vector).
- Radius and height, in case of a capsule or a cylinder (pass the radius as the first vector element and the height as the second element).
- Dimensions along the X, Y and Z axes, in case of the box.


## void setShapeType ( int type )

Sets a new shape type of the physical trigger.
### Arguments

- *int* **type** - The shape type of the physical trigger:

  - 0 - Sphere
  - 1 - Capsule
  - 2 - Cylinder
  - 3 - Box

## int getShapeType () const

Returns the current shape type of the physical trigger.
### Return value

Current shape type of the physical trigger:
- 0 - Sphere
- 1 - Capsule
- 2 - Cylinder
- 3 - Box


## int getNumContacts () const

Returns the current total number of contacts with bodies, shapes, and colliding surfaces in which a physical trigger participated.
### Return value

Current number of contacts.
## int getNumBodies () const

Returns the current total number of bodies intersecting with the physical trigger.
### Return value

Current number of bodies.
## void setLeaveCallbackName ( const char * name )

Sets a new name of the callback function fired on leaving the physical trigger. This callback function is set via [setLeaveCallbackName()](#setLeaveCallbackName_cstr_void) .
### Arguments

- *const char ** **name** - The name of the callback function.

## const char * getLeaveCallbackName () const

Returns the current name of the callback function fired on leaving the physical trigger. This callback function is set via [setLeaveCallbackName()](#setLeaveCallbackName_cstr_void) .
### Return value

Current name of the callback function.
## void setExclusionMask ( int mask )

Sets a new bit mask that prevents detecting collisions with shapes and bodies. This mask is independent of the collision mask. To avoid detecting collisions by a physical trigger for bodies and shapes with matching collision masks, at least one bit in exclusion masks should match.
### Arguments

- *int* **mask** - The integer, each bit of which is a mask.

## int getExclusionMask () const

Returns the current bit mask that prevents detecting collisions with shapes and bodies. This mask is independent of the collision mask. To avoid detecting collisions by a physical trigger for bodies and shapes with matching collision masks, at least one bit in exclusion masks should match.
### Return value

Current integer, each bit of which is a mask.
## void setEnterCallbackName ( const char * name )

Sets a new name of the callback function fired on entering the physical trigger.
### Arguments

- *const char ** **name** - The name of the callback function.

## const char * getEnterCallbackName () const

Returns the current name of the callback function fired on entering the physical trigger.
### Return value

Current name of the callback function.
## void setCollisionMask ( int mask )

Sets a new collision bit mask for the trigger:
- the trigger will be activated if the entered body will have a matching [physical mask](../../../api/library/physics/class.body_cpp.md#setPhysicalMask_int_void) and at the same time its shape will have a matching [collision mask](../../../api/library/physics/class.shape_cpp.md#setCollisionMask_int_void).


### Arguments

- *int* **mask** - The integer, each bit of which is a mask.

## int getCollisionMask () const

Returns the current collision bit mask for the trigger:
- the trigger will be activated if the entered body will have a matching [physical mask](../../../api/library/physics/class.body_cpp.md#setPhysicalMask_int_void) and at the same time its shape will have a matching [collision mask](../../../api/library/physics/class.shape_cpp.md#setCollisionMask_int_void).


### Return value

Current integer, each bit of which is a mask.
## Event<const Ptr < Body > &> getEventLeave () const

Event triggered when a body leaves the physical trigger. The event handler must receive a [*Body*](../../../api/library/physics/class.body_cpp.md) as its first argument. In addition, it can also take **2** arguments of any type. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Body> & **body**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Leave event handler
void leave_event_handler(const Ptr<Body> & body)
{
	Log::message("\Handling Leave event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections leave_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventLeave().connect(leave_event_connections, leave_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventLeave().connect(leave_event_connections, [](const Ptr<Body> & body) {
		Log::message("\Handling Leave event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
leave_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection leave_event_connection;

// subscribe to the Leave event with a handler function keeping the connection
publisher->getEventLeave().connect(leave_event_connection, leave_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
leave_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
leave_event_connection.setEnabled(true);

// ...

// remove subscription to the Leave event via the connection
leave_event_connection.disconnect();

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

	// A Leave event handler implemented as a class member
	void event_handler(const Ptr<Body> & body)
	{
		Log::message("\Handling Leave event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventLeave().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId leave_handler_id;

// subscribe to the Leave event with a lambda handler function and keeping connection ID
leave_handler_id = publisher->getEventLeave().connect(e_connections, [](const Ptr<Body> & body) {
		Log::message("\Handling Leave event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventLeave().disconnect(leave_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Leave events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventLeave().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventLeave().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < Body > &> getEventEnter () const

Event triggered when a body enters the physical trigger. The callback function must receive a [*Body*](../../../api/library/physics/class.body_cpp.md) as its first argument. In addition, it can also take 2 arguments of any type. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Body> & **body**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Enter event handler
void enter_event_handler(const Ptr<Body> & body)
{
	Log::message("\Handling Enter event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections enter_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEnter().connect(enter_event_connections, enter_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEnter().connect(enter_event_connections, [](const Ptr<Body> & body) {
		Log::message("\Handling Enter event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
enter_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection enter_event_connection;

// subscribe to the Enter event with a handler function keeping the connection
publisher->getEventEnter().connect(enter_event_connection, enter_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
enter_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
enter_event_connection.setEnabled(true);

// ...

// remove subscription to the Enter event via the connection
enter_event_connection.disconnect();

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

	// A Enter event handler implemented as a class member
	void event_handler(const Ptr<Body> & body)
	{
		Log::message("\Handling Enter event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEnter().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId enter_handler_id;

// subscribe to the Enter event with a lambda handler function and keeping connection ID
enter_handler_id = publisher->getEventEnter().connect(e_connections, [](const Ptr<Body> & body) {
		Log::message("\Handling Enter event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEnter().disconnect(enter_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Enter events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEnter().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEnter().setEnabled(true);

```

</details>

### Return value

Event instance.
---

## static PhysicalTriggerPtr create ( Shape::TYPE type , const Math:: vec3 & size )

Constructor. Creates a physical trigger of the specified shape and size.
### Arguments

- *[Shape::TYPE](../../../api/library/physics/class.shape_cpp.md#TYPE)* **type** - Shape of the physical trigger:

  - 0 = *Sphere*
  - 1 = *Capsule*
  - 2 = *Cylinder*
  - 3 = *Box*
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **size** - Size of the physical trigger:

  - *Radius*, in case of a sphere
  - *Radius* and *height*, in case of a capsule or a cylinder
  - *Dimensions*, in case of the box

## Ptr < Body > getBody ( int num )

Returns the specified body that intersects the physical trigger.
### Arguments

- *int* **num** - Body number.

### Return value

Intersected body.
## float getContactDepth ( int contact ) const

Returns penetration depth by the given contact.
### Arguments

- *int* **contact** - Contact number.

### Return value

Penetration depth.
## Math:: vec3 getContactNormal ( int contact ) const

Returns a normal of the contact point, in world coordinates.
### Arguments

- *int* **contact** - Contact number.

### Return value

Normal of the contact point.
## Ptr < Object > getContactObject ( int contact ) const

Returns an object participating in the contact with a physical trigger .
### Arguments

- *int* **contact** - Contact number.

### Return value

Object in contact.
## Math:: Vec3 getContactPoint ( int contact ) const

Returns world coordinates of the contact point.
### Arguments

- *int* **contact** - Contact number.

### Return value

Contact point.
## Ptr < Shape > getContactShape ( int contact ) const

Returns a shape that collided with a physical trigger.
### Arguments

- *int* **contact** - Contact number.

### Return value

Shape in contact.
## int getContactSurface ( int contact ) const

Returns the surface of the current object, which is in contact .
### Arguments

- *int* **contact** - Contact number.

### Return value

Surface number.
## static int type ( )

Returns the type of the node.
### Return value

[Physical trigger](../../../api/library/nodes/class.node_cpp.md#PHYSICAL_TRIGGER) type identifier.
## void updateContacts ( )

Forces a physical trigger to be updated, i.e. to recalculate its intersections with physical objects and colliders. After that, you can access all updated data; however, event handler functions themselves will be executed only when physics flush is over.
