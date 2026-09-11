# Unigine::Body Class (CS)


This class is used to simulate [physical bodies](../../../principles/physics/bodies/index.md) that allow an object to participate in physical interactions. A body can have one or several collision [shapes](../../../api/library/physics/class.shape_cs.md) assigned and can be connected together with [joints](../../../api/library/physics/class.joint_cs.md).


> **Notice:** The maximum number of collision shapes for one body is limited to 32768.


To transform a body, one of the following can be used:


- **[Transform](../../...md#setTransform_Mat4_void)**
- **[SetPreserveTransform()](../../...md#setPreserveTransform_Mat4_void)**
- **[SetVelocityTransform()](../../...md#setVelocityTransform_Mat4_void)**


All of these functions take effect when physics calculations are over and **[UpdatePhysics()](../../../code/fundamentals/execution_sequence/main_loop.md#physics)** is performed. Only after that transformations of the body are applied to the rendered node. If a node needs to be transformed immediately after its physical body, **[FlushTransform()](../../...md#flushTransform_void)** is to be called.


The simulation of the body can be [frozen](../../../principles/physics/bodies/index.md#freezing) (if the *[Frozen](#setFrozen_int_void)* flag is set).


Bodies interact with each other via joints or contacts. A contact can be handled by any of the bodies that participate in it. To which body a contact is assigned is random. If the contact is assigned to and handled by the body it is called an **internal** one, otherwise it is called **external** (handled by another body). The total number of contacts for the body includes all, internal and external ones. Iterating through internal contacts is much faster than through external ones, thus you might want a certain body to handle most of the contacts it participates in. This can be done for a rigid body by raising a priority for it via **[BodyRigid.HighPriorityContacts](../../../api/library/physics/class.bodyrigid_cs.md#setHighPriorityContacts_int_void)**.


Within the body contacts are referred to via their **numbers**, in the range from 0 to the [total number of contacts](#getNumContacts_int). While globally each contact has an ID to refer to it, this can be used.


You can subscribe for certain events of a body to handle them:


- *[Frozen](#getEventFrozen_Event)* - to perform some actions when a body [freezes/unfreezes](../../../principles/physics/bodies/index.md#freezing).
- *[Position](#getEventPosition_Event)* - to perform some actions when a body changes its position.
- *[ContactEnter](#getEventContactEnter_Event)* - to perform some actions when a contact emerges (body starts touching another body or collidable surface).
- *[ContactLeave](#getEventContactLeave_Event)* - to perform some actions when a contact ends (body stops touching another body or collidable surface).
- *[Contacts](#getEventContacts_Event)* - to get **all contacts** of the body including new ones (enter) and the ending ones (leave). Leave contacts are removed after the callback execution stage, so this is the only point where you can still get them.


### See Also


- The [Creating and Attaching a Cloth](../../../code/usage/cloth_particle_joint/index_cs.md) usage example demonstrating how to create objects, assign bodies, and add shapes to them
- C++ sample
- C# Component sample
- UnigineScript samples:

  -
  -
  -
- The [Handling Contacts on Collision](../../../code/usage/handling_contacts_on_collision/index_cs.md) usage example


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

### Properties

## 🔒︎ int NumContacts

The total number of contacts in which the body participates. It includes internal (handled by the body) and external [contacts](#contacts) (handled by other bodies).
## 🔒︎ int NumJoints

The number of joints in the body.
## 🔒︎ int NumShapes

The number of shapes comprising the body.
## 🔒︎ int NumChildren

The number of child bodies.
## quat Rotation

The rotation in the world coordinates.
## vec3 Position

The body position (in world coordinates). When setting the value, body's linear and angular velocities will be reset to **0**.
## mat4 Transform

The transformation matrix of the body (in world coordinates). This matrix describes position and orientation of the body. When setting the value, the body's linear and angular velocities are reset to defaults, forces and torques are set to zeros, counted down frozen frames are nullified. Setting the value is required, for example, when the node is dragged to a new position in the editor.
## int PhysicalMask

The bit mask for interactions with [physicals](../../../api/library/physics/class.physical_cs.md). Two objects interact, if they both have matching masks.
## string Name

The name of the body.
## bool Gravity

The value indicating if [gravity](../../../api/library/physics/class.physics_cs.md#setGravity_vec3_void) is affecting the body.
## bool Immovable

The value indicating if the body is immovable (static), i.e. not affected by any forces or collisions.
## bool Frozen

The value indicating if the body is frozen. When a body is frozen, it is not simulated (though its contacts are still calculated) until a collision with a non-frozen body occurs or a force is applied.
## 🔒︎ bool IsEnabledSelf

The value indicating if the body is enabled by its own flag, regardless of the enabled state it may inherit from its node or the physics simulation.
## bool Enabled

The value indicating if physical interactions with the body are enabled.
## 🔒︎ string TypeName

The name of the body type.
## 🔒︎ Body.TYPE Type

The type of the body.
## int ID

The unique ID of the body.
## Object Object

The object whose physical properties and behavior are defined by this body.
## 🔒︎ Body Parent

The parent of the body.
## 🔒︎ vec3 Direction

The normalized direction vector of the body (in world coordinates). By default, a direction vector points along **-Z** axis. It always has an unit length.
## 🔒︎ Event< Body > EventContacts

The event triggered after adding new contacts and before removing the ones that cease to exist. This event can be used to get **all contacts** of the body including new ones (*enter*) and the ending ones (*leave*). *Leave* contacts are removed after the event is triggered, so this is the only point where you can still get them. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** Physics-based events are executed in the main thread, as they are mainly used for creation, destruction or modification of other objects.


> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Body **body**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Contacts event handler
void contacts_event_handler(Body body)
{
	Log.Message("\Handling Contacts event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections contacts_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventContacts.Connect(contacts_event_connections, contacts_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventContacts.Connect(contacts_event_connections, (Body body) => {
		Log.Message("Handling Contacts event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
contacts_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Contacts event with a handler function
publisher.EventContacts.Connect(contacts_event_handler);

// remove subscription to the Contacts event later by the handler function
publisher.EventContacts.Disconnect(contacts_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection contacts_event_connection;

// subscribe to the Contacts event with a lambda handler function and keeping the connection
contacts_event_connection = publisher.EventContacts.Connect((Body body) => {
		Log.Message("Handling Contacts event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
contacts_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
contacts_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
contacts_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Contacts events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventContacts.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventContacts.Enabled = true;

```

</details>

## 🔒︎ Event< Body , int> EventContactLeave

The event triggered when a contact with the body ends (the body stops touching another body). You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** Physics-based events are executed in the main thread, as they are mainly used for creation, destruction or modification of other objects.


> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Body **body**, int **contact_id**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the ContactLeave event handler
void contactleave_event_handler(Body body,  int contact_id)
{
	Log.Message("\Handling ContactLeave event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections contactleave_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventContactLeave.Connect(contactleave_event_connections, contactleave_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventContactLeave.Connect(contactleave_event_connections, (Body body,  int contact_id) => {
		Log.Message("Handling ContactLeave event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
contactleave_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the ContactLeave event with a handler function
publisher.EventContactLeave.Connect(contactleave_event_handler);

// remove subscription to the ContactLeave event later by the handler function
publisher.EventContactLeave.Disconnect(contactleave_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection contactleave_event_connection;

// subscribe to the ContactLeave event with a lambda handler function and keeping the connection
contactleave_event_connection = publisher.EventContactLeave.Connect((Body body,  int contact_id) => {
		Log.Message("Handling ContactLeave event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
contactleave_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
contactleave_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
contactleave_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring ContactLeave events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventContactLeave.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventContactLeave.Enabled = true;

```

</details>

## 🔒︎ Event< Body , int> EventContactEnter

The event triggered when a contact with the body occurs (the body begins touching another body). You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** Physics-based events are executed in the main thread, as they are mainly used for creation, destruction or modification of other objects.


> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Body **body**, int **contact_id**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the ContactEnter event handler
void contactenter_event_handler(Body body,  int contact_id)
{
	Log.Message("\Handling ContactEnter event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections contactenter_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventContactEnter.Connect(contactenter_event_connections, contactenter_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventContactEnter.Connect(contactenter_event_connections, (Body body,  int contact_id) => {
		Log.Message("Handling ContactEnter event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
contactenter_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the ContactEnter event with a handler function
publisher.EventContactEnter.Connect(contactenter_event_handler);

// remove subscription to the ContactEnter event later by the handler function
publisher.EventContactEnter.Disconnect(contactenter_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection contactenter_event_connection;

// subscribe to the ContactEnter event with a lambda handler function and keeping the connection
contactenter_event_connection = publisher.EventContactEnter.Connect((Body body,  int contact_id) => {
		Log.Message("Handling ContactEnter event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
contactenter_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
contactenter_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
contactenter_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring ContactEnter events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventContactEnter.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventContactEnter.Enabled = true;

```

</details>

## 🔒︎ Event< Body > EventPosition

The event triggered when a given body moves a certain distance (rotation is not taken into account). You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** Physics-based events are executed in the main thread, as they are mainly used for creation, destruction or modification of other objects.


> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Body **body**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Position event handler
void position_event_handler(Body body)
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
publisher.EventPosition.Connect(position_event_connections, (Body body) => {
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
position_event_connection = publisher.EventPosition.Connect((Body body) => {
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

## 🔒︎ Event< Body > EventFrozen

The event triggered when a given body [freezes/unfreezes](#isFrozen_int) (i.e. its *Frozen* state changes). Use **[Frozen](../../...md#isFrozen_int)** to define whether the body is frozen or unfrozen at the moment. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** Physics-based events are executed in the main thread, as they are mainly used for creation, destruction or modification of other objects.


> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Body **body**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Frozen event handler
void frozen_event_handler(Body body)
{
	Log.Message("\Handling Frozen event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections frozen_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventFrozen.Connect(frozen_event_connections, frozen_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventFrozen.Connect(frozen_event_connections, (Body body) => {
		Log.Message("Handling Frozen event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
frozen_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Frozen event with a handler function
publisher.EventFrozen.Connect(frozen_event_handler);

// remove subscription to the Frozen event later by the handler function
publisher.EventFrozen.Disconnect(frozen_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection frozen_event_connection;

// subscribe to the Frozen event with a lambda handler function and keeping the connection
frozen_event_connection = publisher.EventFrozen.Connect((Body body) => {
		Log.Message("Handling Frozen event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
frozen_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
frozen_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
frozen_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Frozen events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventFrozen.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventFrozen.Enabled = true;

```

</details>

### Members

---

## Body CreateBody ( int type )

Creates a new body of the specified type.
### Arguments

- *int* **type** - Body type. One of the [BODY_*](#BODY_CLOTH) values.

### Return value

New created body instance.
## Body CreateBody ( string type_name )

Creates a new body of the specified type.
### Arguments

- *string* **type_name** - Body type name.

### Return value

New created body instance.
## string GetTypeName ( int type )

Returns the name of a body type with a given ID.
### Arguments

- *int* **type** - Body type ID. One of the [BODY_*](#BODY_CLOTH) values.

### Return value

Body type name.
## bool SetObject ( Object object , bool update )

Sets an object, which the body approximates.
### Arguments

- *[Object](../../../api/library/objects/class.object_cs.md)* **object** - Object to approximate.
- *bool* **update** - Update flag: true to update the object after assigning the body (by default), false not to update right after body assignment.

### Return value

true if the body is assigned to the specified object successfully; otherwise, false.
## void SetPreserveTransform ( mat4 transform )

Sets a transformation matrix for the body (in world coordinates). This method safely preserves body's linear and angular velocities. It changes only body coordinates - all other body parameters stay the same.
### Arguments

- *mat4* **transform** - Transformation matrix. This matrix describes position, orientation and scale of the body.

## void SetVelocityTransform ( mat4 transform )

Sets a transformation matrix (in world coordinates) and computes linear and angular velocities of the body depending on its trajectory from the current position to the specified one. The time used in calculations corresponds to [physics ticks](../../../api/library/physics/class.physics_cs.md#setIFps_float_void). It clears forces and torques to zeros and nullifies counted down frozen frames.
### Arguments

- *mat4* **transform** - Transformation matrix. This matrix describes position, orientation and scale of the body.

## void FlushTransform ( )

Forces to set the transformations of the body for the node.
## void SetDirection ( vec3 dir , vec3 up )

Updates the direction vector of the body (in world coordinates). By default, a direction vector points along **-Z** axis. This function changes its direction and reorients the body.
### Arguments

- *vec3* **dir** - New direction vector in the world coordinates. The direction vector always has unit length.
- *vec3* **up** - New up vector in the world coordinates.

## int IsChild ( Body body )

Checks if a given body is a child of the body.
### Arguments

- *[Body](../../../api/library/physics/class.body_cs.md)* **body** - Body to check.

### Return value

**1** if the provided body is a child; otherwise, **0**.
## int FindChild ( string name )

Searches for a child body with a given name.
### Arguments

- *string* **name** - Name of the child body.

### Return value

Number of the child in the list of children, if it is found; otherwise, **-1**.
## Body GetChild ( int num )

Returns a given child body.
### Arguments

- *int* **num** - Child number.

### Return value

Corresponding body.
## void AddShape ( Shape shape , mat4 transform )

Adds a shape to the list of shapes comprising the body.
### Arguments

- *[Shape](../../../api/library/physics/class.shape_cs.md)* **shape** - New shape to add.
- *mat4* **transform** - Shape transformation matrix (in the body's coordinate system).

## void AddShape ( Shape shape )

Adds a shape to the list of shapes comprising the body.
### Arguments

- *[Shape](../../../api/library/physics/class.shape_cs.md)* **shape** - New shape to add.

## void RemoveShape ( Shape shape , bool destroy = false )

Removes a given shape from the body.
### Arguments

- *[Shape](../../../api/library/physics/class.shape_cs.md)* **shape** - Shape to be removed.
- *bool* **destroy** - Flag indicating whether the shape is to be destroyed after removal: use true to destroy the shape after removal, or false if you plan to use the shape later. The default value is false.

## void RemoveShape ( int num , bool destroy = false )

Removes a shape with a given number from the body.
### Arguments

- *int* **num** - Shape number.
- *bool* **destroy** - Flag indicating whether the shape is to be destroyed after removal: use true to destroy the shape after removal, or false if you plan to use the shape later. The default value is false.

## void ClearShapes ( int destroy = 0 )

Clears all shapes from the body.
### Arguments

- *int* **destroy** - Flag indicating whether shapes are to be destroyed after removal: use 1 to destroy shapes after removal, or 0 if you plan to use them later. The default value is 0.

## int IsShape ( Shape shape )

Checks if a given shape belongs to the body.
### Arguments

- *[Shape](../../../api/library/physics/class.shape_cs.md)* **shape** - Shape to check.

### Return value

**1** if the shape belongs to the body; otherwise, **0**.
## bool InsertShape ( int pos , Shape shape )

Inserts a given shape at the specified position in the list of body's shapes.
### Arguments

- *int* **pos** - Position in the list at which the shape is to be inserted in the range from 0 to the [number of shapes](#getNumShapes_int).
- *[Shape](../../../api/library/physics/class.shape_cs.md)* **shape** - [Shape](../../../api/library/physics/class.shape_cs.md) to be inserted.

### Return value

true if a shape was successfully inserted; otherwise, false.
## bool InsertShape ( int pos , Shape shape , mat4 transform )

Inserts a given shape at the specified position in the list of body's shapes and sets the specified transformation for it.
### Arguments

- *int* **pos** - Position in the list at which the shape is to be inserted in the range from 0 to the [number of shapes](#getNumShapes_int).
- *[Shape](../../../api/library/physics/class.shape_cs.md)* **shape** - [Shape](../../../api/library/physics/class.shape_cs.md) to be inserted.
- *mat4* **transform** - Shape's transformation (in the body's coordinate system).

### Return value

true if a shape was successfully inserted; otherwise, false.
## int FindShape ( string name )

Searches for a shape with a given name.
### Arguments

- *string* **name** - Name of the shape.

### Return value

Number of the shape in the list of shapes, if it is found; otherwise, **-1**.
## Shape GetShape ( int num )

Returns a given shape.
### Arguments

- *int* **num** - Shape number.

### Return value

Corresponding shape object.
## void SetShapeTransform ( int num , mat4 transform )

Sets a transformation matrix for a given shape (in local coordinates). This matrix describes position and orientation of the shape.
### Arguments

- *int* **num** - Shape number.
- *mat4* **transform** - Transformation matrix (in the body's coordinate system).

## mat4 GetShapeTransform ( int num )

Returns the transformation matrix of a given shape (in local coordinates). This matrix describes position and orientation of the shape.
### Arguments

- *int* **num** - Shape number.

### Return value

Transformation matrix.
## void UpdateShapes ( )

Updates all [shapes](#addShape_Shape_void) of the body.
## void AddJoint ( Joint joint )

Adds a joint to the body.
### Arguments

- *[Joint](../../../api/library/physics/class.joint_cs.md)* **joint** - New joint to add.

## void RemoveJoint ( Joint joint )

Removes a given joint from the body.
### Arguments

- *[Joint](../../../api/library/physics/class.joint_cs.md)* **joint** - Joint to be removed.

## void RemoveJoint ( int num )

Removes a joint with a given number from the body.
### Arguments

- *int* **num** - Joint number.

## void InsertJoint ( Joint joint , int num )

Inserts a given joint at the specified position in the list of body's joints.
### Arguments

- *[Joint](../../../api/library/physics/class.joint_cs.md)* **joint** - [Joint](../../../api/library/physics/class.joint_cs.md) to be inserted.
- *int* **num** - Position in the list at which the joint is to be inserted in the range from 0 to the [number of joints](#getNumJoints_int).

## int IsJoint ( Joint joint )

Checks if a given joint belongs to the body.
### Arguments

- *[Joint](../../../api/library/physics/class.joint_cs.md)* **joint** - Joint to check.

### Return value

**1** if the joint belongs to the body; otherwise, **0**.
## int FindJoint ( string name )

Searches for a joint with a given name.
### Arguments

- *string* **name** - Name of the joint.

### Return value

Number of the joint in the list of joints, if it is found; otherwise, **-1**.
## Joint GetJoint ( int num )

Returns a given joint.
### Arguments

- *int* **num** - Joint number.

### Return value

Corresponding joint.
## Shape GetIntersection ( vec3 p0 , vec3 p1 , int mask , vec3[] OUT_ret_point , vec3[] OUT_ret_normal )


Performs tracing from the p0 point to the p1 point to find a body shape intersected by this line. Intersection is found only for objects with a matching intersection mask. On success *ret_point* and *ret_normal* shall contain information about intersection.


> **Notice:** World space coordinates are used for this function.


### Arguments

- *vec3* **p0** - Start point of the line (in world coordinates).
- *vec3* **p1** - End point of the line (in world coordinates).
- *int* **mask** - Intersection mask.
- *vec3[]* **OUT_ret_point** - Container to which [contact](#contacts) point coordinates (if any) shall be put (in world coordinate system). > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *vec3[]* **OUT_ret_normal** - Container to which [contact](#contacts) point normal coordinates (if any) shall be put (in world coordinate system). > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

First intersected shape, if found; otherwise, 0.
## ulong GetContactID ( int num )

Returns the contact ID by the [contact](#contacts) number.
### Arguments

- *int* **num** - [Contact](#contacts) number in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

Contact ID.
## int FindContactByID ( ulong id )

Returns the number of the [contact](#contacts) by its ID.
### Arguments

- *ulong* **id** - Contact ID.

### Return value

Number of the [contact](#contacts) with the specified ID if it exists, otherwise -1.
## bool IsContactInternal ( int num )

Returns a value indicating whether the [contact](#contacts) with the specified number is internal (handled by the body) or not (handled by another body). A contact can be handled by any of the bodies that participate in it. To which body a contact is assigned is random. If the contact is assigned to and handled by the body it is called an *internal* one, otherwise it is called *external* (handled by another body). The total number of contacts for the body includes all, internal and external ones. Iterating through internal contacts is much faster than through external ones, thus you might want a certain body to handle most of the contacts it participates in. This can be done for a rigid body by raising a priority for the body via **[BodyRigid.HighPriorityContacts](../../../api/library/physics/class.bodyrigid_cs.md#setHighPriorityContacts_int_void)**.
### Arguments

- *int* **num** - [Contact](#contacts) number in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

true if the contact with the specified number is internal; otherwise false.
## bool IsContactEnter ( int num )

Returns a value indicating if the body has begun touching another body at the [contact](#contacts) point with the specified number (the contact has just occurred).
### Arguments

- *int* **num** - [Contact](#contacts) number in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

true if the body has begun touching another body at the contact point with the specified number (the contact has just occurred); otherwise false.
## bool IsContactLeave ( int num )

Returns a value indicating if the body has stopped touching another body at the [contact](#contacts) point with the specified number.
### Arguments

- *int* **num** - [Contact](#contacts) number in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

true if the body has stopped touching another body at the contact point with the specified number; otherwise false.
## bool IsContactStay ( int num )

Returns a value indicating if the body keeps touching another body at the [contact](#contacts) point with the specified number (the contact lasts).
### Arguments

- *int* **num** - [Contact](#contacts) number in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

true if the body keeps touching another body at the contact point with the specified number (the contact lasts); otherwise false.
## vec3 GetContactPoint ( int num )

Returns world coordinates of the [contact](#contacts) point.
### Arguments

- *int* **num** - [Contact](#contacts) number in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

Contact point (in world coordinates).
## vec3 GetContactNormal ( int num )

Returns a normal of the [contact](#contacts) point, in world coordinates.
### Arguments

- *int* **num** - [Contact](#contacts) number in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

Contact normal (in world coordinates).
## vec3 GetContactVelocity ( int num )

Returns relative velocity at the given [contact](#contacts) point.
### Arguments

- *int* **num** - [Contact](#contacts) number in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

Velocity vector.
## float GetContactImpulse ( int num )

Returns the relative impulse at the given [contact](#contacts) point.
### Arguments

- *int* **num** - [Contact](#contacts) number in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

Impulse value.
## float GetContactTime ( int num )

Returns the time when the given [contact](#contacts) occurs. In case of [CCD](../../../api/library/physics/class.shape_cs.md#isContinuous_int), it returns the time starting from the current physics simulation tick to the moment when the calculated contact is bound to happen. In case of non-continuous collision detection, **0** is always returned.
### Arguments

- *int* **num** - [Contact](#contacts) number in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

Time of the calculated contact to happen, in seconds.
## float GetContactDepth ( int num )

Returns the depth by which the body penetrated with an obstacle by the given [contact](#contacts). This distance is measured along the contact normal.
### Arguments

- *int* **num** - [Contact](#contacts) number in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

Penetration depth, in units.
## float GetContactFriction ( int num )

Returns relative friction at the given [contact](#contacts) point.
### Arguments

- *int* **num** - [Contact](#contacts) number in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

Friction value.
## float GetContactRestitution ( int num )

Returns relative restitution at the given [contact](#contacts) point.
### Arguments

- *int* **num** - [Contact](#contacts) number in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

Restitution.
## Body GetContactBody0 ( int num )

Returns the first body participating in a given [contact](#contacts). This is not necessarily the current body.
### Arguments

- *int* **num** - [Contact](#contacts) number in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

First body.
## Body GetContactBody1 ( int num )

Returns the second body participating in a given [contact](#contacts). This is not necessarily the current body.
### Arguments

- *int* **num** - [Contact](#contacts) in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

Second body.
## Shape GetContactShape0 ( int num )

Returns the first shape participating in a given [contact](#contacts). This shape does not necessarily belong to the current body.
### Arguments

- *int* **num** - [Contact](#contacts) in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

First shape.
## Shape GetContactShape1 ( int num )

Returns the second shape participating in a given [contact](#contacts). This shape does not necessarily belong to the current body.
### Arguments

- *int* **num** - [Contact](#contacts) in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

Second shape.
## Object GetContactObject ( int num )

Returns an object participating in the [contact](#contacts) (used for collisions with non-physical object).
### Arguments

- *int* **num** - [Contact](#contacts) in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

Object in contact.
## int GetContactSurface ( int num )

Returns the surface of the current object, which is in [contact](#contacts) (used for collisions with non-physical object).
### Arguments

- *int* **num** - [Contact](#contacts) in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

Surface number.
## void RenderContacts ( )

Renders all [contact](#contacts) points of the body including internal and external ones (handled by other bodies).
> **Notice:** You should enable the engine visualizer via the `show_visualizer 1` console command.


## void RenderExternalContacts ( )

Renders all external [contacts](#contacts) of the body (handled by other bodies).
> **Notice:** You should enable the engine visualizer via the `show_visualizer 1` console command.


## void RenderInternalContacts ( )

Renders all internal [contacts](#contacts) of the body (handled by it).
> **Notice:** You should enable the engine visualizer via the `show_visualizer 1` console command.


## void RenderJoints ( )

Renders joints to which the body is connected.
> **Notice:** You should enable the engine visualizer via the `show_visualizer 1` console command.


## void RenderShapes ( )

Renders shapes comprising the body.
> **Notice:** You should enable the engine visualizer via the `show_visualizer 1` console command.


## void RenderVisualizer ( )

Renders shapes, joints and [contact](#contacts) points of the body.
> **Notice:** You should enable the engine visualizer via the `show_visualizer 1` console command.


## Body Clone ( Object object )

Clones the body and assigns a copy to a given object.
### Arguments

- *[Object](../../../api/library/objects/class.object_cs.md)* **object** - Object, to which the copy will be assigned.

### Return value

Copy of the body.
## void Swap ( Body body )

Swaps the bodies saving the pointers.
### Arguments

- *[Body](../../../api/library/physics/class.body_cs.md)* **body** - Body to swap.

## int SaveState ( Stream stream )

Saves the state of a given body into a binary stream.
**Example** using *saveState()* and *[restoreState()](#restoreState_Stream_int)* methods:


```csharp
// set the body state
body.Position = new vec3(1, 1, 0);

// save state
Blob blob_state = new Blob();
body.SaveState(blob_state);

// change the state
body.Position = new vec3(0, 0, 0);

// restore state
blob_state.SeekSet(0);        // returning the carriage to the start of the blob
body.RestoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream to save body state data.

### Return value

true if the body state is successfully saved; otherwise, false.
## int RestoreState ( Stream stream )

Restores the state of a given body from a binary stream.
**Example** using *[saveState()](#saveState_Stream_int)* and *RestoreState()* methods:


```csharp
// set the body state
body.Position = new vec3(1, 1, 0);

// save state
Blob blob_state = new Blob();
body.SaveState(blob_state);

// change the state
body.Position = new vec3(0, 0, 0);

// restore state
blob_state.SeekSet(0);        // returning the carriage to the start of the blob
body.RestoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream with saved body state data.

### Return value

true if the body state is successfully restored; otherwise, false.
