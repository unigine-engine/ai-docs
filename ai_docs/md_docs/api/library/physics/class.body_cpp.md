# Unigine::Body Class (CPP)

**Header:** #include <UniginePhysics.h>


This class is used to simulate [physical bodies](../../../principles/physics/bodies/index.md) that allow an object to participate in physical interactions. A body can have one or several collision [shapes](../../../api/library/physics/class.shape_cpp.md) assigned and can be connected together with [joints](../../../api/library/physics/class.joint_cpp.md).


> **Notice:** The maximum number of collision shapes for one body is limited to 32768.


To transform a body, one of the following can be used:


- **[setTransform()](../../...md#setTransform_Mat4_void)**
- **[setPreserveTransform()](../../...md#setPreserveTransform_Mat4_void)**
- **[setVelocityTransform()](../../...md#setVelocityTransform_Mat4_void)**


All of these functions take effect when physics calculations are over and **[updatePhysics()](../../../code/fundamentals/execution_sequence/main_loop.md#physics)** is performed. Only after that transformations of the body are applied to the rendered node. If a node needs to be transformed immediately after its physical body, **[flushTransform()](../../...md#flushTransform_void)** is to be called.


The simulation of the body can be [frozen](../../../principles/physics/bodies/index.md#freezing) (if the *[Frozen](#setFrozen_int_void)* flag is set).


Bodies interact with each other via joints or contacts. A contact can be handled by any of the bodies that participate in it. To which body a contact is assigned is random. If the contact is assigned to and handled by the body it is called an **internal** one, otherwise it is called **external** (handled by another body). The total number of contacts for the body includes all, internal and external ones. Iterating through internal contacts is much faster than through external ones, thus you might want a certain body to handle most of the contacts it participates in. This can be done for a rigid body by raising a priority for it via **[BodyRigid::setHighPriorityContacts()](../../../api/library/physics/class.bodyrigid_cpp.md#setHighPriorityContacts_int_void)**.


Within the body contacts are referred to via their **numbers**, in the range from 0 to the [total number of contacts](#getNumContacts_int). While globally each contact has an ID to refer to it, this can be used.


You can subscribe for certain events of a body to handle them:


- *[Frozen](#getEventFrozen_Event)* - to perform some actions when a body [freezes/unfreezes](../../../principles/physics/bodies/index.md#freezing).
- *[Position](#getEventPosition_Event)* - to perform some actions when a body changes its position.
- *[ContactEnter](#getEventContactEnter_Event)* - to perform some actions when a contact emerges (body starts touching another body or collidable surface).
- *[ContactLeave](#getEventContactLeave_Event)* - to perform some actions when a contact ends (body stops touching another body or collidable surface).
- *[Contacts](#getEventContacts_Event)* - to get **all contacts** of the body including new ones (enter) and the ending ones (leave). Leave contacts are removed after the callback execution stage, so this is the only point where you can still get them.


### See Also


- The [Creating and Attaching a Cloth](../../../code/usage/cloth_particle_joint/index_cpp.md) usage example demonstrating how to create objects, assign bodies, and add shapes to them
- C++ sample
- C# Component sample
- UnigineScript samples:

  -
  -
  -
- The [Handling Contacts on Collision](../../../code/usage/handling_contacts_on_collision/index_cpp.md) usage example


## Body Class

### Enums

## TYPE

Type of the body defining its physical properties.
| Name | Description |
|---|---|
| **BODY_DUMMY** = 0 | This body is used to create an immovable collider for an object. |
| **BODY_RIGID** = 1 | This is a basic type of body describing a rigid object. |
| **BODY_RAGDOLL** = 2 | This body contains joints connecting parts of the body (represented with [rigid bodies](#BODY_RIGID)). |
| **BODY_FRACTURE** = 3 | This body simulates breakable objects. |
| **BODY_ROPE** = 4 | This body simulates ropes. |
| **BODY_CLOTH** = 5 | This body simulates cloth. |
| **BODY_WATER** = 6 | This body simulates water and other fluids. |
| **BODY_PATH** = 7 | This body simulates a path along which rigid bodies are moving, for example, like a train along the railtrack. |
| **NUM_BODIES** = 8 | The number of bodies. |

### Members

## int getNumContacts () const

Returns the current total number of contacts in which the body participates. It includes internal (handled by the body) and external [contacts](#contacts) (handled by other bodies).
### Return value

Current number of [contacts](#contacts).
## int getNumJoints () const

Returns the current number of joints in the body.
### Return value

Current number of joints in the body.
## int getNumShapes () const

Returns the current number of shapes comprising the body.
### Return value

Current number of shapes.
## int getNumChildren () const

Returns the current number of child bodies.
### Return value

Current number of children.
## void setRotation ( const Math:: quat & rotation )

Sets a new rotation in the world coordinates.
### Arguments

- *const  Math::[quat](../../../api/library/math/class.quat_cpp.md)&* **rotation** - The rotation in the world coordinates.

## Math:: quat getRotation () const

Returns the current rotation in the world coordinates.
### Return value

Current rotation in the world coordinates.
## void setPosition ( const Math:: Vec3 & position )

Sets a new body position (in world coordinates). When setting the value, body's linear and angular velocities will be reset to **0**.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md)&* **position** - The position in the world coordinates.

## Math:: Vec3 getPosition () const

Returns the current body position (in world coordinates). When setting the value, body's linear and angular velocities will be reset to **0**.
### Return value

Current position in the world coordinates.
## void setTransform ( const Math:: Mat4 & transform )

Sets a new transformation matrix of the body (in world coordinates). This matrix describes position and orientation of the body. When setting the value, the body's linear and angular velocities are reset to defaults, forces and torques are set to zeros, counted down frozen frames are nullified. Setting the value is required, for example, when the node is dragged to a new position in the editor.
### Arguments

- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md)&* **transform** - The transformation matrix. This matrix describes position, orientation and scale of the body.

## Math:: Mat4 getTransform () const

Returns the current transformation matrix of the body (in world coordinates). This matrix describes position and orientation of the body. When setting the value, the body's linear and angular velocities are reset to defaults, forces and torques are set to zeros, counted down frozen frames are nullified. Setting the value is required, for example, when the node is dragged to a new position in the editor.
### Return value

Current transformation matrix. This matrix describes position, orientation and scale of the body.
## void setPhysicalMask ( int mask )

Sets a new bit mask for interactions with [physicals](../../../api/library/physics/class.physical_cpp.md). Two objects interact, if they both have matching masks.
### Arguments

- *int* **mask** - The integer, each bit of which is a mask.

## int getPhysicalMask () const

Returns the current bit mask for interactions with [physicals](../../../api/library/physics/class.physical_cpp.md). Two objects interact, if they both have matching masks.
### Return value

Current integer, each bit of which is a mask.
## void setName ( const char * name )

Sets a new name of the body.
### Arguments

- *const char ** **name** - The name of the body.

## const char * getName () const

Returns the current name of the body.
### Return value

Current name of the body.
## void setGravity ( bool gravity )

Sets a new value indicating if [gravity](../../../api/library/physics/class.physics_cpp.md#setGravity_vec3_void) is affecting the body.
### Arguments

- *bool* **gravity** - Set **true** to enable the body is affected by gravity; **false** - to disable it.

## bool isGravity () const

Returns the current value indicating if [gravity](../../../api/library/physics/class.physics_cpp.md#setGravity_vec3_void) is affecting the body.
### Return value

**true** if the body is affected by gravity; otherwise **false**.
## void setImmovable ( bool immovable )

Sets a new value indicating if the body is immovable (static), i.e. not affected by any forces or collisions.
### Arguments

- *bool* **immovable** - Set **true** to enable the body is immovable (static); **false** - to disable it.

## bool isImmovable () const

Returns the current value indicating if the body is immovable (static), i.e. not affected by any forces or collisions.
### Return value

**true** if the body is immovable (static); otherwise **false**.
## void setFrozen ( bool frozen )

Sets a new value indicating if the body is frozen. When a body is frozen, it is not simulated (though its contacts are still calculated) until a collision with a non-frozen body occurs or a force is applied.
### Arguments

- *bool* **frozen** - Set **true** to enable body simulation freezing; **false** - to disable it.

## bool isFrozen () const

Returns the current value indicating if the body is frozen. When a body is frozen, it is not simulated (though its contacts are still calculated) until a collision with a non-frozen body occurs or a force is applied.
### Return value

**true** if body simulation freezing is enabled ; otherwise **false**.
## bool isEnabledSelf () const

Returns the current value indicating if the body is enabled by its own flag, regardless of the enabled state it may inherit from its node or the physics simulation.
### Return value

**true** if the body is enabled by its own flag; otherwise **false**.
## void setEnabled ( bool enabled )

Sets a new value indicating if physical interactions with the body are enabled.
### Arguments

- *bool* **enabled** - Set **true** to enable physical simulation of the body; **false** - to disable it.

## bool isEnabled () const

Returns the current value indicating if physical interactions with the body are enabled.
### Return value

**true** if physical simulation of the body is enabled ; otherwise **false**.
## const char * getTypeName () const

Returns the current name of the body type.
### Return value

Current name of the body type.
## Body::TYPE getType () const

Returns the current type of the body.
### Return value

Current type of the body, one of the *[BODY_*](#BODY_RIGID)* pre-defined variables.
## void setID ( int id )

Sets a new unique ID of the body.
### Arguments

- *int* **id** - The unique ID of the body.

## int getID () const

Returns the current unique ID of the body.
### Return value

Current unique ID of the body.
## void setObject ( const Ptr < Object >& object )

Sets a new object whose physical properties and behavior are defined by this body.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Object](../../../api/library/objects/class.object_cpp.md)>&* **object** - The object whose physical properties and behavior are defined by this body.

## Ptr < Object > getObject () const

Returns the current object whose physical properties and behavior are defined by this body.
### Return value

Current object whose physical properties and behavior are defined by this body.
## Ptr < Body > getParent () const

Returns the current parent of the body.
### Return value

Current parent of the body.
## Math:: vec3 getDirection () const

Returns the current normalized direction vector of the body (in world coordinates). By default, a direction vector points along **-Z** axis. It always has an unit length.
### Return value

Current normalized direction vector in the world coordinates.
## Event<const Ptr < Body > &> getEventContacts () const

event triggered after adding new contacts and before removing the ones that cease to exist. This event can be used to get **all contacts** of the body including new ones (*enter*) and the ending ones (*leave*). *Leave* contacts are removed after the event is triggered, so this is the only point where you can still get them. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** Physics-based events are executed in the main thread, as they are mainly used for creation, destruction or modification of other objects.


> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Body> & **body**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Contacts event handler
void contacts_event_handler(const Ptr<Body> & body)
{
	Log::message("\Handling Contacts event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections contacts_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventContacts().connect(contacts_event_connections, contacts_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventContacts().connect(contacts_event_connections, [](const Ptr<Body> & body) {
		Log::message("\Handling Contacts event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
contacts_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection contacts_event_connection;

// subscribe to the Contacts event with a handler function keeping the connection
publisher->getEventContacts().connect(contacts_event_connection, contacts_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
contacts_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
contacts_event_connection.setEnabled(true);

// ...

// remove subscription to the Contacts event via the connection
contacts_event_connection.disconnect();

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

	// A Contacts event handler implemented as a class member
	void event_handler(const Ptr<Body> & body)
	{
		Log::message("\Handling Contacts event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventContacts().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId contacts_handler_id;

// subscribe to the Contacts event with a lambda handler function and keeping connection ID
contacts_handler_id = publisher->getEventContacts().connect(e_connections, [](const Ptr<Body> & body) {
		Log::message("\Handling Contacts event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventContacts().disconnect(contacts_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Contacts events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventContacts().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventContacts().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < Body > &, int> getEventContactLeave () const

event triggered when a contact with the body ends (the body stops touching another body). You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** Physics-based events are executed in the main thread, as they are mainly used for creation, destruction or modification of other objects.


> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Body> & **body**, int **contact_id**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the ContactLeave event handler
void contactleave_event_handler(const Ptr<Body> & body,  int contact_id)
{
	Log::message("\Handling ContactLeave event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections contactleave_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventContactLeave().connect(contactleave_event_connections, contactleave_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventContactLeave().connect(contactleave_event_connections, [](const Ptr<Body> & body,  int contact_id) {
		Log::message("\Handling ContactLeave event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
contactleave_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection contactleave_event_connection;

// subscribe to the ContactLeave event with a handler function keeping the connection
publisher->getEventContactLeave().connect(contactleave_event_connection, contactleave_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
contactleave_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
contactleave_event_connection.setEnabled(true);

// ...

// remove subscription to the ContactLeave event via the connection
contactleave_event_connection.disconnect();

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

	// A ContactLeave event handler implemented as a class member
	void event_handler(const Ptr<Body> & body,  int contact_id)
	{
		Log::message("\Handling ContactLeave event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventContactLeave().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId contactleave_handler_id;

// subscribe to the ContactLeave event with a lambda handler function and keeping connection ID
contactleave_handler_id = publisher->getEventContactLeave().connect(e_connections, [](const Ptr<Body> & body,  int contact_id) {
		Log::message("\Handling ContactLeave event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventContactLeave().disconnect(contactleave_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all ContactLeave events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventContactLeave().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventContactLeave().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < Body > &, int> getEventContactEnter () const

event triggered when a contact with the body occurs (the body begins touching another body). You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** Physics-based events are executed in the main thread, as they are mainly used for creation, destruction or modification of other objects.


<details>
<summary>See Example | Close</summary>

**Usage Example**


```cpp
// implement the ContactEnter event handler
void contactenter_event_handler(const Ptr<Body> & body,  int contact_id)
{
	Log::message("\Handling ContactEnter event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections contactenter_event_connections;

// link to this instance when subscribing for an event (subscription for various events can be linked)
body->getEventContactEnter().connect(contactenter_event_connections, contactenter_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
body->getEventContactEnter().connect(contactenter_event_connections, [](const Ptr<Body> & body,  int contact_id) {
		Log::message("\Handling ContactEnter event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
contactenter_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection contactenter_event_connection;

// subscribe for the ContactEnter event with a handler function keeping the connection
body->getEventContactEnter().connect(contactenter_event_connection, contactenter_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
contactenter_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
contactenter_event_connection.setEnabled(true);

// ...

// remove subscription for the ContactEnter event via the connection
contactenter_event_connection.disconnect();

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

	// A ContactEnter event handler implemented as a class member
	void event_handler(const Ptr<Body> & body,  int contact_id)
	{
		Log::message("\Handling ContactEnter event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
body->getEventContactEnter().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//  4. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe for the ContactEnter event with a handler function
body->getEventContactEnter().connect(contactenter_event_handler);

// remove subscription for the ContactEnter event later by the handler function
body->getEventContactEnter().disconnect(contactenter_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   5. Subscribe to an event saving an ID and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////

// define a connection ID to be used to unsubscribe later
EventConnectionId contactenter_handler_id;

// subscribe for the ContactEnter event with a lambda handler function and keeping connection ID
contactenter_handler_id = body->getEventContactEnter().connect([](const Ptr<Body> & body,  int contact_id) {
		Log::message("\Handling ContactEnter event (lambda).\n");
	}
);

// remove the subscription later using the ID
body->getEventContactEnter().disconnect(contactenter_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   6. Ignoring all ContactEnter events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
body->getEventContactEnter().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
body->getEventContactEnter().setEnabled(true);
```

</details>


> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Body> & **body**, int **contact_id**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the ContactEnter event handler
void contactenter_event_handler(const Ptr<Body> & body,  int contact_id)
{
	Log::message("\Handling ContactEnter event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections contactenter_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventContactEnter().connect(contactenter_event_connections, contactenter_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventContactEnter().connect(contactenter_event_connections, [](const Ptr<Body> & body,  int contact_id) {
		Log::message("\Handling ContactEnter event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
contactenter_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection contactenter_event_connection;

// subscribe to the ContactEnter event with a handler function keeping the connection
publisher->getEventContactEnter().connect(contactenter_event_connection, contactenter_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
contactenter_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
contactenter_event_connection.setEnabled(true);

// ...

// remove subscription to the ContactEnter event via the connection
contactenter_event_connection.disconnect();

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

	// A ContactEnter event handler implemented as a class member
	void event_handler(const Ptr<Body> & body,  int contact_id)
	{
		Log::message("\Handling ContactEnter event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventContactEnter().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId contactenter_handler_id;

// subscribe to the ContactEnter event with a lambda handler function and keeping connection ID
contactenter_handler_id = publisher->getEventContactEnter().connect(e_connections, [](const Ptr<Body> & body,  int contact_id) {
		Log::message("\Handling ContactEnter event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventContactEnter().disconnect(contactenter_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all ContactEnter events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventContactEnter().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventContactEnter().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < Body > &> getEventPosition () const

event triggered when a given body moves a certain distance (rotation is not taken into account). You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** Physics-based events are executed in the main thread, as they are mainly used for creation, destruction or modification of other objects.


> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Body> & **body**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Position event handler
void position_event_handler(const Ptr<Body> & body)
{
	Log::message("\Handling Position event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections position_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventPosition().connect(position_event_connections, position_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventPosition().connect(position_event_connections, [](const Ptr<Body> & body) {
		Log::message("\Handling Position event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
position_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection position_event_connection;

// subscribe to the Position event with a handler function keeping the connection
publisher->getEventPosition().connect(position_event_connection, position_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
position_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
position_event_connection.setEnabled(true);

// ...

// remove subscription to the Position event via the connection
position_event_connection.disconnect();

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

	// A Position event handler implemented as a class member
	void event_handler(const Ptr<Body> & body)
	{
		Log::message("\Handling Position event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventPosition().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId position_handler_id;

// subscribe to the Position event with a lambda handler function and keeping connection ID
position_handler_id = publisher->getEventPosition().connect(e_connections, [](const Ptr<Body> & body) {
		Log::message("\Handling Position event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventPosition().disconnect(position_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Position events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventPosition().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventPosition().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < Body > &> getEventFrozen () const

event triggered when a given body [freezes/unfreezes](#isFrozen_int) (i.e. its *Frozen* state changes). Use **[isFrozen()](../../...md#isFrozen_int)** to define whether the body is frozen or unfrozen at the moment. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** Physics-based events are executed in the main thread, as they are mainly used for creation, destruction or modification of other objects.


> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Body> & **body**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Frozen event handler
void frozen_event_handler(const Ptr<Body> & body)
{
	Log::message("\Handling Frozen event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections frozen_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventFrozen().connect(frozen_event_connections, frozen_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventFrozen().connect(frozen_event_connections, [](const Ptr<Body> & body) {
		Log::message("\Handling Frozen event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
frozen_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection frozen_event_connection;

// subscribe to the Frozen event with a handler function keeping the connection
publisher->getEventFrozen().connect(frozen_event_connection, frozen_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
frozen_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
frozen_event_connection.setEnabled(true);

// ...

// remove subscription to the Frozen event via the connection
frozen_event_connection.disconnect();

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

	// A Frozen event handler implemented as a class member
	void event_handler(const Ptr<Body> & body)
	{
		Log::message("\Handling Frozen event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventFrozen().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId frozen_handler_id;

// subscribe to the Frozen event with a lambda handler function and keeping connection ID
frozen_handler_id = publisher->getEventFrozen().connect(e_connections, [](const Ptr<Body> & body) {
		Log::message("\Handling Frozen event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventFrozen().disconnect(frozen_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Frozen events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventFrozen().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventFrozen().setEnabled(true);

```

</details>

### Return value

Event instance.
---

## Ptr < Body > createBody ( int type )

Creates a new body of the specified type.
### Arguments

- *int* **type** - Body type. One of the [BODY_*](#BODY_CLOTH) values.

### Return value

New created body smart pointer.
## Ptr < Body > createBody ( const char * type_name )

Creates a new body of the specified type.
### Arguments

- *const char ** **type_name** - Body type name.

### Return value

New created body smart pointer.
## const char * getTypeName ( int type )

Returns the name of a body type with a given ID.
### Arguments

- *int* **type** - Body type ID. One of the [BODY_*](#BODY_CLOTH) values.

### Return value

Body type name.
## bool setObject ( const Ptr < Object > & object , bool update )

Sets an object, which the body approximates.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Object](../../../api/library/objects/class.object_cpp.md)> &* **object** - Object to approximate.
- *bool* **update** - Update flag: true to update the object after assigning the body (by default), false not to update right after body assignment.

### Return value

true if the body is assigned to the specified object successfully; otherwise, false.
## void setPreserveTransform ( const Math:: Mat4 & transform )

Sets a transformation matrix for the body (in world coordinates). This method safely preserves body's linear and angular velocities. It changes only body coordinates - all other body parameters stay the same.
### Arguments

- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix. This matrix describes position, orientation and scale of the body.

## void setVelocityTransform ( const Math:: Mat4 & transform )

Sets a transformation matrix (in world coordinates) and computes linear and angular velocities of the body depending on its trajectory from the current position to the specified one. The time used in calculations corresponds to [physics ticks](../../../api/library/physics/class.physics_cpp.md#setIFps_float_void). It clears forces and torques to zeros and nullifies counted down frozen frames.
### Arguments

- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix. This matrix describes position, orientation and scale of the body.

## void flushTransform ( ) const

Forces to set the transformations of the body for the node.
## void setDirection ( const Math:: vec3 & dir , const Math:: vec3 & up )

Updates the direction vector of the body (in world coordinates). By default, a direction vector points along **-Z** axis. This function changes its direction and reorients the body.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **dir** - New direction vector in the world coordinates. The direction vector always has unit length.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **up** - New up vector in the world coordinates.

## int isChild ( const Ptr < Body > & body ) const

Checks if a given body is a child of the body.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Body](../../../api/library/physics/class.body_cpp.md)> &* **body** - Body to check.

### Return value

**1** if the provided body is a child; otherwise, **0**.
## int findChild ( const char * name ) const

Searches for a child body with a given name.
### Arguments

- *const char ** **name** - Name of the child body.

### Return value

Number of the child in the list of children, if it is found; otherwise, **-1**.
## Ptr < Body > getChild ( int num ) const

Returns a given child body.
### Arguments

- *int* **num** - Child number.

### Return value

Corresponding body.
## void addShape ( const Ptr < Shape > & shape , const Math:: mat4 & transform )

Adds a shape to the list of shapes comprising the body.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Shape](../../../api/library/physics/class.shape_cpp.md)> &* **shape** - New shape to add.
- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Shape transformation matrix (in the body's coordinate system).

## void addShape ( const Ptr < Shape > & shape )

Adds a shape to the list of shapes comprising the body.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Shape](../../../api/library/physics/class.shape_cpp.md)> &* **shape** - New shape to add.

## void removeShape ( const Ptr < Shape > & shape , bool destroy = false )

Removes a given shape from the body.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Shape](../../../api/library/physics/class.shape_cpp.md)> &* **shape** - Shape to be removed.
- *bool* **destroy** - Flag indicating whether the shape is to be destroyed after removal: use true to destroy the shape after removal, or false if you plan to use the shape later. The default value is false.

## void removeShape ( int num , bool destroy = false )

Removes a shape with a given number from the body.
### Arguments

- *int* **num** - Shape number.
- *bool* **destroy** - Flag indicating whether the shape is to be destroyed after removal: use true to destroy the shape after removal, or false if you plan to use the shape later. The default value is false.

## void clearShapes ( int destroy = 0 )

Clears all shapes from the body.
### Arguments

- *int* **destroy** - Flag indicating whether shapes are to be destroyed after removal: use 1 to destroy shapes after removal, or 0 if you plan to use them later. The default value is 0.

## int isShape ( const Ptr < Shape > & shape ) const

Checks if a given shape belongs to the body.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Shape](../../../api/library/physics/class.shape_cpp.md)> &* **shape** - Shape to check.

### Return value

**1** if the shape belongs to the body; otherwise, **0**.
## bool insertShape ( int pos , const Ptr < Shape > & shape )

Inserts a given shape at the specified position in the list of body's shapes.
### Arguments

- *int* **pos** - Position in the list at which the shape is to be inserted in the range from 0 to the [number of shapes](#getNumShapes_int).
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Shape](../../../api/library/physics/class.shape_cpp.md)> &* **shape** - [Shape](../../../api/library/physics/class.shape_cpp.md) to be inserted.

### Return value

true if a shape was successfully inserted; otherwise, false.
## bool insertShape ( int pos , const Ptr < Shape > & shape , const Math:: mat4 & transform )

Inserts a given shape at the specified position in the list of body's shapes and sets the specified transformation for it.
### Arguments

- *int* **pos** - Position in the list at which the shape is to be inserted in the range from 0 to the [number of shapes](#getNumShapes_int).
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Shape](../../../api/library/physics/class.shape_cpp.md)> &* **shape** - [Shape](../../../api/library/physics/class.shape_cpp.md) to be inserted.
- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Shape's transformation (in the body's coordinate system).

### Return value

true if a shape was successfully inserted; otherwise, false.
## int findShape ( const char * name ) const

Searches for a shape with a given name.
### Arguments

- *const char ** **name** - Name of the shape.

### Return value

Number of the shape in the list of shapes, if it is found; otherwise, **-1**.
## Ptr < Shape > getShape ( int num ) const

Returns a given shape.
### Arguments

- *int* **num** - Shape number.

### Return value

Corresponding shape object.
## void setShapeTransform ( int num , const Math:: mat4 & transform )

Sets a transformation matrix for a given shape (in local coordinates). This matrix describes position and orientation of the shape.
### Arguments

- *int* **num** - Shape number.
- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix (in the body's coordinate system).

## Math:: mat4 getShapeTransform ( int num ) const

Returns the transformation matrix of a given shape (in local coordinates). This matrix describes position and orientation of the shape.
### Arguments

- *int* **num** - Shape number.

### Return value

Transformation matrix.
## void updateShapes ( )

Updates all [shapes](#addShape_Shape_void) of the body.
## void addJoint ( const Ptr < Joint > & joint )

Adds a joint to the body.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Joint](../../../api/library/physics/class.joint_cpp.md)> &* **joint** - New joint to add.

## void removeJoint ( const Ptr < Joint > & joint )

Removes a given joint from the body.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Joint](../../../api/library/physics/class.joint_cpp.md)> &* **joint** - Joint to be removed.

## void removeJoint ( int num )

Removes a joint with a given number from the body.
### Arguments

- *int* **num** - Joint number.

## void insertJoint ( const Ptr < Joint > & joint , int num )

Inserts a given joint at the specified position in the list of body's joints.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Joint](../../../api/library/physics/class.joint_cpp.md)> &* **joint** - [Joint](../../../api/library/physics/class.joint_cpp.md) to be inserted.
- *int* **num** - Position in the list at which the joint is to be inserted in the range from 0 to the [number of joints](#getNumJoints_int).

## int isJoint ( const Ptr < Joint > & joint ) const

Checks if a given joint belongs to the body.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Joint](../../../api/library/physics/class.joint_cpp.md)> &* **joint** - Joint to check.

### Return value

**1** if the joint belongs to the body; otherwise, **0**.
## int findJoint ( const char * name ) const

Searches for a joint with a given name.
### Arguments

- *const char ** **name** - Name of the joint.

### Return value

Number of the joint in the list of joints, if it is found; otherwise, **-1**.
## Ptr < Joint > getJoint ( int num ) const

Returns a given joint.
### Arguments

- *int* **num** - Joint number.

### Return value

Corresponding joint.
## Ptr < Shape > getIntersection ( const Math:: Vec3 & p0 , const Math:: Vec3 & p1 , int mask , Math:: Vec3 * OUT_ret_point , Math:: vec3 * OUT_ret_normal )


Performs tracing from the p0 point to the p1 point to find a body shape intersected by this line. Intersection is found only for objects with a matching intersection mask. On success *ret_point* and *ret_normal* shall contain information about intersection.


> **Notice:** World space coordinates are used for this function.


### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - Start point of the line (in world coordinates).
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - End point of the line (in world coordinates).
- *int* **mask** - Intersection mask.
- *Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) ** **OUT_ret_point** - Container to which [contact](#contacts) point coordinates (if any) shall be put (in world coordinate system). > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md) ** **OUT_ret_normal** - Container to which [contact](#contacts) point normal coordinates (if any) shall be put (in world coordinate system). > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

First intersected shape, if found; otherwise, 0.
## unsigned long long getContactID ( int num ) const

Returns the contact ID by the [contact](#contacts) number.
### Arguments

- *int* **num** - [Contact](#contacts) number in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

Contact ID.
## int findContactByID ( unsigned long long id ) const

Returns the number of the [contact](#contacts) by its ID.
### Arguments

- *unsigned long long* **id** - Contact ID.

### Return value

Number of the [contact](#contacts) with the specified ID if it exists, otherwise -1.
## bool isContactInternal ( int num ) const

Returns a value indicating whether the [contact](#contacts) with the specified number is internal (handled by the body) or not (handled by another body). A contact can be handled by any of the bodies that participate in it. To which body a contact is assigned is random. If the contact is assigned to and handled by the body it is called an *internal* one, otherwise it is called *external* (handled by another body). The total number of contacts for the body includes all, internal and external ones. Iterating through internal contacts is much faster than through external ones, thus you might want a certain body to handle most of the contacts it participates in. This can be done for a rigid body by raising a priority for the body via **[BodyRigid::setHighPriorityContacts()](../../../api/library/physics/class.bodyrigid_cpp.md#setHighPriorityContacts_int_void)**.
### Arguments

- *int* **num** - [Contact](#contacts) number in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

true if the contact with the specified number is internal; otherwise false.
## bool isContactEnter ( int num ) const

Returns a value indicating if the body has begun touching another body at the [contact](#contacts) point with the specified number (the contact has just occurred).
### Arguments

- *int* **num** - [Contact](#contacts) number in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

true if the body has begun touching another body at the contact point with the specified number (the contact has just occurred); otherwise false.
## bool isContactLeave ( int num ) const

Returns a value indicating if the body has stopped touching another body at the [contact](#contacts) point with the specified number.
### Arguments

- *int* **num** - [Contact](#contacts) number in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

true if the body has stopped touching another body at the contact point with the specified number; otherwise false.
## bool isContactStay ( int num ) const

Returns a value indicating if the body keeps touching another body at the [contact](#contacts) point with the specified number (the contact lasts).
### Arguments

- *int* **num** - [Contact](#contacts) number in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

true if the body keeps touching another body at the contact point with the specified number (the contact lasts); otherwise false.
## Math:: Vec3 getContactPoint ( int num ) const

Returns world coordinates of the [contact](#contacts) point.
### Arguments

- *int* **num** - [Contact](#contacts) number in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

Contact point (in world coordinates).
## Math:: vec3 getContactNormal ( int num ) const

Returns a normal of the [contact](#contacts) point, in world coordinates.
### Arguments

- *int* **num** - [Contact](#contacts) number in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

Contact normal (in world coordinates).
## Math:: vec3 getContactVelocity ( int num ) const

Returns relative velocity at the given [contact](#contacts) point.
### Arguments

- *int* **num** - [Contact](#contacts) number in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

Velocity vector.
## float getContactImpulse ( int num ) const

Returns the relative impulse at the given [contact](#contacts) point.
### Arguments

- *int* **num** - [Contact](#contacts) number in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

Impulse value.
## float getContactTime ( int num ) const

Returns the time when the given [contact](#contacts) occurs. In case of [CCD](../../../api/library/physics/class.shape_cpp.md#isContinuous_int), it returns the time starting from the current physics simulation tick to the moment when the calculated contact is bound to happen. In case of non-continuous collision detection, **0** is always returned.
### Arguments

- *int* **num** - [Contact](#contacts) number in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

Time of the calculated contact to happen, in seconds.
## float getContactDepth ( int num ) const

Returns the depth by which the body penetrated with an obstacle by the given [contact](#contacts). This distance is measured along the contact normal.
### Arguments

- *int* **num** - [Contact](#contacts) number in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

Penetration depth, in units.
## float getContactFriction ( int num ) const

Returns relative friction at the given [contact](#contacts) point.
### Arguments

- *int* **num** - [Contact](#contacts) number in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

Friction value.
## float getContactRestitution ( int num ) const

Returns relative restitution at the given [contact](#contacts) point.
### Arguments

- *int* **num** - [Contact](#contacts) number in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

Restitution.
## Ptr < Body > getContactBody0 ( int num ) const

Returns the first body participating in a given [contact](#contacts). This is not necessarily the current body.
### Arguments

- *int* **num** - [Contact](#contacts) number in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

First body.
## Ptr < Body > getContactBody1 ( int num ) const

Returns the second body participating in a given [contact](#contacts). This is not necessarily the current body.
### Arguments

- *int* **num** - [Contact](#contacts) in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

Second body.
## Ptr < Shape > getContactShape0 ( int num ) const

Returns the first shape participating in a given [contact](#contacts). This shape does not necessarily belong to the current body.
### Arguments

- *int* **num** - [Contact](#contacts) in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

First shape.
## Ptr < Shape > getContactShape1 ( int num ) const

Returns the second shape participating in a given [contact](#contacts). This shape does not necessarily belong to the current body.
### Arguments

- *int* **num** - [Contact](#contacts) in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

Second shape.
## Ptr < Object > getContactObject ( int num ) const

Returns an object participating in the [contact](#contacts) (used for collisions with non-physical object).
### Arguments

- *int* **num** - [Contact](#contacts) in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

Object in contact.
## int getContactSurface ( int num ) const

Returns the surface of the current object, which is in [contact](#contacts) (used for collisions with non-physical object).
### Arguments

- *int* **num** - [Contact](#contacts) in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

Surface number.
## void renderContacts ( )

Renders all [contact](#contacts) points of the body including internal and external ones (handled by other bodies).
> **Notice:** You should enable the engine visualizer via the `show_visualizer 1` console command.


## void renderExternalContacts ( )

Renders all external [contacts](#contacts) of the body (handled by other bodies).
> **Notice:** You should enable the engine visualizer via the `show_visualizer 1` console command.


## void renderInternalContacts ( )

Renders all internal [contacts](#contacts) of the body (handled by it).
> **Notice:** You should enable the engine visualizer via the `show_visualizer 1` console command.


## void renderJoints ( )

Renders joints to which the body is connected.
> **Notice:** You should enable the engine visualizer via the `show_visualizer 1` console command.


## void renderShapes ( )

Renders shapes comprising the body.
> **Notice:** You should enable the engine visualizer via the `show_visualizer 1` console command.


## void renderVisualizer ( )

Renders shapes, joints and [contact](#contacts) points of the body.
> **Notice:** You should enable the engine visualizer via the `show_visualizer 1` console command.


## Ptr < Body > clone ( const Ptr < Object > & object ) const

Clones the body and assigns a copy to a given object.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Object](../../../api/library/objects/class.object_cpp.md)> &* **object** - Object, to which the copy will be assigned.

### Return value

Copy of the body.
## void swap ( const Ptr < Body > & body ) const

Swaps the bodies saving the pointers.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Body](../../../api/library/physics/class.body_cpp.md)> &* **body** - Body to swap.

## int saveState ( const Ptr < Stream > & stream ) const

Saves the state of a given body into a binary stream.
**Example** using saveState() and [restoreState()](#restoreState_Stream_int) methods:


```cpp
// set the body state
body->setPosition(vec3(1, 1, 0));

// save state
BlobPtr blob_state = Blob::create();
body->saveState(blob_state);

// change the state
body->setPosition(vec3(0, 0, 0));

// restore state
blob_state->seekSet(0);       // returning the carriage to the start of the blob
body->restoreState(blob_state);

```


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream to save body state data.

### Return value

true if the body state is successfully saved; otherwise, false.
## int restoreState ( const Ptr < Stream > & stream )

Restores the state of a given body from a binary stream.
**Example** using *[saveState()](#saveState_Stream_int)* and *restoreState()* methods:


```cpp
// set the body state
body->setPosition(vec3(1, 1, 0));

// save state
BlobPtr blob_state = Blob::create();
body->saveState(blob_state);

// change the state
body->setPosition(vec3(0, 0, 0));

// restore state
blob_state->seekSet(0);       // returning the carriage to the start of the blob
body->restoreState(blob_state);

```


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream with saved body state data.

### Return value

true if the body state is successfully restored; otherwise, false.
