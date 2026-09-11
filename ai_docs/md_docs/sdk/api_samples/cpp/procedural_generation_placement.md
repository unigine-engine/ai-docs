# Procedural Generation & Placement

> **Notice:** The complete sample source code is available on GitHub:
> **[github.com/unigine-engine/cpp-api-samples](https://github.com/unigine-engine/cpp-api-samples)**.


## Clutter-To-Cluster Converter

![](../../../samples/img/cpp_samples_clutter_to_cluster_converter.jpg)

This sample demonstrates how to dynamically generate a clutter (**[ObjectMeshClutter](../../../objects/objects/mesh_clutter/index.md)**) and convert it into an optimized cluster (**[ObjectMeshCluster](../../../objects/objects/mesh_cluster/index.md)**) in real time. The clutter is generated using a random seed, and the conversion process transfers all key parameters from the clutter: materials, surface properties, LOD, shadows, physics, and collision settings.


The resulting cluster inherits the clutter's transform and hierarchy, but lets you **selectively edit and remove individual elements** of the group. Very often when building your worlds it is necessary to scatter meshes across a certain area randomly and then reposition some of them manually (e.g. when creating forests).


**UI Features:**


- **Generate Clutter** - Creates a randomized layout of clutter meshes.
- **Convert to Cluster** - Merges all clutter instances into a single **[ObjectMeshCluster](../../../objects/objects/mesh_cluster/index.md)** with identical visual/physical behavior.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/procedural_generation_placement/clutter_to_cluster_converter*
## Grid-Based Node Spawning

This sample shows how to create nodes and place them across a configurable grid.


Adjust grid dimensions, cell size, and toggle between spawning from corner or center pivot.


The system automatically clears and regenerates the entire grid when parameters are changed, providing real-time visualization of layout modifications.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/procedural_generation_placement/grid_based_node_spawning*
## Procedural Mesh Generation

This sample demonstrates how to generate static mesh geometry at runtime using different procedural mesh generation methods. A grid of *ObjectMeshStatic* objects is created, each receiving its geometry from a user-defined callback that builds a box-shaped mesh surface via the *[Mesh API](../../../api/library/rendering/class.mesh_cpp.md#addBoxSurface_cstr_vec3_int_int)*.


You can experiment with various [procedural modes](../../../api/library/objects/class.objectmeshstatic_cpp.md#PROCEDURAL_MODE) (such as *Dynamic, File*, or *Blob*), as well as configure how geometry is stored and accessed by selecting different [MeshRender usage flags](../../../api/library/rendering/class.meshrender_cpp.md#Flags) (DirectX 12 only). These flags determine whether vertex and/or index data is kept in RAM instead of VRAM, allowing the GPU to render directly from system memory.


- **Dynamic** - fastest performance, stored in RAM and VRAM, not automatically unloaded from memory.
- **Blob** - moderate performance, stored in RAM and VRAM, automatically unloaded from memory.
- **File** - slowest performance, all data stored on disk, automatically unloaded from memory.


The **Field Size** parameter defines how many mesh objects are generated along each axis, forming a square grid.


For each configuration, the sample shows total RAM and VRAM usage, along with the number of active mesh objects. This makes it easier evaluate the performance, memory layout, and behavior of each procedural mode in different runtime conditions.


Use this sample to understand how procedural mesh generation works across different modes, observe how geometry is stored and managed between RAM, VRAM, and disk, profile memory usage for small versus large number of procedural objects, and explore how update strategies influence performance.


Refer to the [Procedural Mesh Workflow](../../../api/library/objects/class.objectmeshstatic_cpp.md#procedural_workflow) article for more details on memory behavior, update strategies, and best practices when working with procedural geometry.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/procedural_generation_placement/procedural_mesh_generation*
## Procedural Mesh Modification

This sample demonstrates how to dynamically generate, modify, and apply procedural geometry at runtime using different procedural mesh modification methods.


The dynamic surface mesh being built and animated over time using trigonometric functions. The geometry is rebuilt each frame depending on current configuration.


You can experiment with various [procedural modes](../../../api/library/objects/class.objectmeshstatic_cpp.md#PROCEDURAL_MODE) (such as *Dynamic, File*, or *Blob*), as well as configure how geometry is stored and accessed by selecting different [MeshRender usage flags](../../../api/library/rendering/class.meshrender_cpp.md#Flags) (DirectX 12 only). These flags determine whether vertex and/or index data is kept in RAM instead of VRAM, allowing the GPU to render directly from system memory.


Additionally, you can choose whether mesh generation occurs on the **Main** thread or in the **Background**, giving you more control over performance and responsiveness during updates.


- **Dynamic** - fastest performance, stored in RAM and VRAM, not automatically unloaded from memory.
- **Blob** - moderate performance, stored in RAM and VRAM, automatically unloaded from memory.
- **File** - slowest performance, all data stored on disk, automatically unloaded from memory.


You can also toggle between different update modes (*Async* or *Force*), choose memory transfer strategies (*Copy* or *Move*), and optionally enable manual control of the *MeshRender*, where you update its content explicitly after modifying mesh data, instead of relying on automatic updates. Additionally, collision data can be generated explicitly after geometry modification, as it is not created automatically.


Use this sample to understand how procedural mesh modification works across different configurations and explore how update strategies influence performance.


Refer to the [Procedural Mesh Workflow](../../../api/library/objects/class.objectmeshstatic_cpp.md#procedural_workflow) article for more details on memory behavior, update strategies, and best practices when working with procedural geometry.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/procedural_generation_placement/procedural_mesh_modification*
## Procedural Mesh Updates Mesh Clusters

This sample demonstrates the correct order of operations for modifying and applying procedural mesh data at runtime. It serves as a minimal example showing how to build geometry, configure procedural mode, and apply changes to an *[ObjectMeshCluster](../../../api/library/objects/class.objectmeshcluster_cpp.md)*.


The same workflow and apply methods are also available for other objects that support procedural meshes, such as *[ObjectMeshStatic](../../../api/library/objects/class.objectmeshstatic_cpp.md)*, *[ObjectGuiMesh](../../../api/library/objects/class.objectguimesh_cpp.md)*, *[DecalMesh](../../../api/library/decals/class.decalmesh_cpp.md)*, and *[ObjectMeshClutter](../../../api/library/objects/class.objectmeshclutter_cpp.md)*.


Inside the component's code, you'll find a linear implementation of the procedural mesh pipeline, demonstrating how geometry is generated and applied in the correct order.


Use this sample to understand the basic flow of procedural mesh updates and try adjusting configurations to find what best suits your needs.


Refer to the [Procedural Mesh Workflow](../../../api/library/objects/class.objectmeshstatic_cpp.md#procedural_workflow) article for more details on memory behavior, update strategies, and best practices when working with procedural geometry.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/procedural_generation_placement/procedural_mesh_updates_mesh_clusters*
## Procedural Spline Mesh Generation

This sample demonstrates procedural generation of spline-based meshes using world points as control nodes. The system creates three geometric types: **RIBBON, SQUARE PIPE**, and **ROUND PIPE**, with adjustable width, subdivision level, and segment length. UV mapping parameters allow texture tiling and stretching control along both length and width.


The generated mesh updates in real-time as control points are manipulated (supporting movement along single axes or planar constraints), with a visualizer showing the spline path and wireframe. An interactive interface provides controls for all generation parameters and mesh type switching.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/procedural_generation_placement/procedural_spline_mesh_generation*
## Real-Time Mesh Editing Marching Cubes

This sample demonstrates a simulation of ground digging, modification of a terrain fragment represented by a mesh via API. The fragment of the ground surfaces is generated using the Marching Cubes algorithm.


Click **LMB** to dig the ground at a certain point (the cutting sphere is visualized around the cursor). Set the desired radius of the cutting sphere (*Digging Radius*) defining the volume of ground to be removed.


**Hold Ctrl + LMB** to add volume instead.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/procedural_generation_placement/real_time_mesh_editing_marching_cubes*
## Timer-Based Node Spawning

This sample demonstrates a configurable node spawner that creates objects at defined intervals. The spawn frequency can be adjusted in real-time, with a visual indicator showing the current spawn cycle progress through a color-changing sphere.


The sample will be useful for generating game objects with a certain periodicity - for example, enemies, bonuses, effects or other elements of the game world.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/procedural_generation_placement/timer_based_node_spawning*
