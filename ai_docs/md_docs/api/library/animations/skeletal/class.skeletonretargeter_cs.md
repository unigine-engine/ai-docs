# SkeletonRetargeter Class (CS)


This is the base class for animation retargeting - transferring skeletal animation poses from one skeleton to another. Different retargeting strategies are implemented by subclasses:


- [SkeletonRetargeterEquals](../../../../api/library/animations/skeletal/class.skeletonretargeterequals_cs.md) - for skeletons with identical joint hierarchies.
- [SkeletonRetargeterNamesMatching](../../../../api/library/animations/skeletal/class.skeletonretargeternamesmatching_cs.md) - maps joints by matching their names.
- [SkeletonRetargeterTranslations](../../../../api/library/animations/skeletal/class.skeletonretargetertranslations_cs.md) - maps joints by matching their translations.


Use the static [findRetargeter()](#findRetargeter_ConstSkeleton_ConstSkeleton_SkeletonRetargeter) method to automatically find a registered retargeter between two skeletons, or create subclass instances directly for custom configuration.


## SkeletonRetargeter Class

### Enums

## TYPE

Retargeter subclass type identifier.
| Name | Description |
|---|---|
| **SKELETON_RETARGETER** = 0 | Base retargeter type. |
| **SKELETON_RETARGETER_EQUALS** = 1 | Retargeter for skeletons with identical joint hierarchies. |
| **SKELETON_RETARGETER_NAMES_MATCHING** = 2 | Retargeter that maps joints by name matching. |
| **SKELETON_RETARGETER_TRANSLATIONS** = 3 | Retargeter that maps joints by translation matching. |

## RETARGET_DIRECTION

Direction of retargeting between two skeletons.
| Name | Description |
|---|---|
| **FORWARD** = 0 | Retarget from the first skeleton to the second. |
| **BACKWARD** = 1 | Retarget from the second skeleton to the first. |

### Properties

## 🔒︎ SkeletonRetargeter.TYPE Type

The type of this retargeter instance, identifying which subclass strategy it implements.
## 🔒︎ string TypeName

The human-readable name of the retargeter type.
## 🔒︎ UGUID FirstFileGUID

The GUID of the first of the two skeleton files this retargeter was registered for.
## 🔒︎ UGUID SecondFileGUID

The GUID of the second of the two skeleton files this retargeter was registered for.
### Members

---

## void Retarget ( SkeletonRetargeter.RETARGET_DIRECTION retarget_direction , SkeletonPoseDecomposed out_pose , SkeletonPoseDecomposed compatible_pose )

Retargets a decomposed pose from one skeleton to another. The compatible_pose provides source joint transforms, and out_pose receives the retargeted result.
### Arguments

- *[SkeletonRetargeter.RETARGET_DIRECTION](../../../../api/library/animations/skeletal/class.skeletonretargeter_cs.md#RETARGET_DIRECTION)* **retarget_direction** - Direction of retargeting.
- *[SkeletonPoseDecomposed](../../../../api/library/animations/skeletal/class.skeletonposedecomposed_cs.md)* **out_pose** - Output pose that receives the retargeted result.
- *[SkeletonPoseDecomposed](../../../../api/library/animations/skeletal/class.skeletonposedecomposed_cs.md)* **compatible_pose** - Source pose to retarget from.

## void Retarget ( SkeletonRetargeter.RETARGET_DIRECTION retarget_direction , SkeletonPoseMatrix out_pose , SkeletonPoseMatrix compatible_pose )

Retargets a matrix pose from one skeleton to another. The compatible_pose provides source joint transforms, and out_pose receives the retargeted result.
### Arguments

- *[SkeletonRetargeter.RETARGET_DIRECTION](../../../../api/library/animations/skeletal/class.skeletonretargeter_cs.md#RETARGET_DIRECTION)* **retarget_direction** - Direction of retargeting.
- *[SkeletonPoseMatrix](../../../../api/library/animations/skeletal/class.skeletonposematrix_cs.md)* **out_pose** - Output pose that receives the retargeted result.
- *[SkeletonPoseMatrix](../../../../api/library/animations/skeletal/class.skeletonposematrix_cs.md)* **compatible_pose** - Source pose to retarget from.

## void ScaleRootMotion ( SkeletonRetargeter.RETARGET_DIRECTION retarget_direction , FloatTransform delta )

Scales the root motion delta position for proportional retargeting between two skeletons. Only applies to TRANSLATIONS-type retargeters - other types leave the delta unchanged. In BIND retarget mode, the delta position is zeroed out. In PROPORTION mode, the delta position is scaled by the ratio of the root bone lengths between the source and target skeletons.
### Arguments

- *[SkeletonRetargeter.RETARGET_DIRECTION](../../../../api/library/animations/skeletal/class.skeletonretargeter_cs.md#RETARGET_DIRECTION)* **retarget_direction** - Direction of retargeting.
- *FloatTransform* **delta** - Root motion delta transform to be scaled.

## static SkeletonRetargeter FindRetargeter ( Skeleton skeleton_0 , Skeleton skeleton_1 , out int out_retarget_direction )

Searches for a registered retargeter between two skeletons and returns the retarget direction via an output parameter.
### Arguments

- *[Skeleton](../../../../api/library/animations/skeletal/class.skeleton_cs.md)* **skeleton_0** - First skeleton.
- *[Skeleton](../../../../api/library/animations/skeletal/class.skeleton_cs.md)* **skeleton_1** - Second skeleton.
- *out int* **out_retarget_direction** - Output variable receiving the retarget direction for this skeleton pair.

### Return value

Retargeter instance if found; null otherwise.
## static SkeletonRetargeter FindRetargeter ( Skeleton skeleton_0 , Skeleton skeleton_1 )

Searches for a registered retargeter between two skeletons.
### Arguments

- *[Skeleton](../../../../api/library/animations/skeletal/class.skeleton_cs.md)* **skeleton_0** - First skeleton.
- *[Skeleton](../../../../api/library/animations/skeletal/class.skeleton_cs.md)* **skeleton_1** - Second skeleton.

### Return value

Retargeter instance if found; null otherwise.
## static SkeletonRetargeter FindRetargeter ( UGUID skeleton_file_guid_0 , UGUID skeleton_file_guid_1 , out int out_retarget_direction )

Searches for a registered retargeter between two skeletons identified by their file GUIDs and returns the retarget direction via an output parameter.
### Arguments

- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **skeleton_file_guid_0** - File GUID of the first skeleton.
- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **skeleton_file_guid_1** - File GUID of the second skeleton.
- *out int* **out_retarget_direction** - Output variable receiving the retarget direction for this skeleton pair.

### Return value

Retargeter instance if found; null otherwise.
## static SkeletonRetargeter FindRetargeter ( UGUID skeleton_file_guid_0 , UGUID skeleton_file_guid_1 )

Searches for a registered retargeter between two skeletons identified by their file GUIDs.
### Arguments

- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **skeleton_file_guid_0** - File GUID of the first skeleton.
- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **skeleton_file_guid_1** - File GUID of the second skeleton.

### Return value

Retargeter instance if found; null otherwise.
