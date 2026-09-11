# Unigine::LookAtInfo Class (CPP)

**Header:** #include <UnigineSkeletonControlRig.h>


This class stores the parameters of the single-joint Look At solver. The solver rotates one joint so that its local forward axis points at the target. Unlike inverse kinematics, which reaches a target **position**, it aims in a target **direction** and affects rotation only.


An instance of this class is passed to the *[solveLayerLookAt()](../../../../api/library/nodes/class.nodeskeletonpose_cpp.md#solveLayerLookAt_int_LookAtInfo_void)* method of the [NodeSkeletonPose](../../../../api/library/nodes/class.nodeskeletonpose_cpp.md) class.


The same solver is available as the [Joint Look At](../../../../content/animations/graph/node_library/skeleton/joint_look_at.md) node in the animation graph, which is the recommended way to set it up visually. This class is the programmatic equivalent for driving the solver from code.


## LookAtInfo Class

### Members

## void setJoint ( int joint )

Sets a new index of the joint that is rotated toward the target. The default value is -1.
### Arguments

- *int* **joint** - The index of the joint that is rotated toward the target

## int getJoint () const

Returns the current index of the joint that is rotated toward the target. The default value is -1.
### Return value

Current index of the joint that is rotated toward the target
## void setForwardAxis ( const Math:: vec3 & axis )

Sets a new local axis of the joint that is aimed at the target. The default value is (0, 1, 0).
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md)&* **axis** - The local axis of the joint that is aimed at the target

## Math:: vec3 getForwardAxis () const

Returns the current local axis of the joint that is aimed at the target. The default value is (0, 1, 0).
### Return value

Current local axis of the joint that is aimed at the target
## void setUpAxis ( const Math:: vec3 & axis )

Sets a new local up axis of the joint used as the twist reference when the pole is applied. The default value is (0, 0, 1).
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md)&* **axis** - The local up axis used as the twist reference

## Math:: vec3 getUpAxis () const

Returns the current local up axis of the joint used as the twist reference when the pole is applied. The default value is (0, 0, 1).
### Return value

Current local up axis used as the twist reference
## void setTarget ( const Math:: vec3 & target )

Sets a new position the forward axis of the joint is aimed at, in the object space of the skeleton. The default value is (0, 0, 0).
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md)&* **target** - The position the forward axis of the joint is aimed at

## Math:: vec3 getTarget () const

Returns the current position the forward axis of the joint is aimed at, in the object space of the skeleton. The default value is (0, 0, 0).
### Return value

Current position the forward axis of the joint is aimed at
## void setPole ( const Math:: vec3 & pole )

Sets a new position used as the up reference for the twist correction of the joint. It is used only when *[setUsePole()](../../../...md#isUsePole_int)* is enabled and a valid up axis is set. The default value is (0, 0, 0).
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md)&* **pole** - The position used as the up reference for the twist correction

## Math:: vec3 getPole () const

Returns the current position used as the up reference for the twist correction of the joint. It is used only when *[setUsePole()](../../../...md#isUsePole_int)* is enabled and a valid up axis is set. The default value is (0, 0, 0).
### Return value

Current position used as the up reference for the twist correction
## void setWeight ( float weight )

Sets a new blend weight of the Look At result over the input pose, in the [0, 1] range. The default value is 1.0.
### Arguments

- *float* **weight** - The blend weight of the Look At result over the input pose

## float getWeight () const

Returns the current blend weight of the Look At result over the input pose, in the [0, 1] range. The default value is 1.0.
### Return value

Current blend weight of the Look At result over the input pose
## void setUsePole ( bool pole )

Sets a new value indicating if the pole is used to control the twist of the joint around its aim direction. The default value is false.
### Arguments

- *bool* **pole** - Set **true** to enable the pole is used to control the twist of the joint; **false** - to disable it.

## bool isUsePole () const

Returns the current value indicating if the pole is used to control the twist of the joint around its aim direction. The default value is false.
### Return value

**true** if the pole is used to control the twist of the joint; otherwise **false**.
## void setMaxAngle ( float angle )

Sets a new maximum rotation deviation from the animation pose, in degrees, in the [0, 180] range. The clamp is applied relative to the animation pose, not frame to frame, so the joint does not chase a target that jumps beyond this angle. The default value is 180, which imposes no effective limit.
### Arguments

- *float* **angle** - The maximum rotation deviation from the animation pose, in degrees

## float getMaxAngle () const

Returns the current maximum rotation deviation from the animation pose, in degrees, in the [0, 180] range. The clamp is applied relative to the animation pose, not frame to frame, so the joint does not chase a target that jumps beyond this angle. The default value is 180, which imposes no effective limit.
### Return value

Current maximum rotation deviation from the animation pose, in degrees
---

## static LookAtInfoPtr create ( )

Constructor. Creates a new set of Look At parameters with default values.
