# Nodes

> **Notice:** The complete sample source code is available on GitHub:
> **[github.com/unigine-engine/cpp-api-samples](https://github.com/unigine-engine/cpp-api-samples)**.


## Cluster

This sample demonstrates dynamic manipulation of **[ObjectMeshCluster](../../../objects/objects/mesh_cluster/index.md)** in UNIGINE, showcasing how to add/remove mesh instances at runtime through user interaction. A **Mesh Cluster** allows you to bake identical meshes (with the same material applied to their surfaces) into a single object, which provides less cluttered spatial tree, reduces the number of texture fetches and speeds up rendering.


**Core Features:**


- **Placement and Removal** - click on empty ground adds a new mesh at the clicked position, click on existing cluster geometry removes the selected mesh instance from the cluster
- **Raycasting and Intersection Testing** - casts a ray from the camera through the mouse position to detect whether the user clicked on a cluster mesh or terrain


**Use Cases:**


- Scattering objects like rocks, grass, or debris
- Dynamic level editing and environment design
- Performance-sensitive applications with many similar mesh instances.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/nodes/cluster*
## Lights

This sample demonstrates how to create light sources and modify their parameters at runtime:


- **[World Light](../../../objects/lights/world/index.md)** - an infinitely remote light source casting orthographically projected beams onto the scene.
- **[Projected Light](../../../objects/lights/proj/index.md)** - a light source that casts light from a single point forming a focused beam aimed in a specific direction.
- **[Omni Light](../../../objects/lights/omni/index.md)** - a point source emitting light in all directions (360 degrees) and realistically reproducing shadow cast.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/nodes/lights*
## Node Extern

UNIGINE allows you to extend its out-of-the-box functionality in various ways, including adding custom nodes with personalized behavior, functions, and visualization (if needed).


This sample demonstrates how to implement a custom user node based on the **[NodeExtern](../../../api/library/nodes/class.nodeextern_cpp.md)** class, featuring bounding box visualization and runtime configuration of node parameters (e.g., bounding box color). These nodes can then be added to your scene via API.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/nodes/node_extern*
## Object Extern

UNIGINE allows you to extend its out-of-the-box functionality in various ways, including adding your own objects with custom geometry and behavior (e.g., custom particle systems, meshes with custom culling, animated GPU-based crowd rendering solutions, etc.).


This sample demonstrates how to implement custom user objects based on the **[ObjectExtern](../../../api/library/objects/class.objectextern_cpp.md)** class, incorporating custom rendering, physics, and properties, while maintaining full Engine integration. These objects can then be added to your scene via API.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/nodes/object_extern*
## Player Types

This sample demonstrates how to create and configure the four available **[Players](../../../objects/players/index.md)**:


- **[PlayerDummy](../../../objects/players/dummy/index.md)** - a manually controlled camera that has no physical properties and cannot collide with objects.
- **[PlayerPersecutor](../../../objects/players/persecutor/index.md)** - a third-person chase camera that follows a target with adjustable distance.
- **[PlayerSpectator](../../../objects/players/spectator/index.md)** - a free-fly camera without a physical body.
- **[PlayerActor](../../../objects/players/actor/index.md)** - a player with a rigid physical body, which is approximated with a capsule and has physical properties. Can only walk on the ground.


Each player is instantiated with appropriate settings (collision, movement parameters, camera settings), and a GUI panel lets you **switch between them at runtime**. You can also modify camera parameters like **FOV and near/far clipping planes**.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/nodes/players_types*
## Spline Graph

This sample demonstrates how to create and visualize a spline graph (***[SplineGraph](../../../api/library/worlds/class.splinegraph_cpp.md)***), and move an object along it. A **SplineGraph** is created at *Initialization* by adding points and segments using the *addPoint(), addSegment()* API methods, with control points placed randomly.


- A cube mesh is created and added to the scene.
- During the *Update* stage, the cube moves along the spline by switching between its consecutive segments and evaluating a point on it using the *calcSegment** methods.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/nodes/spline_graph*
## Water Surface Parameters Fetch

This sample demonstrates how various parameters influence the accuracy of **fetch** (sampling water height and normal) and **intersection** (ray-water collision detection) operations on the **[Global Water](../../../objects/objects/water/water_object.md)** object across different **[Beaufort](../../../objects/objects/water/water_object.md#creating_waves)** levels (the Beaufort slider).


You can interactively adjust the following parameters:


- **Steepness Quality**: Controls wave detail resolution used in sampling.
- **Amplitude Threshold**: Filters out minor waves to improve performance at the cost of detail.
- **Precision**: Controls ray-water intersection accuracy. Lower values reduce jitter when intersecting at an angle.
- **Intersection Angle**: Adjusts the incoming ray direction for intersection tests, helping evaluate how steep angles affect detection stability.


The UI also allows you to:


- Select between **Fetch** and **Intersection** modes
- Show or hide **normals** at the sampled points
- Adjust the **number of samples** and **visual point size**


> **Notice:** Intersection rays are visualized with blue arrows. If jitter occurs at non-zero intersection angles, try lowering the **Precision** value.


This sample is useful for fine-tuning water interaction accuracy in physics, gameplay, and visual effects - especially when working with sloped or moving viewpoints (e.g., cameras, characters, or objects interacting with water).


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/nodes/water_surface_parameters_fetch*
## Water Waves Customization Gerstner

This sample demonstrates how to control the wave spectrum of **[Global Water](../../../objects/objects/water/water_object.md)** in **Manual** mode via API over wave parameters (octaves - a set of waves at a specific size/frequency level, count per octave, length, amplitude, phase, and steepness).


Because all wave parameters are managed on the CPU side, they can be dynamically generated, modified, or stored for reproducible results and external integration (for example, to process Weather Control packets from IOS).


> **Notice:** The maximum number of waves is 256, but higher values significantly affect performance, so we recommend keeping the number below 100 and using the minimum possible number.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/nodes/water_waves_customization_gerstner*
## Water Waves Generation Field Height

The sample illustrates the effect of simulating waves on a water surface, which is created using the **[Field Height](../../../objects/effects/fields/field_height/index.md)** object.


The code generates a heightmap that is dynamically modulated over time by a sinusoidal function, resulting in an oscillating visual representation.


This approach can be useful for creating ship wake waves, water disturbances around floating objects such as buoys, and more.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/nodes/water_waves_generation_field_height*
## World Spline Graph

This sample demonstrates how to integrate a spline-based geometry system into a world environment.


A *[WorldSplineGraph](../../../api/library/worlds/class.worldsplinegraph_cpp.md)* class instance is created and populated with data from an external `*.spl` file, which defines the spatial structure of the graph. Geometry is then applied to each segment using a predefined `*.node` file, rendered in stretching mode to ensure it conforms seamlessly to the shape and length of each spline.


This approach allows for the efficient construction of roads, pipelines, rails, and other continuous structures within the world.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/nodes/world_spline_graph*
