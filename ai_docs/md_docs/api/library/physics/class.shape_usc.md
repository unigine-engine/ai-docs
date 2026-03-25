# Unigine::Shape Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class creates collision shapes that approximate the finite volume of physical [bodies](../../../api/library/physics/class.body_usc.md) and allow them to collide. Shapes are [assigned to a body](#setBody_Body_void) and are [positioned](../../../api/library/physics/class.body_usc.md#setShapeTransform_int_mat4_void) in its local coordinates.


### See Also


- [Enabling Selective Surface-Based Collision](../../../code/usage/enabling_collision/index_usc.md) usage example demonstrating how to apply the collision mask
- *[Collision Shapes](../../../code/uniginescript/samples/collision_shapes.md)* section of UnigineScript samples


## Shape Class

### Members

---

## vec3 getArea ( )

Returns areas of shape projections on three axes: *x*, *y*, and *z*.
### Return value

A triple of projection areas.
## void setBody ( Body body )

Sets a body, to which the shape belongs.
### Arguments

- *[Body](../../../api/library/physics/class.body_usc.md)* **body** - Body, to which the shape belongs.

## Body getBody ( )

Returns the body, to which the shape belongs.
### Return value

Body, to which the shape belongs.
## void setBodyShapeTransform ( mat4 transform )

Sets a transformation matrix for the shape (in the coordinates of the body). This matrix describes position and orientation of the shape. This method is identical to [setShapeTransform()](../../../api/library/physics/class.body_usc.md#setShapeTransform_int_mat4_void).
### Arguments

- *mat4* **transform** - Transformation matrix

## mat4 getBodyShapeTransform ( )

Returns the transformation matrix of the shape (in the coordinates of the body). This matrix describes position and orientation of the shape. This method is identical to [getShapeTransform()](../../../api/library/physics/class.body_usc.md#getShapeTransform_int_mat4).
### Return value

Transformation matrix
## vec3 getCenterOfMass ( )

Returns local coordinates of the center of mass of the shape.
### Return value

Coordinates of the center of mass.
## int getCollision ( Vector< Contact >& contacts , Vector< Contact >& contacts )

Performs collision check for the shape and puts information on all contacts to the output buffer.
Collisions with the surface can be found only if the following conditions are fulfilled:


1. The surface is enabled.
2. Per-surface [Collision](../../../api/library/objects/class.object_usc.md#setCollision_int_int_void) flag is enabled.
3. The surface has a material assigned.


> **Notice:** The shape must be [enabled](#setEnabled_int_void).


### Arguments

- *Vector<[Contact](../../../api/library/physics/class.contact_usc.md)>&* **contacts** - Output buffer containing information on all detected physical contacts for the shape (if any). Information on each contact can be handled via the [Contact class](../../../api/library/physics/class.contact_usc.md).
- *Vector<[Contact](../../../api/library/physics/class.contact_usc.md)>&* **contacts** - Inverse FPS value.

### Return value

1 if collisions are found; otherwise, 0.
## int getCollision ( Object object , Vector<ShapeContact>& contacts , Object object )

Performs collision check for the shape and puts information on all contacts and contact object to the output buffer.
Collisions with the surface can be found only if the following conditions are fulfilled:


1. The surface is enabled.
2. Per-surface [Collision](../../../api/library/objects/class.object_usc.md#setCollision_int_int_void) flag is enabled.
3. The surface has a material assigned.


> **Notice:** The shape must be [enabled](#setEnabled_int_void).


### Arguments

- *[Object](../../../api/library/objects/class.object_usc.md)* **object** - Contact object instance.
- *Vector<ShapeContact>&* **contacts** - Output buffer containing information on all detected physical contacts for the shape (if any). Information on each contact can be handled via the [Contact class](../../../api/library/physics/class.contact_usc.md).
- *[Object](../../../api/library/objects/class.object_usc.md)* **object** - Inverse FPS value.

### Return value

1 if collisions are found; otherwise, 0.
## void setCollisionMask ( int mask )

Sets a collision mask for the shape. Two objects collide if they both have matching masks. See also details on additional [collision exclusion mask](#setExclusionMask_int_void).
### Arguments

- *int* **mask** - Integer, each bit of which is a mask.

## int getCollisionMask ( )

Returns the collision mask of the actor. Two objects collide if they both have matching masks.See also details on additional [collision exclusion mask](#getExclusionMask_int).
### Return value

Integer, each bit of which is a mask.
## void setContinuous ( int continuous )

Enables or disables continuous collision detection for [spheres](../../../api/library/physics/class.shapesphere_usc.md) or [capsules](../../../api/library/physics/class.shapecapsule_usc.md). Enabled CDD incurs almost no performance penalty. Disabling CCD allows to avoid physics artifacts, if there are any.
### Arguments

- *int* **continuous** - Positive value to enable CCD; **0** to disable.

## int isContinuous ( )

Returns a value indicating if continuous collision detection for [spheres](../../../api/library/physics/class.shapesphere_usc.md) or [capsules](../../../api/library/physics/class.shapecapsule_usc.md) is enabled. Enabled CCD incurs almost no performance penalty. Disabling CCD allows to avoid physics artifacts, if there are any.
### Return value

**1** if CCD is enabled; otherwise, **0**.
## void setDensity ( float density )

Sets density of a shape. Changing the density influences the mass, that is computed by multiplying shape volume by density.
### Arguments

- *float* **density** - Density value. If a negative value is provided, **0** will be used instead.

## float getDensity ( )

Returns the current density of a shape.
### Return value

Density value.
## void setEnabled ( int enable )

Enables or disables physical interactions with the shape.
### Arguments

- *int* **enable** - Positive number to enable physical interactions, **0** to disable them.

## int isEnabled ( )

Returns a value indicating if physical interactions with the shape are enabled.
### Return value

**1** if physical interactions with the shape are enabled; otherwise, **0**.
## int isEnabledSelf ( )

Returns a value indicating if the shape is enabled.
### Return value

**1** if the shape is enabled; otherwise, **0**.
## void setExclusionMask ( int mask )

Sets an bit mask to prevent collisions of the shape with other ones. This mask is independent of the [collision mask](#setCollisionMask_int_void). For shapes with matching collision masks not to collide, at least one bit of their exclusion mask should match.
### Arguments

- *int* **mask** - Integer, each bit of which is a mask.

## int getExclusionMask ( )

Returns the bit mask that prevents collisions of the shape with other ones. This mask is independent of the [collision mask](#getCollisionMask_int). For shape with matching collision masks not to collide, at least one bit of their exclusion mask should match.
### Return value

Integer, each bit of which is a mask.
## void setFriction ( float friction )

Sets a friction coefficient for the shape surface.
### Arguments

- *float* **friction** - Friction coefficient for the shape surface. If a negative value is provided, **0** will be used instead.

## float getFriction ( )

Returns the friction coefficient for the shape surface.
### Return value

Friction coefficient for the shape surface.
## void setID ( int id )

Sets the unique ID for the shape.
### Arguments

- *int* **id** - Unique ID.

## int getID ( )

Returns the unique ID of the shape.
### Return value

Unique ID.
## mat3 getInertia ( )

Returns a matrix that represents inertia tensor describing the resistance of the body to rotation in different directions. It is determined by the distribution of mass throughout the body volume.
### Return value

Inertia tensor.
## int getIntersection ( Vec3 p0 , Vec3 p1 , PhysicsIntersectionNormal intersection )


Performs tracing from the p0 point to the p1 point to find a shape intersected by this line. Intersection is found only for objects with a matching intersection mask.


> **Notice:** World space coordinates are used for this function.


### Arguments

- *Vec3* **p0** - Start point of the line.
- *Vec3* **p1** - End point of the line.
- *[PhysicsIntersectionNormal](../../../api/library/physics/class.physicsintersectionnormal_usc.md)* **intersection** - [PhysicsIntersectionNormal](../../../api/library/physics/class.physicsintersectionnormal_usc.md) class instance containing intersection information

### Return value

1 if an intersection was detected; otherwise - 0.
## int getIntersection ( Vec3 p0 , Vec3 p1 , PhysicsIntersection intersection )


Performs tracing from the p0 point to the p1 point to find a shape intersected by this line. Intersection is found only for objects with a matching intersection mask.


> **Notice:** World space coordinates are used for this function.


**Usage Example**


The following example shows how you can get the intersection information by using the PhysicsIntersection class. In this example the line is an invisible traced line from the point of the camera (vec3 p0) to the point of the mouse pointer (vec3 p1). It is supposed that you have a shape in your world. The executing sequence is the following:

- Define and initialize two points (p0 and p1) by using the *getPlayerMouseDirection()* function from `core/scripts/utils.h`.
- Create an instance of the PhysicsIntersection class to get the information of the intersection point.
- Check, if there is a intersection with a shape and save the result in the integer variable.
- In this example, if there is an intersection of mouse direction with a specific shape called "shape", the PhysicsIntersection class instance gets the and intersection point and show the result in console.


```cpp
#include <core/scripts/utils.h>
/* ... */
// define two vec3 coordinates
vec3 p0,p1;
// get the mouse direction from camera (p0) to cursor pointer (p1)
getPlayerMouseDirection(p0,p1);

// create the instance of the PhysicsIntersection object to save the information about the intersection
PhysicsIntersection intersection = new PhysicsIntersection();
// create an int variable to check the result of intersection
int result;
result = shape2.getIntersection(p0, p1, intersection);
// if there was an intersection, show the message in console
if(result != 0)
{
	log.message("intersection point: %s \n", typeinfo(intersection.getPoint()) );
}
/* ... */

```


### Arguments

- *Vec3* **p0** - Start point of the line.
- *Vec3* **p1** - End point of the line.
- *[PhysicsIntersection](../../../api/library/physics/class.physicsintersection_usc.md)* **intersection** - [PhysicsIntersection](../../../api/library/physics/class.physicsintersection_usc.md) class instance containing intersection information.

### Return value

1 if an intersection was detected; otherwise - 0.
## int getIntersection ( Vec3 p0 , Vec3 p1 , variable v )


Performs tracing from the p0 point to the p1 point to find a shape intersected by this line. Intersection is found only for objects with a matching intersection mask.


> **Notice:** World space coordinates are used for this function.


### Arguments

- *Vec3* **p0** - Start point of the line (in world coordinates).
- *Vec3* **p1** - End point of the line (in world coordinates).
- *variable* **v** - Variable defining which type of intersection object will be returned:

  - PhysicsIntersection intersection — [PhysicsIntersection](../../../api/library/physics/class.physicsintersection_usc.md) class instance containing intersection information (contact point coordinates).
  - PhysicsIntersectionNormal normal — [PhysicsIntersectionNormal](../../../api/library/physics/class.physicsintersectionnormal_usc.md) class instance containing intersection information (contact point and normal coordinates).

### Return value

1 if an intersection was detected; otherwise - 0.
## void setPhysicsIntersectionMask ( int mask )

Sets a [physics intersection mask](../../../principles/bit_masking/index.md#physics_intersection_mask) for the shape.
### Arguments

- *int* **mask** - Integer, each bit of which is a mask.

## int getPhysicsIntersectionMask ( )

Returns a [physics intersection mask](../../../principles/bit_masking/index.md#physics_intersection_mask) of the shape.
### Return value

Integer, each bit of which is a mask.
## void setMass ( float mass )

Sets a mass of the shape. Changing the mass influences the density, that is computed by dividing the mass by shape volume.
> **Notice:** If *g* (Earth's gravity) equals to 9.8 m/s 2, and 1 unit equals to 1 m, a shape with mass value of **1** weighs 1 kg.


### Arguments

- *float* **mass** - Mass of the shape. If a negative value is provided, **0** will be used instead.

## float getMass ( )

Returns the mass of the shape.
> **Notice:** If *g* (Earth's gravity) equals to 9.8 m/s 2, and 1 unit equals to 1 m, the mass is measured in kilograms.


### Return value

Mass of the shape.
## void setName ( string name )

Sets the name of the shape.
### Arguments

- *string* **name** - Name of the shape.

## string getName ( )

Returns the name of the shape.
### Return value

Name of the shape.
## int getNumber ( )

Returns the number of shape instances.
### Return value

Number of shape instances.
## void setRestitution ( float restitution )

Sets a restitution of the shape surface.
### Arguments

- *float* **restitution** - Restitution of the shape surface. The provided value will be saturated in the range **[0; 1]**.

## float getRestitution ( )

Returns the restitution of the shape surface.
### Return value

Restitution of the shape surface.
## void setPosition ( Vec3 position )

Sets shape position. This method resets shape's [velocity](#setVelocity_vec3_float_void) to 0.
> **Notice:** This method should be called only from the object owning this shape. If the shape is owned by the body, it is highly recommended to use the [setShapeTransform()](../../../api/library/physics/class.body_usc.md#setShapeTransform_int_mat4_void) method of the owning body.


### Arguments

- *Vec3* **position** - New shape's position, in world coordinates.

## Vec3 getPosition ( )

Returns the current shape position of the object, in world coordinates.
### Return value

Current shape's position, in world coordinates.
## int isIdentity ( )

Returns a value indicating if the shape has a scale equal to 1 and no rotation.
### Return value

**1** if the shape has a scale equal to 1 and no rotation; otherwise, **0**.
## void setTransform ( Mat4 transform )

Sets a transformation matrix for the shape of the object (in world coordinates). This matrix describes position and orientation of the shape. This method resets shape's linear velocity to **0**.
> **Notice:** This method should be called only from the object owning this shape. If the shape is owned by the body, it is highly recommended to use the [setShapeTransform()](../../../api/library/physics/class.body_usc.md#setShapeTransform_int_mat4_void) method of the owning body.


### Arguments

- *Mat4* **transform** - Transformation matrix

## Mat4 getTransform ( )

Returns the transformation matrix of the shape of the object (in world coordinates). This matrix describes position and orientation of the shape.
### Return value

Transformation matrix
## int getType ( )

Returns the type of the shape.
### Return value

One of the *SHAPE_** pre-defined variables.
## string getTypeName ( )

Returns the name of the shape type.
### Return value

Shape type name.
## string getTypeName ( int type )

Returns the name of a shape type with a given ID.
### Arguments

- *int* **type** - Shape type ID. One of the *[SHAPE_*](#SHAPE_BOX)* values.

### Return value

Shape type name.
## void setVelocity ( vec3 velocity , float ifps )

Sets a new velocity vector for the shape.
### Arguments

- *vec3* **velocity** - Velocity vector, each component represents shape's velocity along the corresponding axis, in units per second.
- *float* **ifps** - Inverse FPS value.

## vec3 getVelocity ( )

Returns the current velocity vector of the shape.
### Return value

Current velocity vector, each component represents shape's velocity along the corresponding axis, in units per second.
## float getVolume ( )

Returns the volume of the shape.
### Return value

Volume of the shape in cubic units.
## Shape clone ( )

Clones the shape.
### Return value

Copy of the shape.
## void renderVisualizer ( vec4 color )

Renders the shape.
> **Notice:** You should enable the engine visualizer by the **show_visualizer 1** console command.


### Arguments

- *vec4* **color** - Color, in which the shape will be rendered.

## int saveState ( Stream stream )

Saves the state of a given node into a binary stream.
- If a node is a parent for other nodes, states of these child nodes need to be saved manually.
- To save the state from a [buffer](../../../api/library/common/class.blob_usc.md), [file](../../../api/library/filesystem/class.file_usc.md) or a message from a [socket](../../../api/library/networking/class.socket_usc.md), make sure the stream is [opened](../../../api/library/common/class.stream_usc.md#isOpened_int). For buffers and files, you also need to set the proper position for reading.


**Example** using saveState() and [restoreState()](#restoreState_Stream_int) methods:


```cpp
// set the shape state
shape.setFriction(0.8f);

// save state
Blob blob_state = new Blob();
shape.saveState(blob_state);

// change state
shape.setFriction(0.4f);

// restore state
blob_state.seekSet(0); // returning the carriage to the start of the blob
shape.restoreState(blob_state);

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
// set the shape state
shape.setFriction(0.8f);

// save state
Blob blob_state = new Blob();
shape.saveState(blob_state);

// change state
shape.setFriction(0.4f);

// restore state
blob_state.seekSet(0); // returning the carriage to the start of the blob
shape.restoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - Stream with saved node state data.

### Return value

**1** if the node state is restored successfully; otherwise, **0**.
## void swap ( Shape shape )

Swaps the shapes saving the pointers.
### Arguments

- *[Shape](../../../api/library/physics/class.shape_usc.md)* **shape** - A shape to swap.

## Shape createShape ( int type )

Creates a new shape of the specified type.
### Arguments

- *int* **type** - Body type. One of the [SHAPE_*](#SHAPE_BOX) values.

### Return value

New created shape instance.
## Shape createShape ( string type_name )

Creates a new shape of the specified type.
### Arguments

- *string* **type_name** - Shape type name.

### Return value

New created shape instance.
## int getTypeID ( string type )

### Arguments

- *string* **type**

## WorldBoundBox getBoundBox ( )

## WorldBoundSphere getBoundSphere ( )
