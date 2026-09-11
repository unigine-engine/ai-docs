# Joint Twist Limit


![](../img/joint_twist_limit.png)

### Description

Restricts the 1-DoF twist rotation of a joint around its **Forward Axis** to a range. Swing perpendicular to the forward axis is preserved. Use it for a forearm pronation joint, or stack it with a [Joint Cone Limit](../../../../../content/animations/graph/node_library/skeleton/joint_cone_limit.md) or a [Joint Cone Asym Limit](../../../../../content/animations/graph/node_library/skeleton/joint_cone_asym_limit.md) on the same joint for cone-plus-twist anatomy.


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


| Joint | The joint whose twist around the forward axis is restricted. |
|---|---|
| Forward Axis | Twist axis (the bone direction) in the joint's bind-local frame. Choose a preset or Custom. |
| Forward Axis (custom) | Twist axis as a bind-local vector. Active only when **Forward Axis** is set to Custom. |
| Mode | Behavior of the limit: Free, Limited, or Locked. The default value is Limited. |
| Twist Min | Lower bound of the twist rotation, in degrees, applied when **Mode** is Limited. Signed by the right-hand rule around the forward axis. The default value is -180. |
| Twist Max | Upper bound of the twist rotation, in degrees. The default value is 180. |
| Preferred Strength | Blend ratio of the soft attractor, in the [0, 1] range, applied after the hard clamp toward the **Preferred Rotation** input. 0 disables the attractor. The default value is 0.0. |


## See Also


- [Joint Cone Twist Limit](../../../../../content/animations/graph/node_library/skeleton/joint_cone_twist_limit.md) node that combines a cone and twist.
- [Joint Limit Set](../../../../../content/animations/graph/node_library/skeleton/joint_limit_set.md) node that aggregates several joint limits.
- The [JointLimitInfoTwist](../../../../../api/library/animations/skeletal/class.jointlimitinfotwist_cpp.md) class used to configure the same limit from the API.
