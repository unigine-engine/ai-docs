# Decal Projected Position Node


![](../img/decal_projected_position.png)

### Description

Outputs the fragment position of the decal mesh (for [Mesh](../../../../../objects/decals/mesh/index.md) decals) or plane (for [Projected](../../../../../objects/decals/proj/index.md) and [Orthographic](../../../../../objects/decals/ortho/index.md) decals) corresponding to the fragment after being projected.


The coordinate space of the output value (*Camera World, Object, View, Absolute World*) can be selected with the Space dropdown parameter (double-click somewhere inside the node to see the dropdown).


> **Notice:** When used on the vertex shader stage (e.g., with [Vertex Intepolation](../../../../../content/materials/graph/node_library/misc/vertex_interpolation.md) or for [vertex adjustment](../../../../../content/materials/graph/node_library/misc/material.md#vertex)), this node provides source geometry positions for *Orthographic* and *Projected* decals as projected values are not available yet.
