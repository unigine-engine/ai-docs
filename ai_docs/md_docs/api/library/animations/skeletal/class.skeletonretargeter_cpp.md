# SkeletonRetargeter Class (CPP)

**Header:** #include <UnigineSkeleton.h>


This is the base class for animation retargeting - transferring skeletal animation poses from one skeleton to another. Different retargeting strategies are implemented by subclasses:


- [SkeletonRetargeterEquals](../../../../api/library/animations/skeletal/class.skeletonretargeterequals_cpp.md) - for skeletons with identical joint hierarchies.
- [SkeletonRetargeterNamesMatching](../../../../api/library/animations/skeletal/class.skeletonretargeternamesmatching_cpp.md) - maps joints by matching their names.
- [SkeletonRetargeterTranslations](../../../../api/library/animations/skeletal/class.skeletonretargetertranslations_cpp.md) - maps joints by matching their translations.


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
| **RETARGET_DIRECTION_FORWARD** = 0 | Retarget from the first skeleton to the second. |
| **RETARGET_DIRECTION_BACKWARD** = 1 | Retarget from the second skeleton to the first. |

### Members

## SkeletonRetargeter::TYPE getType () const

Returns the current type of this retargeter instance, identifying which subclass strategy it implements.
### Return value

Current retargeter type.
## const char * getTypeName () const

Returns the current human-readable name of the retargeter type.
### Return value

Current retargeter type name.
## UGUID getFirstFileGUID () const

Returns the current GUID of the first of the two skeleton files this retargeter was registered for.
### Return value

Current file GUID of the first skeleton
## UGUID getSecondFileGUID () const

Returns the current GUID of the second of the two skeleton files this retargeter was registered for.
### Return value

Current file GUID of the second skeleton
---

## void retarget ( SkeletonRetargeter::RETARGET_DIRECTION retarget_direction , const Ptr < SkeletonPoseDecomposed > & out_pose , const Ptr < SkeletonPoseDecomposed > & compatible_pose ) const

Retargets a decomposed pose from one skeleton to another. The compatible_pose provides source joint transforms, and out_pose receives the retargeted result.
### Arguments

- *[SkeletonRetargeter::RETARGET_DIRECTION](../../../../api/library/animations/skeletal/class.skeletonretargeter_cpp.md#RETARGET_DIRECTION)* **retarget_direction** - Direction of retargeting.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[SkeletonPoseDecomposed](../../../../api/library/animations/skeletal/class.skeletonposedecomposed_cpp.md)> &* **out_pose** - Output pose that receives the retargeted result.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[SkeletonPoseDecomposed](../../../../api/library/animations/skeletal/class.skeletonposedecomposed_cpp.md)> &* **compatible_pose** - Source pose to retarget from.

## void retarget ( SkeletonRetargeter::RETARGET_DIRECTION retarget_direction , const Ptr < SkeletonPoseMatrix > & out_pose , const Ptr < SkeletonPoseMatrix > & compatible_pose ) const

Retargets a matrix pose from one skeleton to another. The compatible_pose provides source joint transforms, and out_pose receives the retargeted result.
### Arguments

- *[SkeletonRetargeter::RETARGET_DIRECTION](../../../../api/library/animations/skeletal/class.skeletonretargeter_cpp.md#RETARGET_DIRECTION)* **retarget_direction** - Direction of retargeting.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[SkeletonPoseMatrix](../../../../api/library/animations/skeletal/class.skeletonposematrix_cpp.md)> &* **out_pose** - Output pose that receives the retargeted result.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[SkeletonPoseMatrix](../../../../api/library/animations/skeletal/class.skeletonposematrix_cpp.md)> &* **compatible_pose** - Source pose to retarget from.

## void scaleRootMotion ( SkeletonRetargeter::RETARGET_DIRECTION retarget_direction , Math::Transform & delta ) const

Scales the root motion delta position for proportional retargeting between two skeletons. Only applies to TRANSLATIONS-type retargeters - other types leave the delta unchanged. In BIND retarget mode, the delta position is zeroed out. In PROPORTION mode, the delta position is scaled by the ratio of the root bone lengths between the source and target skeletons.
### Arguments

- *[SkeletonRetargeter::RETARGET_DIRECTION](../../../../api/library/animations/skeletal/class.skeletonretargeter_cpp.md#RETARGET_DIRECTION)* **retarget_direction** - Direction of retargeting.
- *Math::Transform &* **delta** - Root motion delta transform to be scaled.

## static Ptr < SkeletonRetargeter > findRetargeter ( const Ptr <ConstSkeleton> & skeleton_0 , const Ptr <ConstSkeleton> & skeleton_1 , int & out_retarget_direction )

Searches for a registered retargeter between two skeletons and returns the retarget direction via an output parameter.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<ConstSkeleton> &* **skeleton_0** - First skeleton.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<ConstSkeleton> &* **skeleton_1** - Second skeleton.
- *int &* **out_retarget_direction** - Output variable receiving the retarget direction for this skeleton pair.

### Return value

Retargeter instance if found; null otherwise.
## static Ptr < SkeletonRetargeter > findRetargeter ( const Ptr <ConstSkeleton> & skeleton_0 , const Ptr <ConstSkeleton> & skeleton_1 )

Searches for a registered retargeter between two skeletons.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<ConstSkeleton> &* **skeleton_0** - First skeleton.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<ConstSkeleton> &* **skeleton_1** - Second skeleton.

### Return value

Retargeter instance if found; null otherwise.
## static Ptr < SkeletonRetargeter > findRetargeter ( const UGUID & skeleton_file_guid_0 , const UGUID & skeleton_file_guid_1 , int & out_retarget_direction )

Searches for a registered retargeter between two skeletons identified by their file GUIDs and returns the retarget direction via an output parameter.
### Arguments

- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **skeleton_file_guid_0** - File GUID of the first skeleton.
- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **skeleton_file_guid_1** - File GUID of the second skeleton.
- *int &* **out_retarget_direction** - Output variable receiving the retarget direction for this skeleton pair.

### Return value

Retargeter instance if found; null otherwise.
## static Ptr < SkeletonRetargeter > findRetargeter ( const UGUID & skeleton_file_guid_0 , const UGUID & skeleton_file_guid_1 )

Searches for a registered retargeter between two skeletons identified by their file GUIDs.
### Arguments

- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **skeleton_file_guid_0** - File GUID of the first skeleton.
- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **skeleton_file_guid_1** - File GUID of the second skeleton.

### Return value

Retargeter instance if found; null otherwise.
