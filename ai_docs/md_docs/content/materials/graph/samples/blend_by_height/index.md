# Blend By Height Sample


| [**View Fullscreen**](https://matgraph.unigine.com/SampleBlendByHeight_2.21/fullView) |
|---|


This material graph sample demonstrates how to perform blending based on heightmaps when creating materials.


Texture coordinates taken via the **[Vertex UV 0](../../../../../content/materials/graph/node_library/input/vertex_uv_0.md)** node are [multiplied](../../../../../content/materials/graph/node_library/math/multiply.md) by the first two components of the UV Transform *float4* parameter, representing UV tiling adjustment, and increased by its last two components that represent a UV offset. The modified UV coordinates are connected to all **[Sample Texture](../../../../../content/materials/graph/node_library/textures/sample_texture.md)** nodes via [portals](../../../../../content/materials/graph/index.md) for ease of access.


Two height values sampled from the corresponding textures in accordance with the modified UVs are passed to the **[Blend By Height](../../../../../content/materials/graph/node_library/misc/blend_by_height.md)** node. *Height 0 Scale*, *Height 1 Scale*, and *Contrast* values are taken from parameter **[Sliders](../../../../../content/materials/graph/index.md#params)** enabling you to adjust these values via the *Parameters* panel.


The *Result Height* is connected to the **Tessellation Vertex Offset Tangent Space** port of the material via the 0,0,x [port adapter](../../../../../content/materials/graph/index.md#adapter) (meaning that the value shall control displacement along the Z-axis only, keeping X and Y as they are). The *Result Blend Mask* is used as a blending coefficient for the **[Lerp](../../../../../content/materials/graph/node_library/math/lerp.md)** nodes performing linear interpolation between two sets of *Albedo* and tangent-space *Normal* textures.


![](result.jpg)

*Blend By Height sample*
