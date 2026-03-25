# Unigine::AnimationModifierString Class (CPP)

**Header:** #include <UnigineAnimation.h>

**Inherits from:** AnimationModifier


## AnimationModifierString Class

### Members

## const char * getDefaultValue () const

Returns the current default value of all modifier elements.
### Return value

Current default value of all modifier elements.
## void setCurve ( const Ptr < AnimationCurveString >& curve )

Sets a new curve storing the values used by the modifier.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveString](../../../../api/library/animations/timeline/class.animationcurvestring_cpp.md)>&* **curve** - The curve storing the values used by the modifier.

## Ptr < AnimationCurveString > getCurve () const

Returns the current curve storing the values used by the modifier.
### Return value

Current curve storing the values used by the modifier.
---

## AnimationModifierString ( AnimParams::PARAM param )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be animated by the modifier.

## AnimationModifierString ( AnimParams::PARAM param , int param_index )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be animated by the modifier.
- *int* **param_index** - Index of the parameter.

## AnimationModifierString ( AnimParams::PARAM param , const char * param_name )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be animated by the modifier.
- *const char ** **param_name** - Name of the parameter.

## AnimationModifierString ( const char * param )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *const char ** **param** - Parameter to be animated by the modifier.

## AnimationModifierString ( const char * param , int param_index )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *const char ** **param** - Parameter to be animated by the modifier.
- *int* **param_index** - Index of the parameter.

## AnimationModifierString ( const char * param , const char * param_name )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *const char ** **param** - Parameter to be animated by the modifier.
- *const char ** **param_name** - Name of the parameter.

## void copy ( const Ptr < AnimationModifierString > & modifier )

Copies all data from the specified source animation modifier.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationModifierString](../../../../api/library/animations/timeline/class.animationmodifierstring_cpp.md)> &* **modifier** - Source animation modifier.

## String getValueByTime ( float time )

Returns the value of the modifier at the specified time.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.

### Return value

The modifier value at the specified time.
## String getValueByNormalizedTime ( float normalized_time )

Returns the normalized value of the modifier at the specified time.
### Arguments

- *float* **normalized_time** - The normalized time value.

### Return value

The modifier value at the specified time.
## void addValue ( float time , const char * value )

Adds the value to the modifier at the specified time.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.
- *const char ** **value** - The modifier value at the specified time.
