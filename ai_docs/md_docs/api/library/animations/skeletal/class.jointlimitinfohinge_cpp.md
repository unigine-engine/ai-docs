# Unigine::JointLimitInfoHinge Class (CPP)

**Header:** #include <UnigineSkeletonControlRig.h>

**Inherits from:** JointLimitInfo


This class stores the parameters of a hinge joint limit: a single degree of freedom, a rotation around one axis. Any deflection off that axis is discarded. Use it for a knee, an elbow, or a finger.


A limit is applied either directly, by passing it to the matching **solveLayer*** method of the [NodeSkeletonPose](../../../../api/library/nodes/class.nodeskeletonpose_cpp.md) class, or as a constraint for a chain solver - add it to a [JointLimitSetInfo](../../../../api/library/animations/skeletal/class.jointlimitsetinfo_cpp.md) and assign the set to an [IKInfoChain](../../../../api/library/animations/skeletal/class.ikinfochain_cpp.md) or a [LookAtChainInfo](../../../../api/library/animations/skeletal/class.lookatchaininfo_cpp.md).


An instance of this class is passed to the *[solveLayerJointHingeLimit()](../../../../api/library/nodes/class.nodeskeletonpose_cpp.md#solveLayerJointHingeLimit_int_JointLimitInfoHinge_void)* method of the [NodeSkeletonPose](../../../../api/library/nodes/class.nodeskeletonpose_cpp.md) class. All axes are set in the bind-local frame of the joint.


The same solver is available as the [Joint Hinge Limit](../../../../content/animations/graph/node_library/skeleton/joint_hinge_limit.md) node in the animation graph, which is the recommended way to set it up visually. This class is the programmatic equivalent for driving the solver from code.


## JointLimitInfoHinge Class

### Members

## void setHingeAxis ( const Math:: vec3 & axis )

Sets a new axis the rotation of the joint is allowed around, in the bind-local frame of the joint. The default value is (0, 1, 0).
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md)&* **axis** - The axis the rotation of the joint is allowed around

## Math:: vec3 getHingeAxis () const

Returns the current axis the rotation of the joint is allowed around, in the bind-local frame of the joint. The default value is (0, 1, 0).
### Return value

Current axis the rotation of the joint is allowed around
## void setMinAngle ( float angle )

Sets a new lower bound of the rotation around the hinge axis, in degrees. The default value is -180, which imposes no effective limit.
### Arguments

- *float* **angle** - The lower bound of the rotation around the hinge axis, in degrees

## float getMinAngle () const

Returns the current lower bound of the rotation around the hinge axis, in degrees. The default value is -180, which imposes no effective limit.
### Return value

Current lower bound of the rotation around the hinge axis, in degrees
## void setMaxAngle ( float angle )

Sets a new upper bound of the rotation around the hinge axis, in degrees. The default value is 180, which imposes no effective limit.
### Arguments

- *float* **angle** - The upper bound of the rotation around the hinge axis, in degrees

## float getMaxAngle () const

Returns the current upper bound of the rotation around the hinge axis, in degrees. The default value is 180, which imposes no effective limit.
### Return value

Current upper bound of the rotation around the hinge axis, in degrees
---

## static JointLimitInfoHingePtr create ( )

Constructor. Creates a new set of joint hinge limit parameters with default values.
