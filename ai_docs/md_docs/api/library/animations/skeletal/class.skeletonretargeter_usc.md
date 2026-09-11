# SkeletonRetargeter Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This is the base class for animation retargeting - transferring skeletal animation poses from one skeleton to another. Different retargeting strategies are implemented by subclasses:


- [SkeletonRetargeterEquals](../../../../api/library/animations/skeletal/class.skeletonretargeterequals_usc.md) - for skeletons with identical joint hierarchies.
- [SkeletonRetargeterNamesMatching](../../../../api/library/animations/skeletal/class.skeletonretargeternamesmatching_usc.md) - maps joints by matching their names.
- [SkeletonRetargeterTranslations](../../../../api/library/animations/skeletal/class.skeletonretargetertranslations_usc.md) - maps joints by matching their translations.


Use the static [findRetargeter()](#findRetargeter_ConstSkeleton_ConstSkeleton_SkeletonRetargeter) method to automatically find a registered retargeter between two skeletons, or create subclass instances directly for custom configuration.


## SkeletonRetargeter Class

### Members

## int getType () const

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

## void retarget ( int retarget_direction , SkeletonPoseDecomposed out_pose , SkeletonPoseDecomposed compatible_pose )

Retargets a decomposed pose from one skeleton to another. The compatible_pose provides source joint transforms, and out_pose receives the retargeted result.
### Arguments

- *int* **retarget_direction** - Direction of retargeting.
- *[SkeletonPoseDecomposed](../../../../api/library/animations/skeletal/class.skeletonposedecomposed_usc.md)* **out_pose** - Output pose that receives the retargeted result.
- *[SkeletonPoseDecomposed](../../../../api/library/animations/skeletal/class.skeletonposedecomposed_usc.md)* **compatible_pose** - Source pose to retarget from.

## void retarget ( int retarget_direction , SkeletonPoseMatrix out_pose , SkeletonPoseMatrix compatible_pose )

Retargets a matrix pose from one skeleton to another. The compatible_pose provides source joint transforms, and out_pose receives the retargeted result.
### Arguments

- *int* **retarget_direction** - Direction of retargeting.
- *[SkeletonPoseMatrix](../../../../api/library/animations/skeletal/class.skeletonposematrix_usc.md)* **out_pose** - Output pose that receives the retargeted result.
- *[SkeletonPoseMatrix](../../../../api/library/animations/skeletal/class.skeletonposematrix_usc.md)* **compatible_pose** - Source pose to retarget from.

## void scaleRootMotion ( int retarget_direction , FloatTransform delta )

Scales the root motion delta position for proportional retargeting between two skeletons. Only applies to TRANSLATIONS-type retargeters - other types leave the delta unchanged. In BIND retarget mode, the delta position is zeroed out. In PROPORTION mode, the delta position is scaled by the ratio of the root bone lengths between the source and target skeletons.
### Arguments

- *int* **retarget_direction** - Direction of retargeting.
- *FloatTransform* **delta** - Root motion delta transform to be scaled.
