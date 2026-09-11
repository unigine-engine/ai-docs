# Unigine::AnimationChannelBones Class (CPP)

**Header:** #include <UnigineAnimation.h>

**Inherits from:** AnimationChannel


This channel animates the bones of a skeleton directly, holding a curve per bone for position, rotation and scale. It is what an animation baked from a source clip becomes when it is brought into a [sequence](../../../../api/library/animations/timeline/class.animationsequence_cpp.md) as plain keys.


Unlike the channels that drive a single parameter, this one carries a whole pose, so its keys are read and written as a list of transformation matrices, one per bone.


## AnimationChannelBones Class

### Members

## void setNumBones ( int bones )

Sets a new number of bones animated by the channel. Each bone keeps curves of its own for position, rotation and scale.
### Arguments

- *int* **bones** - The number of bones animated by the channel

## int getNumBones () const

Returns the current number of bones animated by the channel. Each bone keeps curves of its own for position, rotation and scale.
### Return value

Current number of bones animated by the channel
---

## AnimationChannelBones ( )

Constructor. Creates an empty channel.
## void assignFrom ( const Ptr < AnimationChannelBones > & channel )

Copies the content of the specified channel into this one.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationChannelBones](../../../../api/library/animations/timeline/class.animationchannelbones_cpp.md)> &* **channel** - Source channel to copy the content from.

## int getValueByTime ( float time , Vector < Math:: mat4 > & OUT_transforms )

Collects the transformations of all bones at the given moment and puts them to the **transforms** buffer.
### Arguments

- *float* **time** - Moment to be sampled, in seconds.
- *[Vector](../../../../api/library/containers/vector/class.vector_cpp.md)< Math::[mat4](../../../../api/library/math/class.mat4_cpp.md)> &* **OUT_transforms** - Output buffer for the transformation matrices of the bones. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of matrices put to the buffer.
## void addValue ( float time , Vector < Math:: mat4 > & OUT_transforms )

Adds a key holding the transformations of all bones at once.
### Arguments

- *float* **time** - Moment the key is to sit at, in seconds.
- *[Vector](../../../../api/library/containers/vector/class.vector_cpp.md)< Math::[mat4](../../../../api/library/math/class.mat4_cpp.md)> &* **OUT_transforms** - Transformation matrices of the bones. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void setCurvePosX ( int bone_index , const Ptr < AnimationCurveFloat > & in_curve )

Sets the curve that animates the position along the X axis of the specified bone.
### Arguments

- *int* **bone_index** - Number of the bone.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_cpp.md)> &* **in_curve** - Curve to animate the position along the X axis of the bone with.

## Ptr < AnimationCurveFloat > getCurvePosX ( int bone_index ) const

Returns the curve that animates the position along the X axis of the specified bone.
### Arguments

- *int* **bone_index** - Number of the bone.

### Return value

Copy of the curve, or NULL (null in C#) if the bone has none.
## void setCurvePosY ( int bone_index , const Ptr < AnimationCurveFloat > & in_curve )

Sets the curve that animates the position along the Y axis of the specified bone.
### Arguments

- *int* **bone_index** - Number of the bone.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_cpp.md)> &* **in_curve** - Curve to animate the position along the Y axis of the bone with.

## Ptr < AnimationCurveFloat > getCurvePosY ( int bone_index ) const

Returns the curve that animates the position along the Y axis of the specified bone.
### Arguments

- *int* **bone_index** - Number of the bone.

### Return value

Copy of the curve, or NULL (null in C#) if the bone has none.
## void setCurvePosZ ( int bone_index , const Ptr < AnimationCurveFloat > & in_curve )

Sets the curve that animates the position along the Z axis of the specified bone.
### Arguments

- *int* **bone_index** - Number of the bone.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_cpp.md)> &* **in_curve** - Curve to animate the position along the Z axis of the bone with.

## Ptr < AnimationCurveFloat > getCurvePosZ ( int bone_index ) const

Returns the curve that animates the position along the Z axis of the specified bone.
### Arguments

- *int* **bone_index** - Number of the bone.

### Return value

Copy of the curve, or NULL (null in C#) if the bone has none.
## void setCurveRot ( int bone_index , const Ptr < AnimationCurveQuat > & in_curve )

Sets the curve that animates the rotation of the specified bone.
### Arguments

- *int* **bone_index** - Number of the bone.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveQuat](../../../../api/library/animations/timeline/class.animationcurvequat_cpp.md)> &* **in_curve** - Curve to animate the rotation of the bone with.

## Ptr < AnimationCurveQuat > getCurveRot ( int bone_index ) const

Returns the curve that animates the rotation of the specified bone.
### Arguments

- *int* **bone_index** - Number of the bone.

### Return value

Copy of the curve, or NULL (null in C#) if the bone has none.
## void setCurveScaleX ( int bone_index , const Ptr < AnimationCurveFloat > & in_curve )

Sets the curve that animates the scale along the X axis of the specified bone.
### Arguments

- *int* **bone_index** - Number of the bone.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_cpp.md)> &* **in_curve** - Curve to animate the scale along the X axis of the bone with.

## Ptr < AnimationCurveFloat > getCurveScaleX ( int bone_index ) const

Returns the curve that animates the scale along the X axis of the specified bone.
### Arguments

- *int* **bone_index** - Number of the bone.

### Return value

Copy of the curve, or NULL (null in C#) if the bone has none.
## void setCurveScaleY ( int bone_index , const Ptr < AnimationCurveFloat > & in_curve )

Sets the curve that animates the scale along the Y axis of the specified bone.
### Arguments

- *int* **bone_index** - Number of the bone.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_cpp.md)> &* **in_curve** - Curve to animate the scale along the Y axis of the bone with.

## Ptr < AnimationCurveFloat > getCurveScaleY ( int bone_index ) const

Returns the curve that animates the scale along the Y axis of the specified bone.
### Arguments

- *int* **bone_index** - Number of the bone.

### Return value

Copy of the curve, or NULL (null in C#) if the bone has none.
## void setCurveScaleZ ( int bone_index , const Ptr < AnimationCurveFloat > & in_curve )

Sets the curve that animates the scale along the Z axis of the specified bone.
### Arguments

- *int* **bone_index** - Number of the bone.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_cpp.md)> &* **in_curve** - Curve to animate the scale along the Z axis of the bone with.

## Ptr < AnimationCurveFloat > getCurveScaleZ ( int bone_index ) const

Returns the curve that animates the scale along the Z axis of the specified bone.
### Arguments

- *int* **bone_index** - Number of the bone.

### Return value

Copy of the curve, or NULL (null in C#) if the bone has none.
