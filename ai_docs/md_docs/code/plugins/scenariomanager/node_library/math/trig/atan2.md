# Atan2


![](../../img/atan2.png)

### Description

Outputs the angle of the direction given by **A** and **B**, where **A** is the vertical offset and **B** the horizontal one.


Unlike the tangent taken of a single ratio, this node uses the signs of both operands to tell apart directions in all four quadrants, which makes it the way to get a heading from an offset between two positions.


Angles are measured in radians.


> **Notice:** Unlike the single-input trigonometric nodes, this one follows the ordinary rule for two operands: when both offsets are whole numbers the result is whole as well, and the angle loses its fractional part. Connect a real value to either input to get the angle itself.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/any.png) | **A** | The vertical offset. |
| ![](../../img/types/any.png) | **B** | The horizontal offset. |
| ![](../../img/types/any.png) | **Result** | The result of the operation. |


## See Also


- [Tan](../../../../../../code/plugins/scenariomanager/node_library/math/trig/tan.md)
- [Sin](../../../../../../code/plugins/scenariomanager/node_library/math/trig/sin.md)
- [Cos](../../../../../../code/plugins/scenariomanager/node_library/math/trig/cos.md)
