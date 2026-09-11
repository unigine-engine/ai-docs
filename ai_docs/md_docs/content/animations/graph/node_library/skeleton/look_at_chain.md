# Look At Chain


![](../img/look_at_chain.png)

### Description

Multi-joint Look At. The tip joint of the chain aims its bone-local forward axis at the **Target**, and the other joints receive a share of the rotation defined by per-joint weights. Unlike the [IK Chain](../../../../../content/animations/graph/node_library/skeleton/ik_chain.md) node, this node aims at a **direction** rather than reaching a position, the tip joint also rotates, and the per-joint weights are set by the artist.


The chain joints are listed root to tip in the **Joints** property. Each joint adds its own inspector rows for the per-joint weight and axes.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/anim_pose.png) | **Pose** | The input pose to modify. |
| ![](../img/types/vec3.png) | **Target** | Position the tip's forward axis is aimed at. Interpreted according to the **Space** property; the socket label reflects the current value (Target (World Space) or Target (Object Space)). |
| ![](../img/types/vec3.png) | **Pole** | Pole position used as the up reference for the per-bone twist correction. Used only when **Use Pole** is enabled. The socket label reflects the current **Space** value. |
| ![](../img/types/float.png) | **Weight** | Blend weight of the Look At result over the input pose, clamped to the [0, 1] range. Default: 1.0. |
| ![](../img/types/constraint.png) | **Limits** | Optional joint limits applied during solving. Accepts a [Joint Limit Set](../../../../../content/animations/graph/node_library/skeleton/joint_limit_set.md) or a single joint limit node. |
| ![](../img/types/anim_pose.png) | **Pose** | The resulting pose with the chain aimed at the Target. |


## Properties


| Joints (root -> tip) | Ordered list of joints that make up the chain, from the root (for example, the lower spine) to the tip whose forward axis actually aims at the Target (for example, the head). Each listed joint adds its own **Weight**, **Forward**, and **Up** rows below, each suffixed with the joint name. |
|---|---|
| Use Pole | When enabled, each bone receives a small twist around its aim direction so that its up axis projects toward the Pole point, which prevents the chain from rolling around the aim lines as the target moves. The default value is false. |
| Iterations | Maximum number of root-to-tip passes per solve. It matters only when joint limits are connected: without limits the solver always runs a single pass. The default value is 4. |
| Tolerance (deg) | Angle, in degrees, between the tip aim direction and the target direction below which the chain is considered converged and the solver stops iterating. The default value is 0.5. Set to 0 to always run all iterations. |
| Max Angle | Per-frame cap, in degrees in the [0, 180] range, on how much each chain joint may deviate from the current pose. The default value is 180, which imposes no effective cap. The reference for the deviation depends on **Animation Blend** (the previous solved state, the animation pose, or a blend of both). |
| Animation Blend | Solver starting state, in the [0, 1] range, with the same meaning as in the [IK Chain](../../../../../content/animations/graph/node_library/skeleton/ik_chain.md) node. 0 gives a pure warm start; 1 re-converges from the animation pose every frame. A value around 0.5 is recommended when the animation already hints at the correct direction. The default value is 0.0. |
| Space | Coordinate space for the **Target** and **Pole** inputs: World or Object. The default value is World. |


Each joint in the chain adds the following per-joint rows:


| Weight: <joint> | Share of the aiming rotation, in the [0, 1] range, applied to this joint. The default value is 1.0. |
|---|---|
| Forward: <joint> | Bone-local forward axis of this joint, aimed at the Target. Choose a preset, or Custom to enter an arbitrary direction in the **Forward Custom: <joint>** field below it. |
| Up: <joint> | Bone-local up axis of this joint, used as the twist reference. Choose a preset, or Custom to enter an arbitrary direction in the **Up Custom: <joint>** field below it. Shown only when **Use Pole** is enabled. |


## See Also


- [Joint Look At](../../../../../content/animations/graph/node_library/skeleton/joint_look_at.md) node for a single joint.
- [IK Chain](../../../../../content/animations/graph/node_library/skeleton/ik_chain.md) node for reaching a target position.
- The [LookAtChainInfo](../../../../../api/library/animations/skeletal/class.lookatchaininfo_cpp.md) class used to configure the same solver from the API.
