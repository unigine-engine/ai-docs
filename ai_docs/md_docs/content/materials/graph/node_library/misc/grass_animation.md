# Grass Animation Node


![](../img/grass_animation.png)

### Description

This node simulates skewing and bending of grass chunks by offsetting vertex positions based on the input wind settings.


## Usage Example

| [**View Fullscreen**](https://matgraph.unigine.com/DocsGrassAnimation_2.21/fullView) |
|---|

#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/float.png) | **Wind Animation Tiling** | Controls frequency of the wind animation pattern. |
| ![](../img/types/float.png) | **Wind Animation Speed** | Determines how fast wind animation moves. |
| ![](../img/types/float.png) | **Wind Animation Intensity** | Determines how much an object is affected by the wind. |
| ![](../img/types/float2.png) | **Wind Direction** | Controls the direction the wind is blowing across the surface. The first component affects the movement along the object's Y-axis, and the second component affects the movement along the object's X-axis. |
| ![](../img/types/float3.png) | **Normal Tangent Space** | The vertex normal in tangent space, needed for accurate deformation. Vector (0,0,1) in tangent space provided by default. |
| ![](../img/types/float.png) | **Object Height (In Meters)** | The height of the object, used for correct vertical scale. |
| ![](../img/types/float3.png) | **Vertex Position Object Space** | The position of the vertex in object space, used for calculating wind influence. The **[Vertex Position](../../../../../content/materials/graph/node_library/input/vertex_position.md)** node with object space is provided by default. |
| ![](../img/types/float3.png) | **Position Offset Tangent Space** | The calculated offset applied to vertex positions in tangent space for grass movement. |
| ![](../img/types/float3.png) | **Normal Tangent Space** | Modified normal vector after animation process. |
