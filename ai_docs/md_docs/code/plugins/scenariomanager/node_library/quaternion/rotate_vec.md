# Rotate Vector


![](../img/rotate_vector.png)

### Description

Applies the rotation **A** to the vector **B**, turning the direction or offset it describes while keeping its length.


This is how a local direction is expressed in world terms: rotating the forward axis by an object's orientation gives the direction that object faces, and rotating an offset gives a position alongside it that follows as it turns.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/quat.png) | **A** | The rotation to apply. |
| ![](../img/types/vec3.png) | **B** | The vector to rotate. |
| ![](../img/types/vec3.png) | **Result** | The rotated vector. |


## See Also


- [Quat Multiply](../../../../../code/plugins/scenariomanager/node_library/quaternion/multiply.md)
- [Quat Inverse](../../../../../code/plugins/scenariomanager/node_library/quaternion/inverse.md)
- [Mat4 x Vec4](../../../../../code/plugins/scenariomanager/node_library/matrix/transform_vec4.md)
