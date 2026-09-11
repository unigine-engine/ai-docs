# Scene Management

> **Notice:** The complete sample source code is available on GitHub:
> **[github.com/unigine-engine/cpp-api-samples](https://github.com/unigine-engine/cpp-api-samples)**.


## Bounding Volume Object Detection

This sample demonstrates how to detect [intersections](../../../code/usage/intersections/index.md#worldintersections_nodes) between a frustum, sphere, or box and the bounding boxes of nodes. For clarity, the boundaries of the nodes are displayed in the scene, allowing for a quick visual assessment of when the nodes intersect the specified volumes.


This approach can be used to implement systems for determining which objects fall within a bounding volume and triggering events, such as starting dialogues, spawning enemies, activating effects, or any other reaction.


The *init()* function creates three types of bounding volumes: a frustum, a sphere, and a box. The *update()* function performs the intersection checks. It uses the *[World::getIntersection()](../../../api/library/engine/class.world_cpp.md#getIntersection_WorldBoundBox_VECObject_int)* function to get a list of nodes that intersect the given boundaries and changes their color using the *change_color()* function.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/scene_management/bounding_volume_object_detection*
## Control Elements

Demonstration of various types of interactable buttons and levers.
**SDK Path:***<SAMPLES_PROJECT_PATH>/source/scene_management/control_elements*

## Create And Modify Objects

This sample demonstrates the basics of working with ***[Objects](../../../objects/objects/index.md)*** - how to create and modify objects via API, highlighting the differences between various types of objects (*ObjectMeshStatic, ObjectMeshDynamic, ObjectParticles*). **Objects** are characterized by a set of surfaces, an optional physical body and type-specific properties.


In this sample, we create and configure three types of objects with interactive controls:


**1. [Static Mesh Object](../../../objects/objects/mesh/index.md) (Material Ball)**


- Load an existing **.mesh** file *(material_ball.mesh)*.
- Assigns a material to the object.
- Adds a *[Body](../../../principles/physics/bodies/index.md)* with a *[Box-shaped](../../../principles/physics/shapes/index.md#box)* collision.


**2. [Dynamic Mesh Object](../../../objects/objects/mesh_dynamic/index.md) (Tetrahedron)**


- Constructs a custom *ObjectMeshDynamic* manually.
- Applies a glass-like material.
- Adds a *[Body](../../../principles/physics/bodies/index.md)* with a *[Sphere-shaped](../../../principles/physics/shapes/index.md#sphere)* collision.


**3. [Particle System](../../../objects/effects/particles/index.md)**


- Creates a default *ObjectParticles* object.
- Configures *[particle-specific parameters](../../../objects/effects/particles/index.md#emitter_parameters)*, such as spawn rate and lifetime, and enables a *[collision mask](../../../principles/bit_masking/index.md#collision_mask)* for particle interaction.


**Runtime Modifications (via Sample Menu)**


- Adjust the albedo color of the **Static Mesh** material.
- Modify the mesh (tetrahedron base height) in the **Dynamic Mesh**.
- Tune the spawn rate of the **Particle System**.
- Toggle the visualization of surfaces and physical shapes of the objects.


For more complex objects, such as *[ObjectLandscapeTerrain](../../../sdk/api_samples/cpp/terrain_modification_usage.md)*, see the corresponding samples.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/scene_management/create_and_modify_objects*
## Create Mesh Primitives

This sample demonstrates how to create parametric 3D primitives at runtime in UNIGINE.


It showcases the use of the **[Mesh](../../../api/library/rendering/class.mesh_cpp.md)** class and **[ObjectMeshDynamic](../../../objects/objects/mesh_dynamic/index.md)** nodes to procedurally generate a variety of basic shapes (**Box, Sphere, Cylinder, Capsule, Prism with a custom number of sides** and **Plane**) via code.


Each shape is constructed with a customizable size and resolution, added to a mesh surface, and placed in the world at a designated position.


This approach allows dynamic geometry generation for tools, Editor extensions, procedural environments, and rapid prototyping.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/scene_management/create_mesh_primitives*
## Day-Night Cycle

This sample showcases a dynamic day-night cycle driven by the rotation of a **[World Light](../../../objects/lights/world/index.md)** source (sun), animated according to a simulated global time. The sun's position is updated continuously or in response to manual time input. The time progression speed can be adjusted using the *Timescale* slider.


The sun's orientation influences both the overall scene lighting and object-specific responses, enabling or disabling nodes and adjusting the emission states of designated materials depending on whether it's currently day or night. Additional props, such as **[Projected Light](../../../objects/lights/proj/index.md)** node and door closed/open signage, are toggled to reflect the time of day. Red and blue helper vectors visualize the zenith direction and the sun's current orientation, respectively.


**Two control modes are available:**


- **Zenith Angle**: Uses the angle between the sun's direction and the zenith (up vector). If the angle is below a threshold, it is considered daytime.
- **Time-Based**: Defines day/night using configurable *Morning* and *Evening hour boundaries* sliders.


**Use Cases:**


Ideal for **games, simulations**, or **architectural walkthroughs** that need consistent lighting transitions and dynamic environmental response.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/scene_management/day_night_cycle*
## Move By Trajectory

This sample demonstrates three types of movement along a predefined path:


- **Red plane**: linear interpolation.
- **Blue plane**: spline interpolation.
- **Green plane**: path from a file.


The sample contains the *PathTrajectorySaver* component that illustrates how to create your own path file, which is opened via the *[WorldTransformPath](../../../api/library/worlds/class.worldtransformpath_cpp.md)* node.


In the Parameters section, you can toggle **path visualization** on and off, adjust the planes' **velocity**, or **switch between the cameras** to have a first-person view from each plane.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/scene_management/move_by_trajectory*
## Nodes And Widgets Lifetime Control

This sample demonstrates how node and widget lifetime settings affect object persistence during world transitions.


At startup, the sample creates a plane node and a screen button, each with configurable lifetime modes. Switch the widget between **WORLD** and **WINDOW** lifetime modes, and the node between **WORLD** and **ENGINE** modes.


Use the `world_load world_name` console command (e.g., `world_load arcade`) to switch worlds and observe how different lifetime settings affect object survival. *WORLD-lifetime* objects exist only in the current world, while *ENGINE-lifetime* nodes and *WINDOW-lifetime* widgets remain active after loading a different world.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/scene_management/nodes_and_widgets_lifetime_control*
## Node Movement

This sample compares three approaches to 3D object movement and rotation using different node transformation methods, and illustrates that using either of them leads to the same result:


Red cube is controlled using *[translate()](../../../api/library/nodes/class.node_cpp.md#translate_Vec3_void)* and *[rotate()](../../../api/library/nodes/class.node_cpp.md#rotate_quat_void)*.


Green cube: *[setPosition()](../../../api/library/nodes/class.node_cpp.md#setPosition_Vec3_void)* and *[setRotation()](../../../api/library/nodes/class.node_cpp.md#setRotation_quat_int_void)*.


Blue cube: *[setTransform()](../../../api/library/nodes/class.node_cpp.md#setTransform_Mat4_void)*.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/scene_management/node_movement*
## Node State Save-Restore

This sample demonstrates how to save and restore the state of an arbitrary Node using the *saveState()* and *restoreState()* methods. In this sample we:


- At *Initialization* create a ***[Blob](../../../api/library/common/class.blob_cpp.md)*** container for state storage and save the initial state of the referenced node.
- Enable visualizer (a semi-transparent box) at saved position for visualization.
- Save and restore the Node's state at any time by clicking the sample UI panel's *Save* and *Restore* buttons.


**Use Cases**:


- Game saves
- Undo/Redo systems
- Scene serialization


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/scene_management/node_state_save_restore*
## Raycast Detection And Bitmasking

This sample demonstrates how to find [intersections](../../../code/usage/intersections/index.md#worldintersections_object) with geometry using **raycasting** taking into account different *Intersection* bitmasks (using first 8 bits out of 32).


Raycasting involves detecting intersections with scene objects along the path of a ray cast from point **A** to point **B**. This process is visualized in the sample via a laser ray representation (laser length depends on the ray length).


In the *update()* method, the *[World::getIntersection()](../../../api/library/engine/class.world_cpp.md#getIntersection_Vec3_Vec3_int_Object)* function checks for ray intersections with scene objects based on a specified intersection mask. If the ray hits an object with a matching mask (one bit at least), an intersection is detected. After that, the ray is updated and visual spark effects are rendered at the intersection point.


You can change the laser's intersection mask by toggling the corresponding checkboxes. If a wall's mask bit doesn't match the laser's mask, the laser will pass through.


Using raycasting makes it easy to implement various game mechanics, such as shooting or target detection during navigation.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/scene_management/raycast_detection_and_bitmasking*
## Raycast From Mouse Position

This sample demonstrates how to find an intersection between a ray cast from the camera through the mouse cursor and geometry.


The *MouseRayIntersection* component shows how to use *[World::getIntersection()](../../../api/library/engine/class.world_cpp.md#getIntersection_Vec3_Vec3_int_Object)* to detect static mesh objects intersected by a ray cast from the player's position in the direction pointed by the mouse cursor.


The name of the hit object is displayed next to the cursor on the screen.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/scene_management/raycast_from_mouse_position*
## Trigger System Examples

This sample illustrates how to implement a simple trigger component in five different ways:


- **Intersection Trigger** performs the bound check via *[World::getIntersection()](../../../api/library/engine/class.world_cpp.md#getIntersection_Vec3_Vec3_int_VECNode_Object)*.
- **Math Trigger** performs the check if the object is inside the trigger sphere or cube using the object coordinates (the simplest and most performance-friendly way).
- **World Trigger** uses the built-in *[WorldTrigger](../../../api/library/worlds/class.worldtrigger_cpp.md)* node, which automatically detects when nodes enter or leave a predefined volume.
- **Physical Trigger** uses the built-in *[PhysicalTrigger](../../../api/library/physics/class.physicaltrigger_cpp.md)* node, triggers events when a physical object gets inside or outside it. To be detected by the trigger, physical objects are required to have at the same time both a body and a shape.
- **Node Trigger** uses the built-in *[NodeTrigger](../../../api/library/nodes/class.nodetrigger_cpp.md)* node, which has no visual representation and triggers events when being enabled or moved. Press *Cube Active* to see Node Trigger in action. This checkbox toggles the demonstration cube on/off, triggering enable/disable events that change the plate text color and animate the cube's material when it's moved with a manipulator (click the cube for the manipulator to appear).


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/scene_management/trigger_system_examples*
