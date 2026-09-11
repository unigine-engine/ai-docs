# Vec3 Multiply Add


![](../img/vec3_multiply_add.png)

### Description

Multiplies **A** by **B** component by component and adds **C** to the result, combining the two operations in a single node.


Because the multiplication is per component, **B** scales each axis on its own - a uniform scale means giving it the same value in all three components.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/vec3.png) | **A** | The vector to scale. |
| ![](../img/types/vec3.png) | **B** | The per-component factors. |
| ![](../img/types/vec3.png) | **C** | The vector added to the scaled result. |
| ![](../img/types/vec3.png) | **Result** | The result of the operation. |


## See Also


- [Vec3 Scale](../../../../../code/plugins/scenariomanager/node_library/vector/scale.md)
- [Vec3 Add](../../../../../code/plugins/scenariomanager/node_library/vector/add.md)
- [Multiply](../../../../../code/plugins/scenariomanager/node_library/math/multiply.md)
