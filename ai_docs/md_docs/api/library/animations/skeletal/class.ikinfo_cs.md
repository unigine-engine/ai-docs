# Unigine::IKInfo Class (CS)


This is the base class for the parameters of the inverse kinematics solvers. It holds what both solvers have in common: the target, the pole, the blend weight and the behavior at the limit of the reach. It is an abstract class - create an instance of [IKInfoTwoBone](../../../../api/library/animations/skeletal/class.ikinfotwobone_cs.md) or [IKInfoChain](../../../../api/library/animations/skeletal/class.ikinfochain_cs.md) instead.


Positions are set in the object space of the skeleton. See the [Procedural Skeleton Control](../../../../content/animations/procedural_control/index.md) article for the concepts behind the solvers.


## IKInfo Class

### Enums

## TYPE

Type of the IK solver the parameters belong to.
| Name | Description |
|---|---|
| **IK_INFO** = 0 | Base IK parameters type. |
| **IK_INFO_TWO_BONE** = 1 | Parameters of the analytical two-bone solver, see [IKInfoTwoBone](../../../../api/library/animations/skeletal/class.ikinfotwobone_cs.md). |
| **IK_INFO_CHAIN** = 2 | Parameters of the iterative chain solver, see [IKInfoChain](../../../../api/library/animations/skeletal/class.ikinfochain_cs.md). |

## SOLVER_MODE

Solver mode that defines how the chain behaves when the target is out of reach.
| Name | Description |
|---|---|
| **HARD** = 0 | The end of the chain reaches the target exactly up to the full reach, then locks. There is a visible snap at the boundary. |
| **SOFT** = 1 | The chain approaches the full reach asymptotically and never quite reaches the target near the boundary, which avoids the snap. |
| **STRETCHING** = 2 | The bones are stretched past the full reach so that the end reaches the target exactly, capped by the maximum stretch scale. |

### Properties

## 🔒︎ IKInfo.TYPE Type

The type of the solver the parameters belong to.
## vec3 Target

The position the end of the chain reaches toward, in the object space of the skeleton. The default value is (0, 0, 0).
## vec3 Pole

The position that resolves the bending direction of the chain: the chain bends toward it. The default value is (0, 0, 0).
## float Weight

The blend weight of the IK result over the input pose, in the [0, 1] range. The default value is 1.0.
## IKInfo.SOLVER_MODE SolverMode

The solver mode that defines how the chain behaves when the target is out of reach. The default value is HARD.
## float Softness

The fraction of the full chain reach over which the asymptotic blend starts. For example, 0.05 starts the blend at 95% of the reach. Used only in the SOFT solver mode. The default value is 0.05.
## float MaxStretchScale

The upper cap on the bone elongation factor when the target is past the full reach. For example, 1.5 lets the bones stretch up to 1.5 times their natural length. Used only in the STRETCHING solver mode. The default value is 1.5.
