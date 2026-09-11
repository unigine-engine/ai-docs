# Unigine::JointLimitInfoCone Class (CPP)

**Header:** #include <UnigineSkeletonControlRig.h>

**Inherits from:** JointLimitInfo


This class stores the parameters of a symmetric cone joint limit. The bone direction, given by the forward axis, is kept within the cone half-angle of the cone axis; the twist around the forward axis is preserved. The shape is a spherical cap, which stays gimbal-stable across the full sphere. Use it for a joint that tilts by the same amount in every direction, and combine it with a [JointLimitInfoTwist](../../../../api/library/animations/skeletal/class.jointlimitinfotwist_cpp.md) on the same joint to clamp the twist as well.


A limit is applied either directly, by passing it to the matching **solveLayer*** method of the [NodeSkeletonPose](../../../../api/library/nodes/class.nodeskeletonpose_cpp.md) class, or as a constraint for a chain solver - add it to a [JointLimitSetInfo](../../../../api/library/animations/skeletal/class.jointlimitsetinfo_cpp.md) and assign the set to an [IKInfoChain](../../../../api/library/animations/skeletal/class.ikinfochain_cpp.md) or a [LookAtChainInfo](../../../../api/library/animations/skeletal/class.lookatchaininfo_cpp.md).


An instance of this class is passed to the *[solveLayerJointConeLimit()](../../../../api/library/nodes/class.nodeskeletonpose_cpp.md#solveLayerJointConeLimit_int_JointLimitInfoCone_void)* method of the [NodeSkeletonPose](../../../../api/library/nodes/class.nodeskeletonpose_cpp.md) class. All axes are set in the bind-local frame of the joint.


The same solver is available as the [Joint Cone Limit](../../../../content/animations/graph/node_library/skeleton/joint_cone_limit.md) node in the animation graph, which is the recommended way to set it up visually. This class is the programmatic equivalent for driving the solver from code.


## JointLimitInfoCone Class

### Members

## void setForwardAxis ( const Math:: vec3 & axis )

Sets a new bone direction in the bind-local frame of the joint. The clamp keeps this direction within the cone half-angle of the cone axis. The default value is (0, 1, 0).
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md)&* **axis** - The bone direction in the bind-local frame of the joint

## Math:: vec3 getForwardAxis () const

Returns the current bone direction in the bind-local frame of the joint. The clamp keeps this direction within the cone half-angle of the cone axis. The default value is (0, 1, 0).
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
---

## static JointLimitInfoConePtr create ( )

Constructor. Creates a new set of joint cone limit parameters with default values.
