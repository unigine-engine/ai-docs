# Joint Hinge Twist Limit


![](../img/joint_hinge_twist_limit.png)

### Description

Restricts a joint to a 2-DoF coupled hinge and twist: it decomposes the rotation and clamps the hinge swing around the **Hinge Axis** and the twist around the **Forward Axis** independently. This cannot be reproduced by chaining a separate hinge and twist limit, because a plain hinge clamp strips the twist component. A typical use is an elbow, combining flexion (hinge) with forearm pronation (twist).


Like all joint limit nodes, it clamps the pose directly when the **Pose** output is connected, or acts only as a constraint definition when its **Limit** output feeds a [Joint Limit Set](../../../../../content/animations/graph/node_library/skeleton/joint_limit_set.md), an [IK Chain](../../../../../content/animations/graph/node_library/skeleton/ik_chain.md), or a [Look At Chain](../../../../../content/animations/graph/node_library/skeleton/look_at_chain.md).


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/anim_pose.png) | **Pose** | The input pose to clamp. Leave the **Pose** output unconnected to use the node purely as a constraint source. |
| ![](../img/types/float.png) | **Weight** | Blend weight of the clamped result over the input pose, clamped to the [0, 1] range. Default: 1.0. |
| ![](../img/types/quat.png) | **Preferred Rotation** | Target rotation of the soft attractor, used when **Preferred Strength** is greater than zero. Default: identity. It is convenient to drive this input from an [Euler to Quat](../../../../../content/animations/graph/node_library/math/euler_to_quat.md) node. |
| ![](../img/types/anim_pose.png) | **Pose** | The clamped pose. |
| ![](../img/types/constraint.png) | **Limit** | Constraint reference for feeding into a [Joint Limit Set](../../../../../content/animations/graph/node_library/skeleton/joint_limit_set.md), an [IK Chain](../../../../../content/animations/graph/node_library/skeleton/ik_chain.md), or a [Look At Chain](../../../../../content/animations/graph/node_library/skeleton/look_at_chain.md). |


## Properties


| Joint | The joint restricted to a coupled hinge and twist. |
|---|---|
| Forward Axis | Twist axis (the bone direction) in the joint's bind-local frame. For an elbow this is typically +X along the forearm. Choose a preset or Custom. |
| Forward Axis (custom) | Twist axis as a bind-local vector. Active only when **Forward Axis** is set to Custom. |
| Hinge Axis | Hinge swing axis in the bind-local frame, which should be perpendicular to the forward axis. For an elbow this is typically +Y. Choose a preset or Custom. |
| Hinge Axis (custom) | Hinge axis as a bind-local vector. Active only when **Hinge Axis** is set to Custom. |
| Mode | Behavior of the limit: Free, Limited, or Locked. The default value is Limited. |
| Hinge Min | Lower bound of the hinge swing around the hinge axis, in degrees, applied when **Mode** is Limited. For example, an elbow uses 0 to 145. The default value is -180. |
| Hinge Max | Upper bound of the hinge swing, in degrees. The default value is 180. |
| Twist Min | Lower bound of the twist around the forward axis, in degrees. For example, forearm pronation uses about �80. The default value is -180. |
| Twist Max | Upper bound of the twist, in degrees. The default value is 180. |
| Preferred Strength | Blend ratio of the soft attractor, in the [0, 1] range, applied after the hard clamp toward the **Preferred Rotation** input. 0 disables the attractor. The default value is 0.0. |


## See Also


- [Joint Hinge Limit](../../../../../content/animations/graph/node_library/skeleton/joint_hinge_limit.md) node for a pure hinge.
- [Joint Limit Set](../../../../../content/animations/graph/node_library/skeleton/joint_limit_set.md) node that aggregates several joint limits.
- The [JointLimitInfoHingeTwist](../../../../../api/library/animations/skeletal/class.jointlimitinfohingetwist_cpp.md) class used to configure the same limit from the API.
