# Tangent-Space Normal Map Sample


| [**View Fullscreen**](https://matgraph.unigine.com/SampleTangentSpaceNormalMap_2.21/fullView) |
|---|


This material graph sample demonstrates how to use tangent-space normal maps.


The **[Sample Texture](../../../../../content/materials/graph/node_library/textures/sample_texture.md)** node samples tangent-space normals taken from the normal map **[Texture 2D](../../../../../content/materials/graph/node_library/textures/texture_2d.md)** parameter node (enabling you to select a texture asset via the *Parameters* panel in UnigineEditor) in accordance with the default UV.


The [Normal Space](../../../../../content/materials/graph/index.md#normal_space) for the material is set to Tangent, therefore it is simply enough to pass the output to the material's *Normal* input.


The *Albedo* color is defined by the value from the **[Color](../../../../../content/materials/graph/node_library/input/color_float3.md)** node. The *Roughness* value is provided directly via a **[Float](../../../../../content/materials/graph/node_library/input/float.md)** node.
