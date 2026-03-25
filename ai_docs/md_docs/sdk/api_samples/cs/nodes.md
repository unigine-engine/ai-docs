# Nodes

> **Notice:** The complete sample source code is available on GitHub:
> **[github.com/unigine-engine/csharp-component-samples](https://github.com/unigine-engine/csharp-component-samples)**.


## Cluster

This sample demonstrates dynamic manipulation of **[ObjectMeshCluster](../../../objects/objects/mesh_cluster/index.md)** in UNIGINE, showcasing how to add/remove mesh instances at runtime through user interaction. A **Mesh Cluster** allows you to bake identical meshes (with the same material applied to their surfaces) into a single object, which provides less cluttered spatial tree, reduces the number of texture fetches and speeds up rendering.


**Core Features:**


- **Placement and Removal** - click on empty ground adds a new mesh at the clicked position, click on existing cluster geometry removes the selected mesh instance from the cluster
- **Raycasting and Intersection Testing** - casts a ray from the camera through the mouse position to detect whether the user clicked on a cluster mesh or terrain


**Use Cases:**


- Scattering objects like rocks, grass, or debris
- Dynamic level editing and environment design
- Performance-sensitive applications with many similar mesh instances.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/nodes/cluster*
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


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/nodes/water_surface_parameters_fetch*
