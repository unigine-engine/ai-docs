# Unigine::Body Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is used to simulate [physical bodies](../../../principles/physics/bodies/index.md) that allow an object to participate in physical interactions. A body can have one or several collision [shapes](../../../api/library/physics/class.shape_usc.md) assigned and can be connected together with [joints](../../../api/library/physics/class.joint_usc.md).


> **Notice:** The maximum number of collision shapes for one body is limited to 32768.


To transform a body, one of the following functions can be used:


- [setTransform()](#setTransform_Mat4_void)
- [setPreserveTransform()](#setPreserveTransform_Mat4_void)
- [setVelocityTransform()](#setVelocityTransform_Mat4_void)


All of these functions take effect when physics calculations are over and **[updatePhysics()()](../../../code/fundamentals/execution_sequence/main_loop.md#physics)** is performed. Only after that transformations of the body are applied to the rendered node. If a node needs to be transformed immediately after its physical body, **[flushTransform()()](../../...md#flushTransform_void)** is to be called.


The simulation of the body can be [frozen](../../../principles/physics/bodies/index.md#freezing) (if the *[Frozen](#setFrozen_int_void)* flag is set).


You can subscribe for certain events of a body to handle them:


- *[Frozen](#getEventFrozen_Event)* - to perform some actions when a body [freezes/unfreezes](../../../principles/physics/bodies/index.md#freezing).
- *[Position](#getEventPosition_Event)* - to perform some actions when a body changes its position.
- *[ContactEnter](#getEventContactEnter_Event)* - to perform some actions when a contact emerges (body starts touching another body or collidable surface).
- *[ContactLeave](#getEventContactLeave_Event)* - to perform some actions when a contact ends (body stops touching another body or collidable surface).
- *[Contacts](#getEventContacts_Event)* - to get **all contacts** of the body including new ones (enter) and the ending ones (leave). Leave contacts are removed after the callback execution stage, so this is the only point where you can still get them.


### See Also


- The [Creating and Attaching a Cloth](../../../code/usage/cloth_particle_joint/index_usc.md) usage example demonstrating how to create objects, assign bodies, and add shapes to them
- C++ sample
- C# Component sample
- UnigineScript samples:

  -
  -
  -
- The [Handling Contacts on Collision](../../../code/usage/handling_contacts_on_collision/index.md) usage example


## Body Class

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
## void setRotation ( quat rotation )

Sets a new rotation in the world coordinates.
### Arguments

- *quat* **rotation** - The rotation in the world coordinates.

## quat getRotation () const

Returns the current rotation in the world coordinates.
### Return value

Current rotation in the world coordinates.
## void setPosition ( Vec3 position )

Sets a new body position (in world coordinates). When setting the value, body's linear and angular velocities will be reset to **0**.
### Arguments

- *Vec3* **position** - The position in the world coordinates.

## Vec3 getPosition () const

Returns the current body position (in world coordinates). When setting the value, body's linear and angular velocities will be reset to **0**.
### Return value

Current position in the world coordinates.
## void setTransform ( Mat4 transform )

Sets a new transformation matrix of the body (in world coordinates). This matrix describes position and orientation of the body. When setting the value, the body's linear and angular velocities are reset to defaults, forces and torques are set to zeros, counted down frozen frames are nullified. Setting the value is required, for example, when the node is dragged to a new position in the editor.
### Arguments

- *Mat4* **transform** - The transformation matrix. This matrix describes position, orientation and scale of the body.

## Mat4 getTransform () const

Returns the current transformation matrix of the body (in world coordinates). This matrix describes position and orientation of the body. When setting the value, the body's linear and angular velocities are reset to defaults, forces and torques are set to zeros, counted down frozen frames are nullified. Setting the value is required, for example, when the node is dragged to a new position in the editor.
### Return value

Current transformation matrix. This matrix describes position, orientation and scale of the body.
## void setPhysicalMask ( int mask )

Sets a new bit mask for interactions with [physicals](../../../api/library/physics/class.physical_usc.md). Two objects interact, if they both have matching masks.
### Arguments

- *int* **mask** - The integer, each bit of which is a mask.

## int getPhysicalMask () const

Returns the current bit mask for interactions with [physicals](../../../api/library/physics/class.physical_usc.md). Two objects interact, if they both have matching masks.
### Return value

Current integer, each bit of which is a mask.
## void setName ( string name )

Sets a new name of the body.
### Arguments

- *string* **name** - The name of the body.

## const char * getName () const

Returns the current name of the body.
### Return value

Current name of the body.
## void setGravity ( int gravity )

Sets a new value indicating if [gravity](../../../api/library/physics/class.physics_usc.md#setGravity_vec3_void) is affecting the body.
### Arguments

- *int* **gravity** - The the body is affected by gravity

## int isGravity () const

Returns the current value indicating if [gravity](../../../api/library/physics/class.physics_usc.md#setGravity_vec3_void) is affecting the body.
### Return value

Current the body is affected by gravity
## void setImmovable ( int immovable )

Sets a new value indicating if the body is immovable (static), i.e. not affected by any forces or collisions.
### Arguments

- *int* **immovable** - The the body is immovable (static)

## int isImmovable () const

Returns the current value indicating if the body is immovable (static), i.e. not affected by any forces or collisions.
### Return value

Current the body is immovable (static)
## void setFrozen ( int frozen )

Sets a new value indicating if the body is frozen. When a body is frozen, it is not simulated (though its contacts are still calculated) until a collision with a non-frozen body occurs or a force is applied.
### Arguments

- *int* **frozen** - The body simulation freezing

## int isFrozen () const

Returns the current value indicating if the body is frozen. When a body is frozen, it is not simulated (though its contacts are still calculated) until a collision with a non-frozen body occurs or a force is applied.
### Return value

Current body simulation freezing
## int isEnabledSelf () const

Returns the current value indicating if the body is enabled by its own flag, regardless of the enabled state it may inherit from its node or the physics simulation.
### Return value

Current the body is enabled by its own flag
## void setEnabled ( int enabled )

Sets a new value indicating if physical interactions with the body are enabled.
### Arguments

- *int* **enabled** - The physical simulation of the body

## int isEnabled () const

Returns the current value indicating if physical interactions with the body are enabled.
### Return value

Current physical simulation of the body
## const char * getTypeName () const

Returns the current name of the body type.
### Return value

Current name of the body type.
## getType () const

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
## void setObject ( )

Sets a new object whose physical properties and behavior are defined by this body.
### Arguments

- **object** - The object whose physical properties and behavior are defined by this body.

## getObject () const

Returns the current object whose physical properties and behavior are defined by this body.
### Return value

Current object whose physical properties and behavior are defined by this body.
## Body getParent () const

Returns the current parent of the body.
### Return value

Current parent of the body.
## vec3 getDirection () const

Returns the current normalized direction vector of the body (in world coordinates). By default, a direction vector points along **-Z** axis. It always has an unit length.
### Return value

Current normalized direction vector in the world coordinates.
## getEventContacts () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventContactLeave () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventContactEnter () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventPosition () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventFrozen () const

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

## Body createBody ( int type )

Creates a new body of the specified type.
### Arguments

- *int* **type** - Body type. One of the [BODY_*](#BODY_CLOTH) values.

### Return value

New created body instance.
## Body createBody ( string type_name )

Creates a new body of the specified type.
### Arguments

- *string* **type_name** - Body type name.

### Return value

New created body instance.
## string getTypeName ( int type )

Returns the name of a body type with a given ID.
### Arguments

- *int* **type** - Body type ID. One of the [BODY_*](#BODY_CLOTH) values.

### Return value

Body type name.
## bool setObject ( bool update )

Sets an object, which the body approximates.
### Arguments

- *bool* **update** - Update flag: true to update the object after assigning the body (by default), false not to update right after body assignment.

### Return value

**1** if the body is assigned to the specified object successfully; otherwise, **0**.
## void setPreserveTransform ( Mat4 transform )

Sets a transformation matrix for the body (in world coordinates). This method safely preserves body's linear and angular velocities. It changes only body coordinates - all other body parameters stay the same.
### Arguments

- *Mat4* **transform** - Transformation matrix. This matrix describes position, orientation and scale of the body.

## void setVelocityTransform ( Mat4 transform )

Sets a transformation matrix (in world coordinates) and computes linear and angular velocities of the body depending on its trajectory from the current position to the specified one. The time used in calculations corresponds to [physics ticks](../../../api/library/physics/class.physics_usc.md#setIFps_float_void). It clears forces and torques to zeros and nullifies counted down frozen frames.
### Arguments

- *Mat4* **transform** - Transformation matrix. This matrix describes position, orientation and scale of the body.

## void flushTransform ( )

Forces to set the transformations of the body for the node.
## void setDirection ( vec3 dir , vec3 up )

Updates the direction vector of the body (in world coordinates). By default, a direction vector points along **-Z** axis. This function changes its direction and reorients the body.
### Arguments

- *vec3* **dir** - New direction vector in the world coordinates. The direction vector always has unit length.
- *vec3* **up** - New up vector in the world coordinates.

## int isChild ( Body body )

Checks if a given body is a child of the body.
### Arguments

- *[Body](../../../api/library/physics/class.body_usc.md)* **body** - Body to check.

### Return value

**1** if the provided body is a child; otherwise, **0**.
## int findChild ( string name )

Searches for a child body with a given name.
### Arguments

- *string* **name** - Name of the child body.

### Return value

Number of the child in the list of children, if it is found; otherwise, **-1**.
## Body getChild ( int num )

Returns a given child body.
### Arguments

- *int* **num** - Child number.

### Return value

Corresponding body.
## void addShape ( Shape shape , mat4 transform )

Adds a shape to the list of shapes comprising the body.
### Arguments

- *[Shape](../../../api/library/physics/class.shape_usc.md)* **shape** - New shape to add.
- *mat4* **transform** - Shape transformation matrix (in the body's coordinate system).

## void addShape ( Shape shape )

Adds a shape to the list of shapes comprising the body.
### Arguments

- *[Shape](../../../api/library/physics/class.shape_usc.md)* **shape** - New shape to add.

## void clearShapes ( int destroy = 0 )

Clears all shapes from the body.
### Arguments

- *int* **destroy** - Flag indicating whether shapes are to be destroyed after removal: use 1 to destroy shapes after removal, or 0 if you plan to use them later. The default value is 0.

## int isShape ( Shape shape )

Checks if a given shape belongs to the body.
### Arguments

- *[Shape](../../../api/library/physics/class.shape_usc.md)* **shape** - Shape to check.

### Return value

**1** if the shape belongs to the body; otherwise, **0**.
## int insertShape ( int pos , Shape shape )

Inserts a given shape at the specified position in the list of body's shapes.
### Arguments

- *int* **pos** - Position in the list at which the shape is to be inserted in the range from 0 to the [number of shapes](#getNumShapes_int).
- *[Shape](../../../api/library/physics/class.shape_usc.md)* **shape** - [Shape](../../../api/library/physics/class.shape_usc.md) to be inserted.

### Return value

**1** if a shape was successfully inserted; otherwise, **0**.
## int insertShape ( int pos , Shape shape , mat4 transform )

Inserts a given shape at the specified position in the list of body's shapes and sets the specified transformation for it.
### Arguments

- *int* **pos** - Position in the list at which the shape is to be inserted in the range from 0 to the [number of shapes](#getNumShapes_int).
- *[Shape](../../../api/library/physics/class.shape_usc.md)* **shape** - [Shape](../../../api/library/physics/class.shape_usc.md) to be inserted.
- *mat4* **transform** - Shape's transformation (in the body's coordinate system).

### Return value

**1** if a shape was successfully inserted; otherwise, **0**.
## int findShape ( string name )

Searches for a shape with a given name.
### Arguments

- *string* **name** - Name of the shape.

### Return value

Number of the shape in the list of shapes, if it is found; otherwise, **-1**.
## Shape getShape ( int num )

Returns a given shape.
### Arguments

- *int* **num** - Shape number.

### Return value

Corresponding shape object.
## void setShapeTransform ( int num , mat4 transform )

Sets a transformation matrix for a given shape (in local coordinates). This matrix describes position and orientation of the shape.
### Arguments

- *int* **num** - Shape number.
- *mat4* **transform** - Transformation matrix (in the body's coordinate system).

## mat4 getShapeTransform ( int num )

Returns the transformation matrix of a given shape (in local coordinates). This matrix describes position and orientation of the shape.
### Arguments

- *int* **num** - Shape number.

### Return value

Transformation matrix.
## void updateShapes ( )

Updates all [shapes](#addShape_Shape_void) of the body.
## void addJoint ( Joint joint )

Adds a joint to the body.
### Arguments

- *[Joint](../../../api/library/physics/class.joint_usc.md)* **joint** - New joint to add.

## void removeJoint ( )

Removes a given joint from the body.
### Arguments

## void insertJoint ( Joint joint , int num )

Inserts a given joint at the specified position in the list of body's joints.
### Arguments

- *[Joint](../../../api/library/physics/class.joint_usc.md)* **joint** - [Joint](../../../api/library/physics/class.joint_usc.md) to be inserted.
- *int* **num** - Position in the list at which the joint is to be inserted in the range from 0 to the [number of joints](#getNumJoints_int).

## int isJoint ( Joint joint )

Checks if a given joint belongs to the body.
### Arguments

- *[Joint](../../../api/library/physics/class.joint_usc.md)* **joint** - Joint to check.

### Return value

**1** if the joint belongs to the body; otherwise, **0**.
## int findJoint ( string name )

Searches for a joint with a given name.
### Arguments

- *string* **name** - Name of the joint.

### Return value

Number of the joint in the list of joints, if it is found; otherwise, **-1**.
## Joint getJoint ( int num )

Returns a given joint.
### Arguments

- *int* **num** - Joint number.

### Return value

Corresponding joint.
## getIntersection ( int mask , variable v )


Performs tracing from the p0 point to the p1 point to find a body shape intersected by this line. Intersection is found only for objects with a matching intersection mask. On success *ret_point* and *ret_normal* shall contain information about intersection.


> **Notice:** World space coordinates are used for this function.


Depending on the variable passed as an argument, the result can be presented as a [PhysicsIntersection](../../../api/library/physics/class.physicsintersection_usc.md) or [PhysicsIntersectionNormal](../../../api/library/physics/class.physicsintersectionnormal_usc.md) class instance.


### Arguments

- *int* **mask** - Intersection mask.
- *variable* **v** - Variable defining which type of intersection object will be returned:

  - PhysicsIntersection intersection � [PhysicsIntersection](../../../api/library/physics/class.physicsintersection_usc.md) class instance containing intersection information (contact point coordinates).
  - PhysicsIntersectionNormal normal � [PhysicsIntersectionNormal](../../../api/library/physics/class.physicsintersectionnormal_usc.md) class instance containing intersection information (contact point and normal coordinates).

### Return value

First intersected shape, if found; otherwise, 0.
## long getContactID ( int num )

Returns the contact ID by the [contact](#contacts) number.
### Arguments

- *int* **num** - [Contact](#contacts) number in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

Contact ID.
## int findContactByID ( long id )

Returns the number of the [contact](#contacts) by its ID.
### Arguments

- *long* **id** - Contact ID.

### Return value

Number of the [contact](#contacts) with the specified ID if it exists, otherwise -1.
## int isContactInternal ( int num )

Returns a value indicating whether the [contact](#contacts) with the specified number is internal (handled by the body) or not (handled by another body). A contact can be handled by any of the bodies that participate in it. To which body a contact is assigned is random. If the contact is assigned to and handled by the body it is called an *internal* one, otherwise it is called *external* (handled by another body). The total number of contacts for the body includes all, internal and external ones. Iterating through internal contacts is much faster than through external ones, thus you might want a certain body to handle most of the contacts it participates in. This can be done for a rigid body by raising a priority for the body via **[BodyRigid::setHighPriorityContacts()()](../../../api/library/physics/class.bodyrigid_usc.md#setHighPriorityContacts_int_void)**.
### Arguments

- *int* **num** - [Contact](#contacts) number in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

**1** if the contact with the specified number is internal; otherwise **0**.
## int isContactEnter ( int num )

Returns a value indicating if the body has begun touching another body at the [contact](#contacts) point with the specified number (the contact has just occurred).
### Arguments

- *int* **num** - [Contact](#contacts) number in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

**1** if the body has begun touching another body at the contact point with the specified number (the contact has just occurred); otherwise **0**.
## int isContactLeave ( int num )

Returns a value indicating if the body has stopped touching another body at the [contact](#contacts) point with the specified number.
### Arguments

- *int* **num** - [Contact](#contacts) number in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

**1** if the body has stopped touching another body at the contact point with the specified number; otherwise **0**.
## int isContactStay ( int num )

Returns a value indicating if the body keeps touching another body at the [contact](#contacts) point with the specified number (the contact lasts).
### Arguments

- *int* **num** - [Contact](#contacts) number in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

**1** if the body keeps touching another body at the contact point with the specified number (the contact lasts); otherwise **0**.
## Vec3 getContactPoint ( int num )

Returns world coordinates of the [contact](#contacts) point.
### Arguments

- *int* **num** - [Contact](#contacts) number in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

Contact point (in world coordinates).
## vec3 getContactNormal ( int num )

Returns a normal of the [contact](#contacts) point, in world coordinates.
### Arguments

- *int* **num** - [Contact](#contacts) number in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

Contact normal (in world coordinates).
## vec3 getContactVelocity ( int num )

Returns relative velocity at the given [contact](#contacts) point.
### Arguments

- *int* **num** - [Contact](#contacts) number in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

Velocity vector.
## float getContactImpulse ( int num )

Returns the relative impulse at the given [contact](#contacts) point.
### Arguments

- *int* **num** - [Contact](#contacts) number in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

Impulse value.
## float getContactTime ( int num )

Returns the time when the given [contact](#contacts) occurs. In case of [CCD](../../../api/library/physics/class.shape_usc.md#isContinuous_int), it returns the time starting from the current physics simulation tick to the moment when the calculated contact is bound to happen. In case of non-continuous collision detection, **0** is always returned.
### Arguments

- *int* **num** - [Contact](#contacts) number in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

Time of the calculated contact to happen, in seconds.
## float getContactDepth ( int num )

Returns the depth by which the body penetrated with an obstacle by the given [contact](#contacts). This distance is measured along the contact normal.
### Arguments

- *int* **num** - [Contact](#contacts) number in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

Penetration depth, in units.
## float getContactFriction ( int num )

Returns relative friction at the given [contact](#contacts) point.
### Arguments

- *int* **num** - [Contact](#contacts) number in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

Friction value.
## float getContactRestitution ( int num )

Returns relative restitution at the given [contact](#contacts) point.
### Arguments

- *int* **num** - [Contact](#contacts) number in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

Restitution.
## Body getContactBody0 ( int num )

Returns the first body participating in a given [contact](#contacts). This is not necessarily the current body.
### Arguments

- *int* **num** - [Contact](#contacts) number in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

First body.
## Body getContactBody1 ( int num )

Returns the second body participating in a given [contact](#contacts). This is not necessarily the current body.
### Arguments

- *int* **num** - [Contact](#contacts) in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

Second body.
## Shape getContactShape0 ( int num )

Returns the first shape participating in a given [contact](#contacts). This shape does not necessarily belong to the current body.
### Arguments

- *int* **num** - [Contact](#contacts) in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

First shape.
## Shape getContactShape1 ( int num )

Returns the second shape participating in a given [contact](#contacts). This shape does not necessarily belong to the current body.
### Arguments

- *int* **num** - [Contact](#contacts) in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

Second shape.
## Object getContactObject ( int num )

Returns an object participating in the [contact](#contacts) (used for collisions with non-physical object).
### Arguments

- *int* **num** - [Contact](#contacts) in the range from 0 to the [total number of contacts](#getNumContacts_int).

### Return value

Object in contact.
## int getContactSurface ( int num )

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


## Body clone ( Object object )

Clones the body and assigns a copy to a given object.
### Arguments

- *[Object](../../../api/library/objects/class.object_usc.md)* **object** - Object, to which the copy will be assigned.

### Return value

Copy of the body.
## void swap ( Body body )

Swaps the bodies saving the pointers.
### Arguments

- *[Body](../../../api/library/physics/class.body_usc.md)* **body** - Body to swap.

## int saveState ( Stream stream )

Saves the state of a given body into a binary stream.
**Example** using *saveState()* and *[restoreState()](#restoreState_Stream_int)* methods:


```cpp
// set the body state
body.setPosition(vec3(1, 1, 0));

// save state
Blob blob_state = new Blob();
body.saveState(blob_state);

// change state
body.setPosition(vec3(0, 0, 0));

// restore state
blob_state.seekSet(0); // returning the carriage to the start of the blob
body.restoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - Stream to save body state data.

### Return value

**1** if the body state is successfully saved; otherwise, **0**.
## int restoreState ( Stream stream )

Restores the state of a given body from a binary stream.
**Example** using [saveState()](#saveState_Stream_int) and restoreState() methods:


```cpp
// set the body state
body.setPosition(vec3(1, 1, 0));

// save state
Blob blob_state = new Blob();
body.saveState(blob_state);

// change state
body.setPosition(vec3(0, 0, 0));

// restore state
blob_state.seekSet(0); // returning the carriage to the start of the blob
body.restoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - Stream with saved body state data.

### Return value

**1** if the body state is successfully restored; otherwise, **0**.
