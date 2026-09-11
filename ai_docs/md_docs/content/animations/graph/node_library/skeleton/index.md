# Skeleton


Nodes for procedural skeleton control. They modify the pose after it has been evaluated by the animation part of the graph: aim a bone or a chain at a target, reach an end-effector to a point with inverse kinematics, or restrict a joint's rotation to anatomically valid limits.


## Node Groups


The category contains three kinds of nodes:


- **Inverse kinematics** - [Two Bone IK](../../../../../content/animations/graph/node_library/skeleton/two_bone_ik.md) (analytical, for a three-joint chain) and [IK Chain](../../../../../content/animations/graph/node_library/skeleton/ik_chain.md) (iterative, for a chain of arbitrary length). Both bend the chain so its end reaches a target position.
- **Look At** - [Joint Look At](../../../../../content/animations/graph/node_library/skeleton/joint_look_at.md) (rotates a single joint toward a target) and [Look At Chain](../../../../../content/animations/graph/node_library/skeleton/look_at_chain.md) (distributes the aiming rotation across a chain).
- **Joint limits** - seven nodes that clamp the local rotation of a joint to anatomical bounds, plus the [Joint Limit Set](../../../../../content/animations/graph/node_library/skeleton/joint_limit_set.md) aggregator. Each limit node can either modify the pose directly or act as a constraint fed into an IK Chain or a Look At Chain.


## See Also


- A set of [Transform](../../../../../content/animations/graph/node_library/transform/index.md) nodes to read and write individual joint transforms.


## Articles in This Section

- [Two Bone IK Node](../../../../../content/animations/graph/node_library/skeleton/two_bone_ik.md)

- [IK Chain Node](../../../../../content/animations/graph/node_library/skeleton/ik_chain.md)

- [Joint Look At Node](../../../../../content/animations/graph/node_library/skeleton/joint_look_at.md)

- [Look At Chain Node](../../../../../content/animations/graph/node_library/skeleton/look_at_chain.md)

- [Joint Hinge Limit Node](../../../../../content/animations/graph/node_library/skeleton/joint_hinge_limit.md)

- [Joint Cone Limit Node](../../../../../content/animations/graph/node_library/skeleton/joint_cone_limit.md)

- [Joint Cone Asym Limit Node](../../../../../content/animations/graph/node_library/skeleton/joint_cone_asym_limit.md)

- [Joint Twist Limit Node](../../../../../content/animations/graph/node_library/skeleton/joint_twist_limit.md)

- [Joint Hinge Twist Limit Node](../../../../../content/animations/graph/node_library/skeleton/joint_hinge_twist_limit.md)

- [Joint Cone Twist Limit Node](../../../../../content/animations/graph/node_library/skeleton/joint_cone_twist_limit.md)

- [Joint Cone Asym Twist Limit Node](../../../../../content/animations/graph/node_library/skeleton/joint_cone_asym_twist_limit.md)

- [Joint Limit Set Node](../../../../../content/animations/graph/node_library/skeleton/joint_limit_set.md)
