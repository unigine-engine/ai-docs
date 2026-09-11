# Unigine::Joint Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is used to simulate various types of [joints](../../../principles/physics/joints/index.md) and define common parameters shared by all joints.


### See Also


- C# Component sample
- C++ sample
- UnigineScript sample


## Joint Class

### Members

## void setWorldAnchor ( Vec3 anchor )

Sets a new anchor point in the world coordinates.
### Arguments

- *Vec3* **anchor** - The coordinates of the anchor point in the world space.

## Vec3 getWorldAnchor () const

Returns the current anchor point in the world coordinates.
### Return value

Current coordinates of the anchor point in the world space.
## void setAnchor1 ( Vec3 anchor1 )

Sets a new coordinates of the anchor point in a system of coordinates of the second connected body.
### Arguments

- *Vec3* **anchor1** - The coordinates of the anchor point in the body coordinate space.

## Vec3 getAnchor1 () const

Returns the current coordinates of the anchor point in a system of coordinates of the second connected body.
### Return value

Current coordinates of the anchor point in the body coordinate space.
## void setAnchor0 ( Vec3 anchor0 )

Sets a new coordinates of the anchor point in a system of coordinates of the first connected body.
### Arguments

- *Vec3* **anchor0** - The coordinates of the anchor point in the body coordinate space.

## Vec3 getAnchor0 () const

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
## void setName ( string name )

Sets a new name of the joint.
### Arguments

- *string* **name** - The name of the joint.

## const char * getName () const

Returns the current name of the joint.
### Return value

Current name of the joint.
## void setFrozen ( int frozen )

Sets a new value indicating if the joint is frozen.
### Arguments

- *int* **frozen** - The the joint frozen state

## int isFrozen () const

Returns the current value indicating if the joint is frozen.
### Return value

Current the joint frozen state
## void setBroken ( int broken )

Sets a new value indicating if the joint is broken or intact.
### Arguments

- *int* **broken** - The the joint broken state

## int isBroken () const

Returns the current value indicating if the joint is broken or intact.
### Return value

Current the joint broken state
## void setCollision ( int collision )

Sets a new value indicating if collisions between the connected bodies are enabled.
### Arguments

- *int* **collision** - The value indicating if collisions between the connected bodies are enabled: positive number for enabled collisions between the bodies, **0** for disabled collisions.

## int getCollision () const

Returns the current value indicating if collisions between the connected bodies are enabled.
### Return value

Current value indicating if collisions between the connected bodies are enabled: positive number for enabled collisions between the bodies, **0** for disabled collisions.
## int isEnabledSelf () const

Returns the current value indicating if the joint is enabled by its own flag, regardless of the effective enabled state derived from the connected bodies.
### Return value

Current the joint is enabled by its own flag
## void setEnabled ( int enabled )

Sets a new value indicating if the joint calculations are enabled.
### Arguments

- *int* **enabled** - The joint calculation

## int isEnabled () const

Returns the current value indicating if the joint calculations are enabled.
### Return value

Current joint calculation
## void setBody1 ( Body body1 )

Sets a new second body connected using the joint.
### Arguments

- *[Body](../../../api/library/physics/class.body_usc.md)* **body1** - The second body connected with the joint.

## Body getBody1 () const

Returns the current second body connected using the joint.
### Return value

Current second body connected with the joint.
## void setBody0 ( Body body0 )

Sets a new first body connected using the joint.
### Arguments

- *[Body](../../../api/library/physics/class.body_usc.md)* **body0** - The first body connected with the joint.

## Body getBody0 () const

Returns the current first body connected using the joint.
### Return value

Current first body connected with the joint.
## const char * getTypeName () const

Returns the current name of the joint type.
### Return value

Current name of the joint type.
## int getType () const

Returns the current type of the joint.
### Return value

Current type of the joint, one of the *JOINT_** pre-defined variables.
## void setNode1 ( Node node1 )

Sets a new node possessing the second body connected to the joint.
### Arguments

- *[Node](../../../api/library/nodes/class.node_usc.md)* **node1** - The node possessing the second body connected to the joint is assigned. The node must be an object and must have a body assigned.

## Node getNode1 () const

Returns the current node possessing the second body connected to the joint.
### Return value

Current node possessing the second body connected to the joint is assigned. The node must be an object and must have a body assigned.
## void setNode0 ( Node node0 )

Sets a new node possessing the first body connected to the joint.
### Arguments

- *[Node](../../../api/library/nodes/class.node_usc.md)* **node0** - The node possessing the first body connected to the joint is assigned. The node must be an object and must have a body assigned.

## Node getNode0 () const

Returns the current node possessing the first body connected to the joint.
### Return value

Current node possessing the first body connected to the joint is assigned. The node must be an object and must have a body assigned.
## getEventBroken () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
---

## Joint createJoint ( int type )

Creates a new joint of the specified type.
### Arguments

- *int* **type** - Joint type. One of the [JOINT_*](#JOINT_BALL) values.

### Return value

New created joint instance.
## Joint createJoint ( string type_name )

Creates a new joint of the specified type.
### Arguments

- *string* **type_name** - Joint type name.

### Return value

New created joint instance.
## BodyRigid getBodyRigid0 ( )

Returns the first connected body as a rigid body.
### Return value

The first rigid body connected using the joint or **NULL** (**0**), if the body is not rigid.
## BodyRigid getBodyRigid1 ( )

Returns the second connected body as a rigid body.
### Return value

The second rigid body connected using the joint or **NULL** (**0**), if the body is not rigid.
## int setID ( int id )

Sets the unique ID for the joint.
### Arguments

- *int* **id** - Unique ID.

### Return value

1 if the ID is set successfully; otherwise, 0.
## int getID ( )

Returns the unique ID of the joint.
### Return value

Unique ID.
## string getTypeName ( int type )

Returns the name of a joint type with a given ID.
### Arguments

- *int* **type** - Joint type ID. One of the [JOINT_*](#JOINT_BALL) values.

### Return value

Joint type name.
## Joint clone ( )

Clones the joint.
### Return value

Copy of the joint.
## void renderVisualizer ( vec4 color )

Renders the joint.
> **Notice:** You should enable the engine visualizer by the **show_visualizer 1** console command.


### Arguments

- *vec4* **color** - Color, in which the joint will be rendered.

## int saveState ( Stream stream )

Saves the state of a given node into a binary stream.
- If a node is a parent for other nodes, states of these child nodes need to be saved manually.
- To save the state from a [buffer](../../../api/library/common/class.blob_usc.md), [file](../../../api/library/filesystem/class.file_usc.md) or a message from a [socket](../../../api/library/networking/class.socket_usc.md), make sure the stream is [opened](../../../api/library/common/class.stream_usc.md#isOpened_int). For buffers and files, you also need to set the proper position for reading.


**Example** using saveState() and [restoreState()](#restoreState_Stream_int) methods:


```cpp
// set the joint state
joint.angularRestitution(0.8f);

// save state
Blob blob_state = new Blob();
joint.saveState(blob_state);

// change state
joint.angularRestitution(0.4f);

// restore state
blob_state.seekSet(0); // returning the carriage to the start of the blob
joint.restoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - Stream to save node state data.

### Return value

**1** if the node state is saved successfully; otherwise, **0**.
## int restoreState ( Stream stream )

Restores the state of a given node from a binary stream.
- If a node is a parent for other nodes, states of these child nodes need to be restored manually.
- To save the state into a [buffer](../../../api/library/common/class.blob_usc.md), [file](../../../api/library/filesystem/class.file_usc.md) or a message from a [socket](../../../api/library/networking/class.socket_usc.md), make sure the stream is [opened](../../../api/library/common/class.stream_usc.md#isOpened_int). If necessary, you can set a position for writing for buffers and files.


**Example** using [saveState()](#saveState_Stream_int) and restoreState() methods:


```cpp
// set the joint state
joint.angularRestitution(0.8f);

// save state
Blob blob_state = new Blob();
joint.saveState(blob_state);

// change state
joint.angularRestitution(0.4f);

// restore state
blob_state.seekSet(0); // returning the carriage to the start of the blob
joint.restoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - Stream with saved node state data.

### Return value

**1** if the node state is restored successfully; otherwise, **0**.
## void swap ( Joint joint )

Swaps the joints saving the pointers.
### Arguments

- *[Joint](../../../api/library/physics/class.joint_usc.md)* **joint** - A joint to swap.
