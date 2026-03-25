# Unigine::AnimationModifierInt Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** AnimationModifier


## AnimationModifierInt Class

### Members

## void setCurve ( AnimationCurveInt curve )

Sets a new curve storing the values used by the modifier.
### Arguments

- *[AnimationCurveInt](../../../../api/library/animations/timeline/class.animationcurveint_usc.md)* **curve** - The curve storing the values used by the modifier.

## AnimationCurveInt getCurve () const

Returns the current curve storing the values used by the modifier.
### Return value

Current curve storing the values used by the modifier.
## getDefaultValue () const

Returns the current default value of all modifier elements.
### Return value

Current default value of all modifier elements.
---

## AnimationModifierInt ( int param )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *int* **param** - Parameter to be animated by the modifier.

## AnimationModifierInt ( int param , int param_index )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *int* **param** - Parameter to be animated by the modifier.
- *int* **param_index** - Index of the parameter.

## AnimationModifierInt ( int param , string param_name )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *int* **param** - Parameter to be animated by the modifier.
- *string* **param_name** - Name of the parameter.

## AnimationModifierInt ( string param )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *string* **param** - Parameter to be animated by the modifier.

## AnimationModifierInt ( string param , int param_index )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *string* **param** - Parameter to be animated by the modifier.
- *int* **param_index** - Index of the parameter.

## AnimationModifierInt ( string param , string param_name )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *string* **param** - Parameter to be animated by the modifier.
- *string* **param_name** - Name of the parameter.

## void copy ( AnimationModifierInt modifier )

Copies all data from the specified source animation modifier.
### Arguments

- *[AnimationModifierInt](../../../../api/library/animations/timeline/class.animationmodifierint_usc.md)* **modifier** - Source animation modifier.

## int getValueByTime ( float time )

Returns the value of the modifier at the specified time.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.

### Return value

The modifier value at the specified time.
## int getValueByNormalizedTime ( float normalized_time )

Returns the normalized value of the modifier at the specified time.
### Arguments

- *float* **normalized_time** - The normalized time value.

### Return value

The modifier value at the specified time.
## void addValue ( float time , int value , int type = Enum.AnimationCurve.KEY_TYPE.LINEAR )

Adds the value to the modifier at the specified time.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.
- *int* **value** - The modifier value at the specified time.
- *int* **type** - Interpolation type set for the key, one of the [ANIMATION_CURVE_KEY_TYPE_*](../../../../api/library/animations/timeline/class.animationcurve_usc.md#KEY_TYPE_CONSTANT) values.
