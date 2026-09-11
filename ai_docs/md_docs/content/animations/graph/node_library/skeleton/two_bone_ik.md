# Two Bone IK


![](../img/two_bone_ik.png)

### Description

Analytical inverse kinematics for a three-joint chain (for example, shoulder-elbow-wrist or hip-knee-ankle). The node bends the **Root** and **Mid** joints so that the **End** joint reaches toward the **Target**. The rotation of the End joint is not modified: if you need to control the orientation of the wrist or the foot, chain a [Set Joint Transform](../../../../../content/animations/graph/node_library/transform/set_joint_transform.md) node afterward.


Root, Mid, and End are selected explicitly, so any hierarchy works, including twist or helper bones placed between the solved joints. The **Pole** input defines the bend direction of the chain.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/anim_pose.png) | **Pose** | The input pose to modify. |
| ![](../img/types/vec3.png) | **Target** | Position the End joint reaches toward. Interpreted according to the **Space** property; the socket label reflects the current value (Target (World Space) or Target (Object Space)). |
| ![](../img/types/vec3.png) | **Pole** | Pole position that defines the bend direction of the chain (the plane through the root, the end, and the pole). Used only when **Use Pole** is enabled. The socket label reflects the current **Space** value. |
| ![](../img/types/float.png) | **Weight** | Blend weight of the IK result over the input pose, clamped to the [0, 1] range. Default: 1.0. |
| ![](../img/types/bool.png) | **Use Pole** | Whether the **Pole** input is used to control the bend direction. When disabled, the current bend plane of the chain is kept. Default: false. |
| ![](../img/types/anim_pose.png) | **Pose** | The resulting pose with the chain solved. |


## Properties


| Root Joint | Start of the IK chain, typically a shoulder or a hip joint. The solver writes a new local rotation here so the chain reaches toward the Target. Twist or helper bones between Root and Mid are preserved. |
|---|---|
| Mid Joint | Middle joint that bends, typically an elbow or a knee. Must be a descendant of the Root joint. |
| End Joint | End-effector that reaches for the Target, typically a wrist or an ankle. Must be a descendant of the Mid joint. Its rotation is not modified. |
| Solver Mode | Strategy used when the Target is near or beyond the full reach of the chain: - Hard - the chain reaches the Target exactly until full reach, then locks. There is a visible snap at the boundary. - Soft - the chain asymptotically approaches full reach and never quite reaches the Target near the boundary, avoiding the snap. Recommended for foot and hand IK on humans. - Stretching - the chain extends past full reach so the End reaches the Target exactly, capped by **Max Stretch Scale**. Useful for ledge grabbing, climbing, and foot planting on rough terrain. The default value is Hard. |
| Softness | Available in Soft mode only. Fraction of the full chain reach over which the asymptotic blend starts. For example, 0.05 means blending starts at 95% of the reach. Larger values smooth the approach earlier but increase the gap between the End and the Target. The default value is 0.05. |
| Max Stretch Scale | Available in Stretching mode only. Upper cap on the bone elongation factor when the Target is past full reach. For example, 1.5 means the bones can stretch up to 1.5 times their natural length. The default value is 1.5. |
| Space | Coordinate space for the **Target** and **Pole** inputs: World (world-space positions, matching the preview gizmos) or Object (skeleton object space, skipping the world-to-object conversion at runtime). The default value is World. |


## See Also


- [IK Chain](../../../../../content/animations/graph/node_library/skeleton/ik_chain.md) node for chains longer than three joints.
- The [IKInfoTwoBone](../../../../../api/library/animations/skeletal/class.ikinfotwobone_cpp.md) class used to configure the same solver from the API.
