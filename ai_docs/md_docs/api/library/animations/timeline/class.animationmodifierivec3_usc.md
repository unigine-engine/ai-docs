# Unigine::AnimationModifierIVec3 Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** AnimationModifier


## AnimationModifierIVec3 Class

### Members

## void setCurveX ( AnimationCurveInt x )

Sets a new curve storing the values used by the modifier for the X axis.
### Arguments

- *[AnimationCurveInt](../../../../api/library/animations/timeline/class.animationcurveint_usc.md)* **x** - The curve storing the values used by the modifier for the X axis.

## AnimationCurveInt getCurveX () const

Returns the current curve storing the values used by the modifier for the X axis.
### Return value

Current curve storing the values used by the modifier for the X axis.
## void setCurveY ( AnimationCurveInt y )

Sets a new curve storing the values used by the modifier for the Y axis.
### Arguments

- *[AnimationCurveInt](../../../../api/library/animations/timeline/class.animationcurveint_usc.md)* **y** - The curve storing the values used by the modifier for the Y axis.

## AnimationCurveInt getCurveY () const

Returns the current curve storing the values used by the modifier for the Y axis.
### Return value

Current curve storing the values used by the modifier for the Y axis.
## void setCurveZ ( AnimationCurveInt z )

Sets a new curve storing the values used by the modifier for the Z axis.
### Arguments

- *[AnimationCurveInt](../../../../api/library/animations/timeline/class.animationcurveint_usc.md)* **z** - The curve storing the values used by the modifier for the Z axis.

## AnimationCurveInt getCurveZ () const

Returns the current curve storing the values used by the modifier for the Z axis.
### Return value

Current curve storing the values used by the modifier for the Z axis.
## ivec3 getDefaultValue () const

Returns the current default value of all modifier elements.
### Return value

Current default value of all modifier elements.
---

## AnimationModifierIVec3 ( int param )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *int* **param** - Parameter to be animated by the modifier.

## AnimationModifierIVec3 ( int param , int param_index )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *int* **param** - Parameter to be animated by the modifier.
- *int* **param_index** - Index of the parameter.

## AnimationModifierIVec3 ( int param , string param_name )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *int* **param** - Parameter to be animated by the modifier.
- *string* **param_name** - Name of the parameter.

## AnimationModifierIVec3 ( string param )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *string* **param** - Parameter to be animated by the modifier.

## AnimationModifierIVec3 ( string param , int param_index )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *string* **param** - Parameter to be animated by the modifier.
- *int* **param_index** - Index of the parameter.

## AnimationModifierIVec3 ( string param , string param_name )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *string* **param** - Parameter to be animated by the modifier.
- *string* **param_name** - Name of the parameter.

## void copy ( AnimationModifierIVec3 modifier )

Copies all data from the specified source animation modifier.
### Arguments

- *[AnimationModifierIVec3](../../../../api/library/animations/timeline/class.animationmodifierivec3_usc.md)* **modifier** - Source animation modifier.

## ivec3 getValueByTime ( float time )

Returns the value of the modifier at the specified time.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.

### Return value

The modifier value at the specified time.
## ivec3 getValueByNormalizedTime ( float normalized_time )

Returns the normalized value of the modifier at the specified time.
### Arguments

- *float* **normalized_time** - The normalized time value.

### Return value

The modifier value at the specified time.
## void addValue ( float time , ivec3 value , int type = Enum.AnimationCurve.KEY_TYPE.LINEAR )

Adds the value to the modifier at the specified time.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.
- *ivec3* **value** - The modifier value at the specified time.
- *int* **type** - Interpolation type set for the key, one of the [ANIMATION_CURVE_KEY_TYPE_*](../../../../api/library/animations/timeline/class.animationcurve_usc.md#KEY_TYPE_CONSTANT) values.
