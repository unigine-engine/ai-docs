# Unigine::AnimationModifierBool Class (CS)

**Inherits from:** AnimationModifier


## AnimationModifierBool Class

### Properties

## AnimationCurveBool Curve

The curve storing the values used by the modifier.
### Members

---

## AnimationModifierBool ( AnimParams.PARAM param )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be animated by the modifier.

## AnimationModifierBool ( AnimParams.PARAM param , int param_index )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be animated by the modifier.
- *int* **param_index** - Index of the parameter.

## AnimationModifierBool ( AnimParams.PARAM param , string param_name )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be animated by the modifier.
- *string* **param_name** - Name of the parameter.

## AnimationModifierBool ( string param )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *string* **param** - Parameter to be animated by the modifier.

## AnimationModifierBool ( string param , int param_index )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *string* **param** - Parameter to be animated by the modifier.
- *int* **param_index** - Index of the parameter.

## AnimationModifierBool ( string param , string param_name )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *string* **param** - Parameter to be animated by the modifier.
- *string* **param_name** - Name of the parameter.

## void Copy ( AnimationModifierBool modifier )

Copies all data from the specified source animation modifier.
### Arguments

- *[AnimationModifierBool](../../../../api/library/animations/timeline/class.animationmodifierbool_cs.md)* **modifier** - Source animation modifier.

## bool GetValueByTime ( float time )

Returns the value of the modifier at the specified time.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.

### Return value

The modifier value at the specified time.
## bool GetValueByNormalizedTime ( float normalized_time )

Returns the normalized value of the modifier at the specified time.
### Arguments

- *float* **normalized_time** - The normalized time value.

### Return value

The modifier value at the specified time.
## void AddValue ( float time , bool value , AnimationCurve.KEY_TYPE type = Enum.AnimationCurve.KEY_TYPE.LINEAR )

Adds the value to the modifier at the specified time.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.
- *bool* **value** - The modifier value at the specified time.
- *[AnimationCurve.KEY_TYPE](../../../../api/library/animations/timeline/class.animationcurve_cs.md#KEY_TYPE)* **type** - Interpolation type set for the key, one of the [KEY_TYPE](../../../../api/library/animations/timeline/class.animationcurve_cs.md#KEY_TYPE) values.

## bool GetDefaultValue ( )

Returns the default value for all modifier elements.
### Return value

Default value for all modifier elements.
