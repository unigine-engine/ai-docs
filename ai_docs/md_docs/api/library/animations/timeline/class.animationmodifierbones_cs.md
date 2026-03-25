# Unigine::AnimationModifierBones Class (CS)

**Inherits from:** AnimationModifier


This class allows animating all bones for [ObjectMeshSkinnedLegacy](../../../../api/library/objects/class.objectmeshskinnedlegacy_cs.md).


## AnimationModifierBones Class

### Properties

## int NumBones

The number of bones affected by the animation modifier.
### Members

---

## AnimationModifierBones ( )

Constructor. Creates a new animation modifier for bones.
## void Copy ( AnimationModifierBones modifier )

Copies all data from the specified source animation modifier.
### Arguments

- *[AnimationModifierBones](../../../../api/library/animations/timeline/class.animationmodifierbones_cs.md)* **modifier** - Source animation modifier.

## int GetValueByTime ( float time , mat4[] OUT_transforms )

Returns the number of bones affected by the animation modifier and saves the transformation values of the modifier at the specified time.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.
- *mat4[]* **OUT_transforms** - Transformation matrices to save the returned values. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

The number of bones affected by the animation modifier.
## void AddValue ( float time , mat4[] OUT_transforms )

Adds the transformation values to the modifier at the specified time.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.
- *mat4[]* **OUT_transforms** - Transformation matrices. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void SetCurvePosX ( int bone_index , AnimationCurveFloat in_curve )

Sets the curve storing the bone positions along the X axis.
### Arguments

- *int* **bone_index** - Index of the bone.
- *[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_cs.md)* **in_curve** - The animation curve storing the bone positions along the X axis.

## AnimationCurveFloat GetCurvePosX ( int bone_index )

Returns the curve storing the bone positions along the X axis.
### Arguments

- *int* **bone_index** - Index of the bone.

### Return value

The animation curve storing the bone positions along the X axis.
## void SetCurvePosY ( int bone_index , AnimationCurveFloat in_curve )

Sets the curve storing the bone positions along the Y axis.
### Arguments

- *int* **bone_index** - Index of the bone.
- *[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_cs.md)* **in_curve** - The animation curve storing the bone positions along the Y axis.

## AnimationCurveFloat GetCurvePosY ( int bone_index )

Returns the curve storing the bone positions along the Y axis.
### Arguments

- *int* **bone_index** - Index of the bone.

### Return value

The animation curve storing the bone positions along the Y axis.
## void SetCurvePosZ ( int bone_index , AnimationCurveFloat in_curve )

Sets the curve storing the bone positions along the Z axis.
### Arguments

- *int* **bone_index** - Index of the bone.
- *[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_cs.md)* **in_curve** - The animation curve storing the bone positions along the Z axis.

## AnimationCurveFloat GetCurvePosZ ( int bone_index )

Returns the curve storing the bone positions along the Z axis.
### Arguments

- *int* **bone_index** - Index of the bone.

### Return value

The animation curve storing the bone positions along the Z axis.
## void SetCurveRot ( int bone_index , AnimationCurveQuat in_curve )

Sets the curve storing the bone transforms.
### Arguments

- *int* **bone_index** - Index of the bone.
- *[AnimationCurveQuat](../../../../api/library/animations/timeline/class.animationcurvequat_cs.md)* **in_curve** - The animation curve storing the bone transforms.

## AnimationCurveQuat GetCurveRot ( int bone_index )

Returns the curve storing the bone transforms.
### Arguments

- *int* **bone_index** - Index of the bone.

### Return value

The animation curve storing the bone transforms.
## void SetCurveScaleX ( int bone_index , AnimationCurveFloat in_curve )

Sets the animation curve storing the bone scaling along the X axis.
### Arguments

- *int* **bone_index** - Index of the bone.
- *[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_cs.md)* **in_curve** - The animation curve storing the bone scaling along the X axis.

## AnimationCurveFloat GetCurveScaleX ( int bone_index )

Returns the animation curve storing the bone scaling along the X axis.
### Arguments

- *int* **bone_index** - Index of the bone.

### Return value

The animation curve storing the bone scaling along the X axis.
## void SetCurveScaleY ( int bone_index , AnimationCurveFloat in_curve )

Sets the animation curve storing the bone scaling along the Y axis.
### Arguments

- *int* **bone_index** - Index of the bone.
- *[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_cs.md)* **in_curve** - The animation curve storing the bone scaling along the Y axis.

## AnimationCurveFloat GetCurveScaleY ( int bone_index )

Returns the animation curve storing the bone scaling along the Y axis.
### Arguments

- *int* **bone_index** - Index of the bone.

### Return value

The animation curve storing the bone scaling along the Y axis.
## void SetCurveScaleZ ( int bone_index , AnimationCurveFloat in_curve )

Sets the animation curve storing the bone scaling along the Z axis.
### Arguments

- *int* **bone_index** - Index of the bone.
- *[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_cs.md)* **in_curve** - The animation curve storing the bone scaling along the Z axis.

## AnimationCurveFloat GetCurveScaleZ ( int bone_index )

Returns the animation curve storing the bone scaling along the Z axis.
### Arguments

- *int* **bone_index** - Index of the bone.

### Return value

The animation curve storing the bone scaling along the Z axis.
