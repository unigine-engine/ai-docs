# Unigine::JointLimitInfoHinge Class (CS)

**Inherits from:** JointLimitInfo


This class stores the parameters of a hinge joint limit: a single degree of freedom, a rotation around one axis. Any deflection off that axis is discarded. Use it for a knee, an elbow, or a finger.


A limit is applied either directly, by passing it to the matching **solveLayer*** method of the [NodeSkeletonPose](../../../../api/library/nodes/class.nodeskeletonpose_cs.md) class, or as a constraint for a chain solver - add it to a [JointLimitSetInfo](../../../../api/library/animations/skeletal/class.jointlimitsetinfo_cs.md) and assign the set to an [IKInfoChain](../../../../api/library/animations/skeletal/class.ikinfochain_cs.md) or a [LookAtChainInfo](../../../../api/library/animations/skeletal/class.lookatchaininfo_cs.md).


An instance of this class is passed to the *[SolveLayerJointHingeLimit()](../../../../api/library/nodes/class.nodeskeletonpose_cs.md#solveLayerJointHingeLimit_int_JointLimitInfoHinge_void)* method of the [NodeSkeletonPose](../../../../api/library/nodes/class.nodeskeletonpose_cs.md) class. All axes are set in the bind-local frame of the joint.


The same solver is available as the [Joint Hinge Limit](../../../../content/animations/graph/node_library/skeleton/joint_hinge_limit.md) node in the animation graph, which is the recommended way to set it up visually. This class is the programmatic equivalent for driving the solver from code.


## JointLimitInfoHinge Class

### Properties

## vec3 HingeAxis

The axis the rotation of the joint is allowed around, in the bind-local frame of the joint. The default value is (0, 1, 0).
## float MinAngle

The lower bound of the rotation around the hinge axis, in degrees. The default value is -180, which imposes no effective limit.
## float MaxAngle

The upper bound of the rotation around the hinge axis, in degrees. The default value is 180, which imposes no effective limit.
### Members

---

## JointLimitInfoHinge ( )

Constructor. Creates a new set of joint hinge limit parameters with default values.
