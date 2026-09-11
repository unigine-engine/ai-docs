# Mat4 Transpose


![](../img/mat4_transpose.png)

### Description

Reflects the matrix **A** about its diagonal, exchanging its rows and columns.


For a matrix that only rotates, this is the same as inverting it and is cheaper to compute. That equivalence does not hold once a scale or a position is involved, where [Mat4 inverse](../../../../../code/plugins/scenariomanager/node_library/matrix/inverse.md) is the correct node.


Transposing also converts a matrix between the row-major and column-major conventions, which is what an interface expecting the opposite layout needs.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/mat4.png) | **A** | The matrix to transpose. |
| ![](../img/types/mat4.png) | **Result** | The transposed matrix. |


## See Also


- [Mat4 inverse](../../../../../code/plugins/scenariomanager/node_library/matrix/inverse.md)
- [Mat4 Multiply](../../../../../code/plugins/scenariomanager/node_library/matrix/multiply.md)
- [Break Mat3](../../../../../code/plugins/scenariomanager/node_library/matrix/break/mat3.md)
