# Slerp


![](../img/slerp.png)

### Description

Blends between the rotations **A** and **B** by the factor **C**, so that 0 gives **A**, 1 gives **B**, and 0.5 gives the orientation halfway between them.


The blend follows the shortest arc between the two orientations at a steady angular rate, so turning a camera or an object toward a new heading looks even throughout rather than speeding up in the middle.


This is what distinguishes it from interpolating angles or vectors: [Vec3 Lerp](../../../../../code/plugins/scenariomanager/node_library/vector/lerp.md) applied to two directions cuts across the arc instead of following it, and shortens the result along the way.


The factor is held within the 0 to 1 range, so a value outside it gives the rotation at the nearer end rather than continuing past it.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/quat.png) | **A** | The rotation returned when **C** is 0. |
| ![](../img/types/quat.png) | **B** | The rotation returned when **C** is 1. |
| ![](../img/types/float.png) | **C** | The blend factor. |
| ![](../img/types/quat.png) | **Result** | The blended rotation. |


## See Also


- [Quat Multiply](../../../../../code/plugins/scenariomanager/node_library/quaternion/multiply.md)
- [Vec3 Lerp](../../../../../code/plugins/scenariomanager/node_library/vector/lerp.md)
- [SmoothStep](../../../../../code/plugins/scenariomanager/node_library/math/interpolation/smoothstep.md)
