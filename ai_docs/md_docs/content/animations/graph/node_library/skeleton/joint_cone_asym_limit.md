# Joint Cone Asym Limit


![](../img/joint_cone_asym_limit.png)

### Description

Restricts the swing of a joint to an asymmetric ellipse around the **Cone Axis**, with independent minimum and maximum swing angles toward the up axis and sideways. Use it for a 3-DoF joint such as a shoulder or a hip, where the forward swing differs from the backward swing. Twist around the forward axis is preserved.


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


| Joint | The joint whose swing is restricted to an asymmetric ellipse. |
|---|---|
| Forward Axis | Bone direction in the joint's bind-local frame (the twist axis for the swing-twist decomposition). Choose a preset or Custom. |
| Forward Axis (custom) | Bone direction as a bind-local vector. Active only when **Forward Axis** is set to Custom. |
| Up Axis | Perpendicular reference in the bind-local frame that defines the up direction of the ellipse. Choose a preset or Custom. |
| Up Axis (custom) | Up reference as a bind-local vector. Active only when **Up Axis** is set to Custom. |
| Cone Axis | Center direction of the cone, where the bone is allowed to point. Choose a preset or Custom. |
| Cone Axis (custom) | Cone center as a bind-local vector. Active only when **Cone Axis** is set to Custom. |
| Mode | Behavior of the limit: Free, Limited, or Locked. The default value is Limited. |
| Swing Left | Half-angle of the cone to the left of the cone axis, in degrees. The four swing angles are the semi-axes of an elliptical cone, not a min/max pair: each one caps the deviation in its own direction. The default value is 180, which imposes no effective limit. |
| Swing Right | Half-angle of the cone to the right of the cone axis, in degrees. The default value is 180. |
| Swing Up | Half-angle of the cone upwards from the cone axis, in degrees. The **Up Axis** fixes which way is up. The default value is 180. |
| Swing Down | Half-angle of the cone downwards from the cone axis, in degrees. The default value is 180. |
| Preferred Strength | Blend ratio of the soft attractor, in the [0, 1] range, applied after the hard clamp toward the **Preferred Rotation** input. 0 disables the attractor. The default value is 0.0. |


## See Also


- [Joint Cone Limit](../../../../../content/animations/graph/node_library/skeleton/joint_cone_limit.md) node for a symmetric cone.
- [Joint Limit Set](../../../../../content/animations/graph/node_library/skeleton/joint_limit_set.md) node that aggregates several joint limits.
- The [JointLimitInfoConeAsym](../../../../../api/library/animations/skeletal/class.jointlimitinfoconeasym_cpp.md) class used to configure the same limit from the API.
