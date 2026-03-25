# Vertex Animation Sample


| [**View Fullscreen**](https://matgraph.unigine.com/SampleVertexAnimation_2.21/fullView) |
|---|


This material graph sample demonstrates how to use a vertex animation texture in UNIGINE.


Vertex animation can be baked into a texture via one of the modern DCC tools (the example contains textures baked in Blender) and then exported as a set of several files: a geometry file (`.fbx`) and texture files: textures for the model and textures storing animation (an `.exr` texture with position offsets and a `.tga` texture with normals). Then these files are imported into UNIGINE to create the material graph.


The textures with animation are imported with the following settings:


| Position offsets texture | Normals texture |
|---|---|
| - Image Type: 2D - Image Format: RGBA16F - Mipmap Type: Box - Mipmap sRGB Correction: Enabled | - Image Type: 2D - Image Format: RGB8 - Mipmap Type: Box - Mipmap sRGB Correction: Enabled |


*Albedo* and *Roughness* data for the *Vertex Animation* material are sampled via the **[Sample Texture](../../../../../content/materials/graph/node_library/textures/sample_texture.md)** node from the provided *albedo* and *shading* textures with accordance to the specified UVs (the **[Vertex UV 0](../../../../../content/materials/graph/node_library/input/vertex_uv_0.md)** node). The *Roughness* data is also multiplied by a *roughness coefficient* after sampling.


Object-space *Normal* data for the material is obtained by blending of tangent-space normals sampled via the **[Sample Texture](../../../../../content/materials/graph/node_library/textures/sample_texture.md)** node from the provided *normal* and *animation normal* textures and subsequent transforming the output tangent-space normals to the object-space ones (the **[Rotate Space](../../../../../content/materials/graph/node_library/misc/rotate_space.md)** node).


At that, when sampling of the animation normal texture is performed, the original UV is modified as follows: the **U** coordinate is provided by the **[Vertex UV 1](../../../../../content/materials/graph/node_library/input/vertex_uv_1.md)** node, the **V** coordinate is the time multiplied by the animation speed. After sampling, vertex interpolation is performed (the **[Vertex Interpolation](../../../../../content/materials/graph/node_library/misc/vertex_interpolation.md)** node).


*Vertex Position* data for the material is sampled via the **[Sample Texture](../../../../../content/materials/graph/node_library/textures/sample_texture.md)** node from the provided *position offsets* texture according to the UV that is modified as follows: the **U** coordinate is provided by the **[Vertex UV 1](../../../../../content/materials/graph/node_library/input/vertex_uv_1.md)** node, the **V** coordinate is the time multiplied by the animation speed. After sampling, the data is multiplied by the *vertex offset intensity* and then added to the **[Vertex Position](../../../../../content/materials/graph/node_library/input/vertex_position.md)**.


![](../../../../samples/material_examples/vertex_animation.gif)

*The result*
