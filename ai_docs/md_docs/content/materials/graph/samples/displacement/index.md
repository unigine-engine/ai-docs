# Displacement Sample


| [**View Fullscreen**](https://matgraph.unigine.com/SampleDisplacement_2.21/fullView) |
|---|


This material graph sample demonstrates how to implement displacement mapping in your materials.


The **[Sample Texture](../../../../../content/materials/graph/node_library/textures/sample_texture.md)** node samples data from the tangent-space normal map taken from the normal **[Texture 2D](../../../../../content/materials/graph/node_library/textures/texture_2d.md)** node (enabling you to select a texture asset via the *Parameters* panel in UnigineEditor) in accordance with the default UV, normal vector components are passed to the **[Material](../../../../../content/materials/graph/node_library/misc/material.md)** node.


*Albedo* data for the material is specified directly via a **[Float](../../../../../content/materials/graph/node_library/input/float.md)** node (casting to *float3* is performed automatically).


Data of a single-channel *heightmap* taken from the **[Texture 2D](../../../../../content/materials/graph/node_library/textures/texture_2d.md)** node and sampled by the **[Sample Texture](../../../../../content/materials/graph/node_library/textures/sample_texture.md)** node is passed via the x [port adapter](../../../../../content/materials/graph/index.md#adapter) to the **[Add](../../../../../content/materials/graph/node_library/math/add.md)** node which applies the *displacement offset* according the **Offset [Slider](../../../../../content/materials/graph/index.md#params)** parameter node (enabling you to adjust a float value via the *Parameters* panel in UnigineEditor). The output is then multiplied (the **[Multiply](../../../../../content/materials/graph/node_library/math/multiply.md)** node) by the *displacement height* value provided by the second **[Slider](../../../../../content/materials/graph/index.md#params)** node and passed to the *Tessellation Vertex Offset Tangent Space* port of the material node via the **0,0,x** port adapter (meaning that the value shall control displacement along the Z axis only, keeping X and Y as they are).


*Tessellation Factor* for the material is specified using a **[Slider](../../../../../content/materials/graph/index.md#params)** parameter node enabling you to adjust the value in the *Parameters* panel.


![](result.jpg)

*The result*
