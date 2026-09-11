# Mat4 x Vec4


![](../img/mat4_x_vec4.png)

### Description

Applies the transformation **A** to the vector **B**.


The W component decides how the vector is treated. Setting it to 1 marks the value as a position, which the transformation both rotates and moves; setting it to 0 marks it as a direction, which is rotated but not moved - a heading should not shift because the object carrying it stands elsewhere.


Use [Vec3 to Vec4](../../../../../code/plugins/scenariomanager/node_library/vector/convert/vec3_to_vec4.md) to attach the right W component to a Vec3, and [Vec4 to Vec3](../../../../../code/plugins/scenariomanager/node_library/vector/convert/vec4_to_vec3.md) to drop it again afterwards.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/mat4.png) | **A** | The transformation to apply. |
| ![](../img/types/vec4.png) | **B** | The vector to transform. |
| ![](../img/types/vec4.png) | **Result** | The transformed vector. |


## See Also


- [Mat4 Multiply](../../../../../code/plugins/scenariomanager/node_library/matrix/multiply.md)
- [Rotate Vector](../../../../../code/plugins/scenariomanager/node_library/quaternion/rotate_vec.md)
- [Vec3 to Vec4](../../../../../code/plugins/scenariomanager/node_library/vector/convert/vec3_to_vec4.md)
