# Unigine.PhysicalTrigger Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Physical


***Physical Trigger*** triggers events when a physical object gets inside or outside it. To be detected by the trigger, physical objects are required to have at the same time both:


1. [Bodies](../../../api/library/physics/class.body_usc.md) (with matching [Physical Mask](../../../api/library/physics/class.body_usc.md#setPhysicalMask_int_void)) > **Notice:** For [BodyDummy](../../../api/library/physics/class.bodydummy_usc.md) to trigger PhysicalTrigger, you need to call [updateContacts()](#updateContacts_void) first.
2. [Shapes](../../../api/library/physics/class.shape_usc.md) (with matching [Collision mask](../../../api/library/physics/class.shape_usc.md#setCollisionMask_int_void))


To force update of the physical trigger, [updateContacts()](#updateContacts_void) can be called. After that, you can access all updated data about the contacts in the same frame. However, handler functions will still be executed only when the next engine function is called: that is, before *[updatePhysics()](../../../code/fundamentals/execution_sequence/main_loop.md#physics)* (in the current frame), or before the *[update()](../../../code/fundamentals/execution_sequence/main_loop.md#update)* (in the next frame) � whatever comes first.


> **Notice:** If you have moved some nodes and want to execute event handlers based on changed positions in the same frame, you need to call [updateSpatial()](../../../api/library/engine/class.world_usc.md#updateSpatial_void) first.


### See Also


- Video tutorial on [How To Use Physical Triggers to Catch Physical Objects](../../../videotutorials/how_to/how_to_cs/physical_trigger.md)
- Article on [Event Handling](../../../code/fundamentals/events/index.md)
- UnigineScript samples:

  -
  -
  -


### Usage Example


In this example a physical trigger and two boxes, each with a body and a shape, are created. When a box with matching physical mask enters the physical trigger the **trigger_enter()** function is called, when it leaves the trigger - the **trigger_leave()** function is called.


```cpp
#include <core/scripts/primitives.h>

/* .. */

PhysicalTrigger trigger;
ObjectMeshDynamic box1;
ObjectMeshDynamic box2;

// callback function to be fired when a physical object enters the trigger
void trigger_enter(Body body)
{
	// trying to get an object from the body
	Object obj = body.getObject();
	if (obj == NULL)
		return;

	// enabling material emission for all object's surfaces
	for (int i = 0; i < obj.getNumSurfaces(); i++)
		obj.setMaterialState("emission", 1, i);

	// displaying the name of the object entering trigger area
	log.message("\n %s has entered the trigger area!", body.getObject().getName());
}

// callback function to be fired when a physical object leaves the trigger
void trigger_leave(Body body)
{
	// trying to get an object from the body
	Object obj = body.getObject();
	if (obj == NULL)
		return;

	// disabling material emission for all object's surfaces
	for (int i = 0; i < obj.getNumSurfaces(); i++)
		obj.setMaterialState("emission", 0, i);

	// displaying the name of the object leaving trigger area
	log.message("\n %s has left the trigger area!", body.getObject().getName());
}

// function creating a named box having a specified size, color and transformation with a body and a shape
ObjectMeshDynamic createBodyBox(string name, Vec3 size, float mass, Vec4 color, Mat4 transform, int physical_mask)
{
	// creating geometry and setting up its parameters (name, color and transformation)
	ObjectMeshDynamic box = Unigine::createBox(size);
	box.setWorldTransform(transform);
	box.setMaterialParameterFloat4("albedo_color", color, 0);
	box.setName(name);

	// adding physics, i.e. a rigid body and a box shape with specified mass
	BodyRigid body = class_remove(new BodyRigid(box));
	ShapeBox shape = class_remove(new ShapeBox(size));
	shape.setMass(mass);
	body.addShape(shape, translate(0.0f, 0.0f, 0.0f));
	body.setPhysicalMask(physical_mask);
	body.setFreezable(0);

	return box;
}

/* .. */

int init() {
	// setting up a player
	Player player = new PlayerSpectator();
	player.setPosition(Vec3(0.0f,-3.401f,1.5f));
	player.setDirection(Vec3(0.0f,1.0f,-0.4f));
	engine.game.setPlayer(player);

	// enabling visualizer to render bounds of the physical trigger
	engine.console.run("show_visualizer 1");

	// creating a physical trigger and passing it to the Editor
	trigger = new PhysicalTrigger(3,vec3(2.0f, 2.0f, 1.0f));

	// setting trigger's position
	trigger.setPosition(Vec3(0.0f, 0.0f, 1.0f));

	// setting trigger's physical mask equal to 1
	trigger.setPhysicalMask(1);

	// retrieving trigger size
	vec3 size = trigger.getSize();

	// displaying trigger size and shape type
	log.message("\n Trigger parameters size(%f, %f , %f) type: %d", size.x, size.y, size.z, trigger.getShapeType());

	// setting trigger enter callback function
	trigger.setEnterCallback("trigger_enter");

	// setting trigger leave callback function
	trigger.setLeaveCallback("trigger_leave");

	// creating a box with a body and physical mask value equal to 2 to be ignored by the trigger
	box1 = createBodyBox("Box1", vec3(0.2f), 5.0f, vec4(1.0f, 0.0f, 0.0f, 1.0f), translate(Vec3(0.0f, 0.0f, 2.22f)),2);

	// creating a box with a body and physical mask value equal to 1 to affect the trigger
	box2 = createBodyBox("Box2", vec3(0.2f), 0.0f, vec4(1.0f, 1.0f, 0.0f, 1.0f), translate(Vec3(3.5f, 0.0f, 1.2f)),1);

	// displaying physical masks of both boxes and the trigger
	log.message("\n Box1 Physical mask: %d", box1.getBody().getPhysicalMask());
	log.message("\n Box2 Physical mask: %d", box2.getBody().getPhysicalMask());
	log.message("\n Trigger Physical mask: %d", trigger.getPhysicalMask());

	return 1;
}

int update() {
	/* .. */

	// showing the bounds of the physical trigger
	trigger.renderVisualizer();

	// changing the position of the second box
	box2.setWorldPosition(box2.getWorldPosition() - Vec3(0.5f * engine.game.getIFps(), 0.0f, 0.0f));

	return 1;
}

/* .. */

int updatePhysics() {
	// updating information on trigger contacts
	trigger.updateContacts();

	return 1;
}

```


## PhysicalTrigger Class

### Members

## void setSize ( vec3 size )

Sets a new size of the physical trigger.
### Arguments

- *vec3* **size** - The size of the physical trigger:

  - Radius, in case of a sphere (pass the radius in the first element of the vector).
  - Radius and height, in case of a capsule or a cylinder (pass the radius as the first vector element and the height as the second element).
  - Dimensions along the X, Y and Z axes, in case of the box.

## vec3 getSize () const

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
## void setLeaveCallbackName ( string name )

Sets a new name of the callback function fired on leaving the physical trigger. This callback function is set via [setLeaveCallbackName()](#setLeaveCallbackName_cstr_void) .
### Arguments

- *string* **name** - The name of the callback function.

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
## void setEnterCallbackName ( string name )

Sets a new name of the callback function fired on entering the physical trigger.
### Arguments

- *string* **name** - The name of the callback function.

## const char * getEnterCallbackName () const

Returns the current name of the callback function fired on entering the physical trigger.
### Return value

Current name of the callback function.
## void setCollisionMask ( int mask )

Sets a new
### Arguments

- *int* **mask** - The integer, each bit of which is a mask.

## int getCollisionMask () const

Returns the current
### Return value

Current integer, each bit of which is a mask.
## getEventLeave () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEnter () const

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

## static PhysicalTrigger ( int type , vec3 size )

Constructor. Creates a physical trigger of the specified shape and size.
### Arguments

- *int* **type** - Shape of the physical trigger:

  - 0 = *Sphere*
  - 1 = *Capsule*
  - 2 = *Cylinder*
  - 3 = *Box*
- *vec3* **size** - Size of the physical trigger:

  - *Radius*, in case of a sphere
  - *Radius* and *height*, in case of a capsule or a cylinder
  - *Dimensions*, in case of the box

## Body getBody ( int num )

Returns the specified body that intersects the physical trigger.
### Arguments

- *int* **num** - Body number.

### Return value

Intersected body.
## float getContactDepth ( int contact )

Returns penetration depth by the given contact.
### Arguments

- *int* **contact** - Contact number.

### Return value

Penetration depth.
## vec3 getContactNormal ( int contact )

Returns a normal of the contact point, in world coordinates.
### Arguments

- *int* **contact** - Contact number.

### Return value

Normal of the contact point.
## Object getContactObject ( int contact )

Returns an object participating in the contact with a physical trigger .
### Arguments

- *int* **contact** - Contact number.

### Return value

Object in contact.
## Vec3 getContactPoint ( int contact )

Returns world coordinates of the contact point.
### Arguments

- *int* **contact** - Contact number.

### Return value

Contact point.
## Shape getContactShape ( int contact )

Returns a shape that collided with a physical trigger.
### Arguments

- *int* **contact** - Contact number.

### Return value

Shape in contact.
## int getContactSurface ( int contact )

Returns the surface of the current object, which is in contact .
### Arguments

- *int* **contact** - Contact number.

### Return value

Surface number.
## static int type ( )

Returns the type of the node.
### Return value

[Physical trigger](../../../api/library/nodes/class.node_usc.md#PHYSICAL_TRIGGER) type identifier.
## void updateContacts ( )

Forces a physical trigger to be updated, i.e. to recalculate its intersections with physical objects and colliders. After that, you can access all updated data; however, event handler functions themselves will be executed only when physics flush is over.
