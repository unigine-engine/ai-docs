# IK Chain


![](../img/ik_chain.png)

### Description

Iterative inverse kinematics for a chain of arbitrary length. Suitable for a spine, a tail, a tentacle, or fingers. The node orients the listed joints so the tip reaches toward the **Target**; the tip joint rotation itself is not modified. For a three-joint chain, prefer the analytical [Two Bone IK](../../../../../content/animations/graph/node_library/skeleton/two_bone_ik.md) node, which needs no iterations.


The chain joints are listed root to tip in the **Joints** property. The bend direction is resolved according to the **Limit Source** property: from the pole vector or from connected joint limits. Without joint limits the chain is solved by a FABRIK solver; when limits are attached the node switches to a CCD solver, which clamps every joint inline as it goes.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/anim_pose.png) | **Pose** | The input pose to modify. |
| ![](../img/types/vec3.png) | **Target** | Position the tip of the chain reaches toward. Interpreted according to the **Space** property; the socket label reflects the current value (Target (World Space) or Target (Object Space)). |
| ![](../img/types/vec3.png) | **Pole** | Pole position used to disambiguate the bend direction. Used only when **Limit Source** is set to Pole. The socket label reflects the current **Space** value. |
| ![](../img/types/float.png) | **Weight** | Blend weight of the IK result over the input pose, clamped to the [0, 1] range. Default: 1.0. |
| ![](../img/types/constraint.png) | **Limits** | Optional joint limits applied during solving. Accepts a [Joint Limit Set](../../../../../content/animations/graph/node_library/skeleton/joint_limit_set.md) or a single joint limit node. Used when **Limit Source** is set to Joint Limits. |
| ![](../img/types/anim_pose.png) | **Pose** | The resulting pose with the chain solved. |


## Properties


| Joints (root -> tip) | Ordered list of joints that make up the IK chain, from the root (closest to the body) to the tip (the end-effector reaching for the Target). Each joint must be the direct child of the previous joint in the skeleton. The tip joint rotation is not modified. |
|---|---|
| Limit Source | Strategy that disambiguates the bend direction of the chain: - None - the chain bends following the previous pose. The Pole input is ignored. - Pole - mid-joints rotate to align with the plane through the root, the target, and the pole. This is the industry-standard hint for elbow and knee orientation. - Joint Limits - per-joint limits from connected joint limit nodes are applied each iteration, which is anatomically correct for hinge joints. The Pole input is ignored. The default value is Pole. |
| Iterations | Maximum number of solver iterations per frame. The solver early-exits once the tip is within **Tolerance** of the Target, so excess iterations are cheap on already converged chains. The default value is 8. |
| Tolerance | Object-space distance from the tip to the Target below which the chain is considered converged and the solver stops iterating. The default value is 0.001 (about 1 mm at typical character scale). Set to 0 to always run all iterations. |
| Restart Attempts | Number of extra solve attempts made from deterministic seed poses when the warm solve misses the Target by a wide margin. Each attempt is a full solve, so the value is capped at 32. Shown only when **Limit Source** is set to Joint Limits - the seeds are built from the per-joint limits. The default value is 0, which means a single warm solve. |
| Solver Mode | Strategy used when the Target is near or beyond full reach: Hard, Soft, or Stretching. The behavior matches the [Two Bone IK](../../../../../content/animations/graph/node_library/skeleton/two_bone_ik.md) node. The default value is Hard. |
| Softness | Available in Soft mode only. Fraction of the full chain reach over which the asymptotic blend starts. The default value is 0.05. |
| Max Stretch Scale | Available in Stretching mode only. Upper cap on the bone elongation factor when the Target is past full reach. The default value is 1.5. |
| Space | Coordinate space for the **Target** and **Pole** inputs: World or Object. The default value is World. |
| Output Smooth Time | Time constant, in seconds, of a low-pass filter applied to the solved chain rotations. 0 disables the filter (no lag). The default value is 0.03. Increase it to smooth residual numerical noise at the cost of visible lag during fast tracking. |
| Max Angular Speed | Per-joint angular rate cap, in degrees per second, applied before the smoothing filter. It catches sudden large jumps when the solver switches between valid solutions between frames. 0 disables the cap. The default value is 720. |


## See Also


- [Two Bone IK](../../../../../content/animations/graph/node_library/skeleton/two_bone_ik.md) node for three-joint chains.
- [Joint Limit Set](../../../../../content/animations/graph/node_library/skeleton/joint_limit_set.md) node used to feed the **Limits** input.
- The [IKInfoChain](../../../../../api/library/animations/skeletal/class.ikinfochain_cpp.md) class used to configure the same solver from the API.
