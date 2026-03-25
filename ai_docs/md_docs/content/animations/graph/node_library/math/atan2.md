# 2-Argument Arctangent


![](../img/atan2.png)

### Description

Computes the arctangent of **A** / **B**, in radians. The result is in the range [-PI, PI]. Unlike a simple division, correctly handles cases when **B** is 0 and preserves the quadrant of the angle.


If (**B**, **A**) represents a point (X, Y), returns the angle between the positive X axis and that point.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/float.png) | **A** | Y coordinate. |
| ![](../img/types/float.png) | **B** | X coordinate. |
| ![](../img/types/float.png) | **Result** | The angle in radians. |
