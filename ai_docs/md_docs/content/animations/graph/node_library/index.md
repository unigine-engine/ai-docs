# Animation Graph Node Library


This article lists all available nodes in the Animation Graph system, organized by category. Each node performs a specific operation - from playing animations and blending poses to evaluating math expressions and controlling state machine transitions.


## Type Resolving


Many nodes in the library have [Undefined](../../../../content/animations/index.md#data_types) ports � their type is not fixed and is resolved automatically when you connect a typed port. For example, connecting a Vec3 output to an Undefined input turns that input (and usually the node's output) into Vec3 as well.


When a polymorphic node receives a vector type, it operates component-wise. For example, **[Multiply](../../../../content/animations/graph/node_library/math/multiply.md)** node with two Vec3 inputs multiplies each component separately (this is not a dot or cross product).


Nodes with fixed-type ports (such as Bool or Float) accept only that specific type. See [Data Types](../../../../content/animations/index.md#data_types) for the complete list of available types.


## See Also


- [Animation Graph Overview](../../../../content/animations/index.md)
- [Animation Graph Editor](../../../../content/animations/graph/index.md)


## Articles in This Section

- [Animation](../../../../content/animations/graph/node_library/animation/index.md)

  - [Animation Asset Node](../../../../content/animations/graph/node_library/animation/animation_asset.md)
  - [Animation Player Node](../../../../content/animations/graph/node_library/animation/animation_player.md)
  - [Animation Pose Node](../../../../content/animations/graph/node_library/animation/animation_pose.md)

- [Blend](../../../../content/animations/graph/node_library/blend/index.md)

  - [Blend Poses Node](../../../../content/animations/graph/node_library/blend/blend_poses.md)
  - [Make Additive Node](../../../../content/animations/graph/node_library/blend/make_additive.md)
  - [Apply Additive Node](../../../../content/animations/graph/node_library/blend/apply_additive.md)

- [Blend Space](../../../../content/animations/graph/node_library/blend_space/index.md)

  - [Blend Space 2D Node](../../../../content/animations/graph/node_library/blend_space/blend_space_2d.md)
  - [Blend Space 2D Sync Node](../../../../content/animations/graph/node_library/blend_space/blend_space_2d_sync.md)

- [Transform](../../../../content/animations/graph/node_library/transform/index.md)

  - [Get Joint Transform Node](../../../../content/animations/graph/node_library/transform/get_joint_transform.md)
  - [Set Joint Transform Node](../../../../content/animations/graph/node_library/transform/set_joint_transform.md)
  - [Position Space Node](../../../../content/animations/graph/node_library/transform/position_space.md)
  - [Direction Space Node](../../../../content/animations/graph/node_library/transform/direction_space.md)
  - [Rotation Space Node](../../../../content/animations/graph/node_library/transform/rotation_space.md)

- [Skeleton](../../../../content/animations/graph/node_library/skeleton/index.md)

  - [Two Bone IK Node](../../../../content/animations/graph/node_library/skeleton/two_bone_ik.md)
  - [IK Chain Node](../../../../content/animations/graph/node_library/skeleton/ik_chain.md)
  - [Joint Look At Node](../../../../content/animations/graph/node_library/skeleton/joint_look_at.md)
  - [Look At Chain Node](../../../../content/animations/graph/node_library/skeleton/look_at_chain.md)
  - [Joint Hinge Limit Node](../../../../content/animations/graph/node_library/skeleton/joint_hinge_limit.md)
  - [Joint Cone Limit Node](../../../../content/animations/graph/node_library/skeleton/joint_cone_limit.md)
  - [Joint Cone Asym Limit Node](../../../../content/animations/graph/node_library/skeleton/joint_cone_asym_limit.md)
  - [Joint Twist Limit Node](../../../../content/animations/graph/node_library/skeleton/joint_twist_limit.md)
  - [Joint Hinge Twist Limit Node](../../../../content/animations/graph/node_library/skeleton/joint_hinge_twist_limit.md)
  - [Joint Cone Twist Limit Node](../../../../content/animations/graph/node_library/skeleton/joint_cone_twist_limit.md)
  - [Joint Cone Asym Twist Limit Node](../../../../content/animations/graph/node_library/skeleton/joint_cone_asym_twist_limit.md)
  - [Joint Limit Set Node](../../../../content/animations/graph/node_library/skeleton/joint_limit_set.md)

- [State Machine](../../../../content/animations/graph/node_library/state_machine/index.md)

  - [State Machine Node](../../../../content/animations/graph/node_library/state_machine/state_machine.md)
  - [State Node](../../../../content/animations/graph/node_library/state_machine/state.md)
  - [Condition Node](../../../../content/animations/graph/node_library/state_machine/condition.md)
  - [State Portal Node](../../../../content/animations/graph/node_library/state_machine/state_portal.md)

- [Subgraph](../../../../content/animations/graph/node_library/subgraph/index.md)

  - [SubGraph Node](../../../../content/animations/graph/node_library/subgraph/sub_graph.md)
  - [SubGraph Inputs Node](../../../../content/animations/graph/node_library/subgraph/sub_graph_inputs.md)
  - [SubGraph Outputs Node](../../../../content/animations/graph/node_library/subgraph/sub_graph_outputs.md)
  - [Preview Output Pose Node](../../../../content/animations/graph/node_library/subgraph/preview_output_pose.md)

- [Output](../../../../content/animations/graph/node_library/output/index.md)

  - [Output Pose Node](../../../../content/animations/graph/node_library/output/output_pose.md)

- [Result](../../../../content/animations/graph/node_library/result/index.md)

  - [Transition Result Node](../../../../content/animations/graph/node_library/result/transition_result.md)

- [Portal](../../../../content/animations/graph/node_library/portal/index.md)

  - [Portal In Node](../../../../content/animations/graph/node_library/portal/portal_in.md)
  - [Portal Out Node](../../../../content/animations/graph/node_library/portal/portal_out.md)

- [Expression](../../../../content/animations/graph/node_library/expression/index.md)

  - [Expression Node](../../../../content/animations/graph/node_library/expression/expression.md)

- [Time](../../../../content/animations/graph/node_library/time/index.md)

  - [Time Node](../../../../content/animations/graph/node_library/time/time.md)
  - [State Time Node](../../../../content/animations/graph/node_library/time/state_time.md)
  - [Animation Ended Node](../../../../content/animations/graph/node_library/time/animation_ended.md)
  - [Anim Time Remaining Node](../../../../content/animations/graph/node_library/time/anim_time_remaining.md)
  - [Anim Time Remaining Fraction Node](../../../../content/animations/graph/node_library/time/anim_time_remaining_fraction.md)
  - [Anim Length Node](../../../../content/animations/graph/node_library/time/anim_length.md)
  - [Anim Time Node](../../../../content/animations/graph/node_library/time/anim_time.md)
  - [Anim Time Fraction Node](../../../../content/animations/graph/node_library/time/anim_time_fraction.md)

- [Constants](../../../../content/animations/graph/node_library/constant/index.md)

  - [Float Node](../../../../content/animations/graph/node_library/constant/float.md)
  - [Bool Node](../../../../content/animations/graph/node_library/constant/bool.md)
  - [Int Node](../../../../content/animations/graph/node_library/constant/int.md)
  - [Vec2 Node](../../../../content/animations/graph/node_library/constant/vec2.md)
  - [Vec3 Node](../../../../content/animations/graph/node_library/constant/vec3.md)
  - [Vec4 Node](../../../../content/animations/graph/node_library/constant/vec4.md)
  - [Ivec2 Node](../../../../content/animations/graph/node_library/constant/ivec2.md)
  - [Ivec3 Node](../../../../content/animations/graph/node_library/constant/ivec3.md)
  - [Ivec4 Node](../../../../content/animations/graph/node_library/constant/ivec4.md)
  - [Quaternion Node](../../../../content/animations/graph/node_library/constant/quaternion.md)
  - [Mat3 Node](../../../../content/animations/graph/node_library/constant/mat3.md)
  - [Mat4 Node](../../../../content/animations/graph/node_library/constant/mat4.md)

- [Math](../../../../content/animations/graph/node_library/math/index.md)

  - [Add Node](../../../../content/animations/graph/node_library/math/add.md)
  - [Subtract Node](../../../../content/animations/graph/node_library/math/subtract.md)
  - [Multiply Node](../../../../content/animations/graph/node_library/math/multiply.md)
  - [Divide Node](../../../../content/animations/graph/node_library/math/divide.md)
  - [Minimum Node](../../../../content/animations/graph/node_library/math/min.md)
  - [Maximum Node](../../../../content/animations/graph/node_library/math/max.md)
  - [Power Node](../../../../content/animations/graph/node_library/math/pow.md)
  - [FMod Node](../../../../content/animations/graph/node_library/math/fmod.md)
  - [2-Argument Arctangent Node](../../../../content/animations/graph/node_library/math/atan2.md)
  - [Step Node](../../../../content/animations/graph/node_library/math/step.md)
  - [Clamp Node](../../../../content/animations/graph/node_library/math/clamp.md)
  - [Lerp Node](../../../../content/animations/graph/node_library/math/lerp.md)
  - [Smooth Step Node](../../../../content/animations/graph/node_library/math/smooth_step.md)
  - [Sine Node](../../../../content/animations/graph/node_library/math/sin.md)
  - [Cosine Node](../../../../content/animations/graph/node_library/math/cos.md)
  - [Tangent Node](../../../../content/animations/graph/node_library/math/tan.md)
  - [ArcSine Node](../../../../content/animations/graph/node_library/math/asin.md)
  - [ArcCosine Node](../../../../content/animations/graph/node_library/math/acos.md)
  - [ArcTangent Node](../../../../content/animations/graph/node_library/math/atan.md)
  - [Absolute Node](../../../../content/animations/graph/node_library/math/abs.md)
  - [Sign Node](../../../../content/animations/graph/node_library/math/sign.md)
  - [Floor Node](../../../../content/animations/graph/node_library/math/floor.md)
  - [Ceiling Node](../../../../content/animations/graph/node_library/math/ceil.md)
  - [Round Node](../../../../content/animations/graph/node_library/math/round.md)
  - [Frac Node](../../../../content/animations/graph/node_library/math/frac.md)
  - [Square Root Node](../../../../content/animations/graph/node_library/math/sqrt.md)
  - [Saturate Node](../../../../content/animations/graph/node_library/math/saturate.md)
  - [One Minus Node](../../../../content/animations/graph/node_library/math/one_minus.md)
  - [Reciprocal Node](../../../../content/animations/graph/node_library/math/reciprocal.md)
  - [Deg To Rad Node](../../../../content/animations/graph/node_library/math/deg_to_rad.md)
  - [Rad To Deg Node](../../../../content/animations/graph/node_library/math/rad_to_deg.md)
  - [Inverse Lerp Node](../../../../content/animations/graph/node_library/math/inverse_lerp.md)
  - [Rerange Node](../../../../content/animations/graph/node_library/math/rerange.md)
  - [Base-2 Exponential Node](../../../../content/animations/graph/node_library/math/exp2.md)
  - [Base-E Exponential Node](../../../../content/animations/graph/node_library/math/exp.md)
  - [Base-2 Logarithm Node](../../../../content/animations/graph/node_library/math/log2.md)
  - [Base-10 Logarithm Node](../../../../content/animations/graph/node_library/math/log10.md)
  - [Base-E Logarithm Node](../../../../content/animations/graph/node_library/math/log.md)
  - [To Int Node](../../../../content/animations/graph/node_library/math/to_int.md)
  - [Euler to Quat Node](../../../../content/animations/graph/node_library/math/euler_to_quat.md)
  - [Quat to Euler Node](../../../../content/animations/graph/node_library/math/quat_to_euler.md)

- [Logic](../../../../content/animations/graph/node_library/comparison/index.md)

  - [Branch Node](../../../../content/animations/graph/node_library/comparison/branch.md)
  - [And Node](../../../../content/animations/graph/node_library/comparison/and.md)
  - [Or Node](../../../../content/animations/graph/node_library/comparison/or.md)
  - [Not Node](../../../../content/animations/graph/node_library/comparison/not.md)
  - [Xor Node](../../../../content/animations/graph/node_library/comparison/xor.md)
  - [Nand Node](../../../../content/animations/graph/node_library/comparison/nand.md)
  - [Nor Node](../../../../content/animations/graph/node_library/comparison/nor.md)
  - [Equal Node](../../../../content/animations/graph/node_library/comparison/equal.md)
  - [Not Equal Node](../../../../content/animations/graph/node_library/comparison/not_equal.md)
  - [Greater Node](../../../../content/animations/graph/node_library/comparison/greater.md)
  - [Less Node](../../../../content/animations/graph/node_library/comparison/less.md)
  - [Greater Equal Node](../../../../content/animations/graph/node_library/comparison/greater_equal.md)
  - [Less Equal Node](../../../../content/animations/graph/node_library/comparison/less_equal.md)
  - [Check Range Node](../../../../content/animations/graph/node_library/comparison/check_range.md)

- [Vector](../../../../content/animations/graph/node_library/vector/index.md)

  - [Dot Product Node](../../../../content/animations/graph/node_library/vector/dot_product.md)
  - [Cross Node](../../../../content/animations/graph/node_library/vector/cross.md)
  - [Normalize Node](../../../../content/animations/graph/node_library/vector/normalize.md)
  - [Length Node](../../../../content/animations/graph/node_library/vector/length.md)
  - [Length Squared Node](../../../../content/animations/graph/node_library/vector/length_squared.md)
  - [Distance Node](../../../../content/animations/graph/node_library/vector/distance.md)
  - [Reflect Node](../../../../content/animations/graph/node_library/vector/reflect.md)
  - [Angle Between Vectors Node](../../../../content/animations/graph/node_library/vector/angle_between_vectors.md)
  - [Compose Vec2 Node](../../../../content/animations/graph/node_library/vector/compose_vec2.md)
  - [Compose Vec3 Node](../../../../content/animations/graph/node_library/vector/compose_vec3.md)
  - [Compose Vec4 Node](../../../../content/animations/graph/node_library/vector/compose_vec4.md)
  - [Compose Ivec2 Node](../../../../content/animations/graph/node_library/vector/compose_ivec2.md)
  - [Compose Ivec3 Node](../../../../content/animations/graph/node_library/vector/compose_ivec3.md)
  - [Compose Ivec4 Node](../../../../content/animations/graph/node_library/vector/compose_ivec4.md)
