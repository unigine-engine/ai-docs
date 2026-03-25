# Texture Buffer Direct Lights Node


![](../img/texture_buffer_direct_lights.png)

### Description

Texture buffers are 2D textures used to build a deferred image for various post-effects. To sample data from such a texture connect it to the [Sample Texture](../../../../../content/materials/graph/node_library/textures/sample_texture.md) node and specify UV coordinates and array element index for reading texels from the texture.


This 2D Texture Array contains direct lighting from light sources for opaque materials.


- **Index 0** - direct diffuse lighting from light sources.
- **Index 1** - direct specular lighting from light sources.


> **Notice:** This buffer may contain data of both opaque and transparent materials.
