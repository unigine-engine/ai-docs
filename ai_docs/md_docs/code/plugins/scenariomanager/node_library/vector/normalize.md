# Vec3 Normalize


![](../img/vec3_normalize.png)

### Description

Outputs a vector that points the same way as **A** but is one unit long, reducing it to a pure direction with its magnitude discarded.


Directions are expected to be of unit length by the nodes that compare or rotate them, so normalizing is the usual step between computing an offset and using it as a heading.


> **Notice:** A zero-length vector has no direction. The node returns it unchanged rather than producing an undefined result, so a normalized value may still be zero and is worth checking where that matters.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/vec3.png) | **A** | The vector to normalize. |
| ![](../img/types/vec3.png) | **Result** | The vector scaled to unit length. |


## See Also


- [Length](../../../../../code/plugins/scenariomanager/node_library/vector/length.md)
- [Dot](../../../../../code/plugins/scenariomanager/node_library/vector/dot.md)
- [Vec3 Scale](../../../../../code/plugins/scenariomanager/node_library/vector/scale.md)
