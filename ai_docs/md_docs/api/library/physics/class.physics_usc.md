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
## void setGravity ( vec3 gravity )

Sets a new gravity value.
### Arguments

- *vec3* **gravity** - The gravity vector

## vec3 getGravity () const

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
## void setData ( string data )

Sets a new user string data associated with the world. this string is written directly into the data tag of the `*.world` file.
### Arguments

- *string* **data** - The user string data associated with the world

## const char * getData () const

Returns the current user string data associated with the world. this string is written directly into the data tag of the `*.world` file.
### Return value

Current user string data associated with the world
## void setSyncEngineUpdateWithPhysics ( int physics )

Sets a new flag indicating if the Engine fps is synchronized to physics one. Such fps limitation makes it possible to calculate physics each rendered frame (rather then interpolate it when this flag is unset). In this mode, there are no twitching of physical objects if they have non-linear velocities. If the Engine fps is lower than the physics one, this flag has no effect.
### Arguments

- *int* **physics** - The synchronization of the Engine FPS with physics

## int isSyncEngineUpdateWithPhysics () const

Returns the current flag indicating if the Engine fps is synchronized to physics one. Such fps limitation makes it possible to calculate physics each rendered frame (rather then interpolate it when this flag is unset). In this mode, there are no twitching of physical objects if they have non-linear velocities. If the Engine fps is lower than the physics one, this flag has no effect.
### Return value

Current synchronization of the Engine FPS with physics
## void setDeterminism ( int determinism )

Sets a new value indicating if objects are updated in a definite order or not. the default is 0 (the update order may change). Deterministic mode ensures that all contacts are solved in the predefined order and visualization of physics in the world is repetitive (on one computer). When this mode is enabled the Engine performs additional sorting of bodies, shapes and joints inside islands after building them. Deterministic mode is unavailable in case there are missed frames - it is simply impossible. Moreover, there may be differences between visualization of physics on different hardware (e.g., AMD and Intel).
> **Notice:** Determinism is guaranteed if there are no missed frames, the same Engine version is used, and the CPUs perform SSE operations similarly.
> Please note that deterministic mode does not come for free, it may eat up 10-20% of the frame rate, and it also depends on the scene a lot.

### Arguments

- *int* **determinism** - The deterministic update order

## int isDeterminism () const

Returns the current value indicating if objects are updated in a definite order or not. the default is 0 (the update order may change). Deterministic mode ensures that all contacts are solved in the predefined order and visualization of physics in the world is repetitive (on one computer). When this mode is enabled the Engine performs additional sorting of bodies, shapes and joints inside islands after building them. Deterministic mode is unavailable in case there are missed frames - it is simply impossible. Moreover, there may be differences between visualization of physics on different hardware (e.g., AMD and Intel).
> **Notice:** Determinism is guaranteed if there are no missed frames, the same Engine version is used, and the CPUs perform SSE operations similarly.
> Please note that deterministic mode does not come for free, it may eat up 10-20% of the frame rate, and it also depends on the scene a lot.

### Return value

Current deterministic update order
## void setEnabled ( int enabled )

Sets a new value indicating if physics simulation is enabled. the default is 1.
### Arguments

- *int* **enabled** - The physics simulation

## int isEnabled () const

Returns the current value indicating if physics simulation is enabled. the default is 1.
### Return value

Current physics simulation
## void setMissedFrameLifetime ( float lifetime )

Sets a new lifetime for [missed frames](../../../principles/physics/simulation.md#missed_frames). This value defines how long missed frames are to be kept in the catch-up buffer. In case the current Engine framerate is lower than the [fixed Physics framerate](../../../principles/physics/simulation.md#simulation_rate), some of the physics frames get skipped and the simulation starts looking like in a slo-mo effect (e.g., if the target physics framerate is 60 FPS, when the Engine updates at 30 FPS, the simulation will look 2 times slower). The Physics module will try to catch up everything missed later, when possible (e.g. when the Engine framerate grows higher, while [waiting for GPU](../../../code/fundamentals/execution_sequence/index.md#waiting_gpu) to complete rendering). The missed frames are kept in a buffer for some time (lifetime), as it expires the frame is removed from the buffer and becomes lost forever.
### Arguments

- *float* **lifetime** - The lifetime for missed frames

## float getMissedFrameLifetime () const

Returns the current lifetime for [missed frames](../../../principles/physics/simulation.md#missed_frames). This value defines how long missed frames are to be kept in the catch-up buffer. In case the current Engine framerate is lower than the [fixed Physics framerate](../../../principles/physics/simulation.md#simulation_rate), some of the physics frames get skipped and the simulation starts looking like in a slo-mo effect (e.g., if the target physics framerate is 60 FPS, when the Engine updates at 30 FPS, the simulation will look 2 times slower). The Physics module will try to catch up everything missed later, when possible (e.g. when the Engine framerate grows higher, while [waiting for GPU](../../../code/fundamentals/execution_sequence/index.md#waiting_gpu) to complete rendering). The missed frames are kept in a buffer for some time (lifetime), as it expires the frame is removed from the buffer and becomes lost forever.
### Return value

Current lifetime for missed frames
## void setUpdateMode ( int mode )

Sets a new [physics update mode](../../../principles/physics/simulation.md#update_mode). Physics can be updated either asynchronously (in parallel with rendering) or in the Main thread before rendering. The [async](#UPDATE_MODE_ASYNC_RENDERING) mode is the fastest one and is used by default, however, it has a one-frame lag (calculation results are applied in the next frame) and some nuances regarding user code execution in some cases.
### Arguments

- *int* **mode** - The physics update mode

## int getUpdateMode () const

Returns the current [physics update mode](../../../principles/physics/simulation.md#update_mode). Physics can be updated either asynchronously (in parallel with rendering) or in the Main thread before rendering. The [async](#UPDATE_MODE_ASYNC_RENDERING) mode is the fastest one and is used by default, however, it has a one-frame lag (calculation results are applied in the next frame) and some nuances regarding user code execution in some cases.
### Return value

Current physics update mode
## void setStableFPS ( int fps )

Sets a new value indicating if frame time stabilization is enabled. In case the current Engine framerate is much higher than the [fixed Physics framerate](../../../principles/physics/simulation.md#simulation_rate) (e.g. 120 FPS vs 60 FPS), the physics won't be updated each rendering frame (e.g. it may update during every second frame). The resulting frame time will become unstable, shorter-longer-shorter-longer (*render -> render+physics -> render -> render+physics...*). This option ensures stable frame time for smoother user experience removing unwanted "hiccups" (however, the average framerate is decreased).
> **Notice:** By default, this option is enabled. But you can disable it to increase average framerate in case the application is used for machine learning or for grabbing frame sequences (video grabber), when smoothness is not important.

### Arguments

- *int* **fps** - The frame time stabilization

## int isStableFPS () const

Returns the current value indicating if frame time stabilization is enabled. In case the current Engine framerate is much higher than the [fixed Physics framerate](../../../principles/physics/simulation.md#simulation_rate) (e.g. 120 FPS vs 60 FPS), the physics won't be updated each rendering frame (e.g. it may update during every second frame). The resulting frame time will become unstable, shorter-longer-shorter-longer (*render -> render+physics -> render -> render+physics...*). This option ensures stable frame time for smoother user experience removing unwanted "hiccups" (however, the average framerate is decreased).
> **Notice:** By default, this option is enabled. But you can disable it to increase average framerate in case the application is used for machine learning or for grabbing frame sequences (video grabber), when smoothness is not important.

### Return value

Current frame time stabilization
## void setShowContacts ( int contacts )

Sets a new value indicating if the visualization of physical interactions between the physical bodies is enabled.
### Arguments

- *int* **contacts** - The physical contacts visualization

## int isShowContacts () const

Returns the current value indicating if the visualization of physical interactions between the physical bodies is enabled.
### Return value

Current physical contacts visualization
## void setShowShapes ( int shapes )

Sets a new mode used to visualize physical shapes: one of the [SHOW_TYPE_*](#SHOW_TYPE_DISABLED) values.
### Arguments

- *int* **shapes** - The shapes visualization mode

## int getShowShapes () const

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
## void setShowCollisionSurfaces ( int surfaces )

Sets a new value indicating if the collision surface visualization is enabled.
### Arguments

- *int* **surfaces** - The collision surface visualization

## int isShowCollisionSurfaces () const

Returns the current value indicating if the collision surface visualization is enabled.
### Return value

Current collision surface visualization
## void setShowJoints ( int joints )

Sets a new value indicating if the visualization of joints that connect physical bodies is enabled.
### Arguments

- *int* **joints** - The joints visualization

## int isShowJoints () const

Returns the current value indicating if the visualization of joints that connect physical bodies is enabled.
### Return value

Current joints visualization
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

  - PhysicsIntersection intersection � The [PhysicsIntersection](../../../api/library/physics/class.physicsintersection_usc.md) class instance.
  - PhysicsIntersectionNormal normal � The [PhysicsIntersectionNormal](../../../api/library/physics/class.physicsintersectionnormal_usc.md) class instance.

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

  - PhysicsIntersection intersection � The [PhysicsIntersection](../../../api/library/physics/class.physicsintersection_usc.md) class instance.
  - PhysicsIntersectionNormal normal � The [PhysicsIntersectionNormal](../../../api/library/physics/class.physicsintersectionnormal_usc.md) class instance.

### Return value

The first intersected object, if found; otherwise, 0.
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
