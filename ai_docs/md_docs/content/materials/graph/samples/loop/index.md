# Loop Sample


| [**View Fullscreen**](https://matgraph.unigine.com/SampleLoop_2.21/fullView) |
|---|


This material graph sample demonstrates how to use [loops](../../../../../content/materials/graph/index.md#loops) when creating materials.


*Albedo* RGB data for the *Mesh Opaque PBR* material are generated in the loop: the initial texture (**[Texture](../../../../../content/materials/graph/node_library/textures/texture_2d.md)** node) is applied 32 times (*Maximum Iterations*) with a uniform UV shift along the points on a **[Vogel Disk](../../../../../content/materials/graph/node_library/procedural/vogel_disk.md)** controlled by the **blur** **[Slider](../../../../../content/materials/graph/index.md#params)** parameter node (adjustable via the *Parameters* panel in UnigineEditor).


The **[Loop Begin](../../../../../content/materials/graph/node_library/misc/loop_begin.md)** node has the only variable *Texture Sample* float3 vector. The *Maximum Iterations* corresponds to the desired number of samples and is set to 32.


The logic of each iteration lays between the **[Loop Begin](../../../../../content/materials/graph/node_library/misc/loop_begin.md)** and **[Loop End](../../../../../content/materials/graph/node_library/misc/loop_end.md)** nodes. Each time the following steps are performed:


- The *Index* of the current iteration and the number of all iterations are passed to the **[Vogel Disk](../../../../../content/materials/graph/node_library/procedural/vogel_disk.md)** node providing a uniform UV shift.
- The UV shift is multiplied by the *blur* value (divided by 10), i.e. the intensity of blur is changed.
- The resulting UV shift is added to the texture coordinates (**[Vertex UV 0](../../../../../content/materials/graph/node_library/input/vertex_uv_0.md)** node).
- The RGB value sampled from the texture is added to the previous *Texture Sample* value and passed to the **[Loop End](../../../../../content/materials/graph/node_library/misc/loop_end.md)** node as the result of this iteration.


Thus the *Texture Sample* value is iteratively increasing up to the last iteration.


The result of the **[Add](../../../../../content/materials/graph/node_library/math/add.md)** node is also connected to the **[Divide](../../../../../content/materials/graph/node_library/math/divide.md)** node which performs color intensity reduction (divides the resulting value by the number of loop iterations - increments of color values).
