# Unigine::AnimationModifierBones Class (CPP)

**Header:** #include <UnigineAnimation.h>

**Inherits from:** AnimationModifier


This class allows animating all bones for [ObjectMeshSkinnedLegacy](../../../../api/library/objects/class.objectmeshskinnedlegacy_cpp.md).


## AnimationModifierBones Class

### Members

## void setNumBones ( )

Sets a new number of bones affected by the animation modifier.
### Arguments

- **bones** - The number of bones affected by the animation modifier.

## getNumBones () const

Returns the current number of bones affected by the animation modifier.
### Return value

Current number of bones affected by the animation modifier.
---

## AnimationModifierBones ( )

Constructor. Creates a new animation modifier for bones.
## void copy ( const Ptr < AnimationModifierBones > & modifier )

Copies all data from the specified source animation modifier.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationModifierBones](../../../../api/library/animations/timeline/class.animationmodifierbones_cpp.md)> &* **modifier** - Source animation modifier.

## int getValueByTime ( float time , Vector < Math:: mat4 > & OUT_transforms )

Returns the number of bones affected by the animation modifier and saves the transformation values of the modifier at the specified time.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.
- *[Vector](../../../../api/library/containers/vector/class.vector_cpp.md)< Math::[mat4](../../../../api/library/math/class.mat4_cpp.md)> &* **OUT_transforms** - Transformation matrices to save the returned values. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

The number of bones affected by the animation modifier.
## void addValue ( float time , Vector < Math:: mat4 > & OUT_transforms )

Adds the transformation values to the modifier at the specified time.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.
- *[Vector](../../../../api/library/containers/vector/class.vector_cpp.md)< Math::[mat4](../../../../api/library/math/class.mat4_cpp.md)> &* **OUT_transforms** - Transformation matrices. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void setCurvePosX ( int bone_index , const Ptr < AnimationCurveFloat > & in_curve )

Sets the curve storing the bone positions along the X axis.
### Arguments

- *int* **bone_index** - Index of the bone.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_cpp.md)> &* **in_curve** - The animation curve storing the bone positions along the X axis.

## Ptr < AnimationCurveFloat > getCurvePosX ( int bone_index ) const

Returns the curve storing the bone positions along the X axis.
### Arguments

- *int* **bone_index** - Index of the bone.

### Return value

The animation curve storing the bone positions along the X axis.
## void setCurvePosY ( int bone_index , const Ptr < AnimationCurveFloat > & in_curve )

Sets the curve storing the bone positions along the Y axis.
### Arguments

- *int* **bone_index** - Index of the bone.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_cpp.md)> &* **in_curve** - The animation curve storing the bone positions along the Y axis.

## Ptr < AnimationCurveFloat > getCurvePosY ( int bone_index ) const

Returns the curve storing the bone positions along the Y axis.
### Arguments

- *int* **bone_index** - Index of the bone.

### Return value

The animation curve storing the bone positions along the Y axis.
## void setCurvePosZ ( int bone_index , const Ptr < AnimationCurveFloat > & in_curve )

Sets the curve storing the bone positions along the Z axis.
### Arguments

- *int* **bone_index** - Index of the bone.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_cpp.md)> &* **in_curve** - The animation curve storing the bone positions along the Z axis.

## Ptr < AnimationCurveFloat > getCurvePosZ ( int bone_index ) const

Returns the curve storing the bone positions along the Z axis.
### Arguments

- *int* **bone_index** - Index of the bone.

### Return value

The animation curve storing the bone positions along the Z axis.
## void setCurveRot ( int bone_index , const Ptr < AnimationCurveQuat > & in_curve )

Sets the curve storing the bone transforms.
### Arguments

- *int* **bone_index** - Index of the bone.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveQuat](../../../../api/library/animations/timeline/class.animationcurvequat_cpp.md)> &* **in_curve** - The animation curve storing the bone transforms.

## Ptr < AnimationCurveQuat > getCurveRot ( int bone_index ) const

Returns the curve storing the bone transforms.
### Arguments

- *int* **bone_index** - Index of the bone.

### Return value

The animation curve storing the bone transforms.
## void setCurveScaleX ( int bone_index , const Ptr < AnimationCurveFloat > & in_curve )

Sets the animation curve storing the bone scaling along the X axis.
### Arguments

- *int* **bone_index** - Index of the bone.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_cpp.md)> &* **in_curve** - The animation curve storing the bone scaling along the X axis.

## Ptr < AnimationCurveFloat > getCurveScaleX ( int bone_index ) const

Returns the animation curve storing the bone scaling along the X axis.
### Arguments

- *int* **bone_index** - Index of the bone.

### Return value

The animation curve storing the bone scaling along the X axis.
## void setCurveScaleY ( int bone_index , const Ptr < AnimationCurveFloat > & in_curve )

Sets the animation curve storing the bone scaling along the Y axis.
### Arguments

- *int* **bone_index** - Index of the bone.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_cpp.md)> &* **in_curve** - The animation curve storing the bone scaling along the Y axis.

## Ptr < AnimationCurveFloat > getCurveScaleY ( int bone_index ) const

Returns the animation curve storing the bone scaling along the Y axis.
### Arguments

- *int* **bone_index** - Index of the bone.

### Return value

The animation curve storing the bone scaling along the Y axis.
## void setCurveScaleZ ( int bone_index , const Ptr < AnimationCurveFloat > & in_curve )

Sets the animation curve storing the bone scaling along the Z axis.
### Arguments

- *int* **bone_index** - Index of the bone.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_cpp.md)> &* **in_curve** - The animation curve storing the bone scaling along the Z axis.

## Ptr < AnimationCurveFloat > getCurveScaleZ ( int bone_index ) const

Returns the animation curve storing the bone scaling along the Z axis.
### Arguments

- *int* **bone_index** - Index of the bone.

### Return value

The animation curve storing the bone scaling along the Z axis.
