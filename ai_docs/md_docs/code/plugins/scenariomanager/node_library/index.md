# Scenario Manager Node Library


This article lists all nodes available in the [Scenario Manager](../../../../code/plugins/scenariomanager/index.md), organized by category as they appear in the node palette of the [editor](../../../../code/plugins/scenariomanager/editor.md). Each node performs a single operation - from controlling the order of execution and reacting to events to reading and writing [DataBridge](../../../../code/plugins/databridge/index_cpp.md) parameters.


## Execution and Data Nodes


Nodes are of two kinds, and the difference is visible from their ports:


- **Execution nodes** have white *[execution ports](../../../../code/plugins/scenariomanager/index.md#port_concept)*. They are a part of the execution chain and run when the flow reaches them, in the order the white wires define.
- **Data nodes** have no execution ports. They are evaluated only when another node requests their output, and only as often as that output is needed.


An execution node placed on the canvas but not connected to the execution chain never runs, while a data node connected to nothing is simply never evaluated.


## Port Types


Every port has a *[data type](../../../../code/plugins/scenariomanager/index.md#sm_types)* that determines which connections are valid: types must either match or be implicitly convertible.


Ports of the Any type have no fixed type - it is resolved automatically from the port they are connected to. For example, an Any input that receives a Vec3 connection becomes a Vec3 port, and the node's output usually follows it.


## Parameters and Default Values


Many nodes have parameters set directly in the node body. A parameter is used when the corresponding input port has no connection - as soon as a wire is attached to that port, the value coming through the wire is used instead.


## See Also


- [Scenario Manager Plugin](../../../../code/plugins/scenariomanager/index.md)
- [Scenario Manager Editor](../../../../code/plugins/scenariomanager/editor.md)
- [From Graph to Runtime](../../../../code/plugins/scenariomanager/runtime.md)
- [Preparing Assets](../../../../code/plugins/scenariomanager/assets.md)
- *[ScenarioManager Plugin](../../../../api/library/plugins/scenariomanager/index.md)* classes


## Articles in This Section

- [Array](../../../../code/plugins/scenariomanager/node_library/array/index.md)

  - [Array Append Node](../../../../code/plugins/scenariomanager/node_library/array/append.md)
  - [Array Clear Node](../../../../code/plugins/scenariomanager/node_library/array/clear.md)
  - [Array Create Node](../../../../code/plugins/scenariomanager/node_library/array/create.md)
  - [For Each Node](../../../../code/plugins/scenariomanager/node_library/array/for_each.md)
  - [Get Element Node](../../../../code/plugins/scenariomanager/node_library/array/get.md)
  - [Array Length Node](../../../../code/plugins/scenariomanager/node_library/array/length.md)
  - [Array Make Node](../../../../code/plugins/scenariomanager/node_library/array/make.md)
  - [Set Element Node](../../../../code/plugins/scenariomanager/node_library/array/set.md)

- [Constants](../../../../code/plugins/scenariomanager/node_library/constants/index.md)

  - [Bool Node](../../../../code/plugins/scenariomanager/node_library/constants/bool.md)
  - [DMat4 Identity Node](../../../../code/plugins/scenariomanager/node_library/constants/dmat4.md)
  - [DVec2 Node](../../../../code/plugins/scenariomanager/node_library/constants/dvec2.md)
  - [DVec3 Node](../../../../code/plugins/scenariomanager/node_library/constants/dvec3.md)
  - [DVec4 Node](../../../../code/plugins/scenariomanager/node_library/constants/dvec4.md)
  - [Float Node](../../../../code/plugins/scenariomanager/node_library/constants/float.md)
  - [Int Node](../../../../code/plugins/scenariomanager/node_library/constants/int.md)
  - [IVec2 Node](../../../../code/plugins/scenariomanager/node_library/constants/ivec2.md)
  - [IVec3 Node](../../../../code/plugins/scenariomanager/node_library/constants/ivec3.md)
  - [IVec4 Node](../../../../code/plugins/scenariomanager/node_library/constants/ivec4.md)
  - [Mat2 Identity Node](../../../../code/plugins/scenariomanager/node_library/constants/mat2.md)
  - [Mat3 Identity Node](../../../../code/plugins/scenariomanager/node_library/constants/mat3.md)
  - [Mat4 Identity Node](../../../../code/plugins/scenariomanager/node_library/constants/mat4.md)
  - [Quat Node](../../../../code/plugins/scenariomanager/node_library/constants/quat.md)
  - [String Node](../../../../code/plugins/scenariomanager/node_library/constants/string.md)
  - [Vec2 Node](../../../../code/plugins/scenariomanager/node_library/constants/vec2.md)
  - [Vec3 Node](../../../../code/plugins/scenariomanager/node_library/constants/vec3.md)
  - [Vec4 Node](../../../../code/plugins/scenariomanager/node_library/constants/vec4.md)

- [Convert](../../../../code/plugins/scenariomanager/node_library/convert/index.md)

  - [Float to Int Node](../../../../code/plugins/scenariomanager/node_library/convert/float_to_int.md)
  - [Int to Float Node](../../../../code/plugins/scenariomanager/node_library/convert/int_to_float.md)
  - [To Bool Node](../../../../code/plugins/scenariomanager/node_library/convert/to_bool.md)
  - [To Float Node](../../../../code/plugins/scenariomanager/node_library/convert/to_float.md)
  - [To Int Node](../../../../code/plugins/scenariomanager/node_library/convert/to_int.md)

- [DataBridge](../../../../code/plugins/scenariomanager/node_library/databridge/index.md)

  - [Batch Set Node](../../../../code/plugins/scenariomanager/node_library/databridge/batch_set.md)
  - [Get Parameter Node](../../../../code/plugins/scenariomanager/node_library/databridge/get.md)
  - [List Children Node](../../../../code/plugins/scenariomanager/node_library/databridge/list_children.md)
  - [On Parameter Changed Node](../../../../code/plugins/scenariomanager/node_library/databridge/on_changed.md)
  - [Path Builder Node](../../../../code/plugins/scenariomanager/node_library/databridge/path_builder.md)
  - [Set Parameter Node](../../../../code/plugins/scenariomanager/node_library/databridge/set.md)

- [Debug](../../../../code/plugins/scenariomanager/node_library/debug/index.md)

  - [Assert Node](../../../../code/plugins/scenariomanager/node_library/debug/assert.md)
  - [Comment Node](../../../../code/plugins/scenariomanager/node_library/debug/comment.md)
  - [Console Command Node](../../../../code/plugins/scenariomanager/node_library/debug/console.md)
  - [Format Log Node](../../../../code/plugins/scenariomanager/node_library/debug/flog.md)
  - [Log Node](../../../../code/plugins/scenariomanager/node_library/debug/log.md)
  - [Print to Screen Node](../../../../code/plugins/scenariomanager/node_library/debug/print_screen.md)

- [Events](../../../../code/plugins/scenariomanager/node_library/events/index.md)

  - [On Event Node](../../../../code/plugins/scenariomanager/node_library/events/on_event.md)
  - [On Init Node](../../../../code/plugins/scenariomanager/node_library/events/on_init.md)
  - [On Shutdown Node](../../../../code/plugins/scenariomanager/node_library/events/on_shutdown.md)
  - [On Timer Node](../../../../code/plugins/scenariomanager/node_library/events/on_timer.md)
  - [On Update Node](../../../../code/plugins/scenariomanager/node_library/events/on_update.md)
  - [Send Event Node](../../../../code/plugins/scenariomanager/node_library/events/send_event.md)

- [Flow](../../../../code/plugins/scenariomanager/node_library/flow/index.md)

  - [Branch Node](../../../../code/plugins/scenariomanager/node_library/flow/branch.md)
  - [Conditional Sequence Node](../../../../code/plugins/scenariomanager/node_library/flow/cond_sequence.md)
  - [Delay Node](../../../../code/plugins/scenariomanager/node_library/flow/delay.md)
  - [Do N Node](../../../../code/plugins/scenariomanager/node_library/flow/do_n.md)
  - [Do Once Node](../../../../code/plugins/scenariomanager/node_library/flow/do_once.md)
  - [For Loop Node](../../../../code/plugins/scenariomanager/node_library/flow/for_loop.md)
  - [Gate Node](../../../../code/plugins/scenariomanager/node_library/flow/gate.md)
  - [Latch Node](../../../../code/plugins/scenariomanager/node_library/flow/latch.md)
  - [Run Script Node](../../../../code/plugins/scenariomanager/node_library/flow/run_script.md)
  - [Select Node](../../../../code/plugins/scenariomanager/node_library/flow/select.md)
  - [Sequence Node](../../../../code/plugins/scenariomanager/node_library/flow/sequence.md)
  - [Stop Script Node](../../../../code/plugins/scenariomanager/node_library/flow/stop_script.md)
  - [Switch Node](../../../../code/plugins/scenariomanager/node_library/flow/switch.md)
  - [Throttle Node](../../../../code/plugins/scenariomanager/node_library/flow/throttle.md)
  - [Wait All Node](../../../../code/plugins/scenariomanager/node_library/flow/wait_all.md)
  - [Wait Any Node](../../../../code/plugins/scenariomanager/node_library/flow/wait_any.md)
  - [Wait Until Node](../../../../code/plugins/scenariomanager/node_library/flow/wait_until.md)
  - [Wait While Node](../../../../code/plugins/scenariomanager/node_library/flow/wait_while.md)
  - [While Loop Node](../../../../code/plugins/scenariomanager/node_library/flow/while_loop.md)

- [Math](../../../../code/plugins/scenariomanager/node_library/math/index.md)

  - [Abs Node](../../../../code/plugins/scenariomanager/node_library/math/abs.md)
  - [Add Node](../../../../code/plugins/scenariomanager/node_library/math/add.md)
  - [Ceil Node](../../../../code/plugins/scenariomanager/node_library/math/ceil.md)
  - [Divide Node](../../../../code/plugins/scenariomanager/node_library/math/divide.md)
  - [Floor Node](../../../../code/plugins/scenariomanager/node_library/math/floor.md)
  - [Log Node](../../../../code/plugins/scenariomanager/node_library/math/log.md)
  - [Max Node](../../../../code/plugins/scenariomanager/node_library/math/max.md)
  - [Min Node](../../../../code/plugins/scenariomanager/node_library/math/min.md)
  - [Modulo Node](../../../../code/plugins/scenariomanager/node_library/math/modulo.md)
  - [Multiply Node](../../../../code/plugins/scenariomanager/node_library/math/multiply.md)
  - [Negate Node](../../../../code/plugins/scenariomanager/node_library/math/negate.md)
  - [Pow Node](../../../../code/plugins/scenariomanager/node_library/math/pow.md)
  - [Round Node](../../../../code/plugins/scenariomanager/node_library/math/round.md)
  - [Sign Node](../../../../code/plugins/scenariomanager/node_library/math/sign.md)
  - [Sqrt Node](../../../../code/plugins/scenariomanager/node_library/math/sqrt.md)
  - [Subtract Node](../../../../code/plugins/scenariomanager/node_library/math/subtract.md)
  - [Compare](../../../../code/plugins/scenariomanager/node_library/math/compare/index.md)

    - [Equal Node](../../../../code/plugins/scenariomanager/node_library/math/compare/equal.md)
    - [Greater Node](../../../../code/plugins/scenariomanager/node_library/math/compare/greater.md)
    - [GreaterEqual Node](../../../../code/plugins/scenariomanager/node_library/math/compare/greater_eq.md)
    - [Less Node](../../../../code/plugins/scenariomanager/node_library/math/compare/less.md)
    - [LessEqual Node](../../../../code/plugins/scenariomanager/node_library/math/compare/less_eq.md)
    - [NotEqual Node](../../../../code/plugins/scenariomanager/node_library/math/compare/not_equal.md)
  - [Curves](../../../../code/plugins/scenariomanager/node_library/math/curves/index.md)

    - [Bezier Node](../../../../code/plugins/scenariomanager/node_library/math/curves/bezier.md)
    - [Bezier Vec3 Node](../../../../code/plugins/scenariomanager/node_library/math/curves/bezier_vec3.md)
    - [CatmullRom Node](../../../../code/plugins/scenariomanager/node_library/math/curves/catmullrom.md)
    - [CatmullRom Vec3 Node](../../../../code/plugins/scenariomanager/node_library/math/curves/catmullrom_vec3.md)
  - [Interpolation](../../../../code/plugins/scenariomanager/node_library/math/interpolation/index.md)

    - [Clamp Node](../../../../code/plugins/scenariomanager/node_library/math/interpolation/clamp.md)
    - [Inverse Lerp Node](../../../../code/plugins/scenariomanager/node_library/math/interpolation/inverse_lerp.md)
    - [Lerp Node](../../../../code/plugins/scenariomanager/node_library/math/interpolation/lerp.md)
    - [Remap Node](../../../../code/plugins/scenariomanager/node_library/math/interpolation/remap.md)
    - [SmoothDamp Node](../../../../code/plugins/scenariomanager/node_library/math/interpolation/smoothdamp.md)
    - [SmoothStep Node](../../../../code/plugins/scenariomanager/node_library/math/interpolation/smoothstep.md)
  - [Logic](../../../../code/plugins/scenariomanager/node_library/math/logic/index.md)

    - [ALL Node](../../../../code/plugins/scenariomanager/node_library/math/logic/all.md)
    - [AND Node](../../../../code/plugins/scenariomanager/node_library/math/logic/and.md)
    - [ANY Node](../../../../code/plugins/scenariomanager/node_library/math/logic/any.md)
    - [NOT Node](../../../../code/plugins/scenariomanager/node_library/math/logic/not.md)
    - [OR Node](../../../../code/plugins/scenariomanager/node_library/math/logic/or.md)
    - [XOR Node](../../../../code/plugins/scenariomanager/node_library/math/logic/xor.md)
  - [Random](../../../../code/plugins/scenariomanager/node_library/math/random/index.md)

    - [Random Float Node](../../../../code/plugins/scenariomanager/node_library/math/random/random_float.md)
    - [Random Int Node](../../../../code/plugins/scenariomanager/node_library/math/random/random_int.md)
    - [Random Vec3 Node](../../../../code/plugins/scenariomanager/node_library/math/random/random_vec3.md)
    - [Set Seed Node](../../../../code/plugins/scenariomanager/node_library/math/random/set_seed.md)
  - [Trig](../../../../code/plugins/scenariomanager/node_library/math/trig/index.md)

    - [Acos Node](../../../../code/plugins/scenariomanager/node_library/math/trig/acos.md)
    - [Asin Node](../../../../code/plugins/scenariomanager/node_library/math/trig/asin.md)
    - [Atan2 Node](../../../../code/plugins/scenariomanager/node_library/math/trig/atan2.md)
    - [Cos Node](../../../../code/plugins/scenariomanager/node_library/math/trig/cos.md)
    - [Sin Node](../../../../code/plugins/scenariomanager/node_library/math/trig/sin.md)
    - [Tan Node](../../../../code/plugins/scenariomanager/node_library/math/trig/tan.md)

- [Matrix](../../../../code/plugins/scenariomanager/node_library/matrix/index.md)

  - [Compose TRS Node](../../../../code/plugins/scenariomanager/node_library/matrix/compose.md)
  - [Decompose TRS Node](../../../../code/plugins/scenariomanager/node_library/matrix/decompose.md)
  - [Mat4 inverse Node](../../../../code/plugins/scenariomanager/node_library/matrix/inverse.md)
  - [Mat4 Multiply Node](../../../../code/plugins/scenariomanager/node_library/matrix/multiply.md)
  - [Mat4 x Vec4 Node](../../../../code/plugins/scenariomanager/node_library/matrix/transform_vec4.md)
  - [Mat4 Transpose Node](../../../../code/plugins/scenariomanager/node_library/matrix/transpose.md)
  - [Break](../../../../code/plugins/scenariomanager/node_library/matrix/break/index.md)

    - [Break DMat4 Node](../../../../code/plugins/scenariomanager/node_library/matrix/break/dmat4.md)
    - [Break Mat2 Node](../../../../code/plugins/scenariomanager/node_library/matrix/break/mat2.md)
    - [Break Mat3 Node](../../../../code/plugins/scenariomanager/node_library/matrix/break/mat3.md)
  - [Convert](../../../../code/plugins/scenariomanager/node_library/matrix/convert/index.md)

    - [Mat3 to Mat4 Node](../../../../code/plugins/scenariomanager/node_library/matrix/convert/mat3_to_mat4.md)
    - [Mat3 to Quat Node](../../../../code/plugins/scenariomanager/node_library/matrix/convert/mat3_to_quat.md)
    - [Mat4 to Mat3 Node](../../../../code/plugins/scenariomanager/node_library/matrix/convert/mat4_to_mat3.md)
    - [Mat4 to Quat Node](../../../../code/plugins/scenariomanager/node_library/matrix/convert/mat4_to_quat.md)
    - [Quat to Mat3 Node](../../../../code/plugins/scenariomanager/node_library/matrix/convert/quat_to_mat3.md)
  - [Make](../../../../code/plugins/scenariomanager/node_library/matrix/make/index.md)

    - [Make DMat4 Node](../../../../code/plugins/scenariomanager/node_library/matrix/make/dmat4.md)
    - [Make Mat2 Node](../../../../code/plugins/scenariomanager/node_library/matrix/make/mat2.md)
    - [Make Mat3 (columns) Node](../../../../code/plugins/scenariomanager/node_library/matrix/make/mat3_columns.md)
    - [Make Mat3 (Quat) Node](../../../../code/plugins/scenariomanager/node_library/matrix/make/mat3_quat.md)

- [Quaternion](../../../../code/plugins/scenariomanager/node_library/quaternion/index.md)

  - [Euler to Quat Node](../../../../code/plugins/scenariomanager/node_library/quaternion/from_euler.md)
  - [Quat Inverse Node](../../../../code/plugins/scenariomanager/node_library/quaternion/inverse.md)
  - [Quat Multiply Node](../../../../code/plugins/scenariomanager/node_library/quaternion/multiply.md)
  - [Rotate Vector Node](../../../../code/plugins/scenariomanager/node_library/quaternion/rotate_vec.md)
  - [Slerp Node](../../../../code/plugins/scenariomanager/node_library/quaternion/slerp.md)
  - [Quat to Euler Node](../../../../code/plugins/scenariomanager/node_library/quaternion/to_euler.md)
  - [Break](../../../../code/plugins/scenariomanager/node_library/quaternion/break/index.md)

    - [Break Quat Node](../../../../code/plugins/scenariomanager/node_library/quaternion/break/quat.md)
  - [Make](../../../../code/plugins/scenariomanager/node_library/quaternion/make/index.md)

    - [Make Quat Node](../../../../code/plugins/scenariomanager/node_library/quaternion/make/quat.md)

- [Script](../../../../code/plugins/scenariomanager/node_library/script/index.md)

  - [Get Entity ID Node](../../../../code/plugins/scenariomanager/node_library/script/entity_id.md)
  - [Find Script By Name Node](../../../../code/plugins/scenariomanager/node_library/script/find_script.md)
  - [Get My Script ID Node](../../../../code/plugins/scenariomanager/node_library/script/my_script_id.md)
  - [Get My Script Name Node](../../../../code/plugins/scenariomanager/node_library/script/my_script_name.md)

- [String](../../../../code/plugins/scenariomanager/node_library/string/index.md)

  - [Format Node](../../../../code/plugins/scenariomanager/node_library/string/format.md)
  - [String to Float Node](../../../../code/plugins/scenariomanager/node_library/string/string_to_float.md)
  - [String to Int Node](../../../../code/plugins/scenariomanager/node_library/string/string_to_int.md)
  - [To String Node](../../../../code/plugins/scenariomanager/node_library/string/to_string.md)

- [Subgraph](../../../../code/plugins/scenariomanager/node_library/subgraph/index.md)

  - [Event Subgraph Node](../../../../code/plugins/scenariomanager/node_library/subgraph/event_ref.md)
  - [Exec Done Node](../../../../code/plugins/scenariomanager/node_library/subgraph/exec_done.md)
  - [Exec Trigger Node](../../../../code/plugins/scenariomanager/node_library/subgraph/exec_trigger.md)
  - [Subgraph Input Node](../../../../code/plugins/scenariomanager/node_library/subgraph/input.md)
  - [Subgraph Output Node](../../../../code/plugins/scenariomanager/node_library/subgraph/output.md)
  - [Subgraph Node](../../../../code/plugins/scenariomanager/node_library/subgraph/ref.md)
  - [Portal](../../../../code/plugins/scenariomanager/node_library/subgraph/portal/index.md)

    - [Data Portal In Node](../../../../code/plugins/scenariomanager/node_library/subgraph/portal/data_in.md)
    - [Data Portal Out Node](../../../../code/plugins/scenariomanager/node_library/subgraph/portal/data_out.md)
    - [Exec Portal In Node](../../../../code/plugins/scenariomanager/node_library/subgraph/portal/exec_in.md)
    - [Exec Portal Out Node](../../../../code/plugins/scenariomanager/node_library/subgraph/portal/exec_out.md)

- [Time](../../../../code/plugins/scenariomanager/node_library/time/index.md)

  - [Delta Time Node](../../../../code/plugins/scenariomanager/node_library/time/dt.md)
  - [Frame Count Node](../../../../code/plugins/scenariomanager/node_library/time/frame.md)
  - [Game Time Node](../../../../code/plugins/scenariomanager/node_library/time/time.md)

- [Variables](../../../../code/plugins/scenariomanager/node_library/variables/index.md)

  - [Get Variable Node](../../../../code/plugins/scenariomanager/node_library/variables/get.md)
  - [Get Global Node](../../../../code/plugins/scenariomanager/node_library/variables/get_global.md)
  - [Set Variable Node](../../../../code/plugins/scenariomanager/node_library/variables/set.md)
  - [Set Global Node](../../../../code/plugins/scenariomanager/node_library/variables/set_global.md)

- [Vector](../../../../code/plugins/scenariomanager/node_library/vector/index.md)

  - [Vec3 Add Node](../../../../code/plugins/scenariomanager/node_library/vector/add.md)
  - [Cross Node](../../../../code/plugins/scenariomanager/node_library/vector/cross.md)
  - [Vec3 Distance Node](../../../../code/plugins/scenariomanager/node_library/vector/distance.md)
  - [Vec3 Distance2 Node](../../../../code/plugins/scenariomanager/node_library/vector/distance2.md)
  - [Dot Node](../../../../code/plugins/scenariomanager/node_library/vector/dot.md)
  - [Length Node](../../../../code/plugins/scenariomanager/node_library/vector/length.md)
  - [Vec3 Lerp Node](../../../../code/plugins/scenariomanager/node_library/vector/lerp.md)
  - [Vec3 Multiply Add Node](../../../../code/plugins/scenariomanager/node_library/vector/mad.md)
  - [Vec3 negate Node](../../../../code/plugins/scenariomanager/node_library/vector/negate.md)
  - [Vec3 Normalize Node](../../../../code/plugins/scenariomanager/node_library/vector/normalize.md)
  - [Reflect Node](../../../../code/plugins/scenariomanager/node_library/vector/reflect.md)
  - [Vec3 Scale Node](../../../../code/plugins/scenariomanager/node_library/vector/scale.md)
  - [Vec3 Sub Node](../../../../code/plugins/scenariomanager/node_library/vector/subtract.md)
  - [Break](../../../../code/plugins/scenariomanager/node_library/vector/break/index.md)

    - [Break DVec2 Node](../../../../code/plugins/scenariomanager/node_library/vector/break/dvec2.md)
    - [Break DVec3 Node](../../../../code/plugins/scenariomanager/node_library/vector/break/dvec3.md)
    - [Break DVec4 Node](../../../../code/plugins/scenariomanager/node_library/vector/break/dvec4.md)
    - [Break IVec2 Node](../../../../code/plugins/scenariomanager/node_library/vector/break/ivec2.md)
    - [Break IVec3 Node](../../../../code/plugins/scenariomanager/node_library/vector/break/ivec3.md)
    - [Break IVec4 Node](../../../../code/plugins/scenariomanager/node_library/vector/break/ivec4.md)
    - [Break Vec2 Node](../../../../code/plugins/scenariomanager/node_library/vector/break/vec2.md)
    - [Break Vec3 Node](../../../../code/plugins/scenariomanager/node_library/vector/break/vec3.md)
    - [Break Vec4 Node](../../../../code/plugins/scenariomanager/node_library/vector/break/vec4.md)
  - [Convert](../../../../code/plugins/scenariomanager/node_library/vector/convert/index.md)

    - [DVec2 to Vec2 Node](../../../../code/plugins/scenariomanager/node_library/vector/convert/dvec2_to_vec2.md)
    - [DVec3 to Vec3 Node](../../../../code/plugins/scenariomanager/node_library/vector/convert/dvec3_to_vec3.md)
    - [DVec4 to Vec4 Node](../../../../code/plugins/scenariomanager/node_library/vector/convert/dvec4_to_vec4.md)
    - [IVec2 to Vec2 Node](../../../../code/plugins/scenariomanager/node_library/vector/convert/ivec2_to_vec2.md)
    - [IVec3 to Vec3 Node](../../../../code/plugins/scenariomanager/node_library/vector/convert/ivec3_to_vec3.md)
    - [IVec4 to Vec4 Node](../../../../code/plugins/scenariomanager/node_library/vector/convert/ivec4_to_vec4.md)
    - [Vec2 to DVec2 Node](../../../../code/plugins/scenariomanager/node_library/vector/convert/vec2_to_dvec2.md)
    - [Vec2 to IVec2 Node](../../../../code/plugins/scenariomanager/node_library/vector/convert/vec2_to_ivec2.md)
    - [Vec2 to Vec3 Node](../../../../code/plugins/scenariomanager/node_library/vector/convert/vec2_to_vec3.md)
    - [Vec3 to DVec3 Node](../../../../code/plugins/scenariomanager/node_library/vector/convert/vec3_to_dvec3.md)
    - [Vec3 to IVec3 Node](../../../../code/plugins/scenariomanager/node_library/vector/convert/vec3_to_ivec3.md)
    - [Vec3 to Vec2 Node](../../../../code/plugins/scenariomanager/node_library/vector/convert/vec3_to_vec2.md)
    - [Vec3 to Vec4 Node](../../../../code/plugins/scenariomanager/node_library/vector/convert/vec3_to_vec4.md)
    - [Vec4 to DVec4 Node](../../../../code/plugins/scenariomanager/node_library/vector/convert/vec4_to_dvec4.md)
    - [Vec4 to IVec4 Node](../../../../code/plugins/scenariomanager/node_library/vector/convert/vec4_to_ivec4.md)
    - [Vec4 to Vec3 Node](../../../../code/plugins/scenariomanager/node_library/vector/convert/vec4_to_vec3.md)
  - [Make](../../../../code/plugins/scenariomanager/node_library/vector/make/index.md)

    - [Make DVec2 Node](../../../../code/plugins/scenariomanager/node_library/vector/make/dvec2.md)
    - [Make DVec3 Node](../../../../code/plugins/scenariomanager/node_library/vector/make/dvec3.md)
    - [Make DVec4 Node](../../../../code/plugins/scenariomanager/node_library/vector/make/dvec4.md)
    - [Make IVec2 Node](../../../../code/plugins/scenariomanager/node_library/vector/make/ivec2.md)
    - [Make IVec3 Node](../../../../code/plugins/scenariomanager/node_library/vector/make/ivec3.md)
    - [Make IVec4 Node](../../../../code/plugins/scenariomanager/node_library/vector/make/ivec4.md)
    - [Make Vec2 Node](../../../../code/plugins/scenariomanager/node_library/vector/make/vec2.md)
    - [Make Vec3 Node](../../../../code/plugins/scenariomanager/node_library/vector/make/vec3.md)
    - [Make Vec4 Node](../../../../code/plugins/scenariomanager/node_library/vector/make/vec4.md)
