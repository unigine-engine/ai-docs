# Unigine::LookAtInfo Class (CS)


This class stores the parameters of the single-joint Look At solver. The solver rotates one joint so that its local forward axis points at the target. Unlike inverse kinematics, which reaches a target **position**, it aims in a target **direction** and affects rotation only.


An instance of this class is passed to the *[SolveLayerLookAt()](../../../../api/library/nodes/class.nodeskeletonpose_cs.md#solveLayerLookAt_int_LookAtInfo_void)* method of the [NodeSkeletonPose](../../../../api/library/nodes/class.nodeskeletonpose_cs.md) class.


The same solver is available as the [Joint Look At](../../../../content/animations/graph/node_library/skeleton/joint_look_at.md) node in the animation graph, which is the recommended way to set it up visually. This class is the programmatic equivalent for driving the solver from code.


## LookAtInfo Class

### Properties

## int Joint

The index of the joint that is rotated toward the target. The default value is -1.
## vec3 ForwardAxis

The local axis of the joint that is aimed at the target. The default value is (0, 1, 0).
## vec3 UpAxis

The local up axis of the joint used as the twist reference when the pole is applied. The default value is (0, 0, 1).
## vec3 Target

The position the forward axis of the joint is aimed at, in the object space of the skeleton. The default value is (0, 0, 0).
## vec3 Pole

The position used as the up reference for the twist correction of the joint. It is used only when *[UsePole](../../../...md#isUsePole_int)* is enabled and a valid up axis is set. The default value is (0, 0, 0).
## float Weight

The blend weight of the Look At result over the input pose, in the [0, 1] range. The default value is 1.0.
## bool UsePole

The value indicating if the pole is used to control the twist of the joint around its aim direction. The default value is false.
## float MaxAngle

The maximum rotation deviation from the animation pose, in degrees, in the [0, 180] range. The clamp is applied relative to the animation pose, not frame to frame, so the joint does not chase a target that jumps beyond this angle. The default value is 180, which imposes no effective limit.
### Members

---

## LookAtInfo ( )

Constructor. Creates a new set of Look At parameters with default values.
