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

---

## Math:: vec3 getArea ( ) const

Returns areas of shape projections on three axes: *x*, *y*, and *z*.
### Return value

A triple of projection areas.
## void setBody ( const Ptr < Body > & body )

Sets a body, to which the shape belongs.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Body](../../../api/library/physics/class.body_cpp.md)> &* **body** - Body, to which the shape belongs.

## Ptr < Body > getBody ( ) const

Returns the body, to which the shape belongs.
### Return value

Body, to which the shape belongs.
## void setBodyShapeTransform ( const Math:: mat4 & transform )

Sets a transformation matrix for the shape (in the coordinates of the body). This matrix describes position and orientation of the shape. This method is identical to [setShapeTransform()](../../../api/library/physics/class.body_cpp.md#setShapeTransform_int_mat4_void).
### Arguments

- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix

## Math:: mat4 getBodyShapeTransform ( ) const

Returns the transformation matrix of the shape (in the coordinates of the body). This matrix describes position and orientation of the shape. This method is identical to [getShapeTransform()](../../../api/library/physics/class.body_cpp.md#getShapeTransform_int_mat4).
### Return value

Transformation matrix
## Math:: vec3 getCenterOfMass ( ) const

Returns local coordinates of the center of mass of the shape.
### Return value

Coordinates of the center of mass.
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
## void setCollisionMask ( int mask )

Sets a collision mask for the shape. Two objects collide if they both have matching masks. See also details on additional [collision exclusion mask](#setExclusionMask_int_void).
### Arguments

- *int* **mask** - Integer, each bit of which is a mask.

## int getCollisionMask ( ) const

Returns the collision mask of the actor. Two objects collide if they both have matching masks.See also details on additional [collision exclusion mask](#getExclusionMask_int).
### Return value

Integer, each bit of which is a mask.
## void setContinuous ( bool continuous )

Enables or disables continuous collision detection for [spheres](../../../api/library/physics/class.shapesphere_cpp.md) or [capsules](../../../api/library/physics/class.shapecapsule_cpp.md). Enabled CDD incurs almost no performance penalty. Disabling CCD allows to avoid physics artifacts, if there are any.
### Arguments

- *bool* **continuous** - Positive value to enable CCD; **0** to disable.

## bool isContinuous ( ) const

Returns a value indicating if continuous collision detection for [spheres](../../../api/library/physics/class.shapesphere_cpp.md) or [capsules](../../../api/library/physics/class.shapecapsule_cpp.md) is enabled. Enabled CCD incurs almost no performance penalty. Disabling CCD allows to avoid physics artifacts, if there are any.
### Return value

**1** if CCD is enabled; otherwise, **0**.
## void setDensity ( float density )

Sets density of a shape. Changing the density influences the mass, that is computed by multiplying shape volume by density.
### Arguments

- *float* **density** - Density value. If a negative value is provided, **0** will be used instead.

## float getDensity ( ) const

Returns the current density of a shape.
### Return value

Density value.
## void setEnabled ( bool enable )

Enables or disables physical interactions with the shape.
### Arguments

- *bool* **enable** - Positive number to enable physical interactions, **0** to disable them.

## bool isEnabled ( ) const

Returns a value indicating if physical interactions with the shape are enabled.
### Return value

true if physical interactions with the shape are enabled; otherwise, false.
## bool isEnabledSelf ( ) const

Returns a value indicating if the shape is enabled.
### Return value

true if the shape is enabled; otherwise, false.
## void setExclusionMask ( int mask )

Sets an bit mask to prevent collisions of the shape with other ones. This mask is independent of the [collision mask](#setCollisionMask_int_void). For shapes with matching collision masks not to collide, at least one bit of their exclusion mask should match.
### Arguments

- *int* **mask** - Integer, each bit of which is a mask.

## int getExclusionMask ( ) const

Returns the bit mask that prevents collisions of the shape with other ones. This mask is independent of the [collision mask](#getCollisionMask_int). For shape with matching collision masks not to collide, at least one bit of their exclusion mask should match.
### Return value

Integer, each bit of which is a mask.
## void setFriction ( float friction )

Sets a friction coefficient for the shape surface.
### Arguments

- *float* **friction** - Friction coefficient for the shape surface. If a negative value is provided, **0** will be used instead.

## float getFriction ( ) const

Returns the friction coefficient for the shape surface.
### Return value

Friction coefficient for the shape surface.
## void setID ( int id )

Sets the unique ID for the shape.
### Arguments

- *int* **id** - Unique ID.

## int getID ( ) const

Returns the unique ID of the shape.
### Return value

Unique ID.
## Math:: mat3 getInertia ( ) const

Returns a matrix that represents inertia tensor describing the resistance of the body to rotation in different directions. It is determined by the distribution of mass throughout the body volume.
### Return value

Inertia tensor.
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
## void setPhysicsIntersectionMask ( int mask )

Sets a [physics intersection mask](../../../principles/bit_masking/index.md#physics_intersection_mask) for the shape.
### Arguments

- *int* **mask** - Integer, each bit of which is a mask.

## int getPhysicsIntersectionMask ( ) const

Returns a [physics intersection mask](../../../principles/bit_masking/index.md#physics_intersection_mask) of the shape.
### Return value

Integer, each bit of which is a mask.
## void setMass ( float mass )

Sets a mass of the shape. Changing the mass influences the density, that is computed by dividing the mass by shape volume.
> **Notice:** If *g* (Earth's gravity) equals to 9.8 m/s 2, and 1 unit equals to 1 m, a shape with mass value of **1** weighs 1 kg.


### Arguments

- *float* **mass** - Mass of the shape. If a negative value is provided, **0** will be used instead.

## float getMass ( ) const

Returns the mass of the shape.
> **Notice:** If *g* (Earth's gravity) equals to 9.8 m/s 2, and 1 unit equals to 1 m, the mass is measured in kilograms.


### Return value

Mass of the shape.
## void setName ( const char * name )

Sets the name of the shape.
### Arguments

- *const char ** **name** - Name of the shape.

## const char * getName ( ) const

Returns the name of the shape.
### Return value

Name of the shape.
## int getNumber ( ) const

Returns the number of shape instances.
### Return value

Number of shape instances.
## void setRestitution ( float restitution )

Sets a restitution of the shape surface.
### Arguments

- *float* **restitution** - Restitution of the shape surface. The provided value will be saturated in the range **[0; 1]**.

## float getRestitution ( ) const

Returns the restitution of the shape surface.
### Return value

Restitution of the shape surface.
## void setPosition ( const Math:: Vec3 & position )

Sets shape position. This method resets shape's [velocity](#setVelocity_vec3_float_void) to 0.
> **Notice:** This method should be called only from the object owning this shape. If the shape is owned by the body, it is highly recommended to use the [setShapeTransform()](../../../api/library/physics/class.body_cpp.md#setShapeTransform_int_mat4_void) method of the owning body.


### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **position** - New shape's position, in world coordinates.

## Math:: Vec3 getPosition ( ) const

Returns the current shape position of the object, in world coordinates.
### Return value

Current shape's position, in world coordinates.
## bool isIdentity ( ) const

Returns a value indicating if the shape has a scale equal to 1 and no rotation.
### Return value

**1** if the shape has a scale equal to 1 and no rotation; otherwise, **0**.
## void setTransform ( const Math:: Mat4 & transform )

Sets a transformation matrix for the shape of the object (in world coordinates). This matrix describes position and orientation of the shape. This method resets shape's linear velocity to **0**.
> **Notice:** This method should be called only from the object owning this shape. If the shape is owned by the body, it is highly recommended to use the [setShapeTransform()](../../../api/library/physics/class.body_cpp.md#setShapeTransform_int_mat4_void) method of the owning body.


### Arguments

- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix

## Math:: Mat4 getTransform ( ) const

Returns the transformation matrix of the shape of the object (in world coordinates). This matrix describes position and orientation of the shape.
### Return value

Transformation matrix
## Shape::TYPE getType ( ) const

Returns the type of the shape.
### Return value

One of the *SHAPE_** pre-defined variables.
## const char * getTypeName ( ) const

Returns the name of the shape type.
### Return value

Shape type name.
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

## Math:: vec3 getVelocity ( ) const

Returns the current velocity vector of the shape.
### Return value

Current velocity vector, each component represents shape's velocity along the corresponding axis, in units per second.
## float getVolume ( ) const

Returns the volume of the shape.
### Return value

Volume of the shape in cubic units.
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

### Arguments

- *const char ** **type**

## Math:: WorldBoundBox getBoundBox ( ) const

## Math:: WorldBoundSphere getBoundSphere ( ) const
