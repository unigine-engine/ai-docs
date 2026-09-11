# Unigine::LookAtChainInfo Class (CPP)

**Header:** #include <UnigineSkeletonControlRig.h>


This class stores the parameters of the multi-joint Look At solver. The tip joint of the chain aims its local forward axis at the target, and the other joints take a share of the rotation set by their per-joint weights. Unlike [IKInfoChain](../../../../api/library/animations/skeletal/class.ikinfochain_cpp.md), this solver aims in a **direction** instead of reaching a **position**, and the tip joint rotates as well.


The joints are listed from the root to the tip. Each of them has its own weight, forward axis and up axis, set through the per-joint methods below.


An instance of this class is passed to the *[solveLayerLookAtChain()](../../../../api/library/nodes/class.nodeskeletonpose_cpp.md#solveLayerLookAtChain_int_LookAtChainInfo_void)* method of the [NodeSkeletonPose](../../../../api/library/nodes/class.nodeskeletonpose_cpp.md) class.


The same solver is available as the [Look At Chain](../../../../content/animations/graph/node_library/skeleton/look_at_chain.md) node in the animation graph, which is the recommended way to set it up visually. This class is the programmatic equivalent for driving the solver from code.


## LookAtChainInfo Class

### Members

## void setNumJoints ( int joints )

Sets a new number of joints in the chain, listed from the root to the tip. Changing the value resizes the per-joint lists.
### Arguments

- *int* **joints** - The number of joints in the chain

## int getNumJoints () const

Returns the current number of joints in the chain, listed from the root to the tip. Changing the value resizes the per-joint lists.
### Return value

Current number of joints in the chain
## void setTarget ( const Math:: vec3 & target )

Sets a new position the forward axis of the tip joint is aimed at, in the object space of the skeleton. The default value is (0, 0, 0).
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md)&* **target** - The position the forward axis of the tip joint is aimed at

## Math:: vec3 getTarget () const

Returns the current position the forward axis of the tip joint is aimed at, in the object space of the skeleton. The default value is (0, 0, 0).
### Return value

Current position the forward axis of the tip joint is aimed at
## void setPole ( const Math:: vec3 & pole )

Sets a new position used as the up reference for the per-bone twist correction. It is used only when *[setUsePole()](../../../...md#isUsePole_int)* is enabled. The default value is (0, 0, 0).
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md)&* **pole** - The position used as the up reference for the twist correction

## Math:: vec3 getPole () const

Returns the current position used as the up reference for the per-bone twist correction. It is used only when *[setUsePole()](../../../...md#isUsePole_int)* is enabled. The default value is (0, 0, 0).
### Return value

Current position used as the up reference for the twist correction
## void setUsePole ( bool pole )

Sets a new value indicating if each bone receives a twist around its aim direction so that its up axis projects toward the pole. It keeps the chain from rolling around the aim line as the target moves. The default value is false.
### Arguments

- *bool* **pole** - Set **true** to enable the pole is used as the up reference for the twist correction; **false** - to disable it.

## bool isUsePole () const

Returns the current value indicating if each bone receives a twist around its aim direction so that its up axis projects toward the pole. It keeps the chain from rolling around the aim line as the target moves. The default value is false.
### Return value

**true** if the pole is used as the up reference for the twist correction; otherwise **false**.
## void setNumIterations ( int iterations )

Sets a new maximum number of root-to-tip passes per solve. It matters only when a limit set is assigned: without limits the solver always runs a single pass. The default value is 4.
### Arguments

- *int* **iterations** - The maximum number of root-to-tip passes per solve

## int getNumIterations () const

Returns the current maximum number of root-to-tip passes per solve. It matters only when a limit set is assigned: without limits the solver always runs a single pass. The default value is 4.
### Return value

Current maximum number of root-to-tip passes per solve
## void setAngleTolerance ( float tolerance )

Sets a new angle between the aim direction of the tip and the direction to the target, in degrees, below which the chain is considered converged and the solver stops iterating. The default value is 0.5. Set it to 0 to always run all the iterations.
### Arguments

- *float* **tolerance** - The angle below which the chain is considered converged, in degrees

## float getAngleTolerance () const

Returns the current angle between the aim direction of the tip and the direction to the target, in degrees, below which the chain is considered converged and the solver stops iterating. The default value is 0.5. Set it to 0 to always run all the iterations.
### Return value

Current angle below which the chain is considered converged, in degrees
## void setMaxAngle ( float angle )

Sets a new per-solve cap, in degrees in the [0, 180] range, on how far each joint of the chain may deviate from the input pose. The default value is 180, which imposes no effective limit.
### Arguments

- *float* **angle** - The cap on the deviation of each joint from the input pose, in degrees

## float getMaxAngle () const

Returns the current per-solve cap, in degrees in the [0, 180] range, on how far each joint of the chain may deviate from the input pose. The default value is 180, which imposes no effective limit.
### Return value

Current cap on the deviation of each joint from the input pose, in degrees
## void setWeight ( float weight )

Sets a new blend weight of the Look At result over the input pose, in the [0, 1] range. The default value is 1.0.
### Arguments

- *float* **weight** - The blend weight of the Look At result over the input pose

## float getWeight () const

Returns the current blend weight of the Look At result over the input pose, in the [0, 1] range. The default value is 1.0.
### Return value

Current blend weight of the Look At result over the input pose
## Ptr<JointLimitSetInfo> void setLimitSet ( const Ptr < JointLimitSetInfo >& set )

Sets a new set of per-joint limits applied while solving. The set is owned by the caller and must outlive the solve.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[JointLimitSetInfo](../../../../api/library/animations/skeletal/class.jointlimitsetinfo_cpp.md)>&* **set** - The set of per-joint limits applied while solving

## Ptr<JointLimitSetInfo> Ptr < JointLimitSetInfo > getLimitSet () const

Returns the current set of per-joint limits applied while solving. The set is owned by the caller and must outlive the solve.
### Return value

Current set of per-joint limits applied while solving
---

## static LookAtChainInfoPtr create ( )

Constructor. Creates a new set of Look At chain parameters with default values.
## void setJoint ( int num , int joint )

Sets the skeleton joint at the given position in the chain.
### Arguments

- *int* **num** - Position in the chain, from the root to the tip.
- *int* **joint** - Index of the skeleton joint to put at this position.

## int getJoint ( int num ) const

Returns the skeleton joint at the given position in the chain.
### Arguments

- *int* **num** - Position in the chain, from the root to the tip.

### Return value

Index of the skeleton joint, or -1 if the position is out of range or the joint is not set.
## void setJointForwardAxis ( int num , const Math:: vec3 & forward_axis )

Sets the local axis of the joint at the given position that is aimed at the target. The default value is (0, 1, 0).
### Arguments

- *int* **num** - Position in the chain, from the root to the tip.
- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **forward_axis** - Local axis of the joint that is aimed at the target.

## Math:: vec3 getJointForwardAxis ( int num ) const

Returns the local axis of the joint at the given position that is aimed at the target.
### Arguments

- *int* **num** - Position in the chain, from the root to the tip.

### Return value

Local axis of the joint that is aimed at the target.
## void setJointUpAxis ( int num , const Math:: vec3 & up_axis )

Sets the local up axis of the joint at the given position, used as the twist reference when the pole is applied. The default value is (0, 0, 1).
### Arguments

- *int* **num** - Position in the chain, from the root to the tip.
- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **up_axis** - Local up axis of the joint used as the twist reference.

## Math:: vec3 getJointUpAxis ( int num ) const

Returns the local up axis of the joint at the given position.
### Arguments

- *int* **num** - Position in the chain, from the root to the tip.

### Return value

Local up axis of the joint.
## void setJointWeight ( int num , float weight )

Sets the share of the aiming rotation applied to the joint at the given position. The default value is 1.0.
### Arguments

- *int* **num** - Position in the chain, from the root to the tip.
- *float* **weight** - Share of the aiming rotation applied to this joint, in the [0, 1] range.

## float getJointWeight ( int num ) const

Returns the share of the aiming rotation applied to the joint at the given position.
### Arguments

- *int* **num** - Position in the chain, from the root to the tip.

### Return value

Share of the aiming rotation applied to this joint.
