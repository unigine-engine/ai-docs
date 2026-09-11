# Unigine::JointLimitInfoConeTwist Class (CS)

**Inherits from:** JointLimitInfo


This class stores the parameters of a combined symmetric cone and twist joint limit: the swing of the bone is kept inside a cone and the twist around the forward axis is clamped to its own range.


A limit is applied either directly, by passing it to the matching **solveLayer*** method of the [NodeSkeletonPose](../../../../api/library/nodes/class.nodeskeletonpose_cs.md) class, or as a constraint for a chain solver - add it to a [JointLimitSetInfo](../../../../api/library/animations/skeletal/class.jointlimitsetinfo_cs.md) and assign the set to an [IKInfoChain](../../../../api/library/animations/skeletal/class.ikinfochain_cs.md) or a [LookAtChainInfo](../../../../api/library/animations/skeletal/class.lookatchaininfo_cs.md).


An instance of this class is passed to the *[SolveLayerJointConeTwistLimit()](../../../../api/library/nodes/class.nodeskeletonpose_cs.md#solveLayerJointConeTwistLimit_int_JointLimitInfoConeTwist_void)* method of the [NodeSkeletonPose](../../../../api/library/nodes/class.nodeskeletonpose_cs.md) class. All axes are set in the bind-local frame of the joint.


The same solver is available as the [Joint Cone Twist Limit](../../../../content/animations/graph/node_library/skeleton/joint_cone_twist_limit.md) node in the animation graph, which is the recommended way to set it up visually. This class is the programmatic equivalent for driving the solver from code.


## JointLimitInfoConeTwist Class

### Properties

## vec3 ForwardAxis

The bone direction in the bind-local frame of the joint. The clamp keeps this direction within the cone half-angle of the cone axis, and the twist is measured around it. The default value is (0, 1, 0).
## vec3 ConeAxis

The center direction of the cone in the bind-local frame of the joint, around which the swing of the bone is limited. It may differ from the forward axis to pre-tilt the cone. The default value is (0, 1, 0).
## float ConeAngle

The maximum swing of the bone away from the cone axis, in degrees, in the [0, 180] range. The default value is 180, which imposes no effective limit.
## float TwistMinAngle

The lower bound of the twist around the forward axis, in degrees. The default value is -180, which imposes no effective limit.
## float TwistMaxAngle

The upper bound of the twist around the forward axis, in degrees. The default value is 180, which imposes no effective limit.
### Members

---

## JointLimitInfoConeTwist ( )

Constructor. Creates a new set of joint cone twist limit parameters with default values.
