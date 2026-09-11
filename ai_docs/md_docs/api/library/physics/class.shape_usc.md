# Unigine::Shape Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class creates collision shapes that approximate the finite volume of physical [bodies](../../../api/library/physics/class.body_usc.md) and allow them to collide. Shapes are [assigned to a body](#setBody_Body_void) and are [positioned](../../../api/library/physics/class.body_usc.md#setShapeTransform_int_mat4_void) in its local coordinates.


### See Also


- [Enabling Selective Surface-Based Collision](../../../code/usage/enabling_collision/index_usc.md) usage example demonstrating how to apply the collision mask
- *[Collision Shapes](../../../code/uniginescript/samples/collision_shapes.md)* section of UnigineScript samples


## Shape Class

### Members

## int isIdentity () const

Returns the current value indicating if the shape has an identity transformation matrix (scale equal to 1 and no rotation).
### Return value

Current the shape has an identity transformation matrix (a scale equal to 1 and no rotation)
## void setBodyShapeTransform ( mat4 transform )

Sets a new transformation matrix of the shape (in the coordinates of the body). This matrix describes position and orientation of the shape. It is identical to *[Body.getShapeTransform()](../../../api/library/physics/class.body_usc.md#getShapeTransform_int_mat4)*.
### Arguments

- *mat4* **transform** - The transformation matrix of the shape, in the coordinates of the body

## mat4 getBodyShapeTransform () const

Returns the current transformation matrix of the shape (in the coordinates of the body). This matrix describes position and orientation of the shape. It is identical to *[Body.getShapeTransform()](../../../api/library/physics/class.body_usc.md#getShapeTransform_int_mat4)*.
### Return value

Current transformation matrix of the shape, in the coordinates of the body
## void setTransform ( Mat4 transform )

Sets a new transformation matrix of the shape (in world coordinates). This matrix describes position and orientation of the shape.
### Arguments

- *Mat4* **transform** - The transformation matrix of the shape, in world coordinates

## Mat4 getTransform () const

Returns the current transformation matrix of the shape (in world coordinates). This matrix describes position and orientation of the shape.
### Return value

Current transformation matrix of the shape, in world coordinates
## vec3 getCenterOfMass () const

Returns the current local coordinates of the center of mass of the shape.
### Return value

Current local coordinates of the center of mass of the shape
## mat3 getInertia () const

Returns the current matrix that represents inertia tensor describing the resistance of the body to rotation in different directions. It is determined by the distribution of mass throughout the body volume.
### Return value

Current matrix that represents inertia tensor describing the resistance of the body to rotation in different directions
## float getVolume () const

Returns the current volume of the shape.
### Return value

Current volume of the shape
## vec3 getArea () const

Returns the current areas of shape projections on three axes: *x*, *y*, and *z*.
### Return value

Current areas of shape projections on three axes: x, y, and z
## void setRestitution ( float restitution )

Sets a new restitution coefficient of the shape surface.
### Arguments

- *float* **restitution** - The restitution coefficient of the shape surface

## float getRestitution () const

Returns the current restitution coefficient of the shape surface.
### Return value

Current restitution coefficient of the shape surface
## void setFriction ( float friction )

Sets a new friction coefficient for the shape surface.
### Arguments

- *float* **friction** - The friction coefficient for the shape surface

## float getFriction () const

Returns the current friction coefficient for the shape surface.
### Return value

Current friction coefficient for the shape surface
## void setDensity ( float density )

Sets a new density of the shape.
### Arguments

- *float* **density** - The density of the shape

## float getDensity () const

Returns the current density of the shape.
### Return value

Current density of the shape
## void setMass ( float mass )

Sets a new mass of the shape. If *g* (Earth's gravity) equals to 9.8 m/s2, and 1 unit equals to 1 m, the mass is measured in kilograms.
### Arguments

- *float* **mass** - The mass of the shape

## float getMass () const

Returns the current mass of the shape. If *g* (Earth's gravity) equals to 9.8 m/s2, and 1 unit equals to 1 m, the mass is measured in kilograms.
### Return value

Current mass of the shape
## void setExclusionMask ( int mask )

Sets a new bit mask that prevents collisions of the shape with other ones. This mask is independent of the [collision mask](#getCollisionMask_int). For shape with matching collision masks not to collide, at least one bit of their exclusion mask should match.
### Arguments

- *int* **mask** - The bit mask that prevents collisions of the shape with other ones

## int getExclusionMask () const

Returns the current bit mask that prevents collisions of the shape with other ones. This mask is independent of the [collision mask](#getCollisionMask_int). For shape with matching collision masks not to collide, at least one bit of their exclusion mask should match.
### Return value

Current bit mask that prevents collisions of the shape with other ones
## void setCollisionMask ( int mask )

Sets a new collision mask of the shape. Two objects collide if they both have matching masks. See also details on additional [collision exclusion mask](#getExclusionMask_int).
### Arguments

- *int* **mask** - The collision mask of the shape

## int getCollisionMask () const

Returns the current collision mask of the shape. Two objects collide if they both have matching masks. See also details on additional [collision exclusion mask](#getExclusionMask_int).
### Return value

Current collision mask of the shape
## void setPhysicsIntersectionMask ( int mask )

Sets a new [physics intersection mask](../../../principles/bit_masking/index.md#physics_intersection_mask) of the shape.
### Arguments

- *int* **mask** - The physics intersection mask of the shape

## int getPhysicsIntersectionMask () const

Returns the current [physics intersection mask](../../../principles/bit_masking/index.md#physics_intersection_mask) of the shape.
### Return value

Current physics intersection mask of the shape
## void setName ( string name )

Sets a new name of the shape.
### Arguments

- *string* **name** - The name of the shape

## const char * getName () const

Returns the current name of the shape.
### Return value

Current name of the shape
## void setContinuous ( int continuous )

Sets a new value indicating if continuous collision detection is enabled. Enabled CCD incurs almost no performance penalty. Disabling CCD allows to avoid physics artifacts, if there are any. Is enabled for [spheres](../../../api/library/physics/class.shapesphere_usc.md) or [capsules](../../../api/library/physics/class.shapecapsule_usc.md) by default. For other shape types, it must be enabled manually.
### Arguments

- *int* **continuous** - The continuous collision detection

## int isContinuous () const

Returns the current value indicating if continuous collision detection is enabled. Enabled CCD incurs almost no performance penalty. Disabling CCD allows to avoid physics artifacts, if there are any. Is enabled for [spheres](../../../api/library/physics/class.shapesphere_usc.md) or [capsules](../../../api/library/physics/class.shapecapsule_usc.md) by default. For other shape types, it must be enabled manually.
### Return value

Current continuous collision detection
## int isEnabledSelf () const

Returns the current value indicating if physical interactions with the shape itself are enabled, regardless of the state of the body the shape belongs to.
### Return value

Current physical interactions with the shape itself are enabled, regardless of the state of the body the shape belongs to
## void setEnabled ( int enabled )

Sets a new value indicating if physical interactions with the shape are enabled.
### Arguments

- *int* **enabled** - The physical interaction with the shape

## int isEnabled () const

Returns the current value indicating if physical interactions with the shape are enabled.
### Return value

Current physical interaction with the shape
## void setBody ( Body body )

Sets a new body, to which the shape belongs.
### Arguments

- *[Body](../../../api/library/physics/class.body_usc.md)* **body** - The body, to which the shape belongs

## Body getBody () const

Returns the current body, to which the shape belongs.
### Return value

Current body, to which the shape belongs
## int getNumber () const

Returns the current number of shape instances.
### Return value

Current number of shape instances
## const char * getTypeName () const

Returns the current name of the shape type.
### Return value

Current name of the shape type
## int getType () const

Returns the current type of the shape.
### Return value

Current type of the shape
## void setID ( int id )

Sets a new unique id of the shape.
### Arguments

- *int* **id** - The unique id of the shape

## int getID () const

Returns the current unique id of the shape.
### Return value

Current unique id of the shape
## vec3 getVelocity () const

Returns the current velocity vector of the shape.
### Return value

Current velocity vector of the shape
## void setPosition ( Vec3 position )

Sets a new shape position, in world coordinates.
### Arguments

- *Vec3* **position** - The shape position, in world coordinates

## Vec3 getPosition () const

Returns the current shape position, in world coordinates.
### Return value

Current shape position, in world coordinates
---

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

  - PhysicsIntersection intersection � [PhysicsIntersection](../../../api/library/physics/class.physicsintersection_usc.md) class instance containing intersection information (contact point coordinates).
  - PhysicsIntersectionNormal normal � [PhysicsIntersectionNormal](../../../api/library/physics/class.physicsintersectionnormal_usc.md) class instance containing intersection information (contact point and normal coordinates).

### Return value

1 if an intersection was detected; otherwise - 0.
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

Returns the identifier of a shape type with a given name.
### Arguments

- *string* **type** - Shape type name.

### Return value

Shape type identifier: one of the *[SHAPE_*](#SHAPE_BOX)* values, or -1 if the type name is not recognized.
## WorldBoundBox getBoundBox ( )

Returns the bounding box of the shape, in world coordinates.
### Return value

[Bounding box](../../../api/library/math/bounds/class.worldboundbox_usc.md) of the shape, in world coordinates.
## WorldBoundSphere getBoundSphere ( )

Returns the bounding sphere of the shape, in world coordinates.
### Return value

[Bounding sphere](../../../api/library/math/bounds/class.worldboundsphere_usc.md) of the shape, in world coordinates.
