# Animation Graph Overview


**Animation Graph** is a visual node-based system for creating and controlling character animations in UNIGINE. It enables you to build complex animation behaviors - such as blending between idle, walk, and run cycles, setting up state machines for character locomotion, or creating layered animations - without writing low-level animation code.

   Sorry, your browser does not support embedded videos.
You compose a graph by connecting nodes in a visual editor. Each node performs a specific operation: playing an animation clip, blending between poses, evaluating conditions, or performing math. The resulting graph is automatically compiled and applied to a character's skeleton at runtime.


Animation Graph works with skinned meshes and animation clips that are created in external DCC tools (such as *3ds Max, Maya*, or *Blender*) and imported into UNIGINE as `FBX, glTF`, or `USD` files. The UnigineEditor converts them to native `*.mesh_skinned, *.skeleton`, and `*.anim` assets. The graph itself does not create animations - it controls how existing animations are played, combined, and transitioned between.


## Key Concepts


### Nodes


**Nodes** are the building blocks of an animation graph. Each node represents a specific operation: playing an animation, blending poses, performing a math calculation, or managing state transitions. Nodes have input and output ports that define what data they receive and produce.


![](graph/node_library/img/animation_player.png)

*Animation Player node: input ports on the left, output ports on the right*


### Ports and Connections


**Ports** are connection points on nodes. Input ports are located on the left side of a node, output ports on the right side. Each port has a specific [data type](#data_types) that determines which connections are valid.


**Connections** are links between an output port of one node and an input port of another. They define how data flows through the graph. Connections are type-checked: you can only connect ports with compatible data types. An output port can connect to multiple inputs, but each input port accepts only one connection.


![](ports.png)

*Nodes connected via typed ports. Port colors indicate data types: blue for Animation, green for Bool, pink for Float, yellow for AnimPose. The red Weight port signals a validation error.*


### Parameters


**Parameters** are the interface between the animation graph and application code. Each parameter has a name, a [data type](#data_types) (such as Float, Bool, or Trigger), and a default value. You define parameters in the graph editor and read or write their values at runtime via the *[AnimScript](../../api/library/animations/skeletal/class.animscript_cpp.md)* class API.


![](custom_parameter.png)

*A MoveSpeed parameter node connected to a Blend Poses input, providing a runtime-controlled value to the graph.*


## Graph Structure


An animation graph is a hierarchy of nested graphs. At the top level is the main graph stored in an `*.agraph` file. Inside it, certain nodes can contain their own nested graphs, creating a multi-level structure.


### Animation Graph (Top-Level)


The main graph is a standalone asset (`*.agraph` file) that produces the final animation pose for a character. It contains parameters that can be read and written from application code at runtime. You build the animation logic here by placing and connecting nodes - animation players, blend nodes, state machines, subgraphs, math operations, and others.


![](graph_hierarchy.png)

*An example animation graph with aState Machine, aSub Graph, and aBlend Posesnode. TheGraph Hierarchypanel on the left shows the nesting structure. By default it is located in the bottom-right corner, but can be moved to the left side of the window. See theAnimation Graph Editorarticle for details on working with the editor.*


### Sub Graph


A **Sub Graph** node references a reusable graph stored as a separate `*.asubgraph` file. Subgraphs enable you to encapsulate common animation logic - such as a locomotion blend setup or an upper-body layer - and reuse it across multiple graphs. Each subgraph defines its own input and output ports via special **Inputs** and **Outputs** nodes. When you change a subgraph, all graphs that reference it are automatically regenerated.


![](subgraph_example.png)

*A subgraph with a WaveSpeed input and a Waving Pose output of type AnimPose.*


### State Machine


A **State Machine** node contains a specialized internal graph where you define states and transitions. When you double-click a State Machine node, the editor navigates into it, showing a view where each node represents a state, and connections between states define transitions. Each state, in turn, contains its own nested subgraph with the animation logic for that state. State machines are used to organize animation logic into discrete states (such as Idle, Walking, Running, Jumping) with conditional transitions between them.


Each transition has its own nested condition graph - a small graph that outputs a boolean value determining whether the transition should fire.


![](state_machine_example.png)

*Inside the Locomotion state machine: Entry, Idle, and Walk states with Start Walk / Stop Walk condition transitions. The bottom panel shows the Idle state's internal graph - an Animation Asset connected to an Animation Player and an Output Pose node.*


## Data Types


Every port in the graph has a data type. The following types are available:


| ![](graph/node_library/img/types/float.png) **Float** | ![](graph/node_library/img/types/vec2.png) **Vec2** | ![](graph/node_library/img/types/vec3.png) **Vec3** | ![](graph/node_library/img/types/vec4.png) **Vec4** |
|---|---|---|---|
| ![](graph/node_library/img/types/int.png) **Int** | ![](graph/node_library/img/types/ivec2.png) **Ivec2** | ![](graph/node_library/img/types/ivec3.png) **Ivec3** | ![](graph/node_library/img/types/ivec4.png) **Ivec4** |
| ![](graph/node_library/img/types/mat3.png) **Mat3** - a 3�3 matrix. | ![](graph/node_library/img/types/mat4.png) **Mat4** - a 4�4 matrix. |  |  |
| ![](graph/node_library/img/types/quat.png) **Quat** - a quaternion, used for rotations. |  |  |  |
| ![](graph/node_library/img/types/bool.png) **Bool** - a boolean value (true or false). |  |  |  |
| ![](graph/node_library/img/types/trigger.png) **Trigger** - a one-shot boolean that automatically resets after being consumed. Used for one-time events such as starting a jump. |  |  |  |
| ![](graph/node_library/img/types/anim_pose.png) **AnimPose** - animation pose data containing bone transforms for a skeleton. |  |  |  |
| ![](graph/node_library/img/types/anim_asset.png) **Animation** - a reference to an animation asset. |  |  |  |
| ![](graph/node_library/img/types/constraint.png) **ConstraintRef** - a reference to a joint limit definition. It is produced by the joint limit nodes and consumed by the **[Joint Limit Set](../../content/animations/graph/node_library/skeleton/joint_limit_set.md)**, **[IK Chain](../../content/animations/graph/node_library/skeleton/ik_chain.md)**, and **[Look At Chain](../../content/animations/graph/node_library/skeleton/look_at_chain.md)** nodes. |  |  |  |
| ![](graph/node_library/img/types/undefined.png) **Undefined** - a universal port type resolved automatically based on the connected port. For example, an Undefined input that receives a Vec3 connection becomes a Vec3 port. |  |  |  |


## What's Next


This section covers all aspects of working with animation graphs - from preparing assets and building graphs in the editor to using advanced features like state machines, blend spaces, and root motion. Use the navigation panel to explore the topics.


## Articles in This Section

- [Preparing Animation Assets](../../content/animations/animation_assets/index.md)

- [Animation Graph Editor](../../content/animations/graph/index.md)

- [From Graph to Runtime](../../content/animations/compilation/index.md)

- [State Machines](../../content/animations/state_machines/index.md)

- [Animation Subgraphs](../../content/animations/sub_graphs/index.md)

- [Blend Spaces](../../content/animations/blend_spaces/index.md)

- [Blend Masks](../../content/animations/blend_masks/index.md)

- [Synchronization](../../content/animations/synchronization/index.md)

- [Root Motion](../../content/animations/root_motion/index.md)

- [Retargeting](../../content/animations/retargeting/index.md)

- [Procedural Skeleton Control](../../content/animations/procedural_control/index.md)

- [Animation Graph Nodes](../../content/animations/graph/node_library/index.md)

  - [Animation](../../content/animations/graph/node_library/animation/index.md)

    - [Animation Asset Node](../../content/animations/graph/node_library/animation/animation_asset.md)
    - [Animation Player Node](../../content/animations/graph/node_library/animation/animation_player.md)
    - [Animation Pose Node](../../content/animations/graph/node_library/animation/animation_pose.md)
  - [Blend](../../content/animations/graph/node_library/blend/index.md)

    - [Blend Poses Node](../../content/animations/graph/node_library/blend/blend_poses.md)
    - [Make Additive Node](../../content/animations/graph/node_library/blend/make_additive.md)
    - [Apply Additive Node](../../content/animations/graph/node_library/blend/apply_additive.md)
  - [Blend Space](../../content/animations/graph/node_library/blend_space/index.md)

    - [Blend Space 2D Node](../../content/animations/graph/node_library/blend_space/blend_space_2d.md)
    - [Blend Space 2D Sync Node](../../content/animations/graph/node_library/blend_space/blend_space_2d_sync.md)
  - [Transform](../../content/animations/graph/node_library/transform/index.md)

    - [Get Joint Transform Node](../../content/animations/graph/node_library/transform/get_joint_transform.md)
    - [Set Joint Transform Node](../../content/animations/graph/node_library/transform/set_joint_transform.md)
    - [Position Space Node](../../content/animations/graph/node_library/transform/position_space.md)
    - [Direction Space Node](../../content/animations/graph/node_library/transform/direction_space.md)
    - [Rotation Space Node](../../content/animations/graph/node_library/transform/rotation_space.md)
  - [Skeleton](../../content/animations/graph/node_library/skeleton/index.md)

    - [Two Bone IK Node](../../content/animations/graph/node_library/skeleton/two_bone_ik.md)
    - [IK Chain Node](../../content/animations/graph/node_library/skeleton/ik_chain.md)
    - [Joint Look At Node](../../content/animations/graph/node_library/skeleton/joint_look_at.md)
    - [Look At Chain Node](../../content/animations/graph/node_library/skeleton/look_at_chain.md)
    - [Joint Hinge Limit Node](../../content/animations/graph/node_library/skeleton/joint_hinge_limit.md)
    - [Joint Cone Limit Node](../../content/animations/graph/node_library/skeleton/joint_cone_limit.md)
    - [Joint Cone Asym Limit Node](../../content/animations/graph/node_library/skeleton/joint_cone_asym_limit.md)
    - [Joint Twist Limit Node](../../content/animations/graph/node_library/skeleton/joint_twist_limit.md)
    - [Joint Hinge Twist Limit Node](../../content/animations/graph/node_library/skeleton/joint_hinge_twist_limit.md)
    - [Joint Cone Twist Limit Node](../../content/animations/graph/node_library/skeleton/joint_cone_twist_limit.md)
    - [Joint Cone Asym Twist Limit Node](../../content/animations/graph/node_library/skeleton/joint_cone_asym_twist_limit.md)
    - [Joint Limit Set Node](../../content/animations/graph/node_library/skeleton/joint_limit_set.md)
  - [State Machine](../../content/animations/graph/node_library/state_machine/index.md)

    - [State Machine Node](../../content/animations/graph/node_library/state_machine/state_machine.md)
    - [State Node](../../content/animations/graph/node_library/state_machine/state.md)
    - [Condition Node](../../content/animations/graph/node_library/state_machine/condition.md)
    - [State Portal Node](../../content/animations/graph/node_library/state_machine/state_portal.md)
  - [Subgraph](../../content/animations/graph/node_library/subgraph/index.md)

    - [SubGraph Node](../../content/animations/graph/node_library/subgraph/sub_graph.md)
    - [SubGraph Inputs Node](../../content/animations/graph/node_library/subgraph/sub_graph_inputs.md)
    - [SubGraph Outputs Node](../../content/animations/graph/node_library/subgraph/sub_graph_outputs.md)
    - [Preview Output Pose Node](../../content/animations/graph/node_library/subgraph/preview_output_pose.md)
  - [Output](../../content/animations/graph/node_library/output/index.md)

    - [Output Pose Node](../../content/animations/graph/node_library/output/output_pose.md)
  - [Result](../../content/animations/graph/node_library/result/index.md)

    - [Transition Result Node](../../content/animations/graph/node_library/result/transition_result.md)
  - [Portal](../../content/animations/graph/node_library/portal/index.md)

    - [Portal In Node](../../content/animations/graph/node_library/portal/portal_in.md)
    - [Portal Out Node](../../content/animations/graph/node_library/portal/portal_out.md)
  - [Expression](../../content/animations/graph/node_library/expression/index.md)

    - [Expression Node](../../content/animations/graph/node_library/expression/expression.md)
  - [Time](../../content/animations/graph/node_library/time/index.md)

    - [Time Node](../../content/animations/graph/node_library/time/time.md)
    - [State Time Node](../../content/animations/graph/node_library/time/state_time.md)
    - [Animation Ended Node](../../content/animations/graph/node_library/time/animation_ended.md)
    - [Anim Time Remaining Node](../../content/animations/graph/node_library/time/anim_time_remaining.md)
    - [Anim Time Remaining Fraction Node](../../content/animations/graph/node_library/time/anim_time_remaining_fraction.md)
    - [Anim Length Node](../../content/animations/graph/node_library/time/anim_length.md)
    - [Anim Time Node](../../content/animations/graph/node_library/time/anim_time.md)
    - [Anim Time Fraction Node](../../content/animations/graph/node_library/time/anim_time_fraction.md)
  - [Constants](../../content/animations/graph/node_library/constant/index.md)

    - [Float Node](../../content/animations/graph/node_library/constant/float.md)
    - [Bool Node](../../content/animations/graph/node_library/constant/bool.md)
    - [Int Node](../../content/animations/graph/node_library/constant/int.md)
    - [Vec2 Node](../../content/animations/graph/node_library/constant/vec2.md)
    - [Vec3 Node](../../content/animations/graph/node_library/constant/vec3.md)
    - [Vec4 Node](../../content/animations/graph/node_library/constant/vec4.md)
    - [Ivec2 Node](../../content/animations/graph/node_library/constant/ivec2.md)
    - [Ivec3 Node](../../content/animations/graph/node_library/constant/ivec3.md)
    - [Ivec4 Node](../../content/animations/graph/node_library/constant/ivec4.md)
    - [Quaternion Node](../../content/animations/graph/node_library/constant/quaternion.md)
    - [Mat3 Node](../../content/animations/graph/node_library/constant/mat3.md)
    - [Mat4 Node](../../content/animations/graph/node_library/constant/mat4.md)
  - [Math](../../content/animations/graph/node_library/math/index.md)

    - [Add Node](../../content/animations/graph/node_library/math/add.md)
    - [Subtract Node](../../content/animations/graph/node_library/math/subtract.md)
    - [Multiply Node](../../content/animations/graph/node_library/math/multiply.md)
    - [Divide Node](../../content/animations/graph/node_library/math/divide.md)
    - [Minimum Node](../../content/animations/graph/node_library/math/min.md)
    - [Maximum Node](../../content/animations/graph/node_library/math/max.md)
    - [Power Node](../../content/animations/graph/node_library/math/pow.md)
    - [FMod Node](../../content/animations/graph/node_library/math/fmod.md)
    - [2-Argument Arctangent Node](../../content/animations/graph/node_library/math/atan2.md)
    - [Step Node](../../content/animations/graph/node_library/math/step.md)
    - [Clamp Node](../../content/animations/graph/node_library/math/clamp.md)
    - [Lerp Node](../../content/animations/graph/node_library/math/lerp.md)
    - [Smooth Step Node](../../content/animations/graph/node_library/math/smooth_step.md)
    - [Sine Node](../../content/animations/graph/node_library/math/sin.md)
    - [Cosine Node](../../content/animations/graph/node_library/math/cos.md)
    - [Tangent Node](../../content/animations/graph/node_library/math/tan.md)
    - [ArcSine Node](../../content/animations/graph/node_library/math/asin.md)
    - [ArcCosine Node](../../content/animations/graph/node_library/math/acos.md)
    - [ArcTangent Node](../../content/animations/graph/node_library/math/atan.md)
    - [Absolute Node](../../content/animations/graph/node_library/math/abs.md)
    - [Sign Node](../../content/animations/graph/node_library/math/sign.md)
    - [Floor Node](../../content/animations/graph/node_library/math/floor.md)
    - [Ceiling Node](../../content/animations/graph/node_library/math/ceil.md)
    - [Round Node](../../content/animations/graph/node_library/math/round.md)
    - [Frac Node](../../content/animations/graph/node_library/math/frac.md)
    - [Square Root Node](../../content/animations/graph/node_library/math/sqrt.md)
    - [Saturate Node](../../content/animations/graph/node_library/math/saturate.md)
    - [One Minus Node](../../content/animations/graph/node_library/math/one_minus.md)
    - [Reciprocal Node](../../content/animations/graph/node_library/math/reciprocal.md)
    - [Deg To Rad Node](../../content/animations/graph/node_library/math/deg_to_rad.md)
    - [Rad To Deg Node](../../content/animations/graph/node_library/math/rad_to_deg.md)
    - [Inverse Lerp Node](../../content/animations/graph/node_library/math/inverse_lerp.md)
    - [Rerange Node](../../content/animations/graph/node_library/math/rerange.md)
    - [Base-2 Exponential Node](../../content/animations/graph/node_library/math/exp2.md)
    - [Base-E Exponential Node](../../content/animations/graph/node_library/math/exp.md)
    - [Base-2 Logarithm Node](../../content/animations/graph/node_library/math/log2.md)
    - [Base-10 Logarithm Node](../../content/animations/graph/node_library/math/log10.md)
    - [Base-E Logarithm Node](../../content/animations/graph/node_library/math/log.md)
    - [To Int Node](../../content/animations/graph/node_library/math/to_int.md)
    - [Euler to Quat Node](../../content/animations/graph/node_library/math/euler_to_quat.md)
    - [Quat to Euler Node](../../content/animations/graph/node_library/math/quat_to_euler.md)
  - [Logic](../../content/animations/graph/node_library/comparison/index.md)

    - [Branch Node](../../content/animations/graph/node_library/comparison/branch.md)
    - [And Node](../../content/animations/graph/node_library/comparison/and.md)
    - [Or Node](../../content/animations/graph/node_library/comparison/or.md)
    - [Not Node](../../content/animations/graph/node_library/comparison/not.md)
    - [Xor Node](../../content/animations/graph/node_library/comparison/xor.md)
    - [Nand Node](../../content/animations/graph/node_library/comparison/nand.md)
    - [Nor Node](../../content/animations/graph/node_library/comparison/nor.md)
    - [Equal Node](../../content/animations/graph/node_library/comparison/equal.md)
    - [Not Equal Node](../../content/animations/graph/node_library/comparison/not_equal.md)
    - [Greater Node](../../content/animations/graph/node_library/comparison/greater.md)
    - [Less Node](../../content/animations/graph/node_library/comparison/less.md)
    - [Greater Equal Node](../../content/animations/graph/node_library/comparison/greater_equal.md)
    - [Less Equal Node](../../content/animations/graph/node_library/comparison/less_equal.md)
    - [Check Range Node](../../content/animations/graph/node_library/comparison/check_range.md)
  - [Vector](../../content/animations/graph/node_library/vector/index.md)

    - [Dot Product Node](../../content/animations/graph/node_library/vector/dot_product.md)
    - [Cross Node](../../content/animations/graph/node_library/vector/cross.md)
    - [Normalize Node](../../content/animations/graph/node_library/vector/normalize.md)
    - [Length Node](../../content/animations/graph/node_library/vector/length.md)
    - [Length Squared Node](../../content/animations/graph/node_library/vector/length_squared.md)
    - [Distance Node](../../content/animations/graph/node_library/vector/distance.md)
    - [Reflect Node](../../content/animations/graph/node_library/vector/reflect.md)
    - [Angle Between Vectors Node](../../content/animations/graph/node_library/vector/angle_between_vectors.md)
    - [Compose Vec2 Node](../../content/animations/graph/node_library/vector/compose_vec2.md)
    - [Compose Vec3 Node](../../content/animations/graph/node_library/vector/compose_vec3.md)
    - [Compose Vec4 Node](../../content/animations/graph/node_library/vector/compose_vec4.md)
    - [Compose Ivec2 Node](../../content/animations/graph/node_library/vector/compose_ivec2.md)
    - [Compose Ivec3 Node](../../content/animations/graph/node_library/vector/compose_ivec3.md)
    - [Compose Ivec4 Node](../../content/animations/graph/node_library/vector/compose_ivec4.md)
