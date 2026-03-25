# Unigine::AnimationModifierBones Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** AnimationModifier


This class allows animating all bones for [ObjectMeshSkinnedLegacy](../../../../api/library/objects/class.objectmeshskinnedlegacy_usc.md).


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
## void copy ( AnimationModifierBones modifier )

Copies all data from the specified source animation modifier.
### Arguments

- *[AnimationModifierBones](../../../../api/library/animations/timeline/class.animationmodifierbones_usc.md)* **modifier** - Source animation modifier.

## void setCurvePosX ( int bone_index , AnimationCurveFloat in_curve )

Sets the curve storing the bone positions along the X axis.
### Arguments

- *int* **bone_index** - Index of the bone.
- *[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_usc.md)* **in_curve** - The animation curve storing the bone positions along the X axis.

## AnimationCurveFloat getCurvePosX ( int bone_index )

Returns the curve storing the bone positions along the X axis.
### Arguments

- *int* **bone_index** - Index of the bone.

### Return value

The animation curve storing the bone positions along the X axis.
## void setCurvePosY ( int bone_index , AnimationCurveFloat in_curve )

Sets the curve storing the bone positions along the Y axis.
### Arguments

- *int* **bone_index** - Index of the bone.
- *[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_usc.md)* **in_curve** - The animation curve storing the bone positions along the Y axis.

## AnimationCurveFloat getCurvePosY ( int bone_index )

Returns the curve storing the bone positions along the Y axis.
### Arguments

- *int* **bone_index** - Index of the bone.

### Return value

The animation curve storing the bone positions along the Y axis.
## void setCurvePosZ ( int bone_index , AnimationCurveFloat in_curve )

Sets the curve storing the bone positions along the Z axis.
### Arguments

- *int* **bone_index** - Index of the bone.
- *[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_usc.md)* **in_curve** - The animation curve storing the bone positions along the Z axis.

## AnimationCurveFloat getCurvePosZ ( int bone_index )

Returns the curve storing the bone positions along the Z axis.
### Arguments

- *int* **bone_index** - Index of the bone.

### Return value

The animation curve storing the bone positions along the Z axis.
## void setCurveRot ( int bone_index , AnimationCurveQuat in_curve )

Sets the curve storing the bone transforms.
### Arguments

- *int* **bone_index** - Index of the bone.
- *[AnimationCurveQuat](../../../../api/library/animations/timeline/class.animationcurvequat_usc.md)* **in_curve** - The animation curve storing the bone transforms.

## AnimationCurveQuat getCurveRot ( int bone_index )

Returns the curve storing the bone transforms.
### Arguments

- *int* **bone_index** - Index of the bone.

### Return value

The animation curve storing the bone transforms.
## void setCurveScaleX ( int bone_index , AnimationCurveFloat in_curve )

Sets the animation curve storing the bone scaling along the X axis.
### Arguments

- *int* **bone_index** - Index of the bone.
- *[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_usc.md)* **in_curve** - The animation curve storing the bone scaling along the X axis.

## AnimationCurveFloat getCurveScaleX ( int bone_index )

Returns the animation curve storing the bone scaling along the X axis.
### Arguments

- *int* **bone_index** - Index of the bone.

### Return value

The animation curve storing the bone scaling along the X axis.
## void setCurveScaleY ( int bone_index , AnimationCurveFloat in_curve )

Sets the animation curve storing the bone scaling along the Y axis.
### Arguments

- *int* **bone_index** - Index of the bone.
- *[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_usc.md)* **in_curve** - The animation curve storing the bone scaling along the Y axis.

## AnimationCurveFloat getCurveScaleY ( int bone_index )

Returns the animation curve storing the bone scaling along the Y axis.
### Arguments

- *int* **bone_index** - Index of the bone.

### Return value

The animation curve storing the bone scaling along the Y axis.
## void setCurveScaleZ ( int bone_index , AnimationCurveFloat in_curve )

Sets the animation curve storing the bone scaling along the Z axis.
### Arguments

- *int* **bone_index** - Index of the bone.
- *[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_usc.md)* **in_curve** - The animation curve storing the bone scaling along the Z axis.

## AnimationCurveFloat getCurveScaleZ ( int bone_index )

Returns the animation curve storing the bone scaling along the Z axis.
### Arguments

- *int* **bone_index** - Index of the bone.

### Return value

The animation curve storing the bone scaling along the Z axis.
