# Unigine::AnimationModifierIVec4 Class (CPP)

**Header:** #include <UnigineAnimation.h>

**Inherits from:** AnimationModifier


## AnimationModifierIVec4 Class

### Members

## Math:: ivec4 getDefaultValue () const

Returns the current default value of all modifier elements.
### Return value

Current default value of all modifier elements.
## void setCurveX ( const Ptr < AnimationCurveInt >& x )

Sets a new curve storing the values used by the modifier for the X axis.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveInt](../../../../api/library/animations/timeline/class.animationcurveint_cpp.md)>&* **x** - The curve storing the values used by the modifier for the X axis.

## Ptr < AnimationCurveInt > getCurveX () const

Returns the current curve storing the values used by the modifier for the X axis.
### Return value

Current curve storing the values used by the modifier for the X axis.
## void setCurveY ( const Ptr < AnimationCurveInt >& y )

Sets a new curve storing the values used by the modifier for the Y axis.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveInt](../../../../api/library/animations/timeline/class.animationcurveint_cpp.md)>&* **y** - The curve storing the values used by the modifier for the Y axis.

## Ptr < AnimationCurveInt > getCurveY () const

Returns the current curve storing the values used by the modifier for the Y axis.
### Return value

Current curve storing the values used by the modifier for the Y axis.
## void setCurveZ ( const Ptr < AnimationCurveInt >& z )

Sets a new curve storing the values used by the modifier for the Z axis.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveInt](../../../../api/library/animations/timeline/class.animationcurveint_cpp.md)>&* **z** - The curve storing the values used by the modifier for the Z axis.

## Ptr < AnimationCurveInt > getCurveZ () const

Returns the current curve storing the values used by the modifier for the Z axis.
### Return value

Current curve storing the values used by the modifier for the Z axis.
## void setCurveW ( const Ptr < AnimationCurveInt >& w )

Sets a new curve storing the values used by the modifier for the W axis.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveInt](../../../../api/library/animations/timeline/class.animationcurveint_cpp.md)>&* **w** - The curve storing the values used by the modifier for the W axis.

## Ptr < AnimationCurveInt > getCurveW () const

Returns the current curve storing the values used by the modifier for the W axis.
### Return value

Current curve storing the values used by the modifier for the W axis.
---

## AnimationModifierIVec4 ( AnimParams::PARAM param )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be animated by the modifier.

## AnimationModifierIVec4 ( AnimParams::PARAM param , int param_index )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be animated by the modifier.
- *int* **param_index** - Index of the parameter.

## AnimationModifierIVec4 ( AnimParams::PARAM param , const char * param_name )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be animated by the modifier.
- *const char ** **param_name** - Name of the parameter.

## AnimationModifierIVec4 ( const char * param )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *const char ** **param** - Parameter to be animated by the modifier.

## AnimationModifierIVec4 ( const char * param , int param_index )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *const char ** **param** - Parameter to be animated by the modifier.
- *int* **param_index** - Index of the parameter.

## AnimationModifierIVec4 ( const char * param , const char * param_name )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *const char ** **param** - Parameter to be animated by the modifier.
- *const char ** **param_name** - Name of the parameter.

## void copy ( const Ptr < AnimationModifierIVec4 > & modifier )

Copies all data from the specified source animation modifier.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationModifierIVec4](../../../../api/library/animations/timeline/class.animationmodifierivec4_cpp.md)> &* **modifier** - Source animation modifier.

## Math:: ivec4 getValueByTime ( float time )

Returns the value of the modifier at the specified time.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.

### Return value

The modifier value at the specified time.
## Math:: ivec4 getValueByNormalizedTime ( float normalized_time )

Returns the normalized value of the modifier at the specified time.
### Arguments

- *float* **normalized_time** - The normalized time value.

### Return value

The modifier value at the specified time.
## void addValue ( float time , const Math:: ivec4 & value , AnimationCurve::KEY_TYPE type = Enum.AnimationCurve.KEY_TYPE.LINEAR )

Adds the value to the modifier at the specified time.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.
- *const  Math::[ivec4](../../../../api/library/math/class.ivec4_cpp.md) &* **value** - The modifier value at the specified time.
- *[AnimationCurve::KEY_TYPE](../../../../api/library/animations/timeline/class.animationcurve_cpp.md#KEY_TYPE)* **type** - Interpolation type set for the key, one of the [KEY_TYPE_*](../../../../api/library/animations/timeline/class.animationcurve_cpp.md#KEY_TYPE_CONSTANT) values.
