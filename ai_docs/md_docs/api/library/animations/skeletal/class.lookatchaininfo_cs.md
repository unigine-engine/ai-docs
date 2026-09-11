# Unigine::LookAtChainInfo Class (CS)


This class stores the parameters of the multi-joint Look At solver. The tip joint of the chain aims its local forward axis at the target, and the other joints take a share of the rotation set by their per-joint weights. Unlike [IKInfoChain](../../../../api/library/animations/skeletal/class.ikinfochain_cs.md), this solver aims in a **direction** instead of reaching a **position**, and the tip joint rotates as well.


The joints are listed from the root to the tip. Each of them has its own weight, forward axis and up axis, set through the per-joint methods below.


An instance of this class is passed to the *[SolveLayerLookAtChain()](../../../../api/library/nodes/class.nodeskeletonpose_cs.md#solveLayerLookAtChain_int_LookAtChainInfo_void)* method of the [NodeSkeletonPose](../../../../api/library/nodes/class.nodeskeletonpose_cs.md) class.


The same solver is available as the [Look At Chain](../../../../content/animations/graph/node_library/skeleton/look_at_chain.md) node in the animation graph, which is the recommended way to set it up visually. This class is the programmatic equivalent for driving the solver from code.


## LookAtChainInfo Class

### Properties

## int NumJoints

The number of joints in the chain, listed from the root to the tip. Changing the value resizes the per-joint lists.
## vec3 Target

The position the forward axis of the tip joint is aimed at, in the object space of the skeleton. The default value is (0, 0, 0).
## vec3 Pole

The position used as the up reference for the per-bone twist correction. It is used only when *[UsePole](../../../...md#isUsePole_int)* is enabled. The default value is (0, 0, 0).
## bool UsePole

The value indicating if each bone receives a twist around its aim direction so that its up axis projects toward the pole. It keeps the chain from rolling around the aim line as the target moves. The default value is false.
## int NumIterations

The maximum number of root-to-tip passes per solve. It matters only when a limit set is assigned: without limits the solver always runs a single pass. The default value is 4.
## float AngleTolerance

The angle between the aim direction of the tip and the direction to the target, in degrees, below which the chain is considered converged and the solver stops iterating. The default value is 0.5. Set it to 0 to always run all the iterations.
## float MaxAngle

The per-solve cap, in degrees in the [0, 180] range, on how far each joint of the chain may deviate from the input pose. The default value is 180, which imposes no effective limit.
## float Weight

The blend weight of the Look At result over the input pose, in the [0, 1] range. The default value is 1.0.
## JointLimitSetInfo LimitSet

The set of per-joint limits applied while solving. The set is owned by the caller and must outlive the solve.
### Members

---

## LookAtChainInfo ( )

Constructor. Creates a new set of Look At chain parameters with default values.
## void SetJoint ( int num , int joint )

Sets the skeleton joint at the given position in the chain.
### Arguments

- *int* **num** - Position in the chain, from the root to the tip.
- *int* **joint** - Index of the skeleton joint to put at this position.

## int GetJoint ( int num )

Returns the skeleton joint at the given position in the chain.
### Arguments

- *int* **num** - Position in the chain, from the root to the tip.

### Return value

Index of the skeleton joint, or -1 if the position is out of range or the joint is not set.
## void SetJointForwardAxis ( int num , vec3 forward_axis )

Sets the local axis of the joint at the given position that is aimed at the target. The default value is (0, 1, 0).
### Arguments

- *int* **num** - Position in the chain, from the root to the tip.
- *vec3* **forward_axis** - Local axis of the joint that is aimed at the target.

## vec3 GetJointForwardAxis ( int num )

Returns the local axis of the joint at the given position that is aimed at the target.
### Arguments

- *int* **num** - Position in the chain, from the root to the tip.

### Return value

Local axis of the joint that is aimed at the target.
## void SetJointUpAxis ( int num , vec3 up_axis )

Sets the local up axis of the joint at the given position, used as the twist reference when the pole is applied. The default value is (0, 0, 1).
### Arguments

- *int* **num** - Position in the chain, from the root to the tip.
- *vec3* **up_axis** - Local up axis of the joint used as the twist reference.

## vec3 GetJointUpAxis ( int num )

Returns the local up axis of the joint at the given position.
### Arguments

- *int* **num** - Position in the chain, from the root to the tip.

### Return value

Local up axis of the joint.
## void SetJointWeight ( int num , float weight )

Sets the share of the aiming rotation applied to the joint at the given position. The default value is 1.0.
### Arguments

- *int* **num** - Position in the chain, from the root to the tip.
- *float* **weight** - Share of the aiming rotation applied to this joint, in the [0, 1] range.

## float GetJointWeight ( int num )

Returns the share of the aiming rotation applied to the joint at the given position.
### Arguments

- *int* **num** - Position in the chain, from the root to the tip.

### Return value

Share of the aiming rotation applied to this joint.
