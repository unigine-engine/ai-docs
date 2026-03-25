# Vertex Color Sample


| [**View Fullscreen**](https://matgraph.unigine.com/SampleVertexColor_2.21/fullView) |
|---|


This material graph sample demonstrates how to use vertex color for texture blending when creating materials.


Vertex color data retrieved via the **[Vertex Color](../../../../../content/materials/graph/node_library/input/vertex_color.md)** node is passed to a [portal](../../../../../content/materials/graph/index.md#node_portal) for the ease of access. 4 sets of *Albedo* and tangent-space *Normal* textures are blended with accordance to the channels of the vertex color data:


- Each of the color channels (RGB) gets its own Linear Interpolation expression.
- The data from the first *Albedo A* texture sampled by the **[Sample Texture](../../../../../content/materials/graph/node_library/textures/sample_texture.md)** node is plugged to the **A** port of the first **[Lerp](../../../../../content/materials/graph/node_library/math/lerp.md)** node.
- The data from each of the other three albedo Textures (B-D) sampled by the corresponding **[Sample Texture](../../../../../content/materials/graph/node_library/textures/sample_texture.md)** node is plugged to the **B** port of its corresponding **[Lerp](../../../../../content/materials/graph/node_library/math/lerp.md)** node.
- The first **[Lerp](../../../../../content/materials/graph/node_library/math/lerp.md)** node corresponding to the Texture A plugs into the **A** port of the **[Lerp](../../../../../content/materials/graph/node_library/math/lerp.md)** node corresponding to Texture B, with *Coefficient* driven by the *Red* channel from the vertex color (connected via the **x** [port adapter](../../../../../content/materials/graph/index.md#adapter)).
- The second **[Lerp](../../../../../content/materials/graph/node_library/math/lerp.md)** node corresponding to Texture B plugs into the **A** port of the **[Lerp](../../../../../content/materials/graph/node_library/math/lerp.md)** node corresponding to Texture C, with *Coefficient* driven by the *Green* channel from the vertex color (connected via the **y** port adapter).
- The third **[Lerp](../../../../../content/materials/graph/node_library/math/lerp.md)** node corresponding to Texture C plugs into the **Albedo** port of the master material node, with *Coefficient* driven by the *Blue* channel from the vertex color (connected via the **z** port adapter).
- Four Normal maps sampled by the corresponding **[Sample Texture](../../../../../content/materials/graph/node_library/textures/sample_texture.md)** nodes have the same kind of setup of Linear Interpolation expressions.


Finally, the data output is passed to the **[Final](../../../../../content/materials/graph/node_library/misc/final.md)** node.


![](result.jpg)

*The result*
