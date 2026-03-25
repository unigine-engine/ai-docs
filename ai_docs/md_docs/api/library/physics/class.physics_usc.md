# Unigine::Physics Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


Controls the simulation of physics. For more information on principles and implementation of physics in real-time rendering, see the articles [Execution Sequence](../../../code/fundamentals/execution_sequence/index.md), [Physics](../../../principles/physics/index.md) and [Simulation of Physics](../../../principles/physics/simulation.md).


### See Also


- The [Creating a Car with Suspension Joints](../../../code/usage/car_wheel_joints/index_usc.md) usage example demonstrating how to set up physics parameters
- *[Physics](../../../sdk/api_samples/cpp/physics.md)* section in C++ Samples
- *[Physics](../../../sdk/api_samples/cs/physics.md)* section in C# Component Samples
- *[Physics](../../../code/uniginescript/samples/physics.md)* section in UnigineScript samples


## Physics Class

### Members

---

## Object engine.physics. getIntersection ( Vec3 p0 , Vec3 p1 , int mask , int[] exclude , Variable v )


Performs tracing from the p0 point to the p1 point to find an object located on that line. If an object is assigned a body, intersection occurs with its shape. If an object has no body, this function detects intersection with surfaces (polygons) of objects with intersection flag. Physics intersection shall only be detected for objects with a matching [mask](../../../principles/bit_masking/index.md#physics_intersection_mask). Intersection does not work for disabled objects.


> **Notice:** This function uses world space coordinates.


### Arguments

- *Vec3* **p0** - Line start point coordinates.
- *Vec3* **p1** - Line end point coordinates.
- *int* **mask** - Physics intersection mask. If **0** is passed, the function will return **NULL**.
- *int[]* **exclude** - Array of nodes to exclude.
- *Variable* **v** - Variable. Can be one of the following:

  - PhysicsIntersection intersection — The [PhysicsIntersection](../../../api/library/physics/class.physicsintersection_usc.md) class instance.
  - PhysicsIntersectionNormal normal — The [PhysicsIntersectionNormal](../../../api/library/physics/class.physicsintersectionnormal_usc.md) class instance.

### Return value

The first intersected object, if found; otherwise, 0.
## Object engine.physics. getIntersection ( Vec3 p0 , Vec3 p1 , int mask , Variable v )


Performs tracing from the p0 point to the p1 point to find an collision object located on that line. If an object is assigned a body, intersection occurs with its shape. If an object has no body, this function detects intersection with surfaces (polygons) of objects with intersection flag. Physics intersection shall only be detected for objects with a matching [mask](../../../principles/bit_masking/index.md#physics_intersection_mask).


> **Notice:** This function uses world space coordinates.


Depending on the variable passed as an argument, the result can be presented as the PhysicsIntersection or PhysicsIntersectionNormal node.


**Usage Example**


The following example shows how you can get the intersection information by using the PhysicsIntersection class. In this example the line is an invisible traced line from the point of the camera (vec3 p0) to the point of the mouse pointer (vec3 p1). The executing sequence is the following:

- Define and initialize two points (p0 and p1) by using the *getPlayerMouseDirection()* function from `core/scripts/utils.h`.
- Create an instance of the PhysicsIntersection class to get the intersection information.
- Check, if there is an intersection with an object. The [*engine.physics.getIntersection()*](#getIntersection_Vec3_Vec3_int_Variable) function returns an intersected object when the object intersects with the traced line.
- In this example, when the object intersects with the traced line, all the surfaces of the intersected object change their material parameters. If the object has a shape, its information will be shown in console. The PhysicsIntersection class instance gets the coordinates of the intersection point, the index of the surface and the Shape class object. You can get all these fields by using *[getShape()](../../../api/library/physics/class.physicsintersection_usc.md#getShape_Shape)*, *[getPoint()](../../../api/library/physics/class.physicsintersection_usc.md#getPoint_Vec3)* and *[getSurface()](../../../api/library/physics/class.physicsintersection_usc.md#getSurface_int)* functions


```cpp
#include <core/scripts/utils.h>
/* ... */
// define two vec3 coordinates
vec3 p0,p1;
// get the mouse direction from camera (p0) to cursor pointer (p1)
Unigine::getPlayerMouseDirection(p0,p1);

// create the instance of the PhysicsIntersection object to save the result
PhysicsIntersection intersection = new PhysicsIntersection();
// create an instance for intersected object and check the intersection
Object object = engine.physics.getIntersection(p0,p1,1,intersection);

// if the intersection has been occurred, change the parameter and the texture of the object's material
if(object != NULL)
{
	forloop(int i=0; object.getNumSurfaces())
	{
		object.setMaterialParameterFloat4("diffuse_color", vec4(1.0f, 0.0f, 0.0f, 1.0f),i);
		object.setMaterialTexture("diffuse","", i);
	}

	// if the intersected object has a shape, show the information about the intersection
	Shape shape = intersection.getShape();
	if (shape != NULL)
	{
		log.message("physics intersection info: point: %s shape: %s surface: %i \n", typeinfo(intersection.getPoint()), typeinfo(shape.getType()), intersection.getSurface());
	}
}
/* ... */

```


### Arguments

- *Vec3* **p0** - Line start point coordinates.
- *Vec3* **p1** - Line end point coordinates.
- *int* **mask** - Physics intersection mask. If **0** is passed, the function will return **NULL**.
- *Variable* **v** - Variable. Can be one of the following:

  - PhysicsIntersection intersection — The [PhysicsIntersection](../../../api/library/physics/class.physicsintersection_usc.md) class instance.
  - PhysicsIntersectionNormal normal — The [PhysicsIntersectionNormal](../../../api/library/physics/class.physicsintersectionnormal_usc.md) class instance.

### Return value

The first intersected object, if found; otherwise, 0.
## void engine.physics. setAngularDamping ( float damping )

Updates the current angular damping value.
### Arguments

- *float* **damping** - New angular damping. If a negative value is provided, **0** will be used instead.

## float engine.physics. getAngularDamping ( )

Returns the current angular damping value.
### Return value

Angular damping.
## Body engine.physics. getBody ( int id )

Returns a body with a given ID.
### Arguments

- *int* **id** - Body ID.

### Return value

Body with a given ID or **NULL** (0), if there is no body with a given ID.
## bool engine.physics. isBody ( int id )

Checks if a body with a given ID exists.
### Arguments

- *int* **id** - Body ID.

### Return value

**1** if a body with a given ID exists; otherwise, **0**.
## void engine.physics. setBudget ( float budget )

Sets the physics simulation budget in seconds. Physics isn't simulated when time is out of the budget.
### Arguments

- *float* **budget** - The budget value in seconds. The default value is 1/20.

## float engine.physics. getBudget ( )

Returns the physics simulation budget. Physics isn't simulated when time is out of the budget.
### Return value

The budget value in seconds.
## void engine.physics. setData ( string data )

Updates user data associated with the physics. This string is written directly into a `*.world` file. Namely, into the *data* child tag of the *physics* tag, for example:
```xml
<world version="1.21">
	<physics>
		<data>User data</data>
	</physics>
</world>

```


### Arguments

- *string* **data** - User data. Data can contain an XML formatted string.

## string engine.physics. getData ( )

Returns user data associated with the physics. This string is written directly into a `*.world` file. Namely, into the *data* child tag of the *physics* tag, for example:
```xml
<world version="1.21">
	<physics>
		<data>User data</data>
	</physics>
</world>

```


### Return value

User data. Data can contain an XML formatted string.
## void engine.physics. setDistance ( float distance )

Updates a distance after which the physics will not be simulated.
### Arguments

- *float* **distance** - Distance in units.

## float engine.physics. getDistance ( )

Returns a distance after which the physics will not be simulated.
### Return value

Distance in units.
## void engine.physics. setEnabled ( int enable )

Enables or disables physics simulation.
### Arguments

- *int* **enable** - **1** to enable physics, **0** to disable it.

## int engine.physics. isEnabled ( )

Returns a value indicating if physics simulation is enabled. The default is 1.
### Return value

**1** if physics is enabled; otherwise, **0**.
## void engine.physics. setSyncEngineUpdateWithPhysics ( int fixed )

Sets a flag to synchronize the Engine FPS to physics one. Such FPS limitation allows to calculate physics each rendered frame (rather then interpolate it when this flag is unset). In this mode, there are no twitching of physical objects if they have non-linear velocities. If the Engine FPS is lower than the physics one, this flag has no effect.
### Arguments

- *int* **fixed** - **1** to synchronize the Engine FPS to physics one; **0** to interpolate physics if the Engine FPS is higher.

## int engine.physics. isSyncEngineUpdateWithPhysics ( )

### Return value

**1** if the Engine FPS is synchronized to physics one; **0** if the physics is interpolated if the Engine FPS is higher.
## int engine.physics. getFrame ( )

Returns the current frame of physics update.
### Return value

Frame number.
## void engine.physics. setFrozenAngularVelocity ( float velocity )

Updates the angular velocity threshold for freezing object simulation. If the object angular velocity remains lower than this threshold during the number of [Frozen frames](#setNumFrozenFrames_int_void) (together with linear one), it stops to be updated.
### Arguments

- *float* **velocity** - New "freeze" angular velocity. If a negative value is provided, **0** will be used instead.

## float engine.physics. getFrozenAngularVelocity ( )

Returns the current angular velocity threshold for freezing object simulation. An object stops to be updated if its angular velocity remains lower than this threshold during the number of [Frozen frames](#setNumFrozenFrames_int_void) (together with linear one).
### Return value

"Freeze" angular velocity.
## void engine.physics. setFrozenLinearVelocity ( float velocity )

Updates the linear velocity threshold for freezing object simulation. If the object linear velocity remains lower than this threshold during the number of [Frozen frames](#setNumFrozenFrames_int_void) (together with angular one), it stops to be updated.
### Arguments

- *float* **velocity** - New "freeze" linear velocity. If a negative value is provided, **0** will be used instead.

## float engine.physics. getFrozenLinearVelocity ( )

Returns the current linear velocity threshold for freezing object simulation. An object stops to be updated if its linear velocity remains lower than this threshold during the number of [Frozen frames](#setNumFrozenFrames_int_void) (together with angular one).
### Return value

"Freeze" linear velocity.
## void engine.physics. setGravity ( vec3 gravity )

Updates the current gravity value.
### Arguments

- *vec3* **gravity** - New gravity.

## vec3 engine.physics. getGravity ( )

Returns the current gravity value.
### Return value

Gravity.
## void engine.physics. setIFps ( float ifps )

Updates a frame duration. In fact, this function updates the FPS count used to calculate physics.
### Arguments

- *float* **ifps** - Frame duration (*1/FPS*).

## float engine.physics. getIFps ( )

Returns a physics frame duration.
### Return value

Frame duration (1 / FPS).
## Joint engine.physics. getJoint ( int id )

Returns a joint with a given ID.
### Arguments

- *int* **id** - Joint ID.

### Return value

Joint with a given ID or **NULL** (0), if there is no joint with a given ID.
## int engine.physics. isJoint ( int id )

Checks if a joint with a given ID exists.
### Arguments

- *int* **id** - Joint ID.

### Return value

**1** if a joint with a given ID exists; otherwise, **0**.
## void engine.physics. setLinearDamping ( float damping )

Updates the current linear damping value.
### Arguments

- *float* **damping** - New linear damping. If a negative value is provided, **0** will be used instead.

## float engine.physics. getLinearDamping ( )

Returns the current linear damping value.
### Return value

Linear damping.
## void engine.physics. setMaxAngularVelocity ( float velocity )

Updates the maximum possible angular velocity.
### Arguments

- *float* **velocity** - New maximum velocity value. If a negative value is provided, **0** will be used instead.

## float engine.physics. getMaxAngularVelocity ( )

Returns the current maximum possible angular velocity.
### Return value

Maximum possible angular velocity.
## void engine.physics. setMaxLinearVelocity ( float velocity )

Updates the maximum possible linear velocity.
### Arguments

- *float* **velocity** - New maximum velocity value. If a negative value is provided, **0** will be used instead.

## float engine.physics. getMaxLinearVelocity ( )

Returns the current maximum possible linear velocity.
### Return value

Maximum possible linear velocity.
## float engine.physics. getCollisionTime ( )

Returns the duration of the [collision detection phase](../../../principles/physics/simulation.md#collision_detection), during which collisions between objects are found.
### Return value

Collision detection phase duration, in milliseconds.
## int engine.physics. getNumBodies ( )

Returns the number of [bodies](../../../principles/physics/bodies/index.md) present within the [physics radius](../../../editor2/settings/physics_global/index.md#physics_distance).
### Return value

The number of bodies.
## int engine.physics. getNumContacts ( )

Returns the number of contacts within the [physics radius](../../../editor2/settings/physics_global/index.md#physics_distance); it includes contacts between the bodies (their shapes) and body-mesh contacts.
### Return value

The number of contacts.
## void engine.physics. setNumFrozenFrames ( int frames )

Updates the number of frames, during which an object should keep certain angular and linear velocities to become frozen.
### Arguments

- *int* **frames** - Number of frames. If a non-positive value is provided, **1** will be used instead.

## int engine.physics. getNumFrozenFrames ( )

Returns the current number of frames, during which an object should keep certain angular and linear velocities to become frozen.
### Return value

Number of frames.
## int engine.physics. getNumIslands ( )

Returns the number of physical [islands](../../../principles/physics/collision/index.md#islands) within the [physics radius](../../../editor2/settings/physics_global/index.md#physics_distance) that could be calculated separately. The lower this number, the less efficient multi-threading is, if enabled.
### Return value

The number of physical islands.
## void engine.physics. setNumIterations ( int iterations )

Updates the number of iterations used to solve contacts and constraints. Note that if this value is too low, the precision of calculations will suffer.
### Arguments

- *int* **iterations** - New number of iterations. If a non-positive value is provided, **1** will be used instead.

## int engine.physics. getNumIterations ( )

Returns the current number of iterations used to solve contacts and constraints.
### Return value

Current number of iterations.
## int engine.physics. getNumJoints ( )

Returns the number of [joints](../../../principles/physics/joints/index.md) within the physics [radius](../../../editor2/settings/physics_global/index.md#physics_distance).
### Return value

The number of joints.
## void engine.physics. setPenetrationFactor ( float factor )

Updates the current penalty force factor.
### Arguments

- *float* **factor** - New penetration factor. **0** means no penalty force in contacts. The provided value is saturated in the range **[0; 1]**.

## float engine.physics. getPenetrationFactor ( )

Returns a penalty force factor. **0** means no penalty force in contacts. The maximum value is **1**.
### Return value

Current penetration factor.
## void engine.physics. setPenetrationTolerance ( float tolerance )

Updates the current penetration tolerance.
### Arguments

- *float* **tolerance** - New penetration tolerance. If a negative value is provided, **0** will be used instead, however, this value should be greater than **0** for stable simulation.

## float engine.physics. getPenetrationTolerance ( )

Returns a value indicating how deeply one object can penetrate another.
### Return value

Current penetration tolerance.
## void engine.physics. setScale ( float scale )

Updates a value that is used to scale a frame duration. The provided value is saturated in the range **[0;16]**.
### Arguments

- *float* **scale** - Scaling factor.

## float engine.physics. getScale ( )

Returns a value used to scale a frame duration.
### Return value

Value to scale the frame duration.
## Shape engine.physics. getShape ( int id )

Returns a shape with a given ID.
### Arguments

- *int* **id** - Shape ID.

### Return value

Shape with a given ID or **NULL** (0), if there is no shape with a given ID.
## int engine.physics. isShape ( int id )

Checks if a shape with a given ID exists.
### Arguments

- *int* **id** - Shape ID.

### Return value

**1** if a shape with a given ID exists; otherwise, **0**.
## float engine.physics. getSimulationTime ( )

Returns the duration of all of the simulation phases added together.
### Return value

A simulation phases duration value, milliseconds.
## float engine.physics. getWaitTime ( )

Returns the time period during which the physics module waits for the completion of rendering process.
### Return value

Waiting phase duration value, milliseconds.
## void engine.physics. setDeterminism ( int determinism )

Sets a value indicating if objects are updated in a definite order or not. Deterministic mode ensures that all contacts are solved in the predefined order and visualization of physics in the world is repetitive (on one computer). When this mode is enabled the Engine performs additional sorting of bodies, shapes and joints inside islands after building them. Deterministic mode is unavailable in case there are missed frames — it is simply impossible. Moreover, there may be differences between visualization of physics on different hardware (e.g., AMD and Intel).
> **Notice:** Determinism is guaranteed if there are no missed frames, the same Engine version is used, and the CPUs perform SSE operations similarly.
> Please note that deterministic mode does not come for free, it may eat up 10-20% of the frame rate, and it also depends on the scene a lot.


### Arguments

- *int* **determinism** - **1** to indicate that the objects are updated in a definite order; **0** to indicate that an objects update order may change. The default is **0** (the update order may change).

## int engine.physics. isDeterminism ( )

Returns a value indicating if objects are updated in a definite order or not.Deterministic mode ensures that all contacts are solved in the predefined order and visualization of physics in the world is repetitive (on one computer). When this mode is enabled the Engine performs additional sorting of bodies, shapes and joints inside islands after building them. Deterministic mode is unavailable in case there are missed frames — it is simply impossible. Moreover, there may be differences between visualization of physics on different hardware (e.g., AMD and Intel).
> **Notice:** Determinism is guaranteed if there are no missed frames, the same Engine version is used, and the CPUs perform SSE operations similarly.
> Please note that deterministic mode does not come for free, it may eat up 10-20% of the frame rate, and it also depends on the scene a lot.


### Return value

**1** if the objects are updated in a definite order; otherwise **0**. The default is **0** (the update order may change).
## void engine.physics. setCurrentSubframeTime ( float time )

Forces simulation of physics for a given time. It means, until the set time elapses, physics will be calculated each physics tick (frame) that occurs depending on physics frame rate. It allows to control the starting point for physics simulation.
```cpp
int init() {
	// to prevent physics from being automatically calculated with each update, set one of the following:
	engine.physics.setEnabled(0)
	// or
	engine.physics.setScale(0)
}

int update() {
	// add the time elapsed from the last physics update to the next time count cycle:
	engine.physics.setCurrentSubframeTime(engine.physics.getCurrentSubframeTime()+ifps));
}

```

 In the example, *ifps* is the time between frames of the renderer.
### Arguments

- *float* **time** - Time to continue updating physics in seconds.

## float engine.physics. getCurrentSubframeTime ( )

Returns the current time that can be used when shifting between physics update frames.
### Return value

Time in seconds.
## float engine.physics. getTotalTime ( )

Returns the total time that both rendering and calculating of the frame took (the duration of the [main loop](../../../code/fundamentals/execution_sequence/main_loop.md) in the application [execution sequence](../../../code/fundamentals/execution_sequence/index.md)).
### Return value

The total time value, milliseconds.
## void engine.physics. addUpdateNode ( Node node )

Adds the node for which physical state should be updated. If a node is not added with this function, it won't be updated when out of physics [simulation distance](#setDistance_float_void).
### Arguments

- *[Node](../../../api/library/nodes/class.node_usc.md)* **node** - Node to be updated.

## void engine.physics. addUpdateNodes ( int[] nodes )

Adds the nodes for which physical state should be updated. If nodes are not added with this function, they won't be updated when out of physics [simulation distance](#setDistance_float_void).
### Arguments

- *int[]* **nodes** - Nodes to be updated.

## int engine.physics. loadSettings ( string name )

Loads [physics settings](../../../editor2/settings/physics_global/index.md) from a given file.
### Arguments

- *string* **name** - Path to an XML file with desired settings.

### Return value

**1** if settings are loaded successfully; otherwise, **0**.
## int engine.physics. loadWorld ( Xml xml )

Loads [physics settings](../../../editor2/settings/physics_global/index.md) from the Xml.
### Arguments

- *[Xml](../../../api/library/common/class.xml_usc.md)* **xml** - Xml node.

### Return value

**1** if settings are loaded successfully; otherwise, **0**.
## int engine.physics. saveScene ( )

Saves the current physics scene (physical properties of all objects) into the buffer with the specified ID.
### Return value

Scene buffer ID.
## int engine.physics. restoreScene ( int id )

Restores the previously saved physics scene from the buffer with the specified ID.
### Arguments

- *int* **id** - ID number of the scene.

### Return value

**1** if the scene was restored successfully; otherwise, **0**.
## int engine.physics. removeScene ( int id )

Removes the previously saved physics scene.
### Arguments

- *int* **id** - ID number of the scene.

### Return value

**1** if the scene was removed successfully; otherwise, **0**.
## int engine.physics. saveState ( Stream stream )

Saves [physics settings](../../../editor2/settings/physics_global/index.md) into the stream.
**Example** using saveState() and [restoreState()](#restoreState_Stream_int) methods:


```cpp
// set state
engine.physics.setNumIterations(1); // NumIterations = 1

// save state
Blob blob_state = new Blob();
engine.physics.saveState(blob_state, 1);

// change state
engine.physics.setNumIterations(16); // now NumIterations = 16

// restore state
blob_state.seekSet(0);		// returning the carriage to the start of the blob
engine.physics.restoreState(blob_state); // restore NumIterations = 1

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - Stream to save settings into.

### Return value

**1** if settings are saved successfully; otherwise, **0**.
## int engine.physics. restoreState ( Stream stream )

Restores [physics settings](../../../editor2/settings/physics_global/index.md) from the stream.
**Example** using [saveState()](#saveState_Stream_int) and restoreState() methods:


```cpp
// set state
engine.physics.setNumIterations(1); // NumIterations = 1

// save state
Blob blob_state = new Blob();
engine.physics.saveState(blob_state, 1);

// change state
engine.physics.setNumIterations(16); // now NumIterations = 16

// restore state
blob_state.seekSet(0);		// returning the carriage to the start of the blob
engine.physics.restoreState(blob_state); // restore NumIterations = 1

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - Stream to restore settings from.

### Return value

**1** if settings are restored successfully; otherwise, **0**.
## int engine.physics. saveSettings ( string name , int force = 0 )

Saves the current [physics settings](../../../editor2/settings/physics_global/index.md) to a given file.
### Arguments

- *string* **name** - Path to a target xml file to which the settings will be saved.
- *int* **force** - Forced saving of physics settings.

### Return value

**1** if the settings are saved successfully; otherwise, **0**.
## int engine.physics. saveWorld ( Xml xml , int force = 0 )

Saves [physics settings](../../../editor2/settings/physics_global/index.md) to the given Xml node.
### Arguments

- *[Xml](../../../api/library/common/class.xml_usc.md)* **xml** - Xml node.
- *int* **force** - Forced saving of physics settings.

### Return value

**1** if settings are saved successfully; otherwise, **0**.
## void engine.physics. setStableFPS ( int stablefps )

Returns a value indicating if frame time stabilization is enabled. In case the current Engine framerate is much higher than the [fixed Physics framerate](../../../principles/physics/simulation.md#simulation_rate) (e.g. 120 FPS vs 60 FPS), the physics won't be updated each rendering frame (e.g. it may update during every second frame). The resulting frame time will become unstable, shorter-longer-shorter-longer (*render -> render+physics -> render -> render+physics...*). This option ensures stable frame time for smoother user experience removing unwanted "hiccups" (however, the average framerate is decreased).
> **Notice:** By default, this option is enabled. But you can disable it to increase average framerate in case the application is used for machine learning or for grabbing frame sequences (video grabber), when smoothness is not important.

### Arguments

- *int* **stablefps** - **1** to enable frame time stabilization; **0** — to disable it.

## int engine.physics. isStableFPS ( )

Returns a value indicating if frame time stabilization is enabled. In case the current Engine framerate is much higher than the [fixed Physics framerate](../../../principles/physics/simulation.md#simulation_rate) (e.g. 120 FPS vs 60 FPS), the physics won't be updated each rendering frame (e.g. it may update during every second frame). The resulting frame time will become unstable, shorter-longer-shorter-longer (*render -> render+physics -> render -> render+physics...*). This option ensures stable frame time for smoother user experience removing unwanted "hiccups" (however, the average framerate is decreased).
> **Notice:** By default, this option is enabled. But you can disable it to increase average framerate in case the application is used for machine learning or for grabbing frame sequences (video grabber), when smoothness is not important.

### Return value

**1** if frame time stabilization is enabled; otherwise, **0**.
## void engine.physics. setUpdateMode ( int mode )

Sets the [update mode](../../../principles/physics/simulation.md#update_mode) to be used for physics. Physics can be updated either asynchronously (in parallel with rendering) or in the Main thread before rendering. The [async](#UPDATE_MODE_ASYNC_RENDERING) mode is the fastest one and is used by default, however, it has a one-frame lag (calculation results are applied in the next frame) and some nuances regarding user code execution in some cases.
### Arguments

- *int* **mode** - New physics update mode to be set.

## int engine.physics. getUpdateMode ( )

Returns the current [physics update mode](../../../principles/physics/simulation.md#update_mode). Physics can be updated either asynchronously (in parallel with rendering) or in the Main thread before rendering. The [async](#UPDATE_MODE_ASYNC_RENDERING) mode is the fastest one and is used by default, however, it has a one-frame lag (calculation results are applied in the next frame) and some nuances regarding user code execution in some cases.
### Return value

Current physics update mode.
## void engine.physics. setMissedFrameLifetime ( float lifetime )

Sets the lifetime for [missed frames](../../../principles/physics/simulation.md#missed_frames). This value defines how long missed frames are to be kept in the catch-up buffer. In case the current Engine framerate is lower than the [fixed Physics framerate](../../../principles/physics/simulation.md#simulation_rate), some of the physics frames get skipped and the simulation starts looking like in a slo-mo effect (e.g., if the target physics framerate is 60 FPS, when the Engine updates at 30 FPS, the simulation will look 2 times slower). The Physics module will try to catch up everything missed later, when possible (e.g. when the Engine framerate grows higher, while [waiting for GPU](../../../code/fundamentals/execution_sequence/index.md#waiting_gpu) to complete rendering). The missed frames are kept in a buffer for some time (lifetime), as it expires the frame is removed from the buffer and becomes lost forever.
### Arguments

- *float* **lifetime** - Lifetime for missing frame, in milliseconds. Setting too high values may result in significant memory consumption in case of low hardware capabilities (no catching-up performed with a growing number of missed frames).

## float engine.physics. getMissedFrameLifetime ( )

Sets the lifetime for missed frames. This value defines how long missed frames are to be kept in the catch-up buffer. In case the current Engine framerate is lower than the [fixed Physics framerate](../../../principles/physics/simulation.md#simulation_rate), some of the physics frames get skipped and the simulation starts looking like in a slo-mo effect (e.g., if the target physics framerate is 60 FPS, when the Engine updates at 30 FPS, the simulation will look 2 times slower). The Physics module will try to catch up everything missed later, when possible (e.g. when the Engine framerate grows higher, while [waiting for GPU](../../../code/fundamentals/execution_sequence/index.md#waiting_gpu) to complete rendering). The missed frames are kept in a buffer for some time (lifetime), as it expires the frame is removed from the buffer and becomes lost forever.
### Return value

Lifetime for missing frame, in milliseconds. Setting too high values may result in significant memory consumption in case of low hardware capabilities (no catching-up performed with a growing number of missed frames).
## void engine.physics. setShowShapes ( int shapes )

Sets the shape visualization mode.
### Arguments

- *int* **shapes** - The helper visualization mode.

## int engine.physics. getShowShapes ( )

Returns the shape visualization mode.
### Return value

The shape visualization mode.
## void engine.physics. setShowShapesDistance ( float distance )

Sets the distance from the camera within which the shapes are visualized.
### Arguments

- *float* **distance** - The distance from the camera within which the shapes are visualized.

## float engine.physics. getShowShapesDistance ( )

Returns the distance from the camera within which the shapes are visualized.
### Return value

The distance from the camera within which the shapes are visualized.
## void engine.physics. setShowCollisionSurfaces ( int surfaces )

Sets the value indicating if the collision surface visualization is enabled.
### Arguments

- *int* **surfaces** - **1** to enable the collision surface visualization; **0** — to disable it.

## int engine.physics. isShowCollisionSurfaces ( )

Returns a value indicating if the collision surface visualization is enabled.
### Return value

**1** if the collision surface visualization is enabled; otherwise, **0**.
## void engine.physics. setShowContacts ( int contacts )

Sets the value indicating if the visualization of physical interactions between the physical bodies is enabled.
### Arguments

- *int* **contacts** - **1** to enable the visualization of physical interactions between the physical bodies; **0** — to disable it.

## int engine.physics. isShowContacts ( )

Returns a value indicating if the visualization of physical interactions between the physical bodies is enabled.
### Return value

**1** if the visualization of physical interactions between the physical bodies is enabled; otherwise, **0**.
## void engine.physics. setShowJoints ( int joints )

Sets the value indicating if the visualization of joints that connect physical bodies is enabled.
### Arguments

- *int* **joints** - **1** to enable the visualization of joints that connect physical bodies; **0** — to disable it.

## int engine.physics. isShowJoints ( )

Returns a value indicating if the visualization of joints that connect physical bodies is enabled.
### Return value

**1** if the visualization of joints that connect physical bodies is enabled; otherwise, **0**.
