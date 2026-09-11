# Mat4 Multiply


![](../img/mat4_multiply.png)

### Description

Combines the transformations **A** and **B** into the single transformation that performs both.


This is how a placement relative to something else becomes a placement in the world: multiplying an object's own transformation by that of the thing it is attached to gives where it actually ends up, and the result can be chained further up a hierarchy.


> **Notice:** The order of the inputs matters. Each transformation is applied relative to the frame the other one establishes, so swapping them generally gives a different placement.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/mat4.png) | **A** | The first transformation. |
| ![](../img/types/mat4.png) | **B** | The second transformation. |
| ![](../img/types/mat4.png) | **Result** | The combined transformation. |


## See Also


- [Mat4 inverse](../../../../../code/plugins/scenariomanager/node_library/matrix/inverse.md)
- [Mat4 x Vec4](../../../../../code/plugins/scenariomanager/node_library/matrix/transform_vec4.md)
- [Compose TRS](../../../../../code/plugins/scenariomanager/node_library/matrix/compose.md)
