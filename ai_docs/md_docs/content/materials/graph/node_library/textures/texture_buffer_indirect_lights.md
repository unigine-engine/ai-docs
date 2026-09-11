# Texture Buffer Indirect Lights Node


![](../img/texture_buffer_indirect_lights.png)

### Description

Texture buffers are 2D textures used to build a deferred image for various post-effects. To sample data from such a texture connect it to the [Sample Texture](../../../../../content/materials/graph/node_library/textures/sample_texture.md) node and specify UV coordinates and array element index for reading texels from the texture.


This 2D Texture Array contains indirect lighting from light sources for opaque materials.


- **Index 0** � indirect diffuse lighting (diffuse lighting from probes, sky, and lightmaps).
- **Index 1** � indirect specular lighting (reflections from probes and sky).


> **Notice:** This buffer may contain data of both opaque and transparent materials.
