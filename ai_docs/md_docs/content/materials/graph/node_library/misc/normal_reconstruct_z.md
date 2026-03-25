# Normal Reconstruct Z Node


![](../img/normal_reconstruct_z.png)

### Description

This node outputs a reconstructed vector Z-coordinate using the input X and Y coordinates, which are within the [-1, 1] range, i.e., the resulting vector has a unit length.


This node can be used to calculate the direction vector along a hemisphere: you input X and Y and the output is Z.


For example, if you input [Vertex Position](../../../../../content/materials/graph/node_library/input/vertex_position.md) as X and Y coordinates in the Absolute World space, and input the resulting Z as the vertex Z position into the [Material](../../../../../content/materials/graph/node_library/misc/material.md) node, you'll get a hemisphere form.
