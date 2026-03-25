# Normal From Height Texture Node


![](../img/normal_from_height_texture.png)

### Description

Samples a height value from the Heightmap texture and converts it to tangent-space *Tangent*, *Binormal* and *Normal* vectors.


This node is designed to create normals from an existing heightmap texture when there is no normal map available.


- Heightmap Texture - a texture that is used to create an additional height displacement.
- UV - texture UV coordinates.
- Height - height value (in meters) to which the surface is to be deepened visually if the corresponding texel of the heightmap is black.


## Usage Examples

**Example 1**

The example can be found in the [Normal From Height Texture Sample](https://developer.unigine.com/en/docs/future/content/materials/graph/samples/normal_from_height_texture/?rlang=cs).
