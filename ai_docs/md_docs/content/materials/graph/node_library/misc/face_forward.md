# Face Forward Node


![](../img/face_forward.png)

### Description

Outputs a floating-point, surface normal vector that is facing the view direction.


This node actually flips the surface-normal (if needed) to face in a direction opposite to I; returns the result in N.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/undefined.png) | **N** | The floating-point surface-normal vector that is required to store the result. |
| ![](../img/types/undefined.png) | **I** | A floating-point, incident vector that points from the view position to the shading position. |
| ![](../img/types/undefined.png) | **Ng** | A floating-point surface-normal vector. |
