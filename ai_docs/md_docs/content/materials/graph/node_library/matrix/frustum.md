# Frustum Node


![](../img/frustum.png)

### Description

Outputs the perspective projection matrix:


| 2.0 * znear / (right - left) | 0.0 | (right + left) / (right - left) | 0.0 |
|---|---|---|---|
| 0.0 | 2.0 * znear / (top - bottom) | (top + bottom) / (top - bottom) | 0.0 |
| 0.0 | 0.0 | -(zfar + znear) / (zfar - znear) | -2.0 * zfar * znear / (zfar - znear) |
| 0.0 | 0.0 | -1.0 | 0.0 |


Coordinates of top, left, right, bottom are set relatively to center point of the znear plane.


![](../../../../../api/library/math/frustum_desc.png)


There are two different points (A and B) on the picture above. Since the top, left, right, bottom are coordinates relatively to the center point of the znear plane, coordinates of the A point should be *A(left, bottom, znear)*. Coordinates of the B point are *B(k * left, k * bottom, zfar)*, where *k = zfar/znear.*


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/float.png) | **L** | Left coordinate of the near clipping plane relatively to the center |
| ![](../img/types/float.png) | **R** | Right coordinate of the near clipping plane relatively to the center |
| ![](../img/types/float.png) | **B** | Bottom coordinate of the near clipping plane relatively to the center |
| ![](../img/types/float.png) | **T** | Top coordinate of the near clipping plane relatively to the center |
| ![](../img/types/float.png) | **N** | Distance to the near depth clipping plane |
| ![](../img/types/float.png) | **F** | Distance to the farther depth clipping plane |
