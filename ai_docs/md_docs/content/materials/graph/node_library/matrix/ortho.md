# Ortho Node


![](../img/ortho.png)

### Description

Outputs the parallel projection matrix:


| 2.0 / (right - left) | 0.0 | 0.0 | -(right + left) / (right - left) |
|---|---|---|---|
| 0.0 | 2.0 / (top - bottom) | 0.0 | -(top + bottom) / (top - bottom) |
| 0.0 | 0.0 | -2.0 / (zfar - znear) | -(zfar + znear) / (zfar - znear) |
| 0.0 | 0.0 | 0.0 | 1.0 |


![](../../../../../api/library/math/orthographic_desc.png)


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/float.png) | **L** | Left vertical clipping plane |
| ![](../img/types/float.png) | **R** | Right vertical clipping plane |
| ![](../img/types/float.png) | **B** | Bottom horizontal clipping plane |
| ![](../img/types/float.png) | **T** | Top horizontal clipping plane |
| ![](../img/types/float.png) | **N** | Distance to the near depth clipping plane |
| ![](../img/types/float.png) | **F** | Distance to the farther depth clipping plane |
