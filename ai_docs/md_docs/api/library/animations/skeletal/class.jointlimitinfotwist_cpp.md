# Unigine::JointLimitInfoTwist Class (CPP)

**Header:** #include <UnigineSkeletonControlRig.h>

**Inherits from:** JointLimitInfo


This class stores the parameters of a twist joint limit. The rotation around the bone is kept within a range while the swing is left free. Use it for a forearm, or pair it with a swing limit on the same joint.


A limit is applied either directly, by passing it to the matching **solveLayer*** method of the [NodeSkeletonPose](../../../../api/library/nodes/class.nodeskeletonpose_cpp.md) class, or as a constraint for a chain solver - add it to a [JointLimitSetInfo](../../../../api/library/animations/skeletal/class.jointlimitsetinfo_cpp.md) and assign the set to an [IKInfoChain](../../../../api/library/animations/skeletal/class.ikinfochain_cpp.md) or a [LookAtChainInfo](../../../../api/library/animations/skeletal/class.lookatchaininfo_cpp.md).


An instance of this class is passed to the *[solveLayerJointTwistLimit()](../../../../api/library/nodes/class.nodeskeletonpose_cpp.md#solveLayerJointTwistLimit_int_JointLimitInfoTwist_void)* method of the [NodeSkeletonPose](../../../../api/library/nodes/class.nodeskeletonpose_cpp.md) class. All axes are set in the bind-local frame of the joint.


The same solver is available as the [Joint Twist Limit](../../../../content/animations/graph/node_library/skeleton/joint_twist_limit.md) node in the animation graph, which is the recommended way to set it up visually. This class is the programmatic equivalent for driving the solver from code.


## JointLimitInfoTwist Class

### Members

## void setForwardAxis ( const Math:: vec3 & axis )

Sets a new bone direction in the bind-local frame of the joint. The twist is measured around this axis. The default value is (0, 1, 0).
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md)&* **axis** - The bone direction in the bind-local frame of the joint

## Math:: vec3 getForwardAxis () const

Returns the current bone direction in the bind-local frame of the joint. The twist is measured around this axis. The default value is (0, 1, 0).
### Return value

Current bone direction in the bind-local frame of the joint
## void setMinAngle ( float angle )

Sets a new lower bound of the twist around the forward axis, in degrees. The default value is -180, which imposes no effective limit.
### Arguments

- *float* **angle** - The lower bound of the twist, in degrees

## float getMinAngle () const

Returns the current lower bound of the twist around the forward axis, in degrees. The default value is -180, which imposes no effective limit.
### Return value

Current lower bound of the twist, in degrees
## void setMaxAngle ( float angle )

Sets a new upper bound of the twist around the forward axis, in degrees. The default value is 180, which imposes no effective limit.
### Arguments

- *float* **angle** - The upper bound of the twist, in degrees

## float getMaxAngle () const

Returns the current upper bound of the twist around the forward axis, in degrees. The default value is 180, which imposes no effective limit.
### Return value

Current upper bound of the twist, in degrees
---

## static JointLimitInfoTwistPtr create ( )

Constructor. Creates a new set of joint twist limit parameters with default values.
