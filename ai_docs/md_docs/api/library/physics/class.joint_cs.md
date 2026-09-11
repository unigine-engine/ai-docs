# Unigine::Joint Class (CS)


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

### Properties

## vec3 WorldAnchor

The anchor point in the world coordinates.
## vec3 Anchor1

The coordinates of the anchor point in a system of coordinates of the second connected body.
## vec3 Anchor0

The coordinates of the anchor point in a system of coordinates of the first connected body.
## float AngularSoftness

The angular softness (elasticity) of the joint. when the joint is twisted, angular softness defines whether angular velocities of the bodies are averaged out. for example:
- **0** means that the joint is rigid. Angular velocities of the first and the second body are independent.
- **1** means that the joint is elastic (jelly-like). If the first body changes its velocity, velocity of the second body is equalized with it.


## float LinearSoftness

The linear softness (elasticity) of the joint. when the joint is stretched, linear softness defines whether linear velocities of the bodies are averaged out. for example:
- **0** means that the joint is rigid. Velocities of the first and the second body are independent.
- **1** means that the joint is elastic (jelly-like). If the first body changes its velocity, velocity of the second body is equalized with it.


## float AngularRestitution

The angular restitution (stiffness) of the joint. angular restitution defines how fast the joint compensates for change of the angle between two bodies. when bodies are turned relative each other, restitution controls the magnitude of force which is applied to both bodies so that their anchor points to become aligned again. for example:
- **1** means that the joint is to return bodies in place throughout 1 physics tick.
- **0.2** means that the joint is to return bodies in place throughout 5 physics ticks.

The maximum value of **1** can lead to destabilization of physics (as too great forces are applied).
## float LinearRestitution

The linear restitution (stiffness) of the joint. linear restitution defines how fast the joint compensates for linear coordinate change between two bodies. when bodies are dragged apart, restitution controls the magnitude of force which is applied to both bodies so that their anchor points to become aligned again. for example:
- **1** means that the joint is to return bodies in place throughout 1 physics tick.
- **0.2** means that the joint is to return bodies in place throughout 5 physics ticks.

The maximum value of **1** can lead to destabilization of physics (as too great forces are applied).
## float MaxTorque

The maximum amount of torque that can be exerted on the joint. if this limit is exceeded, the joint breaks.
## float MaxForce

The maximum amount of force that can be exerted on the joint. if this limit is exceeded, the joint breaks.
## int NumIterations

The number of iterations used to solve joints. If a non-positive value is set as a value, **1** will be used instead.
## string Name

The name of the joint.
## bool Frozen

The value indicating if the joint is frozen.
## bool Broken

The value indicating if the joint is broken or intact.
## int Collision

The value indicating if collisions between the connected bodies are enabled.
## 🔒︎ bool IsEnabledSelf

The value indicating if the joint is enabled by its own flag, regardless of the effective enabled state derived from the connected bodies.
## bool Enabled

The value indicating if the joint calculations are enabled.
## Body Body1

The second body connected using the joint.
## Body Body0

The first body connected using the joint.
## 🔒︎ string TypeName

The name of the joint type.
## 🔒︎ Joint.TYPE Type

The type of the joint.
## Node Node1

The node possessing the second body connected to the joint.
## Node Node0

The node possessing the first body connected to the joint.
## 🔒︎ Event< Joint > EventBroken

The Event triggered when the joint breaks. The event handler must receive a *Joint* as an argument. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Joint **joint**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Broken event handler
void broken_event_handler(Joint joint)
{
	Log.Message("\Handling Broken event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections broken_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBroken.Connect(broken_event_connections, broken_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBroken.Connect(broken_event_connections, (Joint joint) => {
		Log.Message("Handling Broken event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
broken_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Broken event with a handler function
publisher.EventBroken.Connect(broken_event_handler);

// remove subscription to the Broken event later by the handler function
publisher.EventBroken.Disconnect(broken_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection broken_event_connection;

// subscribe to the Broken event with a lambda handler function and keeping the connection
broken_event_connection = publisher.EventBroken.Connect((Joint joint) => {
		Log.Message("Handling Broken event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
broken_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
broken_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
broken_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Broken events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBroken.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBroken.Enabled = true;

```

</details>

### Members

---

## Joint CreateJoint ( int type )

Creates a new joint of the specified type.
### Arguments

- *int* **type** - Joint type. One of the [JOINT_*](#JOINT_BALL) values.

### Return value

New created joint instance.
## Joint CreateJoint ( string type_name )

Creates a new joint of the specified type.
### Arguments

- *string* **type_name** - Joint type name.

### Return value

New created joint instance.
## BodyRigid GetBodyRigid0 ( )

Returns the first connected body as a rigid body.
### Return value

The first rigid body connected using the joint or **NULL** (**0**), if the body is not rigid.
## BodyRigid GetBodyRigid1 ( )

Returns the second connected body as a rigid body.
### Return value

The second rigid body connected using the joint or **NULL** (**0**), if the body is not rigid.
## int SetID ( int id )

Sets the unique ID for the joint.
### Arguments

- *int* **id** - Unique ID.

### Return value

1 if the ID is set successfully; otherwise, 0.
## int GetID ( )

Returns the unique ID of the joint.
### Return value

Unique ID.
## string GetTypeName ( int type )

Returns the name of a joint type with a given ID.
### Arguments

- *int* **type** - Joint type ID. One of the [JOINT_*](#JOINT_BALL) values.

### Return value

Joint type name.
## Joint Clone ( )

Clones the joint.
### Return value

Copy of the joint.
## void RenderVisualizer ( vec4 color )

Renders the joint.
> **Notice:** You should enable the engine visualizer by the **show_visualizer 1** console command.


### Arguments

- *vec4* **color** - Color, in which the joint will be rendered.

## int SaveState ( Stream stream )

Saves the state of a given node into a binary stream.
- If a node is a parent for other nodes, states of these child nodes need to be saved manually.
- To save the state from a [buffer](../../../api/library/common/class.blob_cs.md), [file](../../../api/library/filesystem/class.file_cs.md) or a message from a [socket](../../../api/library/networking/class.socket_cs.md), make sure the stream is [opened](../../../api/library/common/class.stream_cs.md#isOpened_int). For buffers and files, you also need to set the proper position for reading.


**Example** using saveState() and [restoreState()](#restoreState_Stream_int) methods:


```csharp
// set the joint state
joint.AngularRestitution = 0.8f;

// save state
Blob blob_state = new Blob();
joint.SaveState(blob_state);

// change the state
joint.AngularRestitution = 0.4f;

// restore state
blob_state.SeekSet(0);        // returning the carriage to the start of the blob
joint.RestoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream to save node state data.

### Return value

true if the node state is saved successfully; otherwise, false.
## int RestoreState ( Stream stream )

Restores the state of a given node from a binary stream.
- If a node is a parent for other nodes, states of these child nodes need to be restored manually.
- To save the state into a [buffer](../../../api/library/common/class.blob_cs.md), [file](../../../api/library/filesystem/class.file_cs.md) or a message from a [socket](../../../api/library/networking/class.socket_cs.md), make sure the stream is [opened](../../../api/library/common/class.stream_cs.md#isOpened_int). If necessary, you can set a position for writing for buffers and files.


**Example** using [saveState()](#saveState_Stream_int) and restoreState() methods:


```csharp
// set the joint state
joint.AngularRestitution = 0.8f;

// save state
Blob blob_state = new Blob();
joint.SaveState(blob_state);

// change the state
joint.AngularRestitution = 0.4f;

// restore state
blob_state.SeekSet(0);        // returning the carriage to the start of the blob
joint.RestoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream with saved node state data.

### Return value

true if the node state is restored successfully; otherwise, false.
## void Swap ( Joint joint )

Swaps the joints saving the pointers.
### Arguments

- *[Joint](../../../api/library/physics/class.joint_cs.md)* **joint** - A joint to swap.
