# Unigine::AnimationModifierIVec3 Class (CS)

**Inherits from:** AnimationModifier


## AnimationModifierIVec3 Class

### Properties

## AnimationCurveInt CurveX

The curve storing the values used by the modifier for the X axis.
## AnimationCurveInt CurveY

The curve storing the values used by the modifier for the Y axis.
## AnimationCurveInt CurveZ

The curve storing the values used by the modifier for the Z axis.
## 🔒︎ ivec3 DefaultValue

The default value of all modifier elements.
### Members

---

## AnimationModifierIVec3 ( AnimParams.PARAM param )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be animated by the modifier.

## AnimationModifierIVec3 ( AnimParams.PARAM param , int param_index )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be animated by the modifier.
- *int* **param_index** - Index of the parameter.

## AnimationModifierIVec3 ( AnimParams.PARAM param , string param_name )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be animated by the modifier.
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

## void Copy ( AnimationModifierIVec3 modifier )

Copies all data from the specified source animation modifier.
### Arguments

- *[AnimationModifierIVec3](../../../../api/library/animations/timeline/class.animationmodifierivec3_cs.md)* **modifier** - Source animation modifier.

## ivec3 GetValueByTime ( float time )

Returns the value of the modifier at the specified time.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.

### Return value

The modifier value at the specified time.
## ivec3 GetValueByNormalizedTime ( float normalized_time )

Returns the normalized value of the modifier at the specified time.
### Arguments

- *float* **normalized_time** - The normalized time value.

### Return value

The modifier value at the specified time.
## void AddValue ( float time , ivec3 value , AnimationCurve.KEY_TYPE type = Enum.AnimationCurve.KEY_TYPE.LINEAR )

Adds the value to the modifier at the specified time.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.
- *ivec3* **value** - The modifier value at the specified time.
- *[AnimationCurve.KEY_TYPE](../../../../api/library/animations/timeline/class.animationcurve_cs.md#KEY_TYPE)* **type** - Interpolation type set for the key, one of the [KEY_TYPE](../../../../api/library/animations/timeline/class.animationcurve_cs.md#KEY_TYPE) values.
