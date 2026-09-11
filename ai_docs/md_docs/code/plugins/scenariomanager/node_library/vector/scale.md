# Vec3 Scale


![](../img/vec3_scale.png)

### Description

Multiplies every component of **A** by the number **B**, changing the length of the vector while keeping its direction.


Scaling a normalized direction by a distance is how a point is placed at a given range along it, and scaling a velocity by elapsed time gives the step for one frame. A negative factor also reverses the direction.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/vec3.png) | **A** | The vector to scale. |
| ![](../img/types/float.png) | **B** | The factor to scale by. |
| ![](../img/types/vec3.png) | **Result** | The scaled vector. |


## See Also


- [Vec3 Normalize](../../../../../code/plugins/scenariomanager/node_library/vector/normalize.md)
- [Vec3 Multiply Add](../../../../../code/plugins/scenariomanager/node_library/vector/mad.md)
- [Vec3 negate](../../../../../code/plugins/scenariomanager/node_library/vector/negate.md)
