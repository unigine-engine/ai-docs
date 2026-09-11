# Unigine::Physics Class (CS)

> **Notice:** This class is a singleton.


Controls the simulation of physics. For more information on principles and implementation of physics in real-time rendering, see the articles [Execution Sequence](../../../code/fundamentals/execution_sequence/index.md), [Physics](../../../principles/physics/index.md) and [Simulation of Physics](../../../principles/physics/simulation.md).


### See Also


- The [Creating a Car with Suspension Joints](../../../code/usage/car_wheel_joints/index_cs.md) usage example demonstrating how to set up physics parameters
- *[Physics](../../../sdk/api_samples/cpp/physics.md)* section in C++ Samples
- *[Physics](../../../sdk/api_samples/cs/physics.md)* section in C# Component Samples
- *[Physics](../../../code/uniginescript/samples/physics.md)* section in UnigineScript samples


## Physics Class

### Enums

## UPDATE_MODE

[Physics update mode](../../../principles/physics/simulation.md#update_mode).
| Name | Description |
|---|---|
| **BEFORE_RENDERING** = 0 | Update Before Rendering. Physics update (along with the spatial tree update and user callbacks) is executed in the Main thread just before rendering is performed (render). The number of physics ticks executed before the rendering frame here is defined by the [physics and the Engine framerates](../../../code/fundamentals/execution_sequence/index.md#cape_framerate). This mode is the most clear and straightforward (everything is executed safely in a strictly determined order) with no frame lag (results of physics calculations are applied in the current frame). But, on the other hand, this mode is the slowest as there are no asynchronous parallel calculations (everything's in the Main thread). Use this mode in case the time lag is unacceptabe for your application (you need all physics calculations to be applied in the current frame) and you want maximum simplicity and strictly determined order of execution for user code (physicsUpdate and physics callbacks). |
| **ASYNC_RENDERING** = 1 | Asynchronous update mode. Physics update is performed asynchronously to rendering. In case of several physics ticks per one rendering frame (when the Engine framerate is lower, or [catching up](../../../principles/physics/simulation.md#catch_up) is performed), only the first one is executed in parallel, then the physics module waits for the completion of the rendering process, returns to the Main thread and executes the rest of the physics ticks. There is a frame lag (results of physics calculations are applied in the next frame) and there is some ambiguity regarding the time, when user code (physicsUpdate and physics callbacks) is to be executed in case of several physics ticks per one rendering frame (some part is executed before rendering while the other just after it). This mode is the fastest one and is used by default. |

## SHOW_TYPE

| Name | Description |
|---|---|
| **DISABLED** = 0 | The helper is not visualized. |
| **WIREFRAME** = 1 | The helper is visualized as a wireframe. |
| **SOLID** = 2 | The helper is visualized as a a solid object. |

### Properties

## 🔒︎ float TotalTime

The total time taken to perform all physics calculations.
## 🔒︎ float SimulationTime

The duration of all of the simulation phases added together.
## 🔒︎ float WaitTime

The Time period during which the physics module waits for the completion of rendering process.
## 🔒︎ int NumJoints

The number of [joints](../../../principles/physics/joints/index.md) within the physics [radius](../../../editor2/settings/physics_global/index.md#physics_distance).
## 🔒︎ int NumIslands

The number of physical [islands](../../../principles/physics/collision/index.md#islands) within the [physics radius](../../../editor2/settings/physics_global/index.md#physics_distance) that could be calculated separately. The lower this number, the less efficient multi-threading is, if enabled.
## 🔒︎ int NumContacts

The number of contacts within the [physics radius](../../../editor2/settings/physics_global/index.md#physics_distance); it includes contacts between the bodies (their shapes) and body-mesh contacts.
## 🔒︎ int NumBodies

The number of [bodies](../../../principles/physics/bodies/index.md) present within the [physics radius](../../../editor2/settings/physics_global/index.md#physics_distance).
## 🔒︎ float CollisionTime

The duration of the [collision detection phase](../../../principles/physics/simulation.md#collision_detection), during which collisions between objects are found.
## 🔒︎ int Frame

The frame of physics update.
## int NumIterations

The number of iterations used to solve contacts and constraints.
## int NumFrozenFrames

The number of frames, during which an object should keep certain angular and linear velocities to become frozen.
## 🔒︎ float CurrentSubframeTime

The time that can be used when shifting between physics update frames.
## float Scale

The value used to scale a frame duration.
## float PenetrationTolerance

The how deeply one object can penetrate another.
## float PenetrationFactor

The penalty force factor. **0** means no penalty force in contacts. The maximum value is **1**.
## float MaxLinearVelocity

The maximum possible linear velocity.
## float MaxAngularVelocity

The maximum possible angular velocity.
## float LinearDamping

The linear damping value.
## float IFps

The physics frame duration.
## vec3 Gravity

The gravity value.
## float FrozenLinearVelocity

The linear velocity threshold for freezing object simulation. an object stops to be updated if its linear velocity remains lower than this threshold during the number of [Frozen frames](#setNumFrozenFrames_int_void) (together with angular one).
## float FrozenAngularVelocity

The angular velocity threshold for freezing object simulation. an object stops to be updated if its angular velocity remains lower than this threshold during the number of [Frozen frames](#setNumFrozenFrames_int_void) (together with linear one).
## float AngularDamping

The angular damping value.
## float Distance

The distance after which the physics will not be simulated.
## float Budget

The physics simulation budget. physics isn't simulated when time is out of the budget.
## string Data

The user string data associated with the world. this string is written directly into the data tag of the `*.world` file.
## bool SyncEngineUpdateWithPhysics

The flag indicating if the Engine fps is synchronized to physics one. Such fps limitation makes it possible to calculate physics each rendered frame (rather then interpolate it when this flag is unset). In this mode, there are no twitching of physical objects if they have non-linear velocities. If the Engine fps is lower than the physics one, this flag has no effect.
## bool Determinism

The value indicating if objects are updated in a definite order or not. the default is 0 (the update order may change). Deterministic mode ensures that all contacts are solved in the predefined order and visualization of physics in the world is repetitive (on one computer). When this mode is enabled the Engine performs additional sorting of bodies, shapes and joints inside islands after building them. Deterministic mode is unavailable in case there are missed frames - it is simply impossible. Moreover, there may be differences between visualization of physics on different hardware (e.g., AMD and Intel).
> **Notice:** Determinism is guaranteed if there are no missed frames, the same Engine version is used, and the CPUs perform SSE operations similarly.
> Please note that deterministic mode does not come for free, it may eat up 10-20% of the frame rate, and it also depends on the scene a lot.

## bool Enabled

The value indicating if physics simulation is enabled. the default is 1.
## float MissedFrameLifetime

The lifetime for [missed frames](../../../principles/physics/simulation.md#missed_frames). This value defines how long missed frames are to be kept in the catch-up buffer. In case the current Engine framerate is lower than the [fixed Physics framerate](../../../principles/physics/simulation.md#simulation_rate), some of the physics frames get skipped and the simulation starts looking like in a slo-mo effect (e.g., if the target physics framerate is 60 FPS, when the Engine updates at 30 FPS, the simulation will look 2 times slower). The Physics module will try to catch up everything missed later, when possible (e.g. when the Engine framerate grows higher, while [waiting for GPU](../../../code/fundamentals/execution_sequence/index.md#waiting_gpu) to complete rendering). The missed frames are kept in a buffer for some time (lifetime), as it expires the frame is removed from the buffer and becomes lost forever.
## UPDATE_MODE UpdateMode

The [physics update mode](../../../principles/physics/simulation.md#update_mode). Physics can be updated either asynchronously (in parallel with rendering) or in the Main thread before rendering. The [async](#UPDATE_MODE_ASYNC_RENDERING) mode is the fastest one and is used by default, however, it has a one-frame lag (calculation results are applied in the next frame) and some nuances regarding user code execution in some cases.
## bool StableFPS

The value indicating if frame time stabilization is enabled. In case the current Engine framerate is much higher than the [fixed Physics framerate](../../../principles/physics/simulation.md#simulation_rate) (e.g. 120 FPS vs 60 FPS), the physics won't be updated each rendering frame (e.g. it may update during every second frame). The resulting frame time will become unstable, shorter-longer-shorter-longer (*render -> render+physics -> render -> render+physics...*). This option ensures stable frame time for smoother user experience removing unwanted "hiccups" (however, the average framerate is decreased).
> **Notice:** By default, this option is enabled. But you can disable it to increase average framerate in case the application is used for machine learning or for grabbing frame sequences (video grabber), when smoothness is not important.

## bool ShowContacts

The value indicating if the visualization of physical interactions between the physical bodies is enabled.
## SHOW_TYPE ShowShapes

The mode used to visualize physical shapes: one of the [SHOW_TYPE_*](#SHOW_TYPE_DISABLED) values.
## float ShowShapesDistance

The distance within which physical shapes are visualized.
## bool ShowCollisionSurfaces

The value indicating if the collision surface visualization is enabled.
## bool ShowJoints

The value indicating if the visualization of joints that connect physical bodies is enabled.
### Members

---

## Body GetBody ( int id )

Returns a body with a given ID.
### Arguments

- *int* **id** - Body ID.

### Return value

Body with a given ID or **NULL** (0), if there is no body with a given ID.
## bool IsBody ( int id )

Checks if a body with a given ID exists.
### Arguments

- *int* **id** - Body ID.

### Return value

true if a body with a given ID exists; otherwise, false.
## Object GetIntersection ( vec3 p0 , vec3 p1 , int mask , Node [] exclude , PhysicsIntersection intersection )


Performs tracing from the p0 point to the p1 point to find a collision object located on that line. If an object is assigned a body, intersection occurs with its shape. If an object has no body, this function detects intersection with surfaces (polygons) of objects with intersection flag set. Intersection is found only for objects with a matching mask if their ID is not found in the *exclude* list. Intersection does not work for disabled objects.


> **Notice:** This function uses world space coordinates.


### Arguments

- *vec3* **p0** - Line start point coordinates.
- *vec3* **p1** - Line end point coordinates.
- *int* **mask** - Physics intersection mask. If **0** is passed, the function will return **NULL**.
- *[Node](../../../api/library/nodes/class.node_cs.md)[]* **exclude** - Array of nodes to be excluded.
- *[PhysicsIntersection](../../../api/library/physics/class.physicsintersection_cs.md)* **intersection** - [PhysicsIntersection](../../../api/library/physics/class.physicsintersection_cs.md) class instance containing intersection data.

### Return value

The first intersected object, if found; otherwise, 0.
## Object GetIntersection ( vec3 p0 , vec3 p1 , int mask , Node [] exclude , Shape.TYPE [] exclude_types , PhysicsIntersection intersection )


Performs tracing from the p0 point to the p1 point to find a collision object located on that line. If an object is assigned a body, intersection occurs with its shape. If an object has no body, this function detects intersection with surfaces (polygons) of objects with intersection flag set. Intersection is found only for objects with a matching mask if their ID is not found in the *exclude* list and only for shape types not mentioned in the *exclude_types* list. Intersection does not work for disabled objects.


> **Notice:** This function uses world space coordinates.


### Arguments

- *vec3* **p0** - Line start point coordinates.
- *vec3* **p1** - Line end point coordinates.
- *int* **mask** - Physics intersection mask. If **0** is passed, the function will return **NULL**.
- *[Node](../../../api/library/nodes/class.node_cs.md)[]* **exclude** - Array of nodes to be excluded.
- *[Shape.TYPE](../../../api/library/physics/class.shape_cs.md#TYPE)[]* **exclude_types** - Array of shape types to be excluded.
- *[PhysicsIntersection](../../../api/library/physics/class.physicsintersection_cs.md)* **intersection** - [PhysicsIntersection](../../../api/library/physics/class.physicsintersection_cs.md) class instance containing intersection data.

### Return value

The first intersected object, if found; otherwise, 0.
## Object GetIntersection ( vec3 p0 , vec3 p1 , int mask , PhysicsIntersection intersection )


Performs tracing from the p0 point to the p1 point to find a collision object located on that line. If an object is assigned a body, intersection occurs with its shape. If an object has no body, this function detects intersection with surfaces (polygons) of objects with intersection flag set. Physics intersection shall only be detected for objects with a matching [mask](../../../principles/bit_masking/index.md#physics_intersection_mask). Intersection does not work for disabled objects.


> **Notice:** This function uses world space coordinates.


**Usage Example**


The following example shows how you can get the intersection information by using the *PhysicsIntersection* class. In this example we specify a line from the point of the camera *(vec3 p0)* to the point of the mouse pointer *(vec3 p1)*. The executing sequence is the following:


1. Define and initialize two points (p0 and p1) by using the *[Player.GetDirectionFromScreen()](../../../api/library/players/class.player_cs.md#getDirectionFromScreen_Vec3_Vec3_int_int_int_int_int_int_void)* function.
2. Create an instance of the *PhysicsIntersection* class to get the intersection information.
3. Check, if there is an intersection with an object with a shape or a collision object. The *[GetIntersection()](../../../api/library/physics/class.physics_cs.md#getIntersection_Vec3_Vec3_int_Variable)* function returns an intersected object when the object intersects with the traced line.
4. When the object intersects with the traced line, all surfaces of the intersected object change their material parameters. If the object has a shape, its information will be shown in console. The *PhysicsIntersection* class instance gets the coordinates of the intersection point and the *Shape* class object. You can get all these fields by using the *[Shape](../../../api/library/physics/class.physicsintersection_cs.md#getShape_Shape), [Point](../../../api/library/physics/class.physicsintersection_cs.md#getPoint_Vec3)* properties.


```csharp
private void Update()
{
	// initialize points of the mouse direction
	Vec3 p0, p1;

	// get the current player (camera)
	Player player = Game.Player;

	// get the size of the current application window
	EngineWindow main_window = WindowManager.MainWindow;
	if (!main_window)
	{
		Engine.Quit();
		return;
	}

	ivec2 main_size = main_window.Size;

	// get the current X and Y coordinates of the mouse pointer
	int mouse_x = Gui.GetCurrent().MouseX;
	int mouse_y = Gui.GetCurrent().MouseY;
	// get the mouse direction from the player's position (p0) to the mouse cursor pointer (p1)
	player.GetDirectionFromScreen(out p0, out p1, mouse_x, mouse_y, 0, 0, main_size.x, main_size.y);

	// create the instance of the PhysicsIntersection object to save the information about the intersection
	PhysicsIntersection intersection = new PhysicsIntersection();
	// get an intersection
	Unigine.Object obj = Physics.GetIntersection(p0, p1, 1, intersection);

	// if the intersection has occurred, change the parameter of the object's material
	if (obj != null)
	{
		for (int i = 0; i < obj.NumSurfaces; i++)
		{
			obj.SetMaterialParameterFloat4("albedo_color", new vec4(1.0f, 1.0f, 0.0f, 1.0f), i);
		}

		// if the intersected object has a shape, show the information about the intersection
		Shape shape = intersection.Shape;
		if (shape != null)
		{
			Log.Message("physics intersection info: point: ({0} {1} {2}) shape: {3}\n", intersection.Point.x, intersection.Point.y, intersection.Point.z, shape.TypeName);
		}
	}

}


```


### Arguments

- *vec3* **p0** - Line start point coordinates.
- *vec3* **p1** - Line end point coordinates.
- *int* **mask** - Physics intersection mask. If **0** is passed, the function will return **NULL**.
- *[PhysicsIntersection](../../../api/library/physics/class.physicsintersection_cs.md)* **intersection** - [PhysicsIntersection](../../../api/library/physics/class.physicsintersection_cs.md) class instance containing intersection data.

### Return value

The first intersected object, if found; otherwise, 0.
## Object GetIntersection ( vec3 p0 , vec3 p1 , int mask , PhysicsIntersectionNormal intersection )


Performs tracing from the p0 point to the p1 point to find a collision object located on that line. If an object is assigned a body, intersection occurs with its shape. If an object has no body, this function detects intersection with surfaces (polygons) of objects with intersection flag set. Physics intersection shall only be detected for objects with a matching [mask](../../../principles/bit_masking/index.md#physics_intersection_mask). Intersection does not work for disabled objects.


> **Notice:** This function uses world space coordinates.


### Arguments

- *vec3* **p0** - Line start point coordinates.
- *vec3* **p1** - Line end point coordinates.
- *int* **mask** - Physics intersection mask. If **0** is passed, the function will return **NULL**.
- *[PhysicsIntersectionNormal](../../../api/library/physics/class.physicsintersectionnormal_cs.md)* **intersection** - [PhysicsIntersectionNormal](../../../api/library/physics/class.physicsintersectionnormal_cs.md) class instance containing intersection data.

### Return value

The first intersected object, if found; otherwise, 0.
## Object GetIntersection ( vec3 p0 , vec3 p1 , int mask , Node [] exclude , PhysicsIntersectionNormal intersection )


Performs tracing from the p0 point to the p1 point to find a collision object located on that line. If an object is assigned a body, intersection occurs with its shape. If an object has no body, this function detects intersection with surfaces (polygons) of objects with intersection flag set. Intersection is found only for objects with a matching mask if their ID is not found in the *exclude* list. Intersection does not work for disabled objects.


> **Notice:** This function uses world space coordinates.


### Arguments

- *vec3* **p0** - Line start point coordinates.
- *vec3* **p1** - Line end point coordinates.
- *int* **mask** - Physics intersection mask. If **0** is passed, the function will return **NULL**.
- *[Node](../../../api/library/nodes/class.node_cs.md)[]* **exclude** - Array of nodes to be excluded.
- *[PhysicsIntersectionNormal](../../../api/library/physics/class.physicsintersectionnormal_cs.md)* **intersection** - [PhysicsIntersectionNormal](../../../api/library/physics/class.physicsintersectionnormal_cs.md) class instance containing intersection data.

### Return value

The first intersected object, if found; otherwise, 0.
## Joint GetJoint ( int id )

Returns a joint with a given ID.
### Arguments

- *int* **id** - Joint ID.

### Return value

Joint with a given ID or **NULL** (0), if there is no joint with a given ID.
## bool IsJoint ( int id )

Checks if a joint with a given ID exists.
### Arguments

- *int* **id** - Joint ID.

### Return value

true if a joint with a given ID exists; otherwise, false.
## Shape GetShape ( int id )

Returns a shape with a given ID.
### Arguments

- *int* **id** - Shape ID.

### Return value

Shape with a given ID or **NULL** (0), if there is no shape with a given ID.
## bool IsShape ( int id )

Checks if a shape with a given ID exists.
### Arguments

- *int* **id** - Shape ID.

### Return value

true if a shape with a given ID exists; otherwise, false.
## void AddUpdateNode ( Node node )

Adds the node for which physical state should be updated. If a node is not added with this function, it won't be updated when out of physics [simulation distance](#setDistance_float_void).
### Arguments

- *[Node](../../../api/library/nodes/class.node_cs.md)* **node** - Node to be updated.

## void addUpdateNodes ( Node [] nodes )

Adds the nodes for which physical state should be updated. If nodes are not added with this function, they won't be updated when out of physics [simulation distance](#setDistance_float_void).
### Arguments

- *[Node](../../../api/library/nodes/class.node_cs.md)[]* **nodes** - Nodes to be updated.

## bool LoadSettings ( string name )

Loads [physics settings](../../../editor2/settings/physics_global/index.md) from a given file.
### Arguments

- *string* **name** - Path to an XML file with desired settings.

### Return value

true if settings are loaded successfully; otherwise, false.
## bool LoadWorld ( Xml xml )

Loads [physics settings](../../../editor2/settings/physics_global/index.md) from the Xml.
### Arguments

- *[Xml](../../../api/library/common/class.xml_cs.md)* **xml** - Xml node.

### Return value

true if settings are loaded successfully; otherwise, false.
## int SaveScene ( )

Saves the current physics scene (physical properties of all objects) into the buffer with the specified ID.
### Return value

Scene buffer ID.
## int RestoreScene ( bool id )

Restores the previously saved physics scene from the buffer with the specified ID.
### Arguments

- *bool* **id** - ID number of the scene.

### Return value

**true** if the scene was restored successfully; otherwise, **false**.
## bool RemoveScene ( int id )

Removes the previously saved physics scene.
### Arguments

- *int* **id** - ID number of the scene.

### Return value

**true** if the scene was removed successfully; otherwise, **false**.
## bool SaveState ( Stream stream )

Saves [physics settings](../../../editor2/settings/physics_global/index.md) into the stream.
**Example** using saveState() and [restoreState()](#restoreState_Stream_int) methods:


```csharp
// set state
Physics.NumIterations = 1; // NumIterations = 1

// save state
Blob blob_state = new Blob();
Physics.SaveState(blob_state);

// change state
Physics.NumIterations = 16; // now NumIterations = 16

// restore state
blob_state.SeekSet(0);		// returning the carriage to the start of the blob
Physics.RestoreState(blob_state); // restore NumIterations = 1

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream to save settings into.

### Return value

true if settings are saved successfully; otherwise, false.
## bool RestoreState ( Stream stream )

Restores [physics settings](../../../editor2/settings/physics_global/index.md) from the stream.
**Example** using [saveState()](#saveState_Stream_int) and restoreState() methods:


```csharp
// set state
Physics.NumIterations = 1; // NumIterations = 1

// save state
Blob blob_state = new Blob();
Physics.SaveState(blob_state);

// change state
Physics.NumIterations = 16; // now NumIterations = 16

// restore state
blob_state.SeekSet(0);		// returning the carriage to the start of the blob
Physics.RestoreState(blob_state); // restore NumIterations = 1

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream to restore settings from.

### Return value

true if settings are restored successfully; otherwise, false.
## bool SaveSettings ( string name , int force = 0 )

Saves the current [physics settings](../../../editor2/settings/physics_global/index.md) to a given file.
### Arguments

- *string* **name** - Path to a target xml file to which the settings will be saved.
- *int* **force** - Forced saving of physics settings.

### Return value

true if the settings are saved successfully; otherwise, false.
## bool SaveWorld ( Xml xml , int force = 0 )

Saves [physics settings](../../../editor2/settings/physics_global/index.md) to the given Xml node.
### Arguments

- *[Xml](../../../api/library/common/class.xml_cs.md)* **xml** - Xml node.
- *int* **force** - Forced saving of physics settings.

### Return value

**true** if settings are saved successfully; otherwise, **false**.
