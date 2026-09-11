# Unigine::JointLimitInfo Class (CS)


This is the base class for the parameters of the joint limits. A joint limit restricts the local rotation of a joint to an anatomically valid range, so that a chain solver cannot reach the target with a pose no real joint could strike - an elbow bent the wrong way, or a knee turned inside out.


It is an abstract class. Seven concrete limits derive from it: four basic ones, each restricting a single kind of motion ([hinge](../../../../api/library/animations/skeletal/class.jointlimitinfohinge_cs.md), [cone](../../../../api/library/animations/skeletal/class.jointlimitinfocone_cs.md), [asymmetric cone](../../../../api/library/animations/skeletal/class.jointlimitinfoconeasym_cs.md) and [twist](../../../../api/library/animations/skeletal/class.jointlimitinfotwist_cs.md)), and three that combine a swing limit with a twist limit ([hinge-twist](../../../../api/library/animations/skeletal/class.jointlimitinfohingetwist_cs.md), [cone-twist](../../../../api/library/animations/skeletal/class.jointlimitinfoconetwist_cs.md) and [asymmetric cone-twist](../../../../api/library/animations/skeletal/class.jointlimitinfoconeasymtwist_cs.md)).


A limit is applied either directly, by passing it to the matching **solveLayer*** method of the [NodeSkeletonPose](../../../../api/library/nodes/class.nodeskeletonpose_cs.md) class, or as a constraint for a chain solver - add it to a [JointLimitSetInfo](../../../../api/library/animations/skeletal/class.jointlimitsetinfo_cs.md) and assign the set to an [IKInfoChain](../../../../api/library/animations/skeletal/class.ikinfochain_cs.md) or a [LookAtChainInfo](../../../../api/library/animations/skeletal/class.lookatchaininfo_cs.md).


This class holds what all the limits have in common: the joint, the mode, the blend weight and the soft attractor. All axes are set in the bind-local frame of the joint.


## JointLimitInfo Class

### Enums

## TYPE

Type of the joint limit the parameters belong to.
| Name | Description |
|---|---|
| **JOINT_LIMIT_INFO** = 0 | Base joint limit parameters type. |
| **JOINT_LIMIT_INFO_HINGE** = 1 | A hinge around one axis, see [JointLimitInfoHinge](../../../../api/library/animations/skeletal/class.jointlimitinfohinge_cs.md). |
| **JOINT_LIMIT_INFO_CONE** = 2 | A symmetric cone swing, see [JointLimitInfoCone](../../../../api/library/animations/skeletal/class.jointlimitinfocone_cs.md). |
| **JOINT_LIMIT_INFO_CONE_ASYM** = 3 | An asymmetric cone swing, see [JointLimitInfoConeAsym](../../../../api/library/animations/skeletal/class.jointlimitinfoconeasym_cs.md). |
| **JOINT_LIMIT_INFO_TWIST** = 4 | A twist around the bone, see [JointLimitInfoTwist](../../../../api/library/animations/skeletal/class.jointlimitinfotwist_cs.md). |
| **JOINT_LIMIT_INFO_HINGE_TWIST** = 5 | A hinge combined with a twist, see [JointLimitInfoHingeTwist](../../../../api/library/animations/skeletal/class.jointlimitinfohingetwist_cs.md). |
| **JOINT_LIMIT_INFO_CONE_TWIST** = 6 | A cone swing combined with a twist, see [JointLimitInfoConeTwist](../../../../api/library/animations/skeletal/class.jointlimitinfoconetwist_cs.md). |
| **JOINT_LIMIT_INFO_CONE_ASYM_TWIST** = 7 | An asymmetric cone swing combined with a twist, see [JointLimitInfoConeAsymTwist](../../../../api/library/animations/skeletal/class.jointlimitinfoconeasymtwist_cs.md). |

## LIMIT_MODE

Behavior of the limit.
| Name | Description |
|---|---|
| **FREE** = 0 | The joint moves without restriction. Use it to switch the limit off without removing it. |
| **LIMITED** = 1 | The joint is kept within the range set by the limit. This is the working mode. |
| **LOCKED** = 2 | The joint is held at its bind reference and does not move at all. |

### Properties

## 🔒︎ JointLimitInfo.TYPE Type

The type of the joint limit the parameters belong to.
## int Joint

The index of the joint the limit is applied to. The default value is -1.
## JointLimitInfo.LIMIT_MODE Mode

The behavior of the limit. The default value is LIMITED.
## float Weight

The blend weight of the clamped result over the input pose, in the [0, 1] range. The default value is 1.0.
## quat PreferredLocalRotation

The target rotation of the soft attractor, in the bind-local frame of the joint. It is used when the preferred strength is greater than zero. The value is normalized on assignment; a zero quaternion is replaced with the identity one. The default value is the identity quaternion.
## float PreferredStrength

The blend ratio of the soft attractor, in the [0, 1] range. After the hard clamp, the rotation of the joint is slerped toward the preferred local rotation by this fraction and then clamped again. The default value is 0.0, which disables the attractor.
