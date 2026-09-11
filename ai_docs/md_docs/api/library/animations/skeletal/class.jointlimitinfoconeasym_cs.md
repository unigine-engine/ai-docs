# Unigine::JointLimitInfoConeAsym Class (CS)

**Inherits from:** JointLimitInfo


This class stores the parameters of an asymmetric cone joint limit. The swing of the bone is kept inside an elliptical cone whose four half-angles may differ, so the joint can be allowed to travel further one way than the other. Use it for a shoulder or a hip, where the forward swing exceeds the backward one.


A limit is applied either directly, by passing it to the matching **solveLayer*** method of the [NodeSkeletonPose](../../../../api/library/nodes/class.nodeskeletonpose_cs.md) class, or as a constraint for a chain solver - add it to a [JointLimitSetInfo](../../../../api/library/animations/skeletal/class.jointlimitsetinfo_cs.md) and assign the set to an [IKInfoChain](../../../../api/library/animations/skeletal/class.ikinfochain_cs.md) or a [LookAtChainInfo](../../../../api/library/animations/skeletal/class.lookatchaininfo_cs.md).


An instance of this class is passed to the *[SolveLayerJointConeAsymLimit()](../../../../api/library/nodes/class.nodeskeletonpose_cs.md#solveLayerJointConeAsymLimit_int_JointLimitInfoConeAsym_void)* method of the [NodeSkeletonPose](../../../../api/library/nodes/class.nodeskeletonpose_cs.md) class. All axes are set in the bind-local frame of the joint.


The same solver is available as the [Joint Cone Asym Limit](../../../../content/animations/graph/node_library/skeleton/joint_cone_asym_limit.md) node in the animation graph, which is the recommended way to set it up visually. This class is the programmatic equivalent for driving the solver from code.


## JointLimitInfoConeAsym Class

### Properties

## vec3 ForwardAxis

The bone direction in the bind-local frame of the joint. The clamp keeps this direction inside the asymmetric cone. The default value is (0, 1, 0).
## vec3 UpAxis

The up reference axis in the bind-local frame of the joint. It fixes which way is up for the asymmetric cone, so that the up and down swing angles are told apart from the left and right ones. The default value is (0, 0, 1).
## vec3 ConeAxis

The center direction of the cone in the bind-local frame of the joint, around which the swing of the bone is limited. It may differ from the forward axis to pre-tilt the cone. The default value is (0, 1, 0).
## float SwingLeftAngle

The half-angle of the asymmetric cone to the left of the cone axis, in degrees. The four swing angles are the semi-axes of an elliptical cone, not a min/max pair: each one caps the deviation in its own direction. The default value is 180, which imposes no effective limit.
## float SwingRightAngle

The half-angle of the asymmetric cone to the right of the cone axis, in degrees. The four swing angles are the semi-axes of an elliptical cone, not a min/max pair: each one caps the deviation in its own direction. The default value is 180, which imposes no effective limit.
## float SwingUpAngle

The half-angle of the asymmetric cone upwards of the cone axis, in degrees. The four swing angles are the semi-axes of an elliptical cone, not a min/max pair: each one caps the deviation in its own direction. The default value is 180, which imposes no effective limit.
## float SwingDownAngle

The half-angle of the asymmetric cone downwards of the cone axis, in degrees. The four swing angles are the semi-axes of an elliptical cone, not a min/max pair: each one caps the deviation in its own direction. The default value is 180, which imposes no effective limit.
### Members

---

## JointLimitInfoConeAsym ( )

Constructor. Creates a new set of joint cone asym limit parameters with default values.
