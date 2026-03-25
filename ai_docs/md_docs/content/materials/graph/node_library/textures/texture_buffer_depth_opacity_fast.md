# Texture Buffer Depth Opacity Fast Node


![](../img/texture_buffer_depth_opacity_fast.png)

### Description

Texture buffers are 2D textures used to build a deferred image for various post-effects. To sample data from such a texture connect it to the [Sample Texture](../../../../../content/materials/graph/node_library/textures/sample_texture.md) node and specify UV coordinates for reading texels from the texture.


This 2D Texture contains camera-to-surface distances of opaque materials. Unlike the [Texture Buffer Depth](../../../../../content/materials/graph/node_library/textures/texture_buffer_depth.md) this buffer has a lower accuracy but has mip levels.


> **Notice:** This buffer contains data of opaque materials only.


This buffer is preferred for complex post-effects with multiple depth reading operations, as reading can be performed from a mipmap instead of full resolution.
