# Unigine::AnimationModifierInt Class (CPP)

**Header:** #include <UnigineAnimation.h>

**Inherits from:** AnimationModifier


## AnimationModifierInt Class

### Members

## void setCurve ( const Ptr < AnimationCurveInt >& curve )

Sets a new curve storing the values used by the modifier.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveInt](../../../../api/library/animations/timeline/class.animationcurveint_cpp.md)>&* **curve** - The curve storing the values used by the modifier.

## Ptr < AnimationCurveInt > getCurve () const

Returns the current curve storing the values used by the modifier.
### Return value

Current curve storing the values used by the modifier.
## getDefaultValue () const

Returns the current default value of all modifier elements.
### Return value

Current default value of all modifier elements.
---

## AnimationModifierInt ( AnimParams::PARAM param )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be animated by the modifier.

## AnimationModifierInt ( AnimParams::PARAM param , int param_index )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be animated by the modifier.
- *int* **param_index** - Index of the parameter.

## AnimationModifierInt ( AnimParams::PARAM param , const char * param_name )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be animated by the modifier.
- *const char ** **param_name** - Name of the parameter.

## AnimationModifierInt ( const char * param )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *const char ** **param** - Parameter to be animated by the modifier.

## AnimationModifierInt ( const char * param , int param_index )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *const char ** **param** - Parameter to be animated by the modifier.
- *int* **param_index** - Index of the parameter.

## AnimationModifierInt ( const char * param , const char * param_name )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *const char ** **param** - Parameter to be animated by the modifier.
- *const char ** **param_name** - Name of the parameter.

## void copy ( const Ptr < AnimationModifierInt > & modifier )

Copies all data from the specified source animation modifier.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationModifierInt](../../../../api/library/animations/timeline/class.animationmodifierint_cpp.md)> &* **modifier** - Source animation modifier.

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
## void addValue ( float time , int value , AnimationCurve::KEY_TYPE type = Enum.AnimationCurve.KEY_TYPE.LINEAR )

Adds the value to the modifier at the specified time.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.
- *int* **value** - The modifier value at the specified time.
- *[AnimationCurve::KEY_TYPE](../../../../api/library/animations/timeline/class.animationcurve_cpp.md#KEY_TYPE)* **type** - Interpolation type set for the key, one of the [KEY_TYPE_*](../../../../api/library/animations/timeline/class.animationcurve_cpp.md#KEY_TYPE_CONSTANT) values.
