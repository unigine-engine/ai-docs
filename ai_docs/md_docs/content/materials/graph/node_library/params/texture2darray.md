# Texture2DArray Parameter Node


![](../img/texture2darray_param.png)

### Description

The **Texture2DArray** parameter is a homogeneous array of 2D textures where each texture has the same data format, filtering type, and dimensions (including mipmap levels).


It is almost the same as [Texture 2D](../../../../../content/materials/graph/node_library/params/texture2d.md) parameter node, but can contain multiple textures that can be referred to via indices. To sample data from such a texture connect it to the [Sample Texture](../../../../../content/materials/graph/node_library/textures/sample_texture.md) node and specify UV coordinates and a layer Index (starting from 0).


You cannot read intermediate value between two layers of the texture array, for this purpose a [Texture 3D](../../../../../content/materials/graph/node_library/params/texture3d.md) should be used.


When selecting the material in UnigineEditor you'll see this parameter in the *Parameters* window as an asset widget enabling you to choose a texture asset from the data directory.
