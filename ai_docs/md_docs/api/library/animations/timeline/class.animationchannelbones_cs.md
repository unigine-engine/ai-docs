# Unigine::AnimationChannelBones Class (CS)

**Inherits from:** AnimationChannel


This channel animates the bones of a skeleton directly, holding a curve per bone for position, rotation and scale. It is what an animation baked from a source clip becomes when it is brought into a [sequence](../../../../api/library/animations/timeline/class.animationsequence_cs.md) as plain keys.


Unlike the channels that drive a single parameter, this one carries a whole pose, so its keys are read and written as a list of transformation matrices, one per bone.


## AnimationChannelBones Class

### Properties

## int NumBones

The number of bones animated by the channel. Each bone keeps curves of its own for position, rotation and scale.
### Members

---

## AnimationChannelBones ( )

Constructor. Creates an empty channel.
## void AssignFrom ( AnimationChannelBones channel )

Copies the content of the specified channel into this one.
### Arguments

- *[AnimationChannelBones](../../../../api/library/animations/timeline/class.animationchannelbones_cs.md)* **channel** - Source channel to copy the content from.

## int GetValueByTime ( float time , mat4[] OUT_transforms )

Collects the transformations of all bones at the given moment and puts them to the **transforms** buffer.
### Arguments

- *float* **time** - Moment to be sampled, in seconds.
- *mat4[]* **OUT_transforms** - Output buffer for the transformation matrices of the bones. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of matrices put to the buffer.
## void AddValue ( float time , mat4[] OUT_transforms )

Adds a key holding the transformations of all bones at once.
### Arguments

- *float* **time** - Moment the key is to sit at, in seconds.
- *mat4[]* **OUT_transforms** - Transformation matrices of the bones. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void SetCurvePosX ( int bone_index , AnimationCurveFloat in_curve )

Sets the curve that animates the position along the X axis of the specified bone.
### Arguments

- *int* **bone_index** - Number of the bone.
- *[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_cs.md)* **in_curve** - Curve to animate the position along the X axis of the bone with.

## AnimationCurveFloat GetCurvePosX ( int bone_index )

Returns the curve that animates the position along the X axis of the specified bone.
### Arguments

- *int* **bone_index** - Number of the bone.

### Return value

Copy of the curve, or NULL (null in C#) if the bone has none.
## void SetCurvePosY ( int bone_index , AnimationCurveFloat in_curve )

Sets the curve that animates the position along the Y axis of the specified bone.
### Arguments

- *int* **bone_index** - Number of the bone.
- *[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_cs.md)* **in_curve** - Curve to animate the position along the Y axis of the bone with.

## AnimationCurveFloat GetCurvePosY ( int bone_index )

Returns the curve that animates the position along the Y axis of the specified bone.
### Arguments

- *int* **bone_index** - Number of the bone.

### Return value

Copy of the curve, or NULL (null in C#) if the bone has none.
## void SetCurvePosZ ( int bone_index , AnimationCurveFloat in_curve )

Sets the curve that animates the position along the Z axis of the specified bone.
### Arguments

- *int* **bone_index** - Number of the bone.
- *[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_cs.md)* **in_curve** - Curve to animate the position along the Z axis of the bone with.

## AnimationCurveFloat GetCurvePosZ ( int bone_index )

Returns the curve that animates the position along the Z axis of the specified bone.
### Arguments

- *int* **bone_index** - Number of the bone.

### Return value

Copy of the curve, or NULL (null in C#) if the bone has none.
## void SetCurveRot ( int bone_index , AnimationCurveQuat in_curve )

Sets the curve that animates the rotation of the specified bone.
### Arguments

- *int* **bone_index** - Number of the bone.
- *[AnimationCurveQuat](../../../../api/library/animations/timeline/class.animationcurvequat_cs.md)* **in_curve** - Curve to animate the rotation of the bone with.

## AnimationCurveQuat GetCurveRot ( int bone_index )

Returns the curve that animates the rotation of the specified bone.
### Arguments

- *int* **bone_index** - Number of the bone.

### Return value

Copy of the curve, or NULL (null in C#) if the bone has none.
## void SetCurveScaleX ( int bone_index , AnimationCurveFloat in_curve )

Sets the curve that animates the scale along the X axis of the specified bone.
### Arguments

- *int* **bone_index** - Number of the bone.
- *[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_cs.md)* **in_curve** - Curve to animate the scale along the X axis of the bone with.

## AnimationCurveFloat GetCurveScaleX ( int bone_index )

Returns the curve that animates the scale along the X axis of the specified bone.
### Arguments

- *int* **bone_index** - Number of the bone.

### Return value

Copy of the curve, or NULL (null in C#) if the bone has none.
## void SetCurveScaleY ( int bone_index , AnimationCurveFloat in_curve )

Sets the curve that animates the scale along the Y axis of the specified bone.
### Arguments

- *int* **bone_index** - Number of the bone.
- *[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_cs.md)* **in_curve** - Curve to animate the scale along the Y axis of the bone with.

## AnimationCurveFloat GetCurveScaleY ( int bone_index )

Returns the curve that animates the scale along the Y axis of the specified bone.
### Arguments

- *int* **bone_index** - Number of the bone.

### Return value

Copy of the curve, or NULL (null in C#) if the bone has none.
## void SetCurveScaleZ ( int bone_index , AnimationCurveFloat in_curve )

Sets the curve that animates the scale along the Z axis of the specified bone.
### Arguments

- *int* **bone_index** - Number of the bone.
- *[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_cs.md)* **in_curve** - Curve to animate the scale along the Z axis of the bone with.

## AnimationCurveFloat GetCurveScaleZ ( int bone_index )

Returns the curve that animates the scale along the Z axis of the specified bone.
### Arguments

- *int* **bone_index** - Number of the bone.

### Return value

Copy of the curve, or NULL (null in C#) if the bone has none.
