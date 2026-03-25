# Texture Buffer Screen Color Old Node


![](../img/texture_buffer_screen_color_old.png)

### Description

Texture buffers are 2D textures used to build a deferred image for various post-effects. To sample data from such a texture connect it to the [Sample Texture](../../../../../content/materials/graph/node_library/textures/sample_texture.md) node and specify UV coordinates for reading texels from the texture.


This 2D Texture stores [Color Old (previous frame) data](../../../../../principles/render/sequence/index.md#linear_depth_for_ss).
