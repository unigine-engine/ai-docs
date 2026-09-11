# Unigine::Joint Class (CPP)

**Header:** #include <UniginePhysics.h>


This class is used to simulate various types of [joints](../../../principles/physics/joints/index.md) and define common parameters shared by all joints.


### See Also


- C# Component sample
- C++ sample
- UnigineScript sample


## Joint Class

### Enums

## TYPE

Type of the joint defining its properties.
| Name | Description |
|---|---|
| **JOINT_FIXED** = 0 | [Fixed joint](../../../principles/physics/joints/index.md#fixed). |
| **JOINT_BALL** = 1 | [Ball joint](../../../principles/physics/joints/index.md#ball). |
| **JOINT_HINGE** = 2 | [Hinge joint](../../../principles/physics/joints/index.md#hinge). |
| **JOINT_PRISMATIC** = 3 | [Prismatic joint](../../../principles/physics/joints/index.md#prismatic). |
| **JOINT_CYLINDRICAL** = 4 | [Cylindrical joint](../../../principles/physics/joints/index.md#cylindrical). |
| **JOINT_SUSPENSION** = 5 | Suspension joint. |
| **JOINT_WHEEL** = 6 | [Wheel joint](../../../principles/physics/joints/index.md#wheel). |
| **JOINT_PARTICLES** = 7 | [Particles joint](../../../principles/physics/joints/index.md#particles). |
| **JOINT_PATH** = 8 | [Path joint](../../../principles/physics/joints/index.md#path). |
| **NUM_JOINTS** = 9 | Number of joints. |

### Members

## void setWorldAnchor ( const Math:: Vec3 & anchor )

Sets a new anchor point in the world coordinates.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md)&* **anchor** - The coordinates of the anchor point in the world space.

## Math:: Vec3 getWorldAnchor () const

Returns the current anchor point in the world coordinates.
### Return value

Current coordinates of the anchor point in the world space.
## void setAnchor1 ( const Math:: Vec3 & anchor1 )

Sets a new coordinates of the anchor point in a system of coordinates of the second connected body.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md)&* **anchor1** - The coordinates of the anchor point in the body coordinate space.

## Math:: Vec3 getAnchor1 () const

Returns the current coordinates of the anchor point in a system of coordinates of the second connected body.
### Return value

Current coordinates of the anchor point in the body coordinate space.
## void setAnchor0 ( const Math:: Vec3 & anchor0 )

Sets a new coordinates of the anchor point in a system of coordinates of the first connected body.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md)&* **anchor0** - The coordinates of the anchor point in the body coordinate space.

## Math:: Vec3 getAnchor0 () const

Returns the current coordinates of the anchor point in a system of coordinates of the first connected body.
### Return value

Current coordinates of the anchor point in the body coordinate space.
## void setAngularSoftness ( float softness )

Sets a new angular softness (elasticity) of the joint. when the joint is twisted, angular softness defines whether angular velocities of the bodies are averaged out. for example:
- **0** means that the joint is rigid. Angular velocities of the first and the second body are independent.
- **1** means that the joint is elastic (jelly-like). If the first body changes its velocity, velocity of the second body is equalized with it.


### Arguments

- *float* **softness** - The angular softness. The provided value will be clamped in the range **[0;1]**.

## float getAngularSoftness () const

Returns the current angular softness (elasticity) of the joint. when the joint is twisted, angular softness defines whether angular velocities of the bodies are averaged out. for example:
- **0** means that the joint is rigid. Angular velocities of the first and the second body are independent.
- **1** means that the joint is elastic (jelly-like). If the first body changes its velocity, velocity of the second body is equalized with it.


### Return value

Current angular softness. The provided value will be clamped in the range **[0;1]**.
## void setLinearSoftness ( float softness )

Sets a new linear softness (elasticity) of the joint. when the joint is stretched, linear softness defines whether linear velocities of the bodies are averaged out. for example:
- **0** means that the joint is rigid. Velocities of the first and the second body are independent.
- **1** means that the joint is elastic (jelly-like). If the first body changes its velocity, velocity of the second body is equalized with it.


### Arguments

- *float* **softness** - The linear softness. The provided value will be clamped in the range **[0;1]**.

## float getLinearSoftness () const

Returns the current linear softness (elasticity) of the joint. when the joint is stretched, linear softness defines whether linear velocities of the bodies are averaged out. for example:
- **0** means that the joint is rigid. Velocities of the first and the second body are independent.
- **1** means that the joint is elastic (jelly-like). If the first body changes its velocity, velocity of the second body is equalized with it.


### Return value

Current linear softness. The provided value will be clamped in the range **[0;1]**.
## void setAngularRestitution ( float restitution )

Sets a new angular restitution (stiffness) of the joint. angular restitution defines how fast the joint compensates for change of the angle between two bodies. when bodies are turned relative each other, restitution controls the magnitude of force which is applied to both bodies so that their anchor points to become aligned again. for example:
- **1** means that the joint is to return bodies in place throughout 1 physics tick.
- **0.2** means that the joint is to return bodies in place throughout 5 physics ticks.

The maximum value of **1** can lead to destabilization of physics (as too great forces are applied).
### Arguments

- *float* **restitution** - The angular restitution. The provided value will be clamped in the range **[0;1]**.

## float getAngularRestitution () const

Returns the current angular restitution (stiffness) of the joint. angular restitution defines how fast the joint compensates for change of the angle between two bodies. when bodies are turned relative each other, restitution controls the magnitude of force which is applied to both bodies so that their anchor points to become aligned again. for example:
- **1** means that the joint is to return bodies in place throughout 1 physics tick.
- **0.2** means that the joint is to return bodies in place throughout 5 physics ticks.

The maximum value of **1** can lead to destabilization of physics (as too great forces are applied).
### Return value

Current angular restitution. The provided value will be clamped in the range **[0;1]**.
## void setLinearRestitution ( float restitution )

Sets a new linear restitution (stiffness) of the joint. linear restitution defines how fast the joint compensates for linear coordinate change between two bodies. when bodies are dragged apart, restitution controls the magnitude of force which is applied to both bodies so that their anchor points to become aligned again. for example:
- **1** means that the joint is to return bodies in place throughout 1 physics tick.
- **0.2** means that the joint is to return bodies in place throughout 5 physics ticks.

The maximum value of **1** can lead to destabilization of physics (as too great forces are applied).
### Arguments

- *float* **restitution** - The linear restitution. The provided value will be clamped in the range **[0;1]**.

## float getLinearRestitution () const

Returns the current linear restitution (stiffness) of the joint. linear restitution defines how fast the joint compensates for linear coordinate change between two bodies. when bodies are dragged apart, restitution controls the magnitude of force which is applied to both bodies so that their anchor points to become aligned again. for example:
- **1** means that the joint is to return bodies in place throughout 1 physics tick.
- **0.2** means that the joint is to return bodies in place throughout 5 physics ticks.

The maximum value of **1** can lead to destabilization of physics (as too great forces are applied).
### Return value

Current linear restitution. The provided value will be clamped in the range **[0;1]**.
## void setMaxTorque ( float torque )

Sets a new maximum amount of torque that can be exerted on the joint. if this limit is exceeded, the joint breaks.
### Arguments

- *float* **torque** - The maximum amount of torque.

## float getMaxTorque () const

Returns the current maximum amount of torque that can be exerted on the joint. if this limit is exceeded, the joint breaks.
### Return value

Current maximum amount of torque.
## void setMaxForce ( float force )

Sets a new maximum amount of force that can be exerted on the joint. if this limit is exceeded, the joint breaks.
### Arguments

- *float* **force** - The maximum amount of force.

## float getMaxForce () const

Returns the current maximum amount of force that can be exerted on the joint. if this limit is exceeded, the joint breaks.
### Return value

Current maximum amount of force.
## void setNumIterations ( int iterations )

Sets a new number of iterations used to solve joints. If a non-positive value is set as a value, **1** will be used instead.
### Arguments

- *int* **iterations** - The number of iterations.

## int getNumIterations () const

Returns the current number of iterations used to solve joints. If a non-positive value is set as a value, **1** will be used instead.
### Return value

Current number of iterations.
## void setName ( const char * name )

Sets a new name of the joint.
### Arguments

- *const char ** **name** - The name of the joint.

## const char * getName () const

Returns the current name of the joint.
### Return value

Current name of the joint.
## void setFrozen ( bool frozen )

Sets a new value indicating if the joint is frozen.
### Arguments

- *bool* **frozen** - Set **true** to enable the joint frozen state; **false** - to disable it.

## bool isFrozen () const

Returns the current value indicating if the joint is frozen.
### Return value

**true** if the joint frozen state is enabled ; otherwise **false**.
## void setBroken ( bool broken )

Sets a new value indicating if the joint is broken or intact.
### Arguments

- *bool* **broken** - Set **true** to enable the joint broken state; **false** - to disable it.

## bool isBroken () const

Returns the current value indicating if the joint is broken or intact.
### Return value

**true** if the joint broken state is enabled ; otherwise **false**.
## void setCollision ( int collision )

Sets a new value indicating if collisions between the connected bodies are enabled.
### Arguments

- *int* **collision** - The value indicating if collisions between the connected bodies are enabled: positive number for enabled collisions between the bodies, **0** for disabled collisions.

## int getCollision () const

Returns the current value indicating if collisions between the connected bodies are enabled.
### Return value

Current value indicating if collisions between the connected bodies are enabled: positive number for enabled collisions between the bodies, **0** for disabled collisions.
## bool isEnabledSelf () const

Returns the current value indicating if the joint is enabled by its own flag, regardless of the effective enabled state derived from the connected bodies.
### Return value

**true** if the joint is enabled by its own flag; otherwise **false**.
## void setEnabled ( bool enabled )

Sets a new value indicating if the joint calculations are enabled.
### Arguments

- *bool* **enabled** - Set **true** to enable joint calculation; **false** - to disable it.

## bool isEnabled () const

Returns the current value indicating if the joint calculations are enabled.
### Return value

**true** if joint calculation is enabled ; otherwise **false**.
## void setBody1 ( const Ptr < Body >& body1 )

Sets a new second body connected using the joint.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Body](../../../api/library/physics/class.body_cpp.md)>&* **body1** - The second body connected with the joint.

## Ptr < Body > getBody1 () const

Returns the current second body connected using the joint.
### Return value

Current second body connected with the joint.
## void setBody0 ( const Ptr < Body >& body0 )

Sets a new first body connected using the joint.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Body](../../../api/library/physics/class.body_cpp.md)>&* **body0** - The first body connected with the joint.

## Ptr < Body > getBody0 () const

Returns the current first body connected using the joint.
### Return value

Current first body connected with the joint.
## const char * getTypeName () const

Returns the current name of the joint type.
### Return value

Current name of the joint type.
## Joint::TYPE getType () const

Returns the current type of the joint.
### Return value

Current type of the joint, one of the *JOINT_** pre-defined variables.
## void setNode1 ( const Ptr < Node >& node1 )

Sets a new node possessing the second body connected to the joint.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>&* **node1** - The node possessing the second body connected to the joint is assigned. The node must be an object and must have a body assigned.

## Ptr < Node > getNode1 () const

Returns the current node possessing the second body connected to the joint.
### Return value

Current node possessing the second body connected to the joint is assigned. The node must be an object and must have a body assigned.
## void setNode0 ( const Ptr < Node >& node0 )

Sets a new node possessing the first body connected to the joint.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>&* **node0** - The node possessing the first body connected to the joint is assigned. The node must be an object and must have a body assigned.

## Ptr < Node > getNode0 () const

Returns the current node possessing the first body connected to the joint.
### Return value

Current node possessing the first body connected to the joint is assigned. The node must be an object and must have a body assigned.
## Event<const Ptr < Joint > &> getEventBroken () const

Event triggered when the joint breaks. The event handler must receive a *Joint* as an argument. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Joint> & **joint**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Broken event handler
void broken_event_handler(const Ptr<Joint> & joint)
{
	Log::message("\Handling Broken event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections broken_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBroken().connect(broken_event_connections, broken_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBroken().connect(broken_event_connections, [](const Ptr<Joint> & joint) {
		Log::message("\Handling Broken event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
broken_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection broken_event_connection;

// subscribe to the Broken event with a handler function keeping the connection
publisher->getEventBroken().connect(broken_event_connection, broken_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
broken_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
broken_event_connection.setEnabled(true);

// ...

// remove subscription to the Broken event via the connection
broken_event_connection.disconnect();

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

	// A Broken event handler implemented as a class member
	void event_handler(const Ptr<Joint> & joint)
	{
		Log::message("\Handling Broken event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBroken().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId broken_handler_id;

// subscribe to the Broken event with a lambda handler function and keeping connection ID
broken_handler_id = publisher->getEventBroken().connect(e_connections, [](const Ptr<Joint> & joint) {
		Log::message("\Handling Broken event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBroken().disconnect(broken_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Broken events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBroken().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBroken().setEnabled(true);

```

</details>

### Return value

Event instance.
---

## Ptr < Joint > createJoint ( int type )

Creates a new joint of the specified type.
### Arguments

- *int* **type** - Joint type. One of the [JOINT_*](#JOINT_BALL) values.

### Return value

New created joint smart pointer.
## Ptr < Joint > createJoint ( const char * type_name )

Creates a new joint of the specified type.
### Arguments

- *const char ** **type_name** - Joint type name.

### Return value

New created joint smart pointer.
## Ptr < BodyRigid > getBodyRigid0 ( )

Returns the first connected body as a rigid body.
### Return value

The first rigid body connected using the joint or **NULL** (**0**), if the body is not rigid.
## Ptr < BodyRigid > getBodyRigid1 ( )

Returns the second connected body as a rigid body.
### Return value

The second rigid body connected using the joint or **NULL** (**0**), if the body is not rigid.
## int setID ( int id )

Sets the unique ID for the joint.
### Arguments

- *int* **id** - Unique ID.

### Return value

1 if the ID is set successfully; otherwise, 0.
## int getID ( ) const

Returns the unique ID of the joint.
### Return value

Unique ID.
## const char * getTypeName ( int type )

Returns the name of a joint type with a given ID.
### Arguments

- *int* **type** - Joint type ID. One of the [JOINT_*](#JOINT_BALL) values.

### Return value

Joint type name.
## Ptr < Joint > clone ( ) const

Clones the joint.
### Return value

Copy of the joint.
## void renderVisualizer ( const Math:: vec4 & color )

Renders the joint.
> **Notice:** You should enable the engine visualizer by the **show_visualizer 1** console command.


### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color, in which the joint will be rendered.

## int saveState ( const Ptr < Stream > & stream ) const

Saves the state of a given node into a binary stream.
- If a node is a parent for other nodes, states of these child nodes need to be saved manually.
- To save the state from a [buffer](../../../api/library/common/class.blob_cpp.md), [file](../../../api/library/filesystem/class.file_cpp.md) or a message from a [socket](../../../api/library/networking/class.socket_cpp.md), make sure the stream is [opened](../../../api/library/common/class.stream_cpp.md#isOpened_int). For buffers and files, you also need to set the proper position for reading.


**Example** using saveState() and [restoreState()](#restoreState_Stream_int) methods:


```cpp
// set the joint state
joint->setAngularRestitution(0.8f);

// save state
BlobPtr blob_state = Blob::create();
joint->saveState(blob_state);

// change the state
joint->setAngularRestitution(0.4f);

// restore state
blob_state->seekSet(0);       // returning the carriage to the start of the blob
joint->restoreState(blob_state);

```


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream to save node state data.

### Return value

true if the node state is saved successfully; otherwise, false.
## int restoreState ( const Ptr < Stream > & stream )

Restores the state of a given node from a binary stream.
- If a node is a parent for other nodes, states of these child nodes need to be restored manually.
- To save the state into a [buffer](../../../api/library/common/class.blob_cpp.md), [file](../../../api/library/filesystem/class.file_cpp.md) or a message from a [socket](../../../api/library/networking/class.socket_cpp.md), make sure the stream is [opened](../../../api/library/common/class.stream_cpp.md#isOpened_int). If necessary, you can set a position for writing for buffers and files.


**Example** using [saveState()](#saveState_Stream_int) and restoreState() methods:


```cpp
// set the joint state
joint->setAngularRestitution(0.8f);

// save state
BlobPtr blob_state = Blob::create();
joint->saveState(blob_state);

// change the state
joint->setAngularRestitution(0.4f);

// restore state
blob_state->seekSet(0);       // returning the carriage to the start of the blob
joint->restoreState(blob_state);

```


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream with saved node state data.

### Return value

true if the node state is restored successfully; otherwise, false.
## void swap ( const Ptr < Joint > & joint )

Swaps the joints saving the pointers.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Joint](../../../api/library/physics/class.joint_cpp.md)> &* **joint** - A joint to swap.
