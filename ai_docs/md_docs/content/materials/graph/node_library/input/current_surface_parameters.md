# Current Surface Parameters Node


![](../img/current_surface_parameters.png)

### Description

Reads the [custom parameters](../../../../../content/materials/custom_parameters/reading_parameters.md) of the surface being shaded. Unlike [Surface Parameters](../../../../../content/materials/graph/node_library/input/surface_parameters.md), this node samples no screen buffer: it takes the ID the renderer passes to the shader together with the draw call.


That ID reaches every pass whatever the write state of the material, so the node works in the material's own pass while the Surface ID Buffers are still being filled - which is what lets a value change the appearance of the surface it belongs to, a wetness darkening the albedo or a wear value fading a decal.


The node is not available in a post-effect graph: such a graph runs over the finished frame and has no current surface. Use *Scene Surface Parameters* there instead.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/int.png) | **Node ID** | ID of the node the surface belongs to. |
| ![](../img/types/int.png) | **Surface** | Number of the surface within that node. This is not the Surface ID, which is never exposed as a port. |
| ![](../img/types/int.png) | **Instance** | Number of the instance for a [Mesh Cluster](../../../../../objects/objects/mesh_cluster/index.md), whose instances carry values of their own. |
| ![](../img/types/int.png) | **Material ID** | ID of the material assigned to the surface. |
| ![](../img/types/int.png) | **Light Map** | Feature bit: the surface is lit by a [lightmap](../../../../../editor2/lighting/gi/lightmaps.md). |
