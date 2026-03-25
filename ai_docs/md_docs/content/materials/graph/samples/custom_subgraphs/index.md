# Custom Subgraphs Sample


This sample demonstrates how to create [Subgraphs](../../../../../content/materials/graph/index.md#subgraphs) and use them in your Material Graphs. There are two Subgraphs included:


1) A simple Subgraph demonstrating all available inputs (`all_types_of_data.msubgraph`)


| [**View Fullscreen**](https://matgraph.unigine.com/SampleAllTypesOfData_2.21/fullView) |
|---|


2) A simple Subgraph implementing UV panning (`uv panner.msubgraph`)


| [**View Fullscreen**](https://matgraph.unigine.com/SampleUVPanner_2.21/fullView) |
|---|


The image below demonstrates how the Subgraphs described above are used in a complex Material Graph.


- The **UV Panner** node (Subgraph) takes the texture coordinates from the **[Vertex UV 0](../../../../../content/materials/graph/node_library/input/vertex_uv_0.md)** node and the speed value from the **[Float2](../../../../../content/materials/graph/node_library/input/float2.md)** parameter node (enabling you to adjust the panner speed via the *Parameters* panel in UnigineEditor). The modified UV is passed to the *UV* input of the **[Sample Texture](../../../../../content/materials/graph/node_library/textures/sample_texture.md)** nodes sampling albedo and normal data from the corresponding **[Texture 2D](../../../../../content/materials/graph/node_library/textures/texture_2d.md)** nodes. Finally, the data output from the master material node is passed to the **[Final](../../../../../content/materials/graph/node_library/misc/final.md)** node.
- Nodes providing all available input types (*float, int, texture*) are connected to the corresponding input ports of the **All Types of Data** Subgraph node.


| [**View Fullscreen**](https://matgraph.unigine.com/SampleTestSubgraphs_2.21/fullView) |
|---|
