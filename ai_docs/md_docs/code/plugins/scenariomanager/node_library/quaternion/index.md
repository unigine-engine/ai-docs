# Quaternion Nodes


Nodes that build, combine and apply rotations. A quaternion stores an orientation in four components that are not read directly - the nodes here are how a rotation is created and used. They have no execution ports and are evaluated whenever their result is needed.


## Why Rotations Are Not Stored as Angles


Three angles around three axes are easy to read but awkward to compute with: their result depends on the order the axes are applied in, two of the axes can line up and cost a degree of freedom, and interpolating between two sets of angles does not follow the shortest path.


Quaternions have none of these problems, which is why rotations are combined and blended in this form and converted to angles only where a person has to read or type them. [Euler to Quat](../../../../../code/plugins/scenariomanager/node_library/quaternion/from_euler.md) and [Quat to Euler](../../../../../code/plugins/scenariomanager/node_library/quaternion/to_euler.md) convert between the two, with angles measured in degrees and applied in the Z, X, Y order.


## Combining and Applying


[Quat Multiply](../../../../../code/plugins/scenariomanager/node_library/quaternion/multiply.md) chains two rotations into one, and the order of its inputs matters: rotating by A and then by B is not the same as the reverse. [Quat Inverse](../../../../../code/plugins/scenariomanager/node_library/quaternion/inverse.md) gives the rotation that undoes another.


[Rotate Vector](../../../../../code/plugins/scenariomanager/node_library/quaternion/rotate_vec.md) applies a rotation to a direction or an offset, and [Slerp](../../../../../code/plugins/scenariomanager/node_library/quaternion/slerp.md) blends between two orientations along the shortest arc.


## Articles in This Section

- [Euler to Quat Node](../../../../../code/plugins/scenariomanager/node_library/quaternion/from_euler.md)

- [Quat Inverse Node](../../../../../code/plugins/scenariomanager/node_library/quaternion/inverse.md)

- [Quat Multiply Node](../../../../../code/plugins/scenariomanager/node_library/quaternion/multiply.md)

- [Rotate Vector Node](../../../../../code/plugins/scenariomanager/node_library/quaternion/rotate_vec.md)

- [Slerp Node](../../../../../code/plugins/scenariomanager/node_library/quaternion/slerp.md)

- [Quat to Euler Node](../../../../../code/plugins/scenariomanager/node_library/quaternion/to_euler.md)

- [Break](../../../../../code/plugins/scenariomanager/node_library/quaternion/break/index.md)

  - [Break Quat Node](../../../../../code/plugins/scenariomanager/node_library/quaternion/break/quat.md)

- [Make](../../../../../code/plugins/scenariomanager/node_library/quaternion/make/index.md)

  - [Make Quat Node](../../../../../code/plugins/scenariomanager/node_library/quaternion/make/quat.md)
