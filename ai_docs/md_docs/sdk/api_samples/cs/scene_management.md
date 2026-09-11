# Scene Management

> **Notice:** The complete sample source code is available on GitHub:
> **[github.com/unigine-engine/csharp-component-samples](https://github.com/unigine-engine/csharp-component-samples)**.


## Bounding Box Object Detection

This sample demonstrates how to find an intersection between the bound box and geometry.


The *BoundBoxIntersection.cs* component shows how to use *[World.GetIntersection()](../../../api/library/engine/class.world_cpp.md#getIntersection_Vec3_Vec3_int_Object)* to detect static mesh objects located within a specified world-space axis-aligned bounding box. The box is highlighted using the *[Visualizer](../../../api/library/engine/class.visualizer_cpp.md)*, and intersected object names are printed to the onscreen console overlay.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/scene_management/bounding_box_object_detection*
## Bounding Frustum Object Detection

This sample demonstrates how to find an intersection between the bound frustum and geometry.


The *BoundFrustumIntersection.cs* component shows how to use *[World.GetIntersection()](../../../api/library/engine/class.world_cpp.md#getIntersection_Vec3_Vec3_int_Object)* to detect static mesh objects located inside a perspective frustum defined in world coordinates. The frustum is highlighted using the *[Visualizer](../../../api/library/engine/class.visualizer_cpp.md)*, and intersected object names are printed to the onscreen console overlay.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/scene_management/bounding_frustum_object_detection*
## Bounding Sphere Object Detection

This sample demonstrates how to find an intersection between the bound sphere and geometry.


The *BoundSphereIntersection.cs* component shows how to use *[World.GetIntersection()](../../../api/library/engine/class.world_cpp.md#getIntersection_Vec3_Vec3_int_Object)* to detect static mesh objects located within a spherical volume defined in world coordinates. The sphere is highlighted using the *[Visualizer](../../../api/library/engine/class.visualizer_cpp.md)*, and intersected object names are printed to the onscreen console overlay.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/scene_management/bounding_sphere_object_detection*
## Create Mesh Primitives

This sample demonstrates how to create parametric 3D primitives at runtime in UNIGINE.


It showcases the use of the **[Mesh](../../../api/library/rendering/class.mesh_cpp.md)** class and **[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cpp.md)** nodes to procedurally generate a variety of basic shapes (**Box, Sphere, Cylinder, Capsule, Prism with a custom number of sides** and **Plane**) via code.


Each shape is constructed with a customizable size and resolution, added to a mesh surface, and placed in the world at a designated position.


This approach allows dynamic geometry generation for tools, Editor extensions, procedural environments, and rapid prototyping.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/scene_management/create_mesh_primitives*
## Day-Night Cycle

This sample showcases a dynamic day-night cycle driven by the rotation of a **[World Light](../../../objects/lights/world/index.md)** source (sun), animated according to a simulated global time. The sun's position is updated continuously or in response to manual time input. The time progression speed can be adjusted using the *Timescale* slider.


The sun's orientation influences both the overall scene lighting and object-specific responses, enabling or disabling nodes and adjusting the emission states of designated materials depending on whether it's currently day or night. Additional props, such as **[Projected Light](../../../objects/lights/proj/index.md)** node and door closed/open signage, are toggled to reflect the time of day. Red and blue helper vectors visualize the zenith direction and the sun's current orientation, respectively.


**Two control modes are available:**


- **Zenith Angle**: Uses the angle between the sun's direction and the zenith (up vector). If the angle is below a threshold, it is considered daytime.
- **Time-Based**: Defines day/night using configurable *Morning* and *Evening hour boundaries* sliders.


**Use Cases:**


Ideal for **games, simulations**, or **architectural walkthroughs** that need consistent lighting transitions and dynamic environmental response.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/scene_management/day_night_cycle*
## Local vs World Space Transforms

This sample demonstrates the difference between local and world transformations. Local transformations are affected by the object's current orientation (movement follows rotation), while world transformations remain consistent regardless of rotation (movement in fixed global directions).


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/scene_management/local_vs_world_space_transforms*
## Move By Trajectory

This sample demonstrates three types of movement along a predefined path:


- **Red plane**: linear interpolation.
- **Blue plane**: spline interpolation.
- **Green plane**: path from a file.


The sample contains the *PathTrajectorySaver* component that illustrates how to create your own path file, which is opened via the *[WorldTransformPath](../../../api/library/worlds/class.worldtransformpath_cpp.md)* node.


In the Parameters section, you can toggle path visualization on and off, adjust the planes' velocity, or switch between the cameras to have a first-person view from each plane.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/scene_management/move_by_trajectory*
## Nodes And Widgets Lifetime Control

This sample demonstrates how node and widget lifetime settings affect object persistence during world transitions.


At startup, the sample creates a plane node and a screen button, each with configurable lifetime modes. Switch the widget between **WORLD** and **WINDOW** lifetime modes, and the node between **WORLD** and **ENGINE** modes.


Use the `world_load world_name` console command (e.g., `world_load arcade`) to switch worlds and observe how different lifetime settings affect object survival. *WORLD-lifetime* objects exist only in the current world, while *ENGINE-lifetime* nodes and *WINDOW-lifetime* widgets remain active after loading a different world.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/scene_management/nodes_and_widgets_lifetime_control*
## Node Movement

This sample compares three approaches to object movement and rotation using different node transformation methods, and illustrates that using either of them leads to the same result:


**Red cube** is controlled using *[Translate()](../../../api/library/nodes/class.node_cpp.md#translate_Vec3_void)* and *[Rotate()](../../../api/library/nodes/class.node_cpp.md#rotate_quat_void)*.


**Green cube** uses *[Position()](../../../api/library/nodes/class.node_cpp.md#setPosition_Vec3_void)* and *[SetRotation()](../../../api/library/nodes/class.node_cpp.md#setRotation_quat_int_void)*.


**Blue cube** uses *[Transform()](../../../api/library/nodes/class.node_cpp.md#setTransform_Mat4_void)*.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/scene_management/node_movement*
## Node Spawning And Deletion

This sample demonstrates how to dynamically create and delete node instances at runtime in UNIGINE.


A specified **.node** asset is instantiated repeatedly at timed intervals, with each new instance positioned in a grid pattern. Once a certain number of nodes are active, the oldest ones are automatically removed (first-in, first-out deletion) to maintain a fixed, memory-safe maximum count in the scene.


**Use Cases:**


- Object pooling and controlled instancing
- Spawning projectiles, enemies, or temporary effects.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/scene_management/node_spawning_and_deletion*
## Raycast Detection And Bitmasking

This sample demonstrates how to find an intersection of a ray with geometry.


The *LaserRayIntersection.cs* component casts a ray from the laser origin in its forward direction and uses *[World.GetIntersection()](../../../api/library/engine/class.world_cpp.md#getIntersection_Vec3_Vec3_int_WorldIntersection_Object)* to detect intersections with geometry. The method provides both the intersection point and the surface normal. Intersected object names are printed to the onscreen console overlay.


If a hit is detected, the laser beam is resized to visually represent the exact distance between its origin and the intersection point. The hit effect object is shown at the intersection point, oriented in accordance with the surface normal. If no intersection is found, the laser beam keeps its default length and the effect remains hidden.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/scene_management/raycast_detection_and_bitmasking*
## Raycast From Mouse Position

This sample demonstrates how to find an intersection between a ray cast from the camera through the mouse cursor and geometry.


The *MouseRayIntersection.cs* component shows how to use *[World.GetIntersection()](../../../api/library/engine/class.world_cpp.md#getIntersection_Vec3_Vec3_int_Object)* to detect static mesh objects intersected by a ray cast from the player's position in the direction pointed by the mouse cursor.


The name of the hit object is displayed next to the cursor on the screen.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/scene_management/raycast_from_mouse_position*
## Trigger System Examples

This sample illustrates how to implement a simple trigger component in five different ways:


- **Intersection Trigger** performs the bound check via *[World.GetIntersection()](../../../api/library/engine/class.world_cpp.md#getIntersection_Vec3_Vec3_int_VECNode_Object)*.
- **Math Trigger** performs the check if the object is inside the trigger sphere or cube using the object coordinates (the simplest and most performance-friendly way).
- **World Trigger** uses the built-in *[WorldTrigger](../../../api/library/worlds/class.worldtrigger_cpp.md)* node, which automatically detects when nodes enter or leave a predefined volume.
- **Physical Trigger** uses the built-in *[PhysicalTrigger](../../../api/library/physics/class.physicaltrigger_cpp.md)* node, triggers events when a physical object gets inside or outside it. To be detected by the trigger, physical objects are required to have at the same time both a body and a shape.
- **Node Trigger** uses the built-in *[NodeTrigger](../../../api/library/nodes/class.nodetrigger_cpp.md)* node, which has no visual representation and triggers events when being enabled or moved. Press *Cube Active* to see Node Trigger in action. This checkbox toggles the demonstration cube on/off, triggering enable/disable events that change the plate text color and animate the cube's material when it's moved with a manipulator (click the cube for the manipulator to appear).


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/scene_management/trigger_system_examples*
