# Unigine::AnimationChannelVec4 Class (CPP)

**Header:** #include <UnigineAnimation.h>

**Inherits from:** AnimationChannel


This channel animates a four-component scalar vector over time. It is one row of a [sequence](../../../../api/library/animations/timeline/class.animationsequence_cpp.md), while everything the channels share, such as the animated parameter, the binding and the clips, comes from the [AnimationChannel](../../../../api/library/animations/timeline/class.animationchannel_cpp.md) base class.


## AnimationChannelVec4 Class

### Members

## Math:: Vec4 getDefaultValue () const

Returns the current value the channel falls back to where it has no keys of its own.
### Return value

Current value the channel falls back to
## void setCurveX ( const Ptr < AnimationCurveScalar >& x )

Sets a new curve of the X component.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveScalar](../../../../api/library/animations/timeline/class.animationcurvescalar_cpp.md)>&* **x** - The curve of the X component

## Ptr < AnimationCurveScalar > getCurveX () const

Returns the current curve of the X component.
### Return value

Current curve of the X component
## void setCurveY ( const Ptr < AnimationCurveScalar >& y )

Sets a new curve of the Y component.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveScalar](../../../../api/library/animations/timeline/class.animationcurvescalar_cpp.md)>&* **y** - The curve of the Y component

## Ptr < AnimationCurveScalar > getCurveY () const

Returns the current curve of the Y component.
### Return value

Current curve of the Y component
## void setCurveZ ( const Ptr < AnimationCurveScalar >& z )

Sets a new curve of the Z component.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveScalar](../../../../api/library/animations/timeline/class.animationcurvescalar_cpp.md)>&* **z** - The curve of the Z component

## Ptr < AnimationCurveScalar > getCurveZ () const

Returns the current curve of the Z component.
### Return value

Current curve of the Z component
## void setCurveW ( const Ptr < AnimationCurveScalar >& w )

Sets a new curve of the W component.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveScalar](../../../../api/library/animations/timeline/class.animationcurvescalar_cpp.md)>&* **w** - The curve of the W component

## Ptr < AnimationCurveScalar > getCurveW () const

Returns the current curve of the W component.
### Return value

Current curve of the W component
---

## AnimationChannelVec4 ( AnimParams::PARAM param )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be animated by the channel. Identifiers are looked up through the [Animations](../../../../api/library/animations/class.animations_cpp.md) class rather than written out by hand.

## AnimationChannelVec4 ( AnimParams::PARAM param , int param_index )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be animated by the channel. Identifiers are looked up through the [Animations](../../../../api/library/animations/class.animations_cpp.md) class rather than written out by hand.
- *int* **param_index** - Slot of the parameter for parameters that come as an array, such as a surface or a bone.

## AnimationChannelVec4 ( AnimParams::PARAM param , const char * param_name )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be animated by the channel. Identifiers are looked up through the [Animations](../../../../api/library/animations/class.animations_cpp.md) class rather than written out by hand.
- *const char ** **param_name** - Name that addresses the parameter when a number is not enough, such as the name of a property parameter or of a surface.

## AnimationChannelVec4 ( const char * param )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *const char ** **param** - Name of the parameter to be animated by the channel.

## AnimationChannelVec4 ( const char * param , int param_index )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *const char ** **param** - Name of the parameter to be animated by the channel.
- *int* **param_index** - Slot of the parameter for parameters that come as an array, such as a surface or a bone.

## AnimationChannelVec4 ( const char * param , const char * param_name )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *const char ** **param** - Name of the parameter to be animated by the channel.
- *const char ** **param_name** - Name that addresses the parameter when a number is not enough, such as the name of a property parameter or of a surface.

## void assignFrom ( const Ptr < AnimationChannelVec4 > & channel )

Copies the content of the specified channel into this one.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationChannelVec4](../../../../api/library/animations/timeline/class.animationchannelvec4_cpp.md)> &* **channel** - Source channel to copy the content from.

## Math:: Vec4 getValueByTime ( float time )

Returns the value the channel holds at the given moment.
### Arguments

- *float* **time** - Moment to be sampled, in seconds.

### Return value

Value the channel holds at the specified moment.
## Math:: Vec4 getValueByNormalizedTime ( float normalized_time )

Returns the value the channel holds at the given moment, addressed as a share of its time span rather than in seconds.
### Arguments

- *float* **normalized_time** - Moment to be sampled, given as a share of the channel time span in the [0.0f, 1.0f] range.

### Return value

Value the channel holds at the specified moment.
## void addValue ( float time , const Math:: Vec4 & value , AnimationCurve::KEY_TYPE type = AnimationCurve::KEY_TYPE_LINEAR )

Adds a key holding the specified value.
### Arguments

- *float* **time** - Moment the key is to sit at, in seconds.
- *const  Math::[Vec4](../../../../api/library/math/class.vec4_cpp.md) &* **value** - Value to be held by the key.
- *[AnimationCurve::KEY_TYPE](../../../../api/library/animations/timeline/class.animationcurve_cpp.md#KEY_TYPE)* **type** - Interpolation type of the key. The default value is [KEY_TYPE_LINEAR](../../../../api/library/animations/timeline/class.animationcurve_cpp.md#KEY_TYPE_LINEAR).
