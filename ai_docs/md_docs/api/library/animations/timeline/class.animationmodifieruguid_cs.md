# Unigine::AnimationModifierUGUID Class (CS)

**Inherits from:** AnimationModifier


## AnimationModifierUGUID Class

### Properties

## 🔒︎ UGUID DefaultValue

The default value of all modifier elements.
## AnimationCurveUGUID Curve

The curve storing the values used by the modifier.
### Members

---

## AnimationModifierUGUID ( AnimParams.PARAM param )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be animated by the modifier.

## AnimationModifierUGUID ( AnimParams.PARAM param , int param_index )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be animated by the modifier.
- *int* **param_index** - Index of the parameter.

## AnimationModifierUGUID ( AnimParams.PARAM param , string param_name )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be animated by the modifier.
- *string* **param_name** - Name of the parameter.

## AnimationModifierUGUID ( string param )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *string* **param** - Parameter to be animated by the modifier.

## AnimationModifierUGUID ( string param , int param_index )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *string* **param** - Parameter to be animated by the modifier.
- *int* **param_index** - Index of the parameter.

## AnimationModifierUGUID ( string param , string param_name )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *string* **param** - Parameter to be animated by the modifier.
- *string* **param_name** - Name of the parameter.

## void Copy ( AnimationModifierUGUID modifier )

Copies all data from the specified source animation modifier.
### Arguments

- *[AnimationModifierUGUID](../../../../api/library/animations/timeline/class.animationmodifieruguid_cs.md)* **modifier** - Source animation modifier.

## UGUID GetValueByTime ( float time )

Returns the value of the modifier at the specified time.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.

### Return value

The modifier value at the specified time.
## UGUID GetValueByNormalizedTime ( float normalized_time )

Returns the normalized value of the modifier at the specified time.
### Arguments

- *float* **normalized_time** - The normalized time value.

### Return value

The modifier value at the specified time.
## void AddValue ( float time , UGUID value )

Adds the value to the modifier at the specified time.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.
- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **value** - The modifier value at the specified time.
