# Unigine::AnimationModifierVec3 Class (CS)

**Inherits from:** AnimationModifier


## AnimationModifierVec3 Class

### Properties

## 🔒︎ vec3 DefaultValue

The default value of all modifier elements.
## AnimationCurveScalar CurveX

The curve storing the values used by the modifier for the X axis.
## AnimationCurveScalar CurveY

The curve storing the values used by the modifier for the Y axis.
## AnimationCurveScalar CurveZ

The curve storing the values used by the modifier for the Z axis.
## 🔒︎ bool IsUniformTime

The value showing if the modifier values are changed uniformly along the timeline.
### Members

---

## AnimationModifierVec3 ( AnimParams.PARAM param )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be animated by the modifier.

## AnimationModifierVec3 ( AnimParams.PARAM param , int param_index )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be animated by the modifier.
- *int* **param_index** - Index of the parameter.

## AnimationModifierVec3 ( AnimParams.PARAM param , string param_name )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be animated by the modifier.
- *string* **param_name** - Name of the parameter.

## AnimationModifierVec3 ( string param )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *string* **param** - Parameter to be animated by the modifier.

## AnimationModifierVec3 ( string param , int param_index )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *string* **param** - Parameter to be animated by the modifier.
- *int* **param_index** - Index of the parameter.

## AnimationModifierVec3 ( string param , string param_name )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *string* **param** - Parameter to be animated by the modifier.
- *string* **param_name** - Name of the parameter.

## void Copy ( AnimationModifierVec3 modifier )

Copies all data from the specified source animation modifier.
### Arguments

- *[AnimationModifierVec3](../../../../api/library/animations/timeline/class.animationmodifiervec3_cs.md)* **modifier** - Source animation modifier.

## vec3 GetValueByTime ( float time )

Returns the value of the modifier at the specified time.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.

### Return value

The modifier value at the specified time.
## vec3 GetValueByNormalizedTime ( float normalized_time )

Returns the normalized value of the modifier at the specified time.
### Arguments

- *float* **normalized_time** - The normalized time value.

### Return value

The modifier value at the specified time.
## void AddValue ( float time , vec3 value , AnimationCurve.KEY_TYPE type = Enum.AnimationCurve.KEY_TYPE.LINEAR )

Adds the value to the modifier at the specified time.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.
- *vec3* **value** - The modifier value at the specified time.
- *[AnimationCurve.KEY_TYPE](../../../../api/library/animations/timeline/class.animationcurve_cs.md#KEY_TYPE)* **type** - Interpolation type set for the key, one of the [KEY_TYPE](../../../../api/library/animations/timeline/class.animationcurve_cs.md#KEY_TYPE) values.

## void UpdateUniformTime ( bool enabled , bool force_update = false )

Changes the value that defines if the modifier values are changed uniformly along the timeline. Enabling the uniform time allows avoiding such cases as speeding up or slowing down due to the curve shape.
### Arguments

- *bool* **enabled** - The current value.
- *bool* **force_update** - The target value.
