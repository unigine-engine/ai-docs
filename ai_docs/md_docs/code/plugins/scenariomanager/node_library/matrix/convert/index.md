# Convert


Nodes that convert between matrix types and between a matrix and a quaternion.


## What a Conversion Costs


Going from a Mat4 to a Mat3 discards the position, which is what leaves a transformation suitable for directions. Going the other way adds a position of zero.


Converting to a quaternion keeps only the orientation, so a scale held by the matrix is lost.


## See Also


- [Make](../../../../../../code/plugins/scenariomanager/node_library/matrix/make/index.md)
- [Break](../../../../../../code/plugins/scenariomanager/node_library/matrix/break/index.md)
- [Quaternion](../../../../../../code/plugins/scenariomanager/node_library/quaternion/index.md)


## Articles in This Section

- [Mat3 to Mat4 Node](../../../../../../code/plugins/scenariomanager/node_library/matrix/convert/mat3_to_mat4.md)

- [Mat3 to Quat Node](../../../../../../code/plugins/scenariomanager/node_library/matrix/convert/mat3_to_quat.md)

- [Mat4 to Mat3 Node](../../../../../../code/plugins/scenariomanager/node_library/matrix/convert/mat4_to_mat3.md)

- [Mat4 to Quat Node](../../../../../../code/plugins/scenariomanager/node_library/matrix/convert/mat4_to_quat.md)

- [Quat to Mat3 Node](../../../../../../code/plugins/scenariomanager/node_library/matrix/convert/quat_to_mat3.md)
