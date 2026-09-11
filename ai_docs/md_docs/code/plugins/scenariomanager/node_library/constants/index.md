# Constants Nodes


Nodes that output a fixed value typed into the node body. They have no inputs and no execution ports, and are used wherever a graph needs a literal - a threshold to compare against, a starting position, or a label.


## Editable Values and Identities


Most of these nodes have editable parameters: a single **Value** for the scalar types, or one parameter per component for vectors and quaternions.


The four matrix nodes have no parameters at all. Each outputs an identity matrix - the matrix that leaves a value unchanged when it is multiplied by it - which serves as the starting point for building a transformation.


To change a value while the scenario is running, use a [variable](../../../../../code/plugins/scenariomanager/node_library/variables/index.md) instead of a constant.


## Articles in This Section

- [Bool Node](../../../../../code/plugins/scenariomanager/node_library/constants/bool.md)

- [DMat4 Identity Node](../../../../../code/plugins/scenariomanager/node_library/constants/dmat4.md)

- [DVec2 Node](../../../../../code/plugins/scenariomanager/node_library/constants/dvec2.md)

- [DVec3 Node](../../../../../code/plugins/scenariomanager/node_library/constants/dvec3.md)

- [DVec4 Node](../../../../../code/plugins/scenariomanager/node_library/constants/dvec4.md)

- [Float Node](../../../../../code/plugins/scenariomanager/node_library/constants/float.md)

- [Int Node](../../../../../code/plugins/scenariomanager/node_library/constants/int.md)

- [IVec2 Node](../../../../../code/plugins/scenariomanager/node_library/constants/ivec2.md)

- [IVec3 Node](../../../../../code/plugins/scenariomanager/node_library/constants/ivec3.md)

- [IVec4 Node](../../../../../code/plugins/scenariomanager/node_library/constants/ivec4.md)

- [Mat2 Identity Node](../../../../../code/plugins/scenariomanager/node_library/constants/mat2.md)

- [Mat3 Identity Node](../../../../../code/plugins/scenariomanager/node_library/constants/mat3.md)

- [Mat4 Identity Node](../../../../../code/plugins/scenariomanager/node_library/constants/mat4.md)

- [Quat Node](../../../../../code/plugins/scenariomanager/node_library/constants/quat.md)

- [String Node](../../../../../code/plugins/scenariomanager/node_library/constants/string.md)

- [Vec2 Node](../../../../../code/plugins/scenariomanager/node_library/constants/vec2.md)

- [Vec3 Node](../../../../../code/plugins/scenariomanager/node_library/constants/vec3.md)

- [Vec4 Node](../../../../../code/plugins/scenariomanager/node_library/constants/vec4.md)
