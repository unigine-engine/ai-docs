# Normal From Height Texture Sample


| [**View Fullscreen**](https://matgraph.unigine.com/SampleNormalFromHeightTexture_2.21/fullView) |
|---|


This material graph sample demonstrates how to convert a height value from a height texture to normals.


The **[Normal From Height Texture](../../../../../content/materials/graph/node_library/misc/normal_from_height_texture.md)** node is accountable for conversion from a heightmap to normals. So the *Height* texture (**[Texture 2D](../../../../../content/materials/graph/node_library/textures/texture_2d.md)** node) and the *Height Value* are connected to it and the *Normal Tangent Space* result is used for normals of the material.


*Albedo, Metalness* and *Roughness* values are obtained from the corresponding parameters.


![](result.jpg)

*Normal From Height Texture sample*
