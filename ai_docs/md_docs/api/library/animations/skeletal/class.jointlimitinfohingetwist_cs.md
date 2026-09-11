# Unigine::JointLimitInfoHingeTwist Class (CS)

**Inherits from:** JointLimitInfo


This class stores the parameters of a combined hinge and twist joint limit: a rotation around the hinge axis and a twist around the forward axis, each clamped to its own range.


A limit is applied either directly, by passing it to the matching **solveLayer*** method of the [NodeSkeletonPose](../../../../api/library/nodes/class.nodeskeletonpose_cs.md) class, or as a constraint for a chain solver - add it to a [JointLimitSetInfo](../../../../api/library/animations/skeletal/class.jointlimitsetinfo_cs.md) and assign the set to an [IKInfoChain](../../../../api/library/animations/skeletal/class.ikinfochain_cs.md) or a [LookAtChainInfo](../../../../api/library/animations/skeletal/class.lookatchaininfo_cs.md).


An instance of this class is passed to the *[SolveLayerJointHingeTwistLimit()](../../../../api/library/nodes/class.nodeskeletonpose_cs.md#solveLayerJointHingeTwistLimit_int_JointLimitInfoHingeTwist_void)* method of the [NodeSkeletonPose](../../../../api/library/nodes/class.nodeskeletonpose_cs.md) class. All axes are set in the bind-local frame of the joint.


The same solver is available as the [Joint Hinge Twist Limit](../../../../content/animations/graph/node_library/skeleton/joint_hinge_twist_limit.md) node in the animation graph, which is the recommended way to set it up visually. This class is the programmatic equivalent for driving the solver from code.


## JointLimitInfoHingeTwist Class

### Properties

## vec3 ForwardAxis

The bone direction in the bind-local frame of the joint. The twist is measured around this axis. The default value is (0, 1, 0).
## vec3 HingeAxis

The axis the hinge rotation of the joint is allowed around, in the bind-local frame of the joint. The default value is (0, 1, 0).
## float HingeMinAngle

The lower bound of the rotation around the hinge axis, in degrees. The default value is -180, which imposes no effective limit.
## float HingeMaxAngle

The upper bound of the rotation around the hinge axis, in degrees. The default value is 180, which imposes no effective limit.
## float TwistMinAngle

The lower bound of the twist around the forward axis, in degrees. The default value is -180, which imposes no effective limit.
## float TwistMaxAngle

The upper bound of the twist around the forward axis, in degrees. The default value is 180, which imposes no effective limit.
### Members

---

## JointLimitInfoHingeTwist ( )

Constructor. Creates a new set of joint hinge twist limit parameters with default values.
