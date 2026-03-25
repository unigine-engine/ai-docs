# Texture Buffer GBuffer Material Mask Node


![](../img/texture_buffer_gbuffer_material_mask.png)

### Description

Texture buffers are 2D textures used to build a deferred image for various post-effects. To sample data from such a texture connect it to the [Sample Texture](../../../../../content/materials/graph/node_library/textures/sample_texture.md) node and specify UV coordinates for reading texels from the texture.


This 2D Texture contains the mask of the material.


> **Notice:** This buffer contains data of opaque materials only.
