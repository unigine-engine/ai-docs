# Panner Sample


| [**View Fullscreen**](https://matgraph.unigine.com/SamplePanner_2.21/fullView) |
|---|


This material graph sample demonstrates how to create a simple UV-panner to animate UV coordinates in a material.


The data from *Albedo* and *Normal* textures (**[Texture 2D](../../../../../content/materials/graph/node_library/textures/texture_2d.md)** node) taken from material's parameters (enabling you to select a texture asset via the *Parameters* panel in UnigineEditor) is sampled by the **[Sample Texture](../../../../../content/materials/graph/node_library/textures/sample_texture.md)** node in accordance with the specified UV coordinates and the result is simply passed to the **[Material](../../../../../content/materials/graph/node_library/misc/material.md)** node.


The logic for animating UV coordinates is simple: both U and V components of the **[Vertex UV 0](../../../../../content/materials/graph/node_library/input/vertex_uv_0.md)** node output (the 0 channel of vertex texture coordinates) are connected to separate **[Add](../../../../../content/materials/graph/node_library/math/add.md)** nodes via corresponding **x** and **y** [port adapters](../../../../../content/materials/graph/index.md). The **[Auto Game Time](../../../../../content/materials/graph/node_library/misc/time.md)** is multiplied by different values provided by the *U Speed* and *V Speed* **[Slider](../../../../../content/materials/graph/index.md#params)** parameter nodes (enabling you to control these values via the *Parameters* panel). The resulting values are passed to the corresponding **Add** nodes, thus increasing the original UV coordinates.


![](../../../../samples/material_examples/panner.gif)

*The result*
