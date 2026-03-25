# Triplanar Color Node


![](../img/triplanar_color.png)

### Description

Samples the color data of the **Texture2D** texture using triplanar mapping.


It's enough to simply pass the texture to the node to get a working [triplanar projection](../../../../../content/materials/library/mesh_base/index.md#uv_base), all the other inputs have appropriate default values.


If you want to fine tune the result override the input parameters. Please note that Vertex Position and Vertex Normal inputs must be in the same space:


- **Object Space** for object-space triplanar mapping.
- **World Space** for world-space triplanar mapping.


> **Notice:** **World-space** triplanar mapping works properly only within the distance range of 10000 units from the origin (regardless of the supported [precision of coordinates](../../../../../code/double_precision/index.md)).


#### Ports

| Name | Description |
|---|---|
| **Texture2D** | Color texture. |
| **Vertex Position** | Vertex position of the geometry. Specify it if you deformed the source geometry. |
| **Vertex Normal** | Vertex normals of the geometry. Specify it if you modified the source geometry normals or to take into account some normal map. |
| **Blend** | Blending intensity between the projection axes, in the [0; 1] range. |
| **Tiling** | Tiling along each projection axis. |
| **Offset** | Offset along each projection axis. |
| **Triplanar Color** | Color sampled from the input texture. |
