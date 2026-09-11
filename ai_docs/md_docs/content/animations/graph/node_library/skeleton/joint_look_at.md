# Joint Look At


![](../img/joint_look_at.png)

### Description

Analytical single-joint Look At. Rotates one joint so that its bone-local forward axis points at the **Target**. Typical uses are head tracking, eye gaze, and weapon aiming. The solver writes only rotation; position and scale stay untouched. Optional twist correction around the aim direction is available through the **Pole** input.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/anim_pose.png) | **Pose** | The input pose to modify. |
| ![](../img/types/vec3.png) | **Target** | Position the joint's forward axis is aimed at. Interpreted according to the **Space** property; the socket label reflects the current value (Target (World Space) or Target (Object Space)). |
| ![](../img/types/vec3.png) | **Pole** | Pole position used for twist correction. After the forward axis is aimed at the Target, the joint is rotated around the aim direction so its up axis points toward the pole. Used only when **Use Pole** is enabled. The socket label reflects the current **Space** value. |
| ![](../img/types/float.png) | **Weight** | Blend weight of the Look At result over the input pose, clamped to the [0, 1] range. Default: 1.0. |
| ![](../img/types/bool.png) | **Use Pole** | Whether the **Pole** input is used for twist correction. Default: false. |
| ![](../img/types/anim_pose.png) | **Pose** | The resulting pose with the joint aimed at the Target. |


## Properties


| Joint | The joint that is rotated to look at the Target. Its children inherit the rotation through the skeleton hierarchy. |
|---|---|
| Forward Axis | Bone-local axis that is pointed at the Target after solving. Choose the preset that matches the bone orientation of the rig (+X, -X, +Y, -Y, +Z, -Z), or Custom to enter an arbitrary direction in the **Forward Axis (custom)** field. |
| Forward Axis (custom) | Bone-local forward direction as a vector. Active only when **Forward Axis** is set to Custom. It does not need to be unit length; the solver normalizes it. |
| Up Axis | Bone-local axis used for twist correction when **Use Pole** is enabled. It should be roughly perpendicular to the forward axis. Choose a preset or Custom. |
| Up Axis (custom) | Bone-local up direction as a vector. Active only when **Up Axis** is set to Custom. It does not need to be unit length; the solver normalizes it. |
| Space | Coordinate space for the **Target** and **Pole** inputs: World or Object. The default value is World. |
| Max Angle | Cap, in degrees in the [0, 180] range, on how far the Look At may rotate the joint away from the underlying animation pose. The default value is 180, which imposes no effective limit. It is recomputed each frame relative to the current animation pose and is not accumulated over time. |


## See Also


- [Look At Chain](../../../../../content/animations/graph/node_library/skeleton/look_at_chain.md) node for distributing the aiming rotation across several joints.
- The [LookAtInfo](../../../../../api/library/animations/skeletal/class.lookatinfo_cpp.md) class used to configure the same solver from the API.
