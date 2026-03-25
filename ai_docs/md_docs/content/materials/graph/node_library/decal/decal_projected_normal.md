# Decal Projected Normal Node


![](../img/decal_projected_normal.png)

### Description

Outputs the normal vector of the projected decal mesh (for [Mesh](../../../../../objects/decals/mesh/index.md) decals) or plane (for [Projected](../../../../../objects/decals/proj/index.md) and [Orthographic](../../../../../objects/decals/ortho/index.md) decals).


The coordinate space of the output value (*World, Object, Tangent, View*) can be selected with the Space dropdown parameter (double-click somewhere inside the node to see the dropdown).


> **Notice:** When used on the vertex shader stage (e.g., with [Vertex Intepolation](../../../../../content/materials/graph/node_library/misc/vertex_interpolation.md) or for [vertex adjustment](../../../../../content/materials/graph/node_library/misc/material.md#vertex)), this node provides source geometry normals as projected values are not available yet.
