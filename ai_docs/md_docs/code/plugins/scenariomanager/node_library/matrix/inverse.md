# Mat4 inverse


![](../img/mat4_inverse.png)

### Description

Outputs the transformation that undoes **A**. Combining a transformation with its inverse leaves a value unchanged.


This is what converts a world placement into a local one. Transforming a world position by the inverse of an object's transformation gives that position as the object sees it - the basis for asking whether something is in front of a vehicle or inside a marked area.


> **Notice:** A transformation that flattens space onto a plane or a line - one whose scale is zero along some axis - cannot be undone, and the result for such a matrix is not meaningful.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/mat4.png) | **A** | The transformation to invert. |
| ![](../img/types/mat4.png) | **Result** | The inverted transformation. |


## See Also


- [Mat4 Multiply](../../../../../code/plugins/scenariomanager/node_library/matrix/multiply.md)
- [Mat4 Transpose](../../../../../code/plugins/scenariomanager/node_library/matrix/transpose.md)
- [Quat Inverse](../../../../../code/plugins/scenariomanager/node_library/quaternion/inverse.md)
