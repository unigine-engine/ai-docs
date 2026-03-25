# Texture 2D Int Node


![](../img/texture_2d_int.png)

### Description

This node represents a single-channel texture of integer values, such as **[Texture Buffer GBuffer Material Mask](../../../../../content/materials/graph/node_library/textures/texture_buffer_gbuffer_material_mask.md)**, for example. [Sampling](../../../../../content/materials/graph/node_library/textures/sample_texture.md) a value from this node outputs an unaltered integer value.


> **Notice:** Only two types of [sampling and filtering](../../../../../content/materials/graph/node_library/textures/sample_texture.md#sample_type) are supported for such textures: Point and Fetch. All other types are automatically switched to Point.
