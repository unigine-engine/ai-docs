# Texture 2D Array Node


![](../img/texture_2d_array.png)

### Description

This node represents almost the same as [Texture 2D](../../../../../content/materials/graph/node_library/textures/texture_2d.md) node, but can contain multiple textures that can be referred to via indices. To sample data from such a texture connect it to the [Sample Texture](../../../../../content/materials/graph/node_library/textures/sample_texture.md) node and specify UV coordinates and a layer Index (starting from 0).


You cannot read intermediate value between two layers of the texture array, for this purpose a [Texture 3D](../../../../../content/materials/graph/node_library/textures/texture_3d.md) should be used.


There is a maximum sampling limit of 16 textures, but using a 2D Texture Array enables you to get around this limitation. If all your textures have the same resolution you can put them all to a single array and read the data as many times as you need using different [Sample Texture](../../../../../content/materials/graph/node_library/textures/sample_texture.md) nodes specifying different layer indices.
