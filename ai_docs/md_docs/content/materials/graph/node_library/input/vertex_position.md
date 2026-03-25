# Vertex Position Node


![](../img/vertex_position.png)

### Description

Provides access to Vertex Positions of initial geometry **before** applying any vertex transformations implemented in shaders. The coordinate space of the output value (*Camera World, Object, View, Absolute World*) can be selected with the Space dropdown parameter (double-click somewhere inside the node to see the dropdown).


> **Notice:** For *Orthographic* and *Projected* decals vertex positions are defined on the closest face of the box and pyramid formed by the decal shape correspondingly.
