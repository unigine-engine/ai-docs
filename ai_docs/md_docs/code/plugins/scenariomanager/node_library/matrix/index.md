# Matrix Nodes


Nodes that work with transformation matrices - the form in which a position, a rotation and a scale are carried together as one value. They have no execution ports and are evaluated whenever their result is needed.


Building matrices from their parts, taking them apart, and converting between matrix types are covered by the [Make](../../../../../code/plugins/scenariomanager/node_library/matrix/make/index.md), [Break](../../../../../code/plugins/scenariomanager/node_library/matrix/break/index.md) and [Convert](../../../../../code/plugins/scenariomanager/node_library/matrix/convert/index.md) subcategories.


## Matrix Types


A Mat3 holds a rotation and a scale but no position, which makes it the type for transforming directions. A Mat4 adds a position and so describes a placement in full.


A DMat4 keeps its position at double precision and is the type used for world transformations, where coordinates far from the origin need the extra range. Rotation is kept at single precision in both, so only the position gains from it.


## Combining Transformations


[Mat4 Multiply](../../../../../code/plugins/scenariomanager/node_library/matrix/multiply.md) combines two transformations into one that performs both. As with rotations, the order of the inputs matters, since each transformation is applied relative to the one before it.


Where a transformation is assembled from or reduced to its separate parts, [Compose TRS](../../../../../code/plugins/scenariomanager/node_library/matrix/compose.md) and [Decompose TRS](../../../../../code/plugins/scenariomanager/node_library/matrix/decompose.md) are more direct than building the matrix by hand.


## Articles in This Section

- [Compose TRS Node](../../../../../code/plugins/scenariomanager/node_library/matrix/compose.md)

- [Decompose TRS Node](../../../../../code/plugins/scenariomanager/node_library/matrix/decompose.md)

- [Mat4 inverse Node](../../../../../code/plugins/scenariomanager/node_library/matrix/inverse.md)

- [Mat4 Multiply Node](../../../../../code/plugins/scenariomanager/node_library/matrix/multiply.md)

- [Mat4 x Vec4 Node](../../../../../code/plugins/scenariomanager/node_library/matrix/transform_vec4.md)

- [Mat4 Transpose Node](../../../../../code/plugins/scenariomanager/node_library/matrix/transpose.md)

- [Break](../../../../../code/plugins/scenariomanager/node_library/matrix/break/index.md)

  - [Break DMat4 Node](../../../../../code/plugins/scenariomanager/node_library/matrix/break/dmat4.md)
  - [Break Mat2 Node](../../../../../code/plugins/scenariomanager/node_library/matrix/break/mat2.md)
  - [Break Mat3 Node](../../../../../code/plugins/scenariomanager/node_library/matrix/break/mat3.md)

- [Convert](../../../../../code/plugins/scenariomanager/node_library/matrix/convert/index.md)

  - [Mat3 to Mat4 Node](../../../../../code/plugins/scenariomanager/node_library/matrix/convert/mat3_to_mat4.md)
  - [Mat3 to Quat Node](../../../../../code/plugins/scenariomanager/node_library/matrix/convert/mat3_to_quat.md)
  - [Mat4 to Mat3 Node](../../../../../code/plugins/scenariomanager/node_library/matrix/convert/mat4_to_mat3.md)
  - [Mat4 to Quat Node](../../../../../code/plugins/scenariomanager/node_library/matrix/convert/mat4_to_quat.md)
  - [Quat to Mat3 Node](../../../../../code/plugins/scenariomanager/node_library/matrix/convert/quat_to_mat3.md)

- [Make](../../../../../code/plugins/scenariomanager/node_library/matrix/make/index.md)

  - [Make DMat4 Node](../../../../../code/plugins/scenariomanager/node_library/matrix/make/dmat4.md)
  - [Make Mat2 Node](../../../../../code/plugins/scenariomanager/node_library/matrix/make/mat2.md)
  - [Make Mat3 (columns) Node](../../../../../code/plugins/scenariomanager/node_library/matrix/make/mat3_columns.md)
  - [Make Mat3 (Quat) Node](../../../../../code/plugins/scenariomanager/node_library/matrix/make/mat3_quat.md)
