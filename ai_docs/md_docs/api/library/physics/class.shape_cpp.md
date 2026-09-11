# Unigine::Shape Class (CPP)

**Header:** #include <UniginePhysics.h>


This class creates collision shapes that approximate the finite volume of physical [bodies](../../../api/library/physics/class.body_cpp.md) and allow them to collide. Shapes are [assigned to a body](#setBody_Body_void) and are [positioned](../../../api/library/physics/class.body_cpp.md#setShapeTransform_int_mat4_void) in its local coordinates.


### See Also


- [Enabling Selective Surface-Based Collision](../../../code/usage/enabling_collision/index_cpp.md) usage example demonstrating how to apply the collision mask
- *[Collision Shapes](../../../code/uniginescript/samples/collision_shapes.md)* section of UnigineScript samples


## Shape Class

### Enums

## TYPE

Types of collision shapes.
| Name | Description |
|---|---|
| **SHAPE_SPHERE** = 0 | Sphere. |
| **SHAPE_CAPSULE** = 1 | Capsule. |
| **SHAPE_CYLINDER** = 2 | Cylinder. |
| **SHAPE_BOX** = 3 | Box. |
| **SHAPE_CONVEX** = 4 | Convex hull. |
| **NUM_SHAPES** = 5 | Number of shape types for the *Particles Field Spacer*. |

### Members

## bool isIdentity () const

Returns the current value indicating if the shape has an identity transformation matrix (scale equal to 1 and no rotation).
### Return value

**true** if the shape has an identity transformation matrix (a scale equal to 1 and no rotation); otherwise **false**.
## void setBodyShapeTransform ( const Math:: mat4 & transform )

Sets a new transformation matrix of the shape (in the coordinates of the body). This matrix describes position and orientation of the shape. It is identical to *[Body.getShapeTransform()](../../../api/library/physics/class.body_cpp.md#getShapeTransform_int_mat4)*.
### Arguments

- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md)&* **transform** - The transformation matrix of the shape, in the coordinates of the body

## Math:: mat4 getBodyShapeTransform () const

Returns the current transformation matrix of the shape (in the coordinates of the body). This matrix describes position and orientation of the shape. It is identical to *[Body.getShapeTransform()](../../../api/library/physics/class.body_cpp.md#getShapeTransform_int_mat4)*.
### Return value

Current transformation matrix of the shape, in the coordinates of the body
## void setTransform ( const Math:: Mat4 & transform )

Sets a new transformation matrix of the shape (in world coordinates). This matrix describes position and orientation of the shape.
### Arguments

- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md)&* **transform** - The transformation matrix of the shape, in world coordinates

## Math:: Mat4 getTransform () const

Returns the current transformation matrix of the shape (in world coordinates). This matrix describes position and orientation of the shape.
### Return value

Current transformation matrix of the shape, in world coordinates
## Math:: vec3 getCenterOfMass () const

Returns the current local coordinates of the center of mass of the shape.
### Return value

Current local coordinates of the center of mass of the shape
## Math:: mat3 getInertia () const

Returns the current matrix that represents inertia tensor describing the resistance of the body to rotation in different directions. It is determined by the distribution of mass throughout the body volume.
### Return value

Current matrix that represents inertia tensor describing the resistance of the body to rotation in different directions
## float getVolume () const

Returns the current volume of the shape.
### Return value

Current volume of the shape
## Math:: vec3 getArea () const

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
## void setName ( const char * name )

Sets a new name of the shape.
### Arguments

- *const char ** **name** - The name of the shape

## const char * getName () const

Returns the current name of the shape.
### Return value

Current name of the shape
## void setContinuous ( bool continuous )

Sets a new value indicating if continuous collision detection is enabled. Enabled CCD incurs almost no performance penalty. Disabling CCD allows to avoid physics artifacts, if there are any. Is enabled for [spheres](../../../api/library/physics/class.shapesphere_cpp.md) or [capsules](../../../api/library/physics/class.shapecapsule_cpp.md) by default. For other shape types, it must be enabled manually.
### Arguments

- *bool* **continuous** - Set **true** to enable continuous collision detection; **false** - to disable it.

## bool isContinuous () const

Returns the current value indicating if continuous collision detection is enabled. Enabled CCD incurs almost no performance penalty. Disabling CCD allows to avoid physics artifacts, if there are any. Is enabled for [spheres](../../../api/library/physics/class.shapesphere_cpp.md) or [capsules](../../../api/library/physics/class.shapecapsule_cpp.md) by default. For other shape types, it must be enabled manually.
### Return value

**true** if continuous collision detection is enabled ; otherwise **false**.
## bool isEnabledSelf () const

Returns the current value indicating if physical interactions with the shape itself are enabled, regardless of the state of the body the shape belongs to.
### Return value

**true** if physical interactions with the shape itself are enabled, regardless of the state of the body the shape belongs to; otherwise **false**.
## void setEnabled ( bool enabled )

Sets a new value indicating if physical interactions with the shape are enabled.
### Arguments

- *bool* **enabled** - Set **true** to enable physical interaction with the shape; **false** - to disable it.

## bool isEnabled () const

Returns the current value indicating if physical interactions with the shape are enabled.
### Return value

**true** if physical interaction with the shape is enabled ; otherwise **false**.
## void setBody ( const Ptr < Body >& body )

Sets a new body, to which the shape belongs.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Body](../../../api/library/physics/class.body_cpp.md)>&* **body** - The body, to which the shape belongs

## Ptr < Body > getBody () const

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
## Shape::TYPE getType () const

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
## Math:: vec3 getVelocity () const

Returns the current velocity vector of the shape.
### Return value

Current velocity vector of the shape
## void setPosition ( const Math:: Vec3 & position )

Sets a new shape position, in world coordinates.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md)&* **position** - The shape position, in world coordinates

## Math:: Vec3 getPosition () const

Returns the current shape position, in world coordinates.
### Return value

Current shape position, in world coordinates
---

## int getCollision ( Vector < Ptr < ShapeContact >> & OUT_contacts , float ifps ) const

Performs collision check for the shape and puts information on all contacts to the output buffer.
Collisions with the surface can be found only if the following conditions are fulfilled:


1. The surface is enabled.
2. Per-surface [Collision](../../../api/library/objects/class.object_cpp.md#setCollision_int_int_void) flag is enabled.
3. The surface has a material assigned.


> **Notice:** The shape must be [enabled](#setEnabled_int_void).


### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[ShapeContact](../../../api/library/physics/class.shapecontact_cpp.md)>> &* **OUT_contacts** - Output buffer containing information on all detected physical contacts for the shape (if any). Information on each contact can be handled via the [ShapeContact class](../../../api/library/physics/class.shapecontact_cpp.md). > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *float* **ifps** - Inverse FPS value.

### Return value

1 if collisions are found; otherwise, 0.
## int getCollision ( const Ptr < Object > & object , Vector < Ptr < ShapeContact >> & OUT_contacts , float ifps ) const

Performs collision check for the shape and puts information on all contacts and contact object to the output buffer.
Collisions with the surface can be found only if the following conditions are fulfilled:


1. The surface is enabled.
2. Per-surface [Collision](../../../api/library/objects/class.object_cpp.md#setCollision_int_int_void) flag is enabled.
3. The surface has a material assigned.


> **Notice:** The shape must be [enabled](#setEnabled_int_void).


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Object](../../../api/library/objects/class.object_cpp.md)> &* **object** - Object to be ignored when detecting collisions. This parameter is used when it is necessary to ignore collisions of the shape with the object it belongs to.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[ShapeContact](../../../api/library/physics/class.shapecontact_cpp.md)>> &* **OUT_contacts** - Output buffer containing information on all detected physical contacts for the shape (if any). Information on each contact can be handled via the [ShapeContact class](../../../api/library/physics/class.shapecontact_cpp.md). > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *float* **ifps** - Inverse FPS value.

### Return value

1 if collisions are found; otherwise, 0.
## int getIntersection ( const Math:: Vec3 & p0 , const Math:: Vec3 & p1 , const Ptr < PhysicsIntersectionNormal > & intersection ) const


Performs tracing from the p0 point to the p1 point to find a shape intersected by this line. Intersection is found only for objects with a matching intersection mask.


> **Notice:** World space coordinates are used for this function.


### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - Start point of the line.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - End point of the line.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[PhysicsIntersectionNormal](../../../api/library/physics/class.physicsintersectionnormal_cpp.md)> &* **intersection** - [PhysicsIntersectionNormal](../../../api/library/physics/class.physicsintersectionnormal_cpp.md) class instance containing intersection information

### Return value

1 if an intersection was detected; otherwise - 0.
## int getIntersection ( const Math:: Vec3 & p0 , const Math:: Vec3 & p1 , const Ptr < PhysicsIntersection > & intersection ) const


Performs tracing from the p0 point to the p1 point to find a shape intersected by this line. Intersection is found only for objects with a matching intersection mask.


> **Notice:** World space coordinates are used for this function.


**Usage Example**


The following example shows how you can get the intersection information by using the PhysicsIntersection class. In this example the line is an invisible traced line from the point of the camera (vec3 p0) to the point of the mouse pointer (vec3 p1). It is supposed that you have a dynamic mesh with a body and a shape assigned. The executing sequence is the following:

- Define and initialize two points (p0 and p1) by using the *[Player::getDirectionFromScreen()](../../../api/library/players/class.player_cpp.md#getDirectionFromScreen_Vec3_Vec3_int_int_int_int_int_int_void)* function.
- Create an instance of the PhysicsIntersection class to get the information of the intersection point.
- Check, if there is a intersection with a shape and save the result in the integer variable.
- In this example, if there is an intersection of mouse direction with a shape, the PhysicsIntersection class instance gets the intersection point. The result is shown in the console.


```cpp
// initialize points of the mouse direction
Vec3 p0, p1;

// get the current player (camera)
PlayerPtr player = Game::getPlayer();
if (player.get() == NULL)
	return 0;

// get width and height of the current application window
ivec2 main_size = ivec2_one;
EngineWindowPtr main_window = WindowManager::getMainWindow();
if (!main_window)
	Engine::get()->quit();

main_size = main_window->getSize();

// get the current X and Y coordinates of the mouse pointer
int mouse_x = Input::getMousePosition().x - main_window->getPosition().x;
int mouse_y = Input::getMousePosition().y - main_window->getPosition().y;

// get the mouse direction from the player's position (p0) to the mouse cursor pointer (p1)
player->getDirectionFromScreen(p0, p1, 0, 0, mouse_x, mouse_y, main_size.x, main_size.y);

// create the instance of the PhysicsIntersection object to save the information about the intersection
PhysicsIntersectionPtr intersection = PhysicsIntersection::create();
// create an integer variable to check the result of intersection
int result = 0;
result = shape->getIntersection(p0, p1, intersection);
// if there was an intersection, show the message in console
if (result != 0)
{
	Log::message("Intersection point: (%f %f %f) \n", intersection->getPoint().x, intersection->getPoint().y, intersection->getPoint().z);
}
/* ... */


```


### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - Start point of the line.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - End point of the line.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[PhysicsIntersection](../../../api/library/physics/class.physicsintersection_cpp.md)> &* **intersection** - [PhysicsIntersection](../../../api/library/physics/class.physicsintersection_cpp.md) class instance containing intersection information.

### Return value

1 if an intersection was detected; otherwise - 0.
## int getIntersection ( const Math:: Vec3 & p0 , const Math:: Vec3 & p1 , Math:: Vec3 * OUT_ret_point , Math:: vec3 * OUT_ret_normal ) const


Performs tracing from the p0 point to the p1 point to find a shape intersected by this line. Intersection is found only for objects with a matching intersection mask.


> **Notice:** World space coordinates are used for this function.


### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - Start point of the line (in world coordinates).
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - End point of the line (in world coordinates).
- *Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) ** **OUT_ret_point** - Container to which contact point coordinates (if any) shall be put (in world coordinate system). > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md) ** **OUT_ret_normal** - Container to which contact point normal coordinates (if any) shall be put (in world coordinate system). > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

1 if an intersection was detected; otherwise - 0.
## const char * getTypeName ( int type )

Returns the name of a shape type with a given ID.
### Arguments

- *int* **type** - Shape type ID. One of the *[SHAPE_*](#SHAPE_BOX)* values.

### Return value

Shape type name.
## void setVelocity ( const Math:: vec3 & velocity , float ifps )

Sets a new velocity vector for the shape.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **velocity** - Velocity vector, each component represents shape's velocity along the corresponding axis, in units per second.
- *float* **ifps** - Inverse FPS value.

## Ptr < Shape > clone ( ) const

Clones the shape.
### Return value

Copy of the shape.
## void renderVisualizer ( const Math:: vec4 & color )

Renders the shape.
> **Notice:** You should enable the engine visualizer by the **show_visualizer 1** console command.


### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color, in which the shape will be rendered.

## bool saveState ( const Ptr < Stream > & stream ) const

Saves the state of a given node into a binary stream.
- If a node is a parent for other nodes, states of these child nodes need to be saved manually.
- To save the state from a [buffer](../../../api/library/common/class.blob_cpp.md), [file](../../../api/library/filesystem/class.file_cpp.md) or a message from a [socket](../../../api/library/networking/class.socket_cpp.md), make sure the stream is [opened](../../../api/library/common/class.stream_cpp.md#isOpened_int). For buffers and files, you also need to set the proper position for reading.


**Example** using saveState() and [restoreState()](#restoreState_Stream_int) methods:


```cpp
// set the shape state
shape->setFriction(0.8f);

// save state
BlobPtr blob_state = Blob::create();
shape->saveState(blob_state);

// change the state
shape->setFriction(0.4f);

// restore state
blob_state->seekSet(0);       // returning the carriage to the start of the blob
shape->restoreState(blob_state);


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
// set the shape state
shape->setFriction(0.8f);

// save state
BlobPtr blob_state = Blob::create();
shape->saveState(blob_state);

// change the state
shape->setFriction(0.4f);

// restore state
blob_state->seekSet(0);       // returning the carriage to the start of the blob
shape->restoreState(blob_state);


```


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream with saved node state data.

### Return value

true if the node state is restored successfully; otherwise, false.
## void swap ( const Ptr < Shape > & shape )

Swaps the shapes saving the pointers.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Shape](../../../api/library/physics/class.shape_cpp.md)> &* **shape** - A shape to swap.

## Ptr < Shape > createShape ( int type )

Creates a new shape of the specified type.
### Arguments

- *int* **type** - Body type. One of the [SHAPE_*](#SHAPE_BOX) values.

### Return value

New created shape smart pointer.
## Ptr < Shape > createShape ( const char * type_name )

Creates a new shape of the specified type.
### Arguments

- *const char ** **type_name** - Shape type name.

### Return value

New created shape smart pointer.
## Shape::TYPE getTypeID ( const char * type )

Returns the identifier of a shape type with a given name.
### Arguments

- *const char ** **type** - Shape type name.

### Return value

Shape type identifier: one of the *[SHAPE_*](#SHAPE_BOX)* values, or -1 if the type name is not recognized.
## Math:: WorldBoundBox getBoundBox ( ) const

Returns the bounding box of the shape, in world coordinates.
### Return value

[Bounding box](../../../api/library/math/bounds/class.worldboundbox_cpp.md) of the shape, in world coordinates.
## Math:: WorldBoundSphere getBoundSphere ( ) const

Returns the bounding sphere of the shape, in world coordinates.
### Return value

[Bounding sphere](../../../api/library/math/bounds/class.worldboundsphere_cpp.md) of the shape, in world coordinates.
