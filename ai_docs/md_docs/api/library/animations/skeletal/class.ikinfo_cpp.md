# Unigine::IKInfo Class (CPP)

**Header:** #include <UnigineSkeletonControlRig.h>


This is the base class for the parameters of the inverse kinematics solvers. It holds what both solvers have in common: the target, the pole, the blend weight and the behavior at the limit of the reach. It is an abstract class - create an instance of [IKInfoTwoBone](../../../../api/library/animations/skeletal/class.ikinfotwobone_cpp.md) or [IKInfoChain](../../../../api/library/animations/skeletal/class.ikinfochain_cpp.md) instead.


Positions are set in the object space of the skeleton. See the [Procedural Skeleton Control](../../../../content/animations/procedural_control/index.md) article for the concepts behind the solvers.


## IKInfo Class

### Enums

## TYPE

Type of the IK solver the parameters belong to.
| Name | Description |
|---|---|
| **IK_INFO** = 0 | Base IK parameters type. |
| **IK_INFO_TWO_BONE** = 1 | Parameters of the analytical two-bone solver, see [IKInfoTwoBone](../../../../api/library/animations/skeletal/class.ikinfotwobone_cpp.md). |
| **IK_INFO_CHAIN** = 2 | Parameters of the iterative chain solver, see [IKInfoChain](../../../../api/library/animations/skeletal/class.ikinfochain_cpp.md). |

## SOLVER_MODE

Solver mode that defines how the chain behaves when the target is out of reach.
| Name | Description |
|---|---|
| **SOLVER_MODE_HARD** = 0 | The end of the chain reaches the target exactly up to the full reach, then locks. There is a visible snap at the boundary. |
| **SOLVER_MODE_SOFT** = 1 | The chain approaches the full reach asymptotically and never quite reaches the target near the boundary, which avoids the snap. |
| **SOLVER_MODE_STRETCHING** = 2 | The bones are stretched past the full reach so that the end reaches the target exactly, capped by the maximum stretch scale. |

### Members

## IKInfo::TYPE getType () const

Returns the current type of the solver the parameters belong to.
### Return value

Current type of the solver
## void setTarget ( const Math:: vec3 & target )

Sets a new position the end of the chain reaches toward, in the object space of the skeleton. The default value is (0, 0, 0).
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md)&* **target** - The position the end of the chain reaches toward

## Math:: vec3 getTarget () const

Returns the current position the end of the chain reaches toward, in the object space of the skeleton. The default value is (0, 0, 0).
### Return value

Current position the end of the chain reaches toward
## void setPole ( const Math:: vec3 & pole )

Sets a new position that resolves the bending direction of the chain: the chain bends toward it. The default value is (0, 0, 0).
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md)&* **pole** - The position that resolves the bending direction of the chain

## Math:: vec3 getPole () const

Returns the current position that resolves the bending direction of the chain: the chain bends toward it. The default value is (0, 0, 0).
### Return value

Current position that resolves the bending direction of the chain
## void setWeight ( float weight )

Sets a new blend weight of the IK result over the input pose, in the [0, 1] range. The default value is 1.0.
### Arguments

- *float* **weight** - The blend weight of the IK result over the input pose

## float getWeight () const

Returns the current blend weight of the IK result over the input pose, in the [0, 1] range. The default value is 1.0.
### Return value

Current blend weight of the IK result over the input pose
## void setSolverMode ( IKInfo::SOLVER_MODE mode )

Sets a new solver mode that defines how the chain behaves when the target is out of reach. The default value is HARD.
### Arguments

- *[IKInfo::SOLVER_MODE](../../../../api/library/animations/skeletal/class.ikinfo_cpp.md#SOLVER_MODE)* **mode** - The solver mode of the chain

## IKInfo::SOLVER_MODE getSolverMode () const

Returns the current solver mode that defines how the chain behaves when the target is out of reach. The default value is HARD.
### Return value

Current solver mode of the chain
## void setSoftness ( float softness )

Sets a new fraction of the full chain reach over which the asymptotic blend starts. For example, 0.05 starts the blend at 95% of the reach. Used only in the SOFT solver mode. The default value is 0.05.
### Arguments

- *float* **softness** - The fraction of the full reach over which the asymptotic blend starts

## float getSoftness () const

Returns the current fraction of the full chain reach over which the asymptotic blend starts. For example, 0.05 starts the blend at 95% of the reach. Used only in the SOFT solver mode. The default value is 0.05.
### Return value

Current fraction of the full reach over which the asymptotic blend starts
## void setMaxStretchScale ( float scale )

Sets a new upper cap on the bone elongation factor when the target is past the full reach. For example, 1.5 lets the bones stretch up to 1.5 times their natural length. Used only in the STRETCHING solver mode. The default value is 1.5.
### Arguments

- *float* **scale** - The upper cap on the bone elongation factor

## float getMaxStretchScale () const

Returns the current upper cap on the bone elongation factor when the target is past the full reach. For example, 1.5 lets the bones stretch up to 1.5 times their natural length. Used only in the STRETCHING solver mode. The default value is 1.5.
### Return value

Current upper cap on the bone elongation factor
