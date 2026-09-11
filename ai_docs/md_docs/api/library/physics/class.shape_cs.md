# Unigine::Shape Class (CS)


This class creates collision shapes that approximate the finite volume of physical [bodies](../../../api/library/physics/class.body_cs.md) and allow them to collide. Shapes are [assigned to a body](#setBody_Body_void) and are [positioned](../../../api/library/physics/class.body_cs.md#setShapeTransform_int_mat4_void) in its local coordinates.


### See Also


- [Enabling Selective Surface-Based Collision](../../../code/usage/enabling_collision/index_cs.md) usage example demonstrating how to apply the collision mask
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

### Properties

## 🔒︎ bool IsIdentity

The value indicating if the shape has an identity transformation matrix (scale equal to 1 and no rotation).
## mat4 BodyShapeTransform

The transformation matrix of the shape (in the coordinates of the body). This matrix describes position and orientation of the shape. It is identical to *[Body.getShapeTransform()](../../../api/library/physics/class.body_cs.md#getShapeTransform_int_mat4)*.
## mat4 Transform

The transformation matrix of the shape (in world coordinates). This matrix describes position and orientation of the shape.
## 🔒︎ vec3 CenterOfMass

The local coordinates of the center of mass of the shape.
## 🔒︎ mat3 Inertia

The matrix that represents inertia tensor describing the resistance of the body to rotation in different directions. It is determined by the distribution of mass throughout the body volume.
## 🔒︎ float Volume

The volume of the shape.
## 🔒︎ vec3 Area

The areas of shape projections on three axes: *x*, *y*, and *z*.
## float Restitution

The restitution coefficient of the shape surface.
## float Friction

The friction coefficient for the shape surface.
## float Density

The density of the shape.
## float Mass

The mass of the shape. If *g* (Earth's gravity) equals to 9.8 m/s2, and 1 unit equals to 1 m, the mass is measured in kilograms.
## int ExclusionMask

The bit mask that prevents collisions of the shape with other ones. This mask is independent of the [collision mask](#getCollisionMask_int). For shape with matching collision masks not to collide, at least one bit of their exclusion mask should match.
## int CollisionMask

The collision mask of the shape. Two objects collide if they both have matching masks. See also details on additional [collision exclusion mask](#getExclusionMask_int).
## int PhysicsIntersectionMask

The [physics intersection mask](../../../principles/bit_masking/index.md#physics_intersection_mask) of the shape.
## string Name

The name of the shape.
## bool Continuous

The value indicating if continuous collision detection is enabled. Enabled CCD incurs almost no performance penalty. Disabling CCD allows to avoid physics artifacts, if there are any. Is enabled for [spheres](../../../api/library/physics/class.shapesphere_cs.md) or [capsules](../../../api/library/physics/class.shapecapsule_cs.md) by default. For other shape types, it must be enabled manually.
## 🔒︎ bool IsEnabledSelf

The value indicating if physical interactions with the shape itself are enabled, regardless of the state of the body the shape belongs to.
## bool Enabled

The value indicating if physical interactions with the shape are enabled.
## Body Body

The body, to which the shape belongs.
## 🔒︎ int Number

The number of shape instances.
## 🔒︎ string TypeName

The name of the shape type.
## 🔒︎ Shape.TYPE Type

The type of the shape.
## int ID

The unique id of the shape.
## 🔒︎ vec3 Velocity

The velocity vector of the shape.
## vec3 Position

The shape position, in world coordinates.
### Members

---

## int GetCollision ( ShapeContact [] OUT_contacts , float ifps )

Performs collision check for the shape and puts information on all contacts to the output buffer.
Collisions with the surface can be found only if the following conditions are fulfilled:


1. The surface is enabled.
2. Per-surface [Collision](../../../api/library/objects/class.object_cs.md#setCollision_int_int_void) flag is enabled.
3. The surface has a material assigned.


> **Notice:** The shape must be [enabled](#setEnabled_int_void).


### Arguments

- *[ShapeContact](../../../api/library/physics/class.shapecontact_cs.md)[]* **OUT_contacts** - Output buffer containing information on all detected physical contacts for the shape (if any). Information on each contact can be handled via the [ShapeContact class](../../../api/library/physics/class.shapecontact_cs.md). > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *float* **ifps** - Inverse FPS value.

### Return value

1 if collisions are found; otherwise, 0.
## int GetCollision ( Object object , ShapeContact [] OUT_contacts , float ifps )

Performs collision check for the shape and puts information on all contacts and contact object to the output buffer.
Collisions with the surface can be found only if the following conditions are fulfilled:


1. The surface is enabled.
2. Per-surface [Collision](../../../api/library/objects/class.object_cs.md#setCollision_int_int_void) flag is enabled.
3. The surface has a material assigned.


> **Notice:** The shape must be [enabled](#setEnabled_int_void).


### Arguments

- *[Object](../../../api/library/objects/class.object_cs.md)* **object** - Object to be ignored when detecting collisions. This parameter is used when it is necessary to ignore collisions of the shape with the object it belongs to.
- *[ShapeContact](../../../api/library/physics/class.shapecontact_cs.md)[]* **OUT_contacts** - Output buffer containing information on all detected physical contacts for the shape (if any). Information on each contact can be handled via the [ShapeContact class](../../../api/library/physics/class.shapecontact_cs.md). > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *float* **ifps** - Inverse FPS value.

### Return value

1 if collisions are found; otherwise, 0.
## int GetIntersection ( vec3 p0 , vec3 p1 , PhysicsIntersectionNormal intersection )


Performs tracing from the p0 point to the p1 point to find a shape intersected by this line. Intersection is found only for objects with a matching intersection mask.


> **Notice:** World space coordinates are used for this function.


### Arguments

- *vec3* **p0** - Start point of the line.
- *vec3* **p1** - End point of the line.
- *[PhysicsIntersectionNormal](../../../api/library/physics/class.physicsintersectionnormal_cs.md)* **intersection** - [PhysicsIntersectionNormal](../../../api/library/physics/class.physicsintersectionnormal_cs.md) class instance containing intersection information

### Return value

1 if an intersection was detected; otherwise - 0.
## int GetIntersection ( vec3 p0 , vec3 p1 , PhysicsIntersection intersection )


Performs tracing from the p0 point to the p1 point to find a shape intersected by this line. Intersection is found only for objects with a matching intersection mask.


> **Notice:** World space coordinates are used for this function.


**Usage Example**


The following example shows how you can get the intersection information by using the PhysicsIntersection class. In this example the line is an invisible traced line from the point of the camera (vec3 p0) to the point of the mouse pointer (vec3 p1). It is supposed that you have a dynamic mesh with a body and a shape assigned. The executing sequence is the following:

- Define and initialize two points (p0 and p1) by using the *[Player.getDirectionFromScreen()](../../../api/library/players/class.player_cs.md#getDirectionFromScreen_Vec3_Vec3_int_int_int_int_int_int_void)* function.
- Create an instance of the PhysicsIntersection class to get the information of the intersection point.
- Check, if there is a intersection with a shape and save the result in the integer variable.
- In this example, if there is an intersection of mouse direction with a shape, the PhysicsIntersection class instance gets the intersection point. The result is shown in the console.


```csharp
/* ... */
// initialize points of the mouse direction
Vec3 p0, p1;

// get the current player (camera)
Player player = Game.Player;
if (player == null)
	return;

// get size (width and height) of the current application window
EngineWindow main_window = WindowManager.MainWindow;
if (!main_window)
	Engine.Quit();

ivec2 main_size = main_window.Size;

// get the current X and Y coordinates of the mouse pointer
int mouse_x = Input.MousePosition.x - main_window.Position.x;
int mouse_y = Input.MousePosition.y - main_window.Position.y;

// get the mouse direction from the player's position (p0) to the mouse cursor pointer (p1)
player.GetDirectionFromScreen(out p0, out p1, 0, 0, mouse_x, mouse_y, main_size.x, main_size.y);

// create the instance of the PhysicsIntersection object to save the information about the intersection
PhysicsIntersection intersection = new PhysicsIntersection();
// create an integer variable to check the result of intersection
int result = 0;
result = shape.GetIntersection(p0, p1, intersection);
// if there was an intersection, show the message in console
if (result != 0)
{
	Log.Message("Intersection point: ({0} {1} {2}) \n", intersection.Point.x, intersection.Point.y, intersection.Point.z);
}
/* ... */


```


### Arguments

- *vec3* **p0** - Start point of the line.
- *vec3* **p1** - End point of the line.
- *[PhysicsIntersection](../../../api/library/physics/class.physicsintersection_cs.md)* **intersection** - [PhysicsIntersection](../../../api/library/physics/class.physicsintersection_cs.md) class instance containing intersection information.

### Return value

1 if an intersection was detected; otherwise - 0.
## int GetIntersection ( vec3 p0 , vec3 p1 , vec3[] OUT_ret_point , vec3[] OUT_ret_normal )


Performs tracing from the p0 point to the p1 point to find a shape intersected by this line. Intersection is found only for objects with a matching intersection mask.


> **Notice:** World space coordinates are used for this function.


### Arguments

- *vec3* **p0** - Start point of the line (in world coordinates).
- *vec3* **p1** - End point of the line (in world coordinates).
- *vec3[]* **OUT_ret_point** - Container to which contact point coordinates (if any) shall be put (in world coordinate system). > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *vec3[]* **OUT_ret_normal** - Container to which contact point normal coordinates (if any) shall be put (in world coordinate system). > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

1 if an intersection was detected; otherwise - 0.
## string GetTypeName ( int type )

Returns the name of a shape type with a given ID.
### Arguments

- *int* **type** - Shape type ID. One of the *[SHAPE_*](#SHAPE_BOX)* values.

### Return value

Shape type name.
## void SetVelocity ( vec3 velocity , float ifps )

Sets a new velocity vector for the shape.
### Arguments

- *vec3* **velocity** - Velocity vector, each component represents shape's velocity along the corresponding axis, in units per second.
- *float* **ifps** - Inverse FPS value.

## Shape Clone ( )

Clones the shape.
### Return value

Copy of the shape.
## void RenderVisualizer ( vec4 color )

Renders the shape.
> **Notice:** You should enable the engine visualizer by the **show_visualizer 1** console command.


### Arguments

- *vec4* **color** - Color, in which the shape will be rendered.

## bool SaveState ( Stream stream )

Saves the state of a given node into a binary stream.
- If a node is a parent for other nodes, states of these child nodes need to be saved manually.
- To save the state from a [buffer](../../../api/library/common/class.blob_cs.md), [file](../../../api/library/filesystem/class.file_cs.md) or a message from a [socket](../../../api/library/networking/class.socket_cs.md), make sure the stream is [opened](../../../api/library/common/class.stream_cs.md#isOpened_int). For buffers and files, you also need to set the proper position for reading.


**Example** using saveState() and [restoreState()](#restoreState_Stream_int) methods:


```csharp
// set the shape state
shape.Friction = 0.8f;

// save state
Blob blob_state = new Blob();
shape.SaveState(blob_state);

// change the state
shape.Friction = 0.4f;

// restore state
blob_state.SeekSet(0);        // returning the carriage to the start of the blob
shape.RestoreState(blob_state);


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
// set the shape state
shape.Friction = 0.8f;

// save state
Blob blob_state = new Blob();
shape.SaveState(blob_state);

// change the state
shape.Friction = 0.4f;

// restore state
blob_state.SeekSet(0);        // returning the carriage to the start of the blob
shape.RestoreState(blob_state);


```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream with saved node state data.

### Return value

true if the node state is restored successfully; otherwise, false.
## void Swap ( Shape shape )

Swaps the shapes saving the pointers.
### Arguments

- *[Shape](../../../api/library/physics/class.shape_cs.md)* **shape** - A shape to swap.

## Shape CreateShape ( int type )

Creates a new shape of the specified type.
### Arguments

- *int* **type** - Body type. One of the [SHAPE_*](#SHAPE_BOX) values.

### Return value

New created shape instance.
## Shape CreateShape ( string type_name )

Creates a new shape of the specified type.
### Arguments

- *string* **type_name** - Shape type name.

### Return value

New created shape instance.
## Shape.TYPE GetTypeID ( string type )

Returns the identifier of a shape type with a given name.
### Arguments

- *string* **type** - Shape type name.

### Return value

Shape type identifier: one of the *[SHAPE_*](#SHAPE_BOX)* values, or -1 if the type name is not recognized.
## WorldBoundBox GetBoundBox ( )

Returns the bounding box of the shape, in world coordinates.
### Return value

[Bounding box](../../../api/library/math/bounds/class.worldboundbox_cs.md) of the shape, in world coordinates.
## WorldBoundSphere GetBoundSphere ( )

Returns the bounding sphere of the shape, in world coordinates.
### Return value

[Bounding sphere](../../../api/library/math/bounds/class.worldboundsphere_cs.md) of the shape, in world coordinates.
