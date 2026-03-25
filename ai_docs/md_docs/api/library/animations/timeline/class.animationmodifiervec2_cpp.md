# Unigine::AnimationModifierVec2 Class (CPP)

**Header:** #include <UnigineAnimation.h>

**Inherits from:** AnimationModifier


## AnimationModifierVec2 Class

### Members

## Math:: Vec2 getDefaultValue () const

Returns the current default value of all modifier elements.
### Return value

Current default value of all modifier elements.
## void setCurveX ( const Ptr < AnimationCurveScalar >& x )

Sets a new curve storing the values used by the modifier for the X axis.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveScalar](../../../../api/library/animations/timeline/class.animationcurvescalar_cpp.md)>&* **x** - The curve storing the values used by the modifier for the X axis.

## Ptr < AnimationCurveScalar > getCurveX () const

Returns the current curve storing the values used by the modifier for the X axis.
### Return value

Current curve storing the values used by the modifier for the X axis.
## void setCurveY ( const Ptr < AnimationCurveScalar >& y )

Sets a new curve storing the values used by the modifier for the Y axis.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveScalar](../../../../api/library/animations/timeline/class.animationcurvescalar_cpp.md)>&* **y** - The curve storing the values used by the modifier for the Y axis.

## Ptr < AnimationCurveScalar > getCurveY () const

Returns the current curve storing the values used by the modifier for the Y axis.
### Return value

Current curve storing the values used by the modifier for the Y axis.
## bool isUniformTime () const

Returns the current value showing if the modifier values are changed uniformly along the timeline.
### Return value

**true** if value showing if the modifier values are changed uniformly along the timeline. is enabled; otherwise **false**.
---

## AnimationModifierVec2 ( AnimParams::PARAM param )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be animated by the modifier.

## AnimationModifierVec2 ( AnimParams::PARAM param , int param_index )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be animated by the modifier.
- *int* **param_index** - Index of the parameter.

## AnimationModifierVec2 ( AnimParams::PARAM param , const char * param_name )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be animated by the modifier.
- *const char ** **param_name** - Name of the parameter.

## AnimationModifierVec2 ( const char * param )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *const char ** **param** - Parameter to be animated by the modifier.

## AnimationModifierVec2 ( const char * param , int param_index )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *const char ** **param** - Parameter to be animated by the modifier.
- *int* **param_index** - Index of the parameter.

## AnimationModifierVec2 ( const char * param , const char * param_name )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *const char ** **param** - Parameter to be animated by the modifier.
- *const char ** **param_name** - Name of the parameter.

## void copy ( const Ptr < AnimationModifierVec2 > & modifier )

Copies all data from the specified source animation modifier.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationModifierVec2](../../../../api/library/animations/timeline/class.animationmodifiervec2_cpp.md)> &* **modifier** - Source animation modifier.

## Math:: Vec2 getValueByTime ( float time )

Returns the value of the modifier at the specified time.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.

### Return value

The modifier value at the specified time.
## Math:: Vec2 getValueByNormalizedTime ( float normalized_time )

Returns the normalized value of the modifier at the specified time.
### Arguments

- *float* **normalized_time** - The normalized time value.

### Return value

The modifier value at the specified time.
## void addValue ( float time , const Math:: Vec2 & value , AnimationCurve::KEY_TYPE type = Enum.AnimationCurve.KEY_TYPE.LINEAR )

Adds the value to the modifier at the specified time.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.
- *const  Math::[Vec2](../../../../api/library/math/class.vec2_cpp.md) &* **value** - The modifier value at the specified time.
- *[AnimationCurve::KEY_TYPE](../../../../api/library/animations/timeline/class.animationcurve_cpp.md#KEY_TYPE)* **type** - Interpolation type set for the key, one of the [KEY_TYPE_*](../../../../api/library/animations/timeline/class.animationcurve_cpp.md#KEY_TYPE_CONSTANT) values.

## void updateUniformTime ( bool enabled , bool force_update = false )

Changes the value that defines if the modifier values are changed uniformly along the timeline. Enabling the uniform time allows avoiding such cases as speeding up or slowing down due to the curve shape.
### Arguments

- *bool* **enabled** - The current value.
- *bool* **force_update** - The target value.
