# UV Tiling and Offset Sample


| [**View Fullscreen**](https://matgraph.unigine.com/SampleUVTilingOffset_2.21/fullView) |
|---|


This material graph sample demonstrates how to implement UV adjustment (tiling and offset) in a material.


The **[UV Tiling Offset](../../../../../content/materials/graph/samples/uv_tiling_offset/index.md)** node accountable for UV adjustment modifies the original UVs (provided by the **[Vertex UV 0](../../../../../content/materials/graph/node_library/input/vertex_uv_0.md)** node) by using the given *UV Tiling* and *Offset* parameter values (enabling you to adjust these values in the *Parameters* panel).


*Albedo* and tangent-space *Normal* data for the *Mesh Opaque PBR* material are sampled via the **[Sample Texture](../../../../../content/materials/graph/node_library/textures/sample_texture.md)** node from the corresponding textures with accordance to the specified UVs.


Finally, the data output from the master material node is passed to the **[Final](../../../../../content/materials/graph/node_library/misc/final.md)** node.


![](result.jpg)

*The result*
