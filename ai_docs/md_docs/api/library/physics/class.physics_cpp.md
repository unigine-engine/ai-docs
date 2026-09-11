# Unigine::Physics Class (CPP)

**Header:** #include <UniginePhysics.h>

> **Notice:** This class is a singleton.


Controls the simulation of physics. For more information on principles and implementation of physics in real-time rendering, see the articles [Execution Sequence](../../../code/fundamentals/execution_sequence/index.md), [Physics](../../../principles/physics/index.md) and [Simulation of Physics](../../../principles/physics/simulation.md).


### See Also


- The [Creating a Car with Suspension Joints](../../../code/usage/car_wheel_joints/index_cpp.md) usage example demonstrating how to set up physics parameters
- *[Physics](../../../sdk/api_samples/cpp/physics.md)* section in C++ Samples
- *[Physics](../../../sdk/api_samples/cs/physics.md)* section in C# Component Samples
- *[Physics](../../../code/uniginescript/samples/physics.md)* section in UnigineScript samples


## Physics Class

### Enums

## UPDATE_MODE

[Physics update mode](../../../principles/physics/simulation.md#update_mode).
| Name | Description |
|---|---|
| **UPDATE_MODE_BEFORE_RENDERING** = 0 | Update Before Rendering. Physics update (along with the spatial tree update and user callbacks) is executed in the Main thread just before rendering is performed (render). The number of physics ticks executed before the rendering frame here is defined by the [physics and the Engine framerates](../../../code/fundamentals/execution_sequence/index.md#cape_framerate). This mode is the most clear and straightforward (everything is executed safely in a strictly determined order) with no frame lag (results of physics calculations are applied in the current frame). But, on the other hand, this mode is the slowest as there are no asynchronous parallel calculations (everything's in the Main thread). Use this mode in case the time lag is unacceptabe for your application (you need all physics calculations to be applied in the current frame) and you want maximum simplicity and strictly determined order of execution for user code (physicsUpdate and physics callbacks). |
| **UPDATE_MODE_ASYNC_RENDERING** = 1 | Asynchronous update mode. Physics update is performed asynchronously to rendering. In case of several physics ticks per one rendering frame (when the Engine framerate is lower, or [catching up](../../../principles/physics/simulation.md#catch_up) is performed), only the first one is executed in parallel, then the physics module waits for the completion of the rendering process, returns to the Main thread and executes the rest of the physics ticks. There is a frame lag (results of physics calculations are applied in the next frame) and there is some ambiguity regarding the time, when user code (physicsUpdate and physics callbacks) is to be executed in case of several physics ticks per one rendering frame (some part is executed before rendering while the other just after it). This mode is the fastest one and is used by default. |

## SHOW_TYPE

| Name | Description |
|---|---|
| **SHOW_TYPE_DISABLED** = 0 | The helper is not visualized. |
| **SHOW_TYPE_WIREFRAME** = 1 | The helper is visualized as a wireframe. |
| **SHOW_TYPE_SOLID** = 2 | The helper is visualized as a a solid object. |

### Members

## float getTotalTime () const

Returns the current total time taken to perform all physics calculations.
### Return value

Current total physics calculation time
## float getSimulationTime () const

Returns the current duration of all of the simulation phases added together.
### Return value

Current duration of all simulation phases
## float getWaitTime () const

Returns the current Time period during which the physics module waits for the completion of rendering process.
### Return value

Current time the physics module waits for the completion stage
## int getNumJoints () const

Returns the current number of [joints](../../../principles/physics/joints/index.md) within the physics [radius](../../../editor2/settings/physics_global/index.md#physics_distance).
### Return value

Current number of joints within the physics radius
## int getNumIslands () const

Returns the current number of physical [islands](../../../principles/physics/collision/index.md#islands) within the [physics radius](../../../editor2/settings/physics_global/index.md#physics_distance) that could be calculated separately. The lower this number, the less efficient multi-threading is, if enabled.
### Return value

Current number of physical islands within the physics radius
## int getNumContacts () const

Returns the current number of contacts within the [physics radius](../../../editor2/settings/physics_global/index.md#physics_distance); it includes contacts between the bodies (their shapes) and body-mesh contacts.
### Return value

Current number of contacts within the physics radius
## int getNumBodies () const

Returns the current number of [bodies](../../../principles/physics/bodies/index.md) present within the [physics radius](../../../editor2/settings/physics_global/index.md#physics_distance).
### Return value

Current number of bodies within the physics radius
## float getCollisionTime () const

Returns the current duration of the [collision detection phase](../../../principles/physics/simulation.md#collision_detection), during which collisions between objects are found.
### Return value

Current duration of the collision detection phase
## int getFrame () const

Returns the current frame of physics update.
### Return value

Current physics update frame
## void setNumIterations ( int iterations )

Sets a new number of iterations used to solve contacts and constraints.
### Arguments

- *int* **iterations** - The number of iterations used to solve contacts and joints

## int getNumIterations () const

Returns the current number of iterations used to solve contacts and constraints.
### Return value

Current number of iterations used to solve contacts and joints
## void setNumFrozenFrames ( int frames )

Sets a new number of frames, during which an object should keep certain angular and linear velocities to become frozen.
### Arguments

- *int* **frames** - The number of frames before an object is frozen

## int getNumFrozenFrames () const

Returns the current number of frames, during which an object should keep certain angular and linear velocities to become frozen.
### Return value

Current number of frames before an object is frozen
## float getCurrentSubframeTime () const

Returns the current time that can be used when shifting between physics update frames.
### Return value

Current time used when shifting between physics subframes
## void setScale ( float scale )

Sets a new value used to scale a frame duration.
### Arguments

- *float* **scale** - The frame duration scale

## float getScale () const

Returns the current value used to scale a frame duration.
### Return value

Current frame duration scale
## void setPenetrationTolerance ( float tolerance )

Sets a new how deeply one object can penetrate another.
### Arguments

- *float* **tolerance** - The allowed penetration depth

## float getPenetrationTolerance () const

Returns the current how deeply one object can penetrate another.
### Return value

Current allowed penetration depth
## void setPenetrationFactor ( float factor )

Sets a new penalty force factor. **0** means no penalty force in contacts. The maximum value is **1**.
### Arguments

- *float* **factor** - The penalty force factor

## float getPenetrationFactor () const

Returns the current penalty force factor. **0** means no penalty force in contacts. The maximum value is **1**.
### Return value

Current penalty force factor
## void setMaxLinearVelocity ( float velocity )

Sets a new maximum possible linear velocity.
### Arguments

- *float* **velocity** - The maximum possible linear velocity

## float getMaxLinearVelocity () const

Returns the current maximum possible linear velocity.
### Return value

Current maximum possible linear velocity
## void setMaxAngularVelocity ( float velocity )

Sets a new maximum possible angular velocity.
### Arguments

- *float* **velocity** - The maximum possible angular velocity

## float getMaxAngularVelocity () const

Returns the current maximum possible angular velocity.
### Return value

Current maximum possible angular velocity
## void setLinearDamping ( float damping )

Sets a new linear damping value.
### Arguments

- *float* **damping** - The linear damping value

## float getLinearDamping () const

Returns the current linear damping value.
### Return value

Current linear damping value
## void setIFps ( float ifps )

Sets a new physics frame duration.
### Arguments

- *float* **ifps** - The physics frame duration

## float getIFps () const

Returns the current physics frame duration.
### Return value

Current physics frame duration
## void setGravity ( const Math:: vec3 & gravity )

Sets a new gravity value.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **gravity** - The gravity vector

## Math:: vec3 getGravity () const

Returns the current gravity value.
### Return value

Current gravity vector
## void setFrozenLinearVelocity ( float velocity )

Sets a new linear velocity threshold for freezing object simulation. an object stops to be updated if its linear velocity remains lower than this threshold during the number of [Frozen frames](#setNumFrozenFrames_int_void) (together with angular one).
### Arguments

- *float* **velocity** - The linear velocity threshold for freezing object simulation

## float getFrozenLinearVelocity () const

Returns the current linear velocity threshold for freezing object simulation. an object stops to be updated if its linear velocity remains lower than this threshold during the number of [Frozen frames](#setNumFrozenFrames_int_void) (together with angular one).
### Return value

Current linear velocity threshold for freezing object simulation
## void setFrozenAngularVelocity ( float velocity )

Sets a new angular velocity threshold for freezing object simulation. an object stops to be updated if its angular velocity remains lower than this threshold during the number of [Frozen frames](#setNumFrozenFrames_int_void) (together with linear one).
### Arguments

- *float* **velocity** - The angular velocity threshold for freezing object simulation

## float getFrozenAngularVelocity () const

Returns the current angular velocity threshold for freezing object simulation. an object stops to be updated if its angular velocity remains lower than this threshold during the number of [Frozen frames](#setNumFrozenFrames_int_void) (together with linear one).
### Return value

Current angular velocity threshold for freezing object simulation
## void setAngularDamping ( float damping )

Sets a new angular damping value.
### Arguments

- *float* **damping** - The angular damping value

## float getAngularDamping () const

Returns the current angular damping value.
### Return value

Current angular damping value
## void setDistance ( float distance )

Sets a new distance after which the physics will not be simulated.
### Arguments

- *float* **distance** - The distance after which physics is not simulated

## float getDistance () const

Returns the current distance after which the physics will not be simulated.
### Return value

Current distance after which physics is not simulated
## void setBudget ( float budget )

Sets a new physics simulation budget. physics isn't simulated when time is out of the budget.
### Arguments

- *float* **budget** - The physics simulation budget

## float getBudget () const

Returns the current physics simulation budget. physics isn't simulated when time is out of the budget.
### Return value

Current physics simulation budget
## void setData ( const char * data )

Sets a new user string data associated with the world. this string is written directly into the data tag of the `*.world` file.
### Arguments

- *const char ** **data** - The user string data associated with the world

## const char * getData () const

Returns the current user string data associated with the world. this string is written directly into the data tag of the `*.world` file.
### Return value

Current user string data associated with the world
## void setSyncEngineUpdateWithPhysics ( bool physics )

Sets a new flag indicating if the Engine fps is synchronized to physics one. Such fps limitation makes it possible to calculate physics each rendered frame (rather then interpolate it when this flag is unset). In this mode, there are no twitching of physical objects if they have non-linear velocities. If the Engine fps is lower than the physics one, this flag has no effect.
### Arguments

- *bool* **physics** - Set **true** to enable synchronization of the Engine FPS with physics; **false** - to disable it.

## bool isSyncEngineUpdateWithPhysics () const

Returns the current flag indicating if the Engine fps is synchronized to physics one. Such fps limitation makes it possible to calculate physics each rendered frame (rather then interpolate it when this flag is unset). In this mode, there are no twitching of physical objects if they have non-linear velocities. If the Engine fps is lower than the physics one, this flag has no effect.
### Return value

**true** if synchronization of the Engine FPS with physics is enabled ; otherwise **false**.
## void setDeterminism ( bool determinism )

Sets a new value indicating if objects are updated in a definite order or not. the default is 0 (the update order may change). Deterministic mode ensures that all contacts are solved in the predefined order and visualization of physics in the world is repetitive (on one computer). When this mode is enabled the Engine performs additional sorting of bodies, shapes and joints inside islands after building them. Deterministic mode is unavailable in case there are missed frames - it is simply impossible. Moreover, there may be differences between visualization of physics on different hardware (e.g., AMD and Intel).
> **Notice:** Determinism is guaranteed if there are no missed frames, the same Engine version is used, and the CPUs perform SSE operations similarly.
> Please note that deterministic mode does not come for free, it may eat up 10-20% of the frame rate, and it also depends on the scene a lot.

### Arguments

- *bool* **determinism** - Set **true** to enable deterministic update order; **false** - to disable it.

## bool isDeterminism () const

Returns the current value indicating if objects are updated in a definite order or not. the default is 0 (the update order may change). Deterministic mode ensures that all contacts are solved in the predefined order and visualization of physics in the world is repetitive (on one computer). When this mode is enabled the Engine performs additional sorting of bodies, shapes and joints inside islands after building them. Deterministic mode is unavailable in case there are missed frames - it is simply impossible. Moreover, there may be differences between visualization of physics on different hardware (e.g., AMD and Intel).
> **Notice:** Determinism is guaranteed if there are no missed frames, the same Engine version is used, and the CPUs perform SSE operations similarly.
> Please note that deterministic mode does not come for free, it may eat up 10-20% of the frame rate, and it also depends on the scene a lot.

### Return value

**true** if deterministic update order is enabled ; otherwise **false**.
## void setEnabled ( bool enabled )

Sets a new value indicating if physics simulation is enabled. the default is 1.
### Arguments

- *bool* **enabled** - Set **true** to enable physics simulation; **false** - to disable it.

## bool isEnabled () const

Returns the current value indicating if physics simulation is enabled. the default is 1.
### Return value

**true** if physics simulation is enabled ; otherwise **false**.
## void setMissedFrameLifetime ( float lifetime )

Sets a new lifetime for [missed frames](../../../principles/physics/simulation.md#missed_frames). This value defines how long missed frames are to be kept in the catch-up buffer. In case the current Engine framerate is lower than the [fixed Physics framerate](../../../principles/physics/simulation.md#simulation_rate), some of the physics frames get skipped and the simulation starts looking like in a slo-mo effect (e.g., if the target physics framerate is 60 FPS, when the Engine updates at 30 FPS, the simulation will look 2 times slower). The Physics module will try to catch up everything missed later, when possible (e.g. when the Engine framerate grows higher, while [waiting for GPU](../../../code/fundamentals/execution_sequence/index.md#waiting_gpu) to complete rendering). The missed frames are kept in a buffer for some time (lifetime), as it expires the frame is removed from the buffer and becomes lost forever.
### Arguments

- *float* **lifetime** - The lifetime for missed frames

## float getMissedFrameLifetime () const

Returns the current lifetime for [missed frames](../../../principles/physics/simulation.md#missed_frames). This value defines how long missed frames are to be kept in the catch-up buffer. In case the current Engine framerate is lower than the [fixed Physics framerate](../../../principles/physics/simulation.md#simulation_rate), some of the physics frames get skipped and the simulation starts looking like in a slo-mo effect (e.g., if the target physics framerate is 60 FPS, when the Engine updates at 30 FPS, the simulation will look 2 times slower). The Physics module will try to catch up everything missed later, when possible (e.g. when the Engine framerate grows higher, while [waiting for GPU](../../../code/fundamentals/execution_sequence/index.md#waiting_gpu) to complete rendering). The missed frames are kept in a buffer for some time (lifetime), as it expires the frame is removed from the buffer and becomes lost forever.
### Return value

Current lifetime for missed frames
## void setUpdateMode ( Physics::UPDATE_MODE mode )

Sets a new [physics update mode](../../../principles/physics/simulation.md#update_mode). Physics can be updated either asynchronously (in parallel with rendering) or in the Main thread before rendering. The [async](#UPDATE_MODE_ASYNC_RENDERING) mode is the fastest one and is used by default, however, it has a one-frame lag (calculation results are applied in the next frame) and some nuances regarding user code execution in some cases.
### Arguments

- *[Physics::UPDATE_MODE](../../../api/library/physics/class.physics_cpp.md#UPDATE_MODE)* **mode** - The physics update mode

## Physics::UPDATE_MODE getUpdateMode () const

Returns the current [physics update mode](../../../principles/physics/simulation.md#update_mode). Physics can be updated either asynchronously (in parallel with rendering) or in the Main thread before rendering. The [async](#UPDATE_MODE_ASYNC_RENDERING) mode is the fastest one and is used by default, however, it has a one-frame lag (calculation results are applied in the next frame) and some nuances regarding user code execution in some cases.
### Return value

Current physics update mode
## void setStableFPS ( bool fps )

Sets a new value indicating if frame time stabilization is enabled. In case the current Engine framerate is much higher than the [fixed Physics framerate](../../../principles/physics/simulation.md#simulation_rate) (e.g. 120 FPS vs 60 FPS), the physics won't be updated each rendering frame (e.g. it may update during every second frame). The resulting frame time will become unstable, shorter-longer-shorter-longer (*render -> render+physics -> render -> render+physics...*). This option ensures stable frame time for smoother user experience removing unwanted "hiccups" (however, the average framerate is decreased).
> **Notice:** By default, this option is enabled. But you can disable it to increase average framerate in case the application is used for machine learning or for grabbing frame sequences (video grabber), when smoothness is not important.

### Arguments

- *bool* **fps** - Set **true** to enable frame time stabilization; **false** - to disable it.

## bool isStableFPS () const

Returns the current value indicating if frame time stabilization is enabled. In case the current Engine framerate is much higher than the [fixed Physics framerate](../../../principles/physics/simulation.md#simulation_rate) (e.g. 120 FPS vs 60 FPS), the physics won't be updated each rendering frame (e.g. it may update during every second frame). The resulting frame time will become unstable, shorter-longer-shorter-longer (*render -> render+physics -> render -> render+physics...*). This option ensures stable frame time for smoother user experience removing unwanted "hiccups" (however, the average framerate is decreased).
> **Notice:** By default, this option is enabled. But you can disable it to increase average framerate in case the application is used for machine learning or for grabbing frame sequences (video grabber), when smoothness is not important.

### Return value

**true** if frame time stabilization is enabled ; otherwise **false**.
## void setShowContacts ( bool contacts )

Sets a new value indicating if the visualization of physical interactions between the physical bodies is enabled.
### Arguments

- *bool* **contacts** - Set **true** to enable physical contacts visualization; **false** - to disable it.

## bool isShowContacts () const

Returns the current value indicating if the visualization of physical interactions between the physical bodies is enabled.
### Return value

**true** if physical contacts visualization is enabled ; otherwise **false**.
## void setShowShapes ( Physics::SHOW_TYPE shapes )

Sets a new mode used to visualize physical shapes: one of the [SHOW_TYPE_*](#SHOW_TYPE_DISABLED) values.
### Arguments

- *[Physics::SHOW_TYPE](../../../api/library/physics/class.physics_cpp.md#SHOW_TYPE)* **shapes** - The shapes visualization mode

## Physics::SHOW_TYPE getShowShapes () const

Returns the current mode used to visualize physical shapes: one of the [SHOW_TYPE_*](#SHOW_TYPE_DISABLED) values.
### Return value

Current shapes visualization mode
## void setShowShapesDistance ( float distance )

Sets a new distance within which physical shapes are visualized.
### Arguments

- *float* **distance** - The distance within which shapes are visualized

## float getShowShapesDistance () const

Returns the current distance within which physical shapes are visualized.
### Return value

Current distance within which shapes are visualized
## void setShowCollisionSurfaces ( bool surfaces )

Sets a new value indicating if the collision surface visualization is enabled.
### Arguments

- *bool* **surfaces** - Set **true** to enable collision surface visualization; **false** - to disable it.

## bool isShowCollisionSurfaces () const

Returns the current value indicating if the collision surface visualization is enabled.
### Return value

**true** if collision surface visualization is enabled ; otherwise **false**.
## void setShowJoints ( bool joints )

Sets a new value indicating if the visualization of joints that connect physical bodies is enabled.
### Arguments

- *bool* **joints** - Set **true** to enable joints visualization; **false** - to disable it.

## bool isShowJoints () const

Returns the current value indicating if the visualization of joints that connect physical bodies is enabled.
### Return value

**true** if joints visualization is enabled ; otherwise **false**.
---

## Ptr < Body > getBody ( int id ) const

Returns a body with a given ID.
### Arguments

- *int* **id** - Body ID.

### Return value

Body with a given ID or **NULL** (0), if there is no body with a given ID.
## bool isBody ( int id ) const

Checks if a body with a given ID exists.
### Arguments

- *int* **id** - Body ID.

### Return value

true if a body with a given ID exists; otherwise, false.
## Ptr < Object > getIntersection ( const Math:: Vec3 & p0 , const Math:: Vec3 & p1 , int mask , const Vector < Ptr < Node > > & exclude , const Ptr < PhysicsIntersection > & intersection )


Performs tracing from the p0 point to the p1 point to find a collision object located on that line. If an object is assigned a body, intersection occurs with its shape. If an object has no body, this function detects intersection with surfaces (polygons) of objects with intersection flag set. Intersection is found only for objects with a matching mask if their ID is not found in the *exclude* list. Intersection does not work for disabled objects.


> **Notice:** This function uses world space coordinates.


### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - Line start point coordinates.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - Line end point coordinates.
- *int* **mask** - Physics intersection mask. If **0** is passed, the function will return **NULL**.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)> > &* **exclude** - Array of nodes to be excluded.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[PhysicsIntersection](../../../api/library/physics/class.physicsintersection_cpp.md)> &* **intersection** - [PhysicsIntersection](../../../api/library/physics/class.physicsintersection_cpp.md) class instance containing intersection data.

### Return value

The first intersected object, if found; otherwise, 0.
## Ptr < Object > getIntersection ( const Math:: Vec3 & p0 , const Math:: Vec3 & p1 , int mask , const Vector < Ptr < Node >> & exclude , const Vector < Shape::TYPE > & exclude_types , const Ptr < PhysicsIntersection > & intersection )


Performs tracing from the p0 point to the p1 point to find a collision object located on that line. If an object is assigned a body, intersection occurs with its shape. If an object has no body, this function detects intersection with surfaces (polygons) of objects with intersection flag set. Intersection is found only for objects with a matching mask if their ID is not found in the *exclude* list and only for shape types not mentioned in the *exclude_types* list. Intersection does not work for disabled objects.


> **Notice:** This function uses world space coordinates.


### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - Line start point coordinates.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - Line end point coordinates.
- *int* **mask** - Physics intersection mask. If **0** is passed, the function will return **NULL**.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>> &* **exclude** - Array of nodes to be excluded.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Shape::TYPE](../../../api/library/physics/class.shape_cpp.md#TYPE)> &* **exclude_types** - Array of shape types to be excluded.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[PhysicsIntersection](../../../api/library/physics/class.physicsintersection_cpp.md)> &* **intersection** - [PhysicsIntersection](../../../api/library/physics/class.physicsintersection_cpp.md) class instance containing intersection data.

### Return value

The first intersected object, if found; otherwise, 0.
## Ptr < Object > getIntersection ( const Math:: Vec3 & p0 , const Math:: Vec3 & p1 , int mask , const Ptr < PhysicsIntersection > & intersection )


Performs tracing from the p0 point to the p1 point to find a collision object located on that line. If an object is assigned a body, intersection occurs with its shape. If an object has no body, this function detects intersection with surfaces (polygons) of objects with intersection flag set. Physics intersection shall only be detected for objects with a matching [mask](../../../principles/bit_masking/index.md#physics_intersection_mask). Intersection does not work for disabled objects.


> **Notice:** This function uses world space coordinates.


**Usage Example**


The following example shows how you can get the intersection information by using the *PhysicsIntersection* class. In this example the line is an invisible traced line from the point of the camera *(vec3 p0)* to the point of the mouse pointer *(vec3 p1)*. The executing sequence is the following:


- Define and initialize two points (p0 and p1) by using the *[Player::getDirectionFromScreen()](../../../api/library/players/class.player_cpp.md#getDirectionFromScreen_Vec3_Vec3_int_int_int_int_int_int_void)* function.
- Create an instance of the *PhysicsIntersection* class to get the intersection information.
- Check, if there is an intersection with an object. The *[getIntersection()](#getIntersection_Vec3_Vec3_int_PhysicsIntersection_Object)* function returns an intersected object when the object intersects with the traced line.
- When the object intersects with the traced line, all the surfaces of the intersected object change their material parameters. If the object has a shape, its information will be shown in the console. The PhysicsIntersection class instance gets the coordinates of the intersection point and the *Shape* class object. You can get all these fields by using *[getShape()](../../../api/library/physics/class.physicsintersection_cpp.md#getShape_Shape), [getPoint()](../../../api/library/physics/class.physicsintersection_cpp.md#getPoint_Vec3)* functions.


```cpp
int AppWorldLogic::update()
{
	// initialize points of the mouse direction
	Vec3 p0, p1;

	// get the current player (camera)
	PlayerPtr player = Game::getPlayer();
	if (player.get() == NULL)
		return 0;
	// get width and height of the main application window
	Math::ivec2 winsize = WindowManager::getMainWindow()->getClientSize();
	int width = winsize.x;
	int height = winsize.y;
	// get the current X and Y coordinates of the mouse pointer
	int mouse_x = Gui::getCurrent()->getMouseX();
	int mouse_y = Gui::getCurrent()->getMouseY();
	// get the mouse direction from the player's position (p0) to the mouse cursor pointer (p1)
	player->getDirectionFromScreen(p0, p1, mouse_x, mouse_y, 0, 0, width, height);

	// create the instance of the PhysicsIntersection object to save the information about the intersection
	PhysicsIntersectionPtr intersection = PhysicsIntersection::create();
	// get an intersection
	ObjectPtr object = Physics::getIntersection(p0, p1, 1, intersection);

	// if the intersection has occurred, change the parameter of the object's material
	if (object)
	{
		for (int i = 0; i < object->getNumSurfaces(); i++)
		{
			object->setMaterialParameterFloat4("albedo_color", vec4(1.0f, 1.0f, 0.0f, 1.0f), i);
		}

		// if the intersected object has a shape, show the information about the intersection
		ShapePtr shape = intersection->getShape();
		if (shape)
		{
			Log::message("physics intersection info: point: (%f %f %f) shape: %s\n", intersection->getPoint().x, intersection->getPoint().y, intersection->getPoint().z, shape->getTypeName());
		}
	}

	return 1;
}


```


### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - Line start point coordinates.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - Line end point coordinates.
- *int* **mask** - Physics intersection mask. If **0** is passed, the function will return **NULL**.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[PhysicsIntersection](../../../api/library/physics/class.physicsintersection_cpp.md)> &* **intersection** - [PhysicsIntersection](../../../api/library/physics/class.physicsintersection_cpp.md) class instance containing intersection data.

### Return value

The first intersected object, if found; otherwise, 0.
## Ptr < Object > getIntersection ( const Math:: Vec3 & p0 , const Math:: Vec3 & p1 , int mask , const Ptr < PhysicsIntersectionNormal > & intersection )


Performs tracing from the p0 point to the p1 point to find a collision object located on that line. If an object is assigned a body, intersection occurs with its shape. If an object has no body, this function detects intersection with surfaces (polygons) of objects with intersection flag set. Physics intersection shall only be detected for objects with a matching [mask](../../../principles/bit_masking/index.md#physics_intersection_mask). Intersection does not work for disabled objects.


> **Notice:** This function uses world space coordinates.


### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - Line start point coordinates.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - Line end point coordinates.
- *int* **mask** - Physics intersection mask. If **0** is passed, the function will return **NULL**.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[PhysicsIntersectionNormal](../../../api/library/physics/class.physicsintersectionnormal_cpp.md)> &* **intersection** - [PhysicsIntersectionNormal](../../../api/library/physics/class.physicsintersectionnormal_cpp.md) class instance containing intersection data.

### Return value

The first intersected object, if found; otherwise, 0.
## Ptr < Object > getIntersection ( const Math:: Vec3 & p0 , const Math:: Vec3 & p1 , int mask , const Vector < Ptr < Node > > & exclude , const Ptr < PhysicsIntersectionNormal > & intersection )


Performs tracing from the p0 point to the p1 point to find a collision object located on that line. If an object is assigned a body, intersection occurs with its shape. If an object has no body, this function detects intersection with surfaces (polygons) of objects with intersection flag set. Intersection is found only for objects with a matching mask if their ID is not found in the *exclude* list. Intersection does not work for disabled objects.


> **Notice:** This function uses world space coordinates.


### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - Line start point coordinates.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - Line end point coordinates.
- *int* **mask** - Physics intersection mask. If **0** is passed, the function will return **NULL**.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)> > &* **exclude** - Array of nodes to be excluded.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[PhysicsIntersectionNormal](../../../api/library/physics/class.physicsintersectionnormal_cpp.md)> &* **intersection** - [PhysicsIntersectionNormal](../../../api/library/physics/class.physicsintersectionnormal_cpp.md) class instance containing intersection data.

### Return value

The first intersected object, if found; otherwise, 0.
## Ptr < Joint > getJoint ( int id ) const

Returns a joint with a given ID.
### Arguments

- *int* **id** - Joint ID.

### Return value

Joint with a given ID or **NULL** (0), if there is no joint with a given ID.
## bool isJoint ( int id ) const

Checks if a joint with a given ID exists.
### Arguments

- *int* **id** - Joint ID.

### Return value

true if a joint with a given ID exists; otherwise, false.
## Ptr < Shape > getShape ( int id ) const

Returns a shape with a given ID.
### Arguments

- *int* **id** - Shape ID.

### Return value

Shape with a given ID or **NULL** (0), if there is no shape with a given ID.
## bool isShape ( int id ) const

Checks if a shape with a given ID exists.
### Arguments

- *int* **id** - Shape ID.

### Return value

true if a shape with a given ID exists; otherwise, false.
## void addUpdateNode ( const Ptr < Node > & node )

Adds the node for which physical state should be updated. If a node is not added with this function, it won't be updated when out of physics [simulation distance](#setDistance_float_void).
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)> &* **node** - Node to be updated.

## void addUpdateNodes ( const Vector < Ptr < Node >> & nodes )

Adds the nodes for which physical state should be updated. If nodes are not added with this function, they won't be updated when out of physics [simulation distance](#setDistance_float_void).
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>> &* **nodes** - Nodes to be updated.

## bool loadSettings ( const char * name ) const

Loads [physics settings](../../../editor2/settings/physics_global/index.md) from a given file.
### Arguments

- *const char ** **name** - Path to an XML file with desired settings.

### Return value

true if settings are loaded successfully; otherwise, false.
## bool loadWorld ( const Ptr < Xml > & xml ) const

Loads [physics settings](../../../editor2/settings/physics_global/index.md) from the Xml.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Xml](../../../api/library/common/class.xml_cpp.md)> &* **xml** - Xml smart pointer.

### Return value

true if settings are loaded successfully; otherwise, false.
## int saveScene ( ) const

Saves the current physics scene (physical properties of all objects) into the buffer with the specified ID.
### Return value

Scene buffer ID.
## int restoreScene ( bool id ) const

Restores the previously saved physics scene from the buffer with the specified ID.
### Arguments

- *bool* **id** - Buffer ID.

### Return value

**true** if the scene was restored successfully; otherwise, **false**.
## bool removeScene ( int id ) const

Removes the previously saved physics scene.
### Arguments

- *int* **id** - Buffer ID.

### Return value

**true** if the scene was removed successfully; otherwise, **false**.
## bool saveState ( const Ptr < Stream > & stream ) const

Saves [physics settings](../../../editor2/settings/physics_global/index.md) into the stream.
**Example** using saveState() and [restoreState()](#restoreState_Stream_int) methods:


```cpp
// set state
Physics::setNumIterations(1); // NumIterations = 1

// save state
BlobPtr blob_state = Blob::create();
Physics::saveState(blob_state);

// change state
Physics::setNumIterations(16); // now NumIterations = 16

// restore state
blob_state->seekSet(0);		// returning the carriage to the start of the blob
Physics::restoreState(blob_state); // restore NumIterations = 1

```


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream smart pointer.

### Return value

true if settings are saved successfully; otherwise, false.
## bool restoreState ( const Ptr < Stream > & stream ) const

Restores [physics settings](../../../editor2/settings/physics_global/index.md) from the stream.
**Example** using [saveState()](#saveState_Stream_int) and restoreState() methods:


```cpp
// set state
Physics::setNumIterations(1); // NumIterations = 1

// save state
BlobPtr blob_state = Blob::create();
Physics::saveState(blob_state);

// change state
Physics::setNumIterations(16); // now NumIterations = 16

// restore state
blob_state->seekSet(0);		// returning the carriage to the start of the blob
Physics::restoreState(blob_state); // restore NumIterations = 1

```


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream smart pointer.

### Return value

true if settings are restored successfully; otherwise, false.
## bool saveSettings ( const char * name , int force = 0 ) const

Saves the current [physics settings](../../../editor2/settings/physics_global/index.md) to a given file.
### Arguments

- *const char ** **name** - Path to a target xml file to which the settings will be saved.
- *int* **force** - Forced saving of physics settings.

### Return value

true if the settings are saved successfully; otherwise, false.
## bool saveWorld ( const Ptr < Xml > & xml , int force = 0 ) const

Saves [physics settings](../../../editor2/settings/physics_global/index.md) to the given Xml node.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Xml](../../../api/library/common/class.xml_cpp.md)> &* **xml** - Xml smart pointer.
- *int* **force** - Forced saving of physics settings.

### Return value

**true** if settings are saved successfully; otherwise, **false**.
