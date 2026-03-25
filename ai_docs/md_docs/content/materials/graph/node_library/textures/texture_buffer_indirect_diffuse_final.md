# Texture Buffer Indirect Diffuse Final Node


![](../img/texture_buffer_indirect_diffuse_final.png)

### Description

Texture buffers are 2D textures used to build a deferred image for various post-effects. To sample data from such a texture connect it to the [Sample Texture](../../../../../content/materials/graph/node_library/textures/sample_texture.md) node and specify UV coordinates and array element index for reading texels from the texture.


This 2D texture contains the output diffuse indirect lighting after the denoiser has been applied to it.
