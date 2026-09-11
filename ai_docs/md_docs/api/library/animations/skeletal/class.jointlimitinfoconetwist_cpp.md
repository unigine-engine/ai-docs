# Unigine::JointLimitInfoConeTwist Class (CPP)

**Header:** #include <UnigineSkeletonControlRig.h>

**Inherits from:** JointLimitInfo


This class stores the parameters of a combined symmetric cone and twist joint limit: the swing of the bone is kept inside a cone and the twist around the forward axis is clamped to its own range.


A limit is applied either directly, by passing it to the matching **solveLayer*** method of the [NodeSkeletonPose](../../../../api/library/nodes/class.nodeskeletonpose_cpp.md) class, or as a constraint for a chain solver - add it to a [JointLimitSetInfo](../../../../api/library/animations/skeletal/class.jointlimitsetinfo_cpp.md) and assign the set to an [IKInfoChain](../../../../api/library/animations/skeletal/class.ikinfochain_cpp.md) or a [LookAtChainInfo](../../../../api/library/animations/skeletal/class.lookatchaininfo_cpp.md).


An instance of this class is passed to the *[solveLayerJointConeTwistLimit()](../../../../api/library/nodes/class.nodeskeletonpose_cpp.md#solveLayerJointConeTwistLimit_int_JointLimitInfoConeTwist_void)* method of the [NodeSkeletonPose](../../../../api/library/nodes/class.nodeskeletonpose_cpp.md) class. All axes are set in the bind-local frame of the joint.


The same solver is available as the [Joint Cone Twist Limit](../../../../content/animations/graph/node_library/skeleton/joint_cone_twist_limit.md) node in the animation graph, which is the recommended way to set it up visually. This class is the programmatic equivalent for driving the solver from code.


## JointLimitInfoConeTwist Class

### Members

## void setForwardAxis ( const Math:: vec3 & axis )

Sets a new bone direction in the bind-local frame of the joint. The clamp keeps this direction within the cone half-angle of the cone axis, and the twist is measured around it. The default value is (0, 1, 0).
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md)&* **axis** - The bone direction in the bind-local frame of the joint

## Math:: vec3 getForwardAxis () const

Returns the current bone direction in the bind-local frame of the joint. The clamp keeps this direction within the cone half-angle of the cone axis, and the twist is measured around it. The default value is (0, 1, 0).
### Return value

Current bone direction in the bind-local frame of the joint
## void setConeAxis ( const Math:: vec3 & axis )

Sets a new center direction of the cone in the bind-local frame of the joint, around which the swing of the bone is limited. It may differ from the forward axis to pre-tilt the cone. The default value is (0, 1, 0).
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md)&* **axis** - The center direction of the cone

## Math:: vec3 getConeAxis () const

Returns the current center direction of the cone in the bind-local frame of the joint, around which the swing of the bone is limited. It may differ from the forward axis to pre-tilt the cone. The default value is (0, 1, 0).
### Return value

Current center direction of the cone
## void setConeAngle ( float angle )

Sets a new maximum swing of the bone away from the cone axis, in degrees, in the [0, 180] range. The default value is 180, which imposes no effective limit.
### Arguments

- *float* **angle** - The maximum swing of the bone away from the cone axis, in degrees

## float getConeAngle () const

Returns the current maximum swing of the bone away from the cone axis, in degrees, in the [0, 180] range. The default value is 180, which imposes no effective limit.
### Return value

Current maximum swing of the bone away from the cone axis, in degrees
## void setTwistMinAngle ( float angle )

Sets a new lower bound of the twist around the forward axis, in degrees. The default value is -180, which imposes no effective limit.
### Arguments

- *float* **angle** - The lower bound of the twist, in degrees

## float getTwistMinAngle () const

Returns the current lower bound of the twist around the forward axis, in degrees. The default value is -180, which imposes no effective limit.
### Return value

Current lower bound of the twist, in degrees
## void setTwistMaxAngle ( float angle )

Sets a new upper bound of the twist around the forward axis, in degrees. The default value is 180, which imposes no effective limit.
### Arguments

- *float* **angle** - The upper bound of the twist, in degrees

## float getTwistMaxAngle () const

Returns the current upper bound of the twist around the forward axis, in degrees. The default value is 180, which imposes no effective limit.
### Return value

Current upper bound of the twist, in degrees
---

## static JointLimitInfoConeTwistPtr create ( )

Constructor. Creates a new set of joint cone twist limit parameters with default values.
