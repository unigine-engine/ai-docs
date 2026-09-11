# Unigine::JointLimitInfoConeAsym Class (CPP)

**Header:** #include <UnigineSkeletonControlRig.h>

**Inherits from:** JointLimitInfo


This class stores the parameters of an asymmetric cone joint limit. The swing of the bone is kept inside an elliptical cone whose four half-angles may differ, so the joint can be allowed to travel further one way than the other. Use it for a shoulder or a hip, where the forward swing exceeds the backward one.


A limit is applied either directly, by passing it to the matching **solveLayer*** method of the [NodeSkeletonPose](../../../../api/library/nodes/class.nodeskeletonpose_cpp.md) class, or as a constraint for a chain solver - add it to a [JointLimitSetInfo](../../../../api/library/animations/skeletal/class.jointlimitsetinfo_cpp.md) and assign the set to an [IKInfoChain](../../../../api/library/animations/skeletal/class.ikinfochain_cpp.md) or a [LookAtChainInfo](../../../../api/library/animations/skeletal/class.lookatchaininfo_cpp.md).


An instance of this class is passed to the *[solveLayerJointConeAsymLimit()](../../../../api/library/nodes/class.nodeskeletonpose_cpp.md#solveLayerJointConeAsymLimit_int_JointLimitInfoConeAsym_void)* method of the [NodeSkeletonPose](../../../../api/library/nodes/class.nodeskeletonpose_cpp.md) class. All axes are set in the bind-local frame of the joint.


The same solver is available as the [Joint Cone Asym Limit](../../../../content/animations/graph/node_library/skeleton/joint_cone_asym_limit.md) node in the animation graph, which is the recommended way to set it up visually. This class is the programmatic equivalent for driving the solver from code.


## JointLimitInfoConeAsym Class

### Members

## void setForwardAxis ( const Math:: vec3 & axis )

Sets a new bone direction in the bind-local frame of the joint. The clamp keeps this direction inside the asymmetric cone. The default value is (0, 1, 0).
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md)&* **axis** - The bone direction in the bind-local frame of the joint

## Math:: vec3 getForwardAxis () const

Returns the current bone direction in the bind-local frame of the joint. The clamp keeps this direction inside the asymmetric cone. The default value is (0, 1, 0).
### Return value

Current bone direction in the bind-local frame of the joint
## void setUpAxis ( const Math:: vec3 & axis )

Sets a new up reference axis in the bind-local frame of the joint. It fixes which way is up for the asymmetric cone, so that the up and down swing angles are told apart from the left and right ones. The default value is (0, 0, 1).
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md)&* **axis** - The up reference axis of the asymmetric cone

## Math:: vec3 getUpAxis () const

Returns the current up reference axis in the bind-local frame of the joint. It fixes which way is up for the asymmetric cone, so that the up and down swing angles are told apart from the left and right ones. The default value is (0, 0, 1).
### Return value

Current up reference axis of the asymmetric cone
## void setConeAxis ( const Math:: vec3 & axis )

Sets a new center direction of the cone in the bind-local frame of the joint, around which the swing of the bone is limited. It may differ from the forward axis to pre-tilt the cone. The default value is (0, 1, 0).
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md)&* **axis** - The center direction of the cone

## Math:: vec3 getConeAxis () const

Returns the current center direction of the cone in the bind-local frame of the joint, around which the swing of the bone is limited. It may differ from the forward axis to pre-tilt the cone. The default value is (0, 1, 0).
### Return value

Current center direction of the cone
## void setSwingLeftAngle ( float angle )

Sets a new half-angle of the asymmetric cone to the left of the cone axis, in degrees. The four swing angles are the semi-axes of an elliptical cone, not a min/max pair: each one caps the deviation in its own direction. The default value is 180, which imposes no effective limit.
### Arguments

- *float* **angle** - The half-angle of the cone to the left, in degrees

## float getSwingLeftAngle () const

Returns the current half-angle of the asymmetric cone to the left of the cone axis, in degrees. The four swing angles are the semi-axes of an elliptical cone, not a min/max pair: each one caps the deviation in its own direction. The default value is 180, which imposes no effective limit.
### Return value

Current half-angle of the cone to the left, in degrees
## void setSwingRightAngle ( float angle )

Sets a new half-angle of the asymmetric cone to the right of the cone axis, in degrees. The four swing angles are the semi-axes of an elliptical cone, not a min/max pair: each one caps the deviation in its own direction. The default value is 180, which imposes no effective limit.
### Arguments

- *float* **angle** - The half-angle of the cone to the right, in degrees

## float getSwingRightAngle () const

Returns the current half-angle of the asymmetric cone to the right of the cone axis, in degrees. The four swing angles are the semi-axes of an elliptical cone, not a min/max pair: each one caps the deviation in its own direction. The default value is 180, which imposes no effective limit.
### Return value

Current half-angle of the cone to the right, in degrees
## void setSwingUpAngle ( float angle )

Sets a new half-angle of the asymmetric cone upwards of the cone axis, in degrees. The four swing angles are the semi-axes of an elliptical cone, not a min/max pair: each one caps the deviation in its own direction. The default value is 180, which imposes no effective limit.
### Arguments

- *float* **angle** - The half-angle of the cone upwards, in degrees

## float getSwingUpAngle () const

Returns the current half-angle of the asymmetric cone upwards of the cone axis, in degrees. The four swing angles are the semi-axes of an elliptical cone, not a min/max pair: each one caps the deviation in its own direction. The default value is 180, which imposes no effective limit.
### Return value

Current half-angle of the cone upwards, in degrees
## void setSwingDownAngle ( float angle )

Sets a new half-angle of the asymmetric cone downwards of the cone axis, in degrees. The four swing angles are the semi-axes of an elliptical cone, not a min/max pair: each one caps the deviation in its own direction. The default value is 180, which imposes no effective limit.
### Arguments

- *float* **angle** - The half-angle of the cone downwards, in degrees

## float getSwingDownAngle () const

Returns the current half-angle of the asymmetric cone downwards of the cone axis, in degrees. The four swing angles are the semi-axes of an elliptical cone, not a min/max pair: each one caps the deviation in its own direction. The default value is 180, which imposes no effective limit.
### Return value

Current half-angle of the cone downwards, in degrees
---

## static JointLimitInfoConeAsymPtr create ( )

Constructor. Creates a new set of joint cone asym limit parameters with default values.
