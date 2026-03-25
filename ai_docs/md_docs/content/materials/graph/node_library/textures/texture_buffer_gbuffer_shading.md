# Texture Buffer GBuffer Shading Node


![](../img/texture_buffer_gbuffer_shading.png)

### Description

Texture buffers are 2D textures used to build a deferred image for various post-effects. To sample data from such a texture connect it to the [Sample Texture](../../../../../content/materials/graph/node_library/textures/sample_texture.md) node and specify UV coordinates for reading texels from the texture.


This 2D Texture contains:


- **R** - metalness of opaque materials.
- **G** - specular of opaque materials.
- **B** - translucent of opaque materials.
- **Alpha** - microfiber of opaque materials.


> **Notice:** This buffer contains data of opaque materials only.
