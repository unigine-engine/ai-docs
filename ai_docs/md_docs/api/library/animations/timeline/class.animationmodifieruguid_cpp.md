# Unigine::AnimationModifierUGUID Class (CPP)

**Header:** #include <UnigineAnimation.h>

**Inherits from:** AnimationModifier


## AnimationModifierUGUID Class

### Members

## UGUID getDefaultValue () const

Returns the current default value of all modifier elements.
### Return value

Current default value of all modifier elements.
## void setCurve ( const Ptr < AnimationCurveUGUID >& curve )

Sets a new curve storing the values used by the modifier.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveUGUID](../../../../api/library/animations/timeline/class.animationcurveuguid_cpp.md)>&* **curve** - The curve storing the values used by the modifier.

## Ptr < AnimationCurveUGUID > getCurve () const

Returns the current curve storing the values used by the modifier.
### Return value

Current curve storing the values used by the modifier.
---

## AnimationModifierUGUID ( AnimParams::PARAM param )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be animated by the modifier.

## AnimationModifierUGUID ( AnimParams::PARAM param , int param_index )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be animated by the modifier.
- *int* **param_index** - Index of the parameter.

## AnimationModifierUGUID ( AnimParams::PARAM param , const char * param_name )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be animated by the modifier.
- *const char ** **param_name** - Name of the parameter.

## AnimationModifierUGUID ( const char * param )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *const char ** **param** - Parameter to be animated by the modifier.

## AnimationModifierUGUID ( const char * param , int param_index )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *const char ** **param** - Parameter to be animated by the modifier.
- *int* **param_index** - Index of the parameter.

## AnimationModifierUGUID ( const char * param , const char * param_name )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *const char ** **param** - Parameter to be animated by the modifier.
- *const char ** **param_name** - Name of the parameter.

## void copy ( const Ptr < AnimationModifierUGUID > & modifier )

Copies all data from the specified source animation modifier.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationModifierUGUID](../../../../api/library/animations/timeline/class.animationmodifieruguid_cpp.md)> &* **modifier** - Source animation modifier.

## UGUID getValueByTime ( float time )

Returns the value of the modifier at the specified time.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.

### Return value

The modifier value at the specified time.
## UGUID getValueByNormalizedTime ( float normalized_time )

Returns the normalized value of the modifier at the specified time.
### Arguments

- *float* **normalized_time** - The normalized time value.

### Return value

The modifier value at the specified time.
## void addValue ( float time , const UGUID & value )

Adds the value to the modifier at the specified time.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.
- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **value** - The modifier value at the specified time.
