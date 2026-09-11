# Unigine::JointLimitInfoTwist Class (CS)

**Inherits from:** JointLimitInfo


This class stores the parameters of a twist joint limit. The rotation around the bone is kept within a range while the swing is left free. Use it for a forearm, or pair it with a swing limit on the same joint.


A limit is applied either directly, by passing it to the matching **solveLayer*** method of the [NodeSkeletonPose](../../../../api/library/nodes/class.nodeskeletonpose_cs.md) class, or as a constraint for a chain solver - add it to a [JointLimitSetInfo](../../../../api/library/animations/skeletal/class.jointlimitsetinfo_cs.md) and assign the set to an [IKInfoChain](../../../../api/library/animations/skeletal/class.ikinfochain_cs.md) or a [LookAtChainInfo](../../../../api/library/animations/skeletal/class.lookatchaininfo_cs.md).


An instance of this class is passed to the *[SolveLayerJointTwistLimit()](../../../../api/library/nodes/class.nodeskeletonpose_cs.md#solveLayerJointTwistLimit_int_JointLimitInfoTwist_void)* method of the [NodeSkeletonPose](../../../../api/library/nodes/class.nodeskeletonpose_cs.md) class. All axes are set in the bind-local frame of the joint.


The same solver is available as the [Joint Twist Limit](../../../../content/animations/graph/node_library/skeleton/joint_twist_limit.md) node in the animation graph, which is the recommended way to set it up visually. This class is the programmatic equivalent for driving the solver from code.


## JointLimitInfoTwist Class

### Properties

## vec3 ForwardAxis

The bone direction in the bind-local frame of the joint. The twist is measured around this axis. The default value is (0, 1, 0).
## float MinAngle

The lower bound of the twist around the forward axis, in degrees. The default value is -180, which imposes no effective limit.
## float MaxAngle

The upper bound of the twist around the forward axis, in degrees. The default value is 180, which imposes no effective limit.
### Members

---

## JointLimitInfoTwist ( )

Constructor. Creates a new set of joint twist limit parameters with default values.
