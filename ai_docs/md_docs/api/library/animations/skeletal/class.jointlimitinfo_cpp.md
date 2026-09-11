# Unigine::JointLimitInfo Class (CPP)

**Header:** #include <UnigineSkeletonControlRig.h>


This is the base class for the parameters of the joint limits. A joint limit restricts the local rotation of a joint to an anatomically valid range, so that a chain solver cannot reach the target with a pose no real joint could strike - an elbow bent the wrong way, or a knee turned inside out.


It is an abstract class. Seven concrete limits derive from it: four basic ones, each restricting a single kind of motion ([hinge](../../../../api/library/animations/skeletal/class.jointlimitinfohinge_cpp.md), [cone](../../../../api/library/animations/skeletal/class.jointlimitinfocone_cpp.md), [asymmetric cone](../../../../api/library/animations/skeletal/class.jointlimitinfoconeasym_cpp.md) and [twist](../../../../api/library/animations/skeletal/class.jointlimitinfotwist_cpp.md)), and three that combine a swing limit with a twist limit ([hinge-twist](../../../../api/library/animations/skeletal/class.jointlimitinfohingetwist_cpp.md), [cone-twist](../../../../api/library/animations/skeletal/class.jointlimitinfoconetwist_cpp.md) and [asymmetric cone-twist](../../../../api/library/animations/skeletal/class.jointlimitinfoconeasymtwist_cpp.md)).


A limit is applied either directly, by passing it to the matching **solveLayer*** method of the [NodeSkeletonPose](../../../../api/library/nodes/class.nodeskeletonpose_cpp.md) class, or as a constraint for a chain solver - add it to a [JointLimitSetInfo](../../../../api/library/animations/skeletal/class.jointlimitsetinfo_cpp.md) and assign the set to an [IKInfoChain](../../../../api/library/animations/skeletal/class.ikinfochain_cpp.md) or a [LookAtChainInfo](../../../../api/library/animations/skeletal/class.lookatchaininfo_cpp.md).


This class holds what all the limits have in common: the joint, the mode, the blend weight and the soft attractor. All axes are set in the bind-local frame of the joint.


## JointLimitInfo Class

### Enums

## TYPE

Type of the joint limit the parameters belong to.
| Name | Description |
|---|---|
| **JOINT_LIMIT_INFO** = 0 | Base joint limit parameters type. |
| **JOINT_LIMIT_INFO_HINGE** = 1 | A hinge around one axis, see [JointLimitInfoHinge](../../../../api/library/animations/skeletal/class.jointlimitinfohinge_cpp.md). |
| **JOINT_LIMIT_INFO_CONE** = 2 | A symmetric cone swing, see [JointLimitInfoCone](../../../../api/library/animations/skeletal/class.jointlimitinfocone_cpp.md). |
| **JOINT_LIMIT_INFO_CONE_ASYM** = 3 | An asymmetric cone swing, see [JointLimitInfoConeAsym](../../../../api/library/animations/skeletal/class.jointlimitinfoconeasym_cpp.md). |
| **JOINT_LIMIT_INFO_TWIST** = 4 | A twist around the bone, see [JointLimitInfoTwist](../../../../api/library/animations/skeletal/class.jointlimitinfotwist_cpp.md). |
| **JOINT_LIMIT_INFO_HINGE_TWIST** = 5 | A hinge combined with a twist, see [JointLimitInfoHingeTwist](../../../../api/library/animations/skeletal/class.jointlimitinfohingetwist_cpp.md). |
| **JOINT_LIMIT_INFO_CONE_TWIST** = 6 | A cone swing combined with a twist, see [JointLimitInfoConeTwist](../../../../api/library/animations/skeletal/class.jointlimitinfoconetwist_cpp.md). |
| **JOINT_LIMIT_INFO_CONE_ASYM_TWIST** = 7 | An asymmetric cone swing combined with a twist, see [JointLimitInfoConeAsymTwist](../../../../api/library/animations/skeletal/class.jointlimitinfoconeasymtwist_cpp.md). |

## LIMIT_MODE

Behavior of the limit.
| Name | Description |
|---|---|
| **LIMIT_MODE_FREE** = 0 | The joint moves without restriction. Use it to switch the limit off without removing it. |
| **LIMIT_MODE_LIMITED** = 1 | The joint is kept within the range set by the limit. This is the working mode. |
| **LIMIT_MODE_LOCKED** = 2 | The joint is held at its bind reference and does not move at all. |

### Members

## JointLimitInfo::TYPE getType () const

Returns the current type of the joint limit the parameters belong to.
### Return value

Current type of the joint limit
## void setJoint ( int joint )

Sets a new index of the joint the limit is applied to. The default value is -1.
### Arguments

- *int* **joint** - The index of the joint the limit is applied to

## int getJoint () const

Returns the current index of the joint the limit is applied to. The default value is -1.
### Return value

Current index of the joint the limit is applied to
## void setMode ( JointLimitInfo::LIMIT_MODE mode )

Sets a new behavior of the limit. The default value is LIMITED.
### Arguments

- *[JointLimitInfo::LIMIT_MODE](../../../../api/library/animations/skeletal/class.jointlimitinfo_cpp.md#LIMIT_MODE)* **mode** - The behavior of the limit

## JointLimitInfo::LIMIT_MODE getMode () const

Returns the current behavior of the limit. The default value is LIMITED.
### Return value

Current behavior of the limit
## void setWeight ( float weight )

Sets a new blend weight of the clamped result over the input pose, in the [0, 1] range. The default value is 1.0.
### Arguments

- *float* **weight** - The blend weight of the clamped result over the input pose

## float getWeight () const

Returns the current blend weight of the clamped result over the input pose, in the [0, 1] range. The default value is 1.0.
### Return value

Current blend weight of the clamped result over the input pose
## void setPreferredLocalRotation ( const Math:: quat & rotation )

Sets a new target rotation of the soft attractor, in the bind-local frame of the joint. It is used when the preferred strength is greater than zero. The value is normalized on assignment; a zero quaternion is replaced with the identity one. The default value is the identity quaternion.
### Arguments

- *const  Math::[quat](../../../../api/library/math/class.quat_cpp.md)&* **rotation** - The target rotation of the soft attractor

## Math:: quat getPreferredLocalRotation () const

Returns the current target rotation of the soft attractor, in the bind-local frame of the joint. It is used when the preferred strength is greater than zero. The value is normalized on assignment; a zero quaternion is replaced with the identity one. The default value is the identity quaternion.
### Return value

Current target rotation of the soft attractor
## void setPreferredStrength ( float strength )

Sets a new blend ratio of the soft attractor, in the [0, 1] range. After the hard clamp, the rotation of the joint is slerped toward the preferred local rotation by this fraction and then clamped again. The default value is 0.0, which disables the attractor.
### Arguments

- *float* **strength** - The blend ratio of the soft attractor

## float getPreferredStrength () const

Returns the current blend ratio of the soft attractor, in the [0, 1] range. After the hard clamp, the rotation of the joint is slerped toward the preferred local rotation by this fraction and then clamped again. The default value is 0.0, which disables the attractor.
### Return value

Current blend ratio of the soft attractor
