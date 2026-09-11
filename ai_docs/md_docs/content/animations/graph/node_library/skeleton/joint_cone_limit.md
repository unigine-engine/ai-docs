# Joint Cone Limit


![](../img/joint_cone_limit.png)

### Description

Restricts the swing of a joint to a symmetric cone (a spherical sphere-cap) around the **Cone Axis**. The bone direction, given by the **Forward Axis**, must stay within the cone half-angle of the cone axis. Twist around the forward axis is preserved; combine this node with a [Joint Twist Limit](../../../../../content/animations/graph/node_library/skeleton/joint_twist_limit.md) on the same joint to clamp twist as well.


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


| Joint | The joint whose swing is restricted to a cone. |
|---|---|
| Forward Axis | Bone direction in the joint's bind-local frame. The clamp keeps this direction within the cone half-angle of the cone axis. Choose a preset or Custom. |
| Forward Axis (custom) | Bone direction as a bind-local vector. Active only when **Forward Axis** is set to Custom. |
| Cone Axis | Center direction of the cone, where the bone is allowed to point. May differ from the forward axis to pre-tilt the cone. Choose a preset or Custom. |
| Cone Axis (custom) | Cone center as a bind-local vector. Active only when **Cone Axis** is set to Custom. |
| Mode | Behavior of the limit: Free (pass-through), Limited (clamp swing to the cone), or Locked (force the joint to its bind reference). The default value is Limited. |
| Cone Half-Angle | Maximum swing angle from the cone axis, in degrees in the [0, 180] range. The default value is 180, which imposes no effective limit. |
| Preferred Strength | Blend ratio of the soft attractor, in the [0, 1] range. After the hard clamp, the joint rotation is slerped toward the **Preferred Rotation** input by this fraction and then re-clamped. 0 disables the attractor. The default value is 0.0. |


## See Also


- [Joint Twist Limit](../../../../../content/animations/graph/node_library/skeleton/joint_twist_limit.md) node to clamp twist on the same joint.
- [Joint Limit Set](../../../../../content/animations/graph/node_library/skeleton/joint_limit_set.md) node that aggregates several joint limits.
- The [JointLimitInfoCone](../../../../../api/library/animations/skeletal/class.jointlimitinfocone_cpp.md) class used to configure the same limit from the API.
