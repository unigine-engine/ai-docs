# Unigine::IKInfoChain Class (CS)

**Inherits from:** IKInfo


This class stores the parameters of the iterative IK solver for a chain of arbitrary length, such as a spine, a tail, a tentacle, or fingers. The solver orients the listed joints so that the tip reaches toward the target. A long chain can bend into many shapes that all reach the target, so the bending direction is resolved by the [limit source](#getLimitSource_int): a pole or the attached joint limits.


For a three-joint chain the analytical [IKInfoTwoBone](../../../../api/library/animations/skeletal/class.ikinfotwobone_cs.md) solver is preferable - it needs no iterations.


An instance of this class is passed to the *[SolveLayerIKChain()](../../../../api/library/nodes/class.nodeskeletonpose_cs.md#solveLayerIKChain_int_IKInfoChain_void)* method of the [NodeSkeletonPose](../../../../api/library/nodes/class.nodeskeletonpose_cs.md) class.


The same solver is available as the [IK Chain](../../../../content/animations/graph/node_library/skeleton/ik_chain.md) node in the animation graph, which is the recommended way to set it up visually. This class is the programmatic equivalent for driving the solver from code.


> **Notice:** The rotation of the tip joint is not modified. To control the orientation of the end effector, set it separately after solving.


## IKInfoChain Class

### Enums

## LIMIT_SOURCE

Source the solver takes the bending direction of the chain from.
| Name | Description |
|---|---|
| **NONE** = 0 | The chain bends following the previous pose. The pole and the attached joint limits are ignored. |
| **POLE** = 1 | The mid joints rotate to align with the plane through the root, the target and the pole. This is the standard elbow and knee hint. |
| **JOINT** = 2 | The per-joint limits from the assigned limit set are applied on every iteration, which is anatomically correct for hinge joints. The pole is ignored. |

### Properties

## int NumJoints

The number of joints in the chain. Changing the value resizes the list of joints; the joints added by it are set to -1.
## int NumIterations

The maximum number of solver iterations per solve. The solver exits early once the tip is within the distance tolerance of the target, so extra iterations cost nothing on an already converged chain. The default value is 8.
## float DistanceTolerance

The distance between the tip and the target, in units, below which the chain is considered converged and the solver stops iterating. The default value is 0.001. Set it to 0 to always run all the iterations.
## int RestartAttempts

The number of extra solve attempts made from deterministic seed poses when the warm solve misses the target. Each attempt is a full solve, so the value is capped at 32. It only has an effect when the bending direction is taken from joint limits. The default value is 0, which means a single warm solve.
## IKInfoChain.LIMIT_SOURCE LimitSource

The source the solver takes the bending direction of the chain from. The default value is POLE.
## JointLimitSetInfo LimitSet

The set of per-joint limits applied while solving. It is used only when the limit source is set to JOINT. The set is owned by the caller and must outlive the solve.
### Members

---

## IKInfoChain ( )

Constructor. Creates a new set of IK chain parameters with default values.
## void SetJoint ( int num , int joint )

Sets the skeleton joint at the given position in the chain. Each joint must be the direct child of the one before it.
### Arguments

- *int* **num** - Position in the chain, from the root to the tip.
- *int* **joint** - Index of the skeleton joint to put at this position.

## int GetJoint ( int num )

Returns the skeleton joint at the given position in the chain.
### Arguments

- *int* **num** - Position in the chain, from the root to the tip.

### Return value

Index of the skeleton joint, or -1 if the position is out of range or the joint is not set.
## void ResetSolveState ( )

Drops the solver state kept between frames. Call it whenever the continuity of the solve is broken - on the first solve, after a skeleton swap, or when the chain is re-entered - so that the solver picks the best candidate instead of protecting continuity with a stale one.
