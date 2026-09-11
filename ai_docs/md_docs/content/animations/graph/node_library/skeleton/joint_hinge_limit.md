# Joint Hinge Limit


![](../img/joint_hinge_limit.png)

### Description

Restricts the local rotation of a joint to a single hinge axis: rotation around the chosen **Hinge Axis** is clamped to a range, and off-axis deflection is discarded. Use it for a 1-DoF joint such as an elbow, a knee, or a finger.


Like all joint limit nodes, it has two roles. If the **Pose** output is connected, the node clamps the pose directly. If instead the **Limit** output is connected to a [Joint Limit Set](../../../../../content/animations/graph/node_library/skeleton/joint_limit_set.md), an [IK Chain](../../../../../content/animations/graph/node_library/skeleton/ik_chain.md), or a [Look At Chain](../../../../../content/animations/graph/node_library/skeleton/look_at_chain.md), the node acts only as a constraint definition and does not modify the pose itself.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/anim_pose.png) | **Pose** | The input pose to clamp. Leave the **Pose** output unconnected to use the node purely as a constraint source. |
| ![](../img/types/float.png) | **Weight** | Blend weight of the clamped result over the input pose, clamped to the [0, 1] range. Default: 1.0. |
| ![](../img/types/quat.png) | **Preferred Rotation** | Target rotation of the soft attractor, used when **Preferred Strength** is greater than zero. Default: identity. It is convenient to drive this input from an [Euler to Quat](../../../../../content/animations/graph/node_library/math/euler_to_quat.md) node to enter the value in degrees. |
| ![](../img/types/anim_pose.png) | **Pose** | The clamped pose. |
| ![](../img/types/constraint.png) | **Limit** | Constraint reference for feeding into a [Joint Limit Set](../../../../../content/animations/graph/node_library/skeleton/joint_limit_set.md), an [IK Chain](../../../../../content/animations/graph/node_library/skeleton/ik_chain.md), or a [Look At Chain](../../../../../content/animations/graph/node_library/skeleton/look_at_chain.md). |


## Properties


| Joint | The joint whose rotation is restricted to a single hinge axis. |
|---|---|
| Hinge Axis | Rotation axis in the joint's bind-local frame. Choose a preset (+X, -X, +Y, -Y, +Z, -Z) or Custom. The default value is +Y. |
| Hinge Axis (custom) | Hinge axis as a bind-local vector. Active only when **Hinge Axis** is set to Custom. The sign of the direction affects the sign of Min and Max by the right-hand rule. |
| Mode | Behavior of the limit: - Free - pass-through; the pose flows unmodified. - Limited - rotation is clamped to the [Min, Max] range and off-axis swing is locked to the bind pose. - Locked - the joint is forced to its bind reference. For a non-zero locked angle, use Limited with equal Min and Max. The default value is Limited. |
| Min | Lower bound of the hinge rotation, in degrees, applied when **Mode** is Limited. The default value is -180. For example, a knee uses Min 0, Max 140. |
| Max | Upper bound of the hinge rotation, in degrees, applied when **Mode** is Limited. The default value is 180. |
| Preferred Strength | Blend ratio of the soft attractor, in the [0, 1] range. After the hard clamp, the joint rotation is slerped toward the **Preferred Rotation** input by this fraction and then re-clamped. 0 disables the attractor. A typical anatomical bias is between 0.05 and 0.2. The default value is 0.0. |


## See Also


- [Joint Limit Set](../../../../../content/animations/graph/node_library/skeleton/joint_limit_set.md) node that aggregates several joint limits.
- The [JointLimitInfoHinge](../../../../../api/library/animations/skeletal/class.jointlimitinfohinge_cpp.md) class used to configure the same limit from the API.
