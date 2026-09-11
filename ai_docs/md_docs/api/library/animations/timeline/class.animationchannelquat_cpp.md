# Unigine::AnimationChannelQuat Class (CPP)

**Header:** #include <UnigineAnimation.h>

**Inherits from:** AnimationChannel


This channel animates an orientation over time. It is one row of a [sequence](../../../../api/library/animations/timeline/class.animationsequence_cpp.md), while everything the channels share, such as the animated parameter, the binding and the clips, comes from the [AnimationChannel](../../../../api/library/animations/timeline/class.animationchannel_cpp.md) base class.


Every mode stores the orientation as three Euler curves and only picks the way the segments between the keys are interpolated, so switching the mode remaps no key.


## AnimationChannelQuat Class

### Enums

## MODE

Way the orientation is interpolated between the keys.
| Name | Description |
|---|---|
| **MODE_QUAT** = 0 | The key quaternions are interpolated along the shortest arc between them, and the tangents of the keys act as an ease of the timing rather than of the path. |
| **MODE_ANGLES_XYZ** = 1 | Each Euler axis is interpolated on its own and the result is composed in the XYZ order. |
| **MODE_ANGLES_ZYX** = 2 | Each Euler axis is interpolated on its own and the result is composed in the ZYX order. |

### Members

## void setMode ( AnimationChannelQuat::MODE mode )

Sets a new way the orientation is interpolated between the keys. Every mode keeps the same three Euler curves, so switching between them remaps no key.
### Arguments

- *[AnimationChannelQuat::MODE](../../../../api/library/animations/timeline/class.animationchannelquat_cpp.md#MODE)* **mode** - The way the orientation is interpolated between the keys

## AnimationChannelQuat::MODE getMode () const

Returns the current way the orientation is interpolated between the keys. Every mode keeps the same three Euler curves, so switching between them remaps no key.
### Return value

Current way the orientation is interpolated between the keys
## Math:: quat getDefaultValue () const

Returns the current value the channel falls back to where it has no keys of its own.
### Return value

Current value the channel falls back to
## void setQuatCurve ( const Ptr < AnimationCurveQuat >& curve )

Sets a new curve that holds the orientation keys.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveQuat](../../../../api/library/animations/timeline/class.animationcurvequat_cpp.md)>&* **curve** - The curve that holds the orientation keys

## Ptr < AnimationCurveQuat > getQuatCurve () const

Returns the current curve that holds the orientation keys.
### Return value

Current curve that holds the orientation keys
## void setCurveX ( const Ptr < AnimationCurveFloat >& x )

Sets a new curve of the X component.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_cpp.md)>&* **x** - The curve of the X component

## Ptr < AnimationCurveFloat > getCurveX () const

Returns the current curve of the X component.
### Return value

Current curve of the X component
## void setCurveY ( const Ptr < AnimationCurveFloat >& y )

Sets a new curve of the Y component.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_cpp.md)>&* **y** - The curve of the Y component

## Ptr < AnimationCurveFloat > getCurveY () const

Returns the current curve of the Y component.
### Return value

Current curve of the Y component
## void setCurveZ ( const Ptr < AnimationCurveFloat >& z )

Sets a new curve of the Z component.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_cpp.md)>&* **z** - The curve of the Z component

## Ptr < AnimationCurveFloat > getCurveZ () const

Returns the current curve of the Z component.
### Return value

Current curve of the Z component
---

## AnimationChannelQuat ( AnimationChannelQuat::MODE mode , AnimParams::PARAM param )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *[AnimationChannelQuat::MODE](../../../../api/library/animations/timeline/class.animationchannelquat_cpp.md#MODE)* **mode** - Way the orientation is interpolated between the keys.
- *AnimParams::PARAM* **param** - Parameter to be animated by the channel. Identifiers are looked up through the [Animations](../../../../api/library/animations/class.animations_cpp.md) class rather than written out by hand.

## AnimationChannelQuat ( AnimationChannelQuat::MODE mode , AnimParams::PARAM param , int param_index )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *[AnimationChannelQuat::MODE](../../../../api/library/animations/timeline/class.animationchannelquat_cpp.md#MODE)* **mode** - Way the orientation is interpolated between the keys.
- *AnimParams::PARAM* **param** - Parameter to be animated by the channel. Identifiers are looked up through the [Animations](../../../../api/library/animations/class.animations_cpp.md) class rather than written out by hand.
- *int* **param_index** - Slot of the parameter for parameters that come as an array, such as a surface or a bone.

## AnimationChannelQuat ( AnimationChannelQuat::MODE mode , AnimParams::PARAM param , const char * param_name )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *[AnimationChannelQuat::MODE](../../../../api/library/animations/timeline/class.animationchannelquat_cpp.md#MODE)* **mode** - Way the orientation is interpolated between the keys.
- *AnimParams::PARAM* **param** - Parameter to be animated by the channel. Identifiers are looked up through the [Animations](../../../../api/library/animations/class.animations_cpp.md) class rather than written out by hand.
- *const char ** **param_name** - Name that addresses the parameter when a number is not enough, such as the name of a property parameter or of a surface.

## AnimationChannelQuat ( AnimationChannelQuat::MODE mode , const char * param )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *[AnimationChannelQuat::MODE](../../../../api/library/animations/timeline/class.animationchannelquat_cpp.md#MODE)* **mode** - Way the orientation is interpolated between the keys.
- *const char ** **param** - Name of the parameter to be animated by the channel.

## AnimationChannelQuat ( AnimationChannelQuat::MODE mode , const char * param , int param_index )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *[AnimationChannelQuat::MODE](../../../../api/library/animations/timeline/class.animationchannelquat_cpp.md#MODE)* **mode** - Way the orientation is interpolated between the keys.
- *const char ** **param** - Name of the parameter to be animated by the channel.
- *int* **param_index** - Slot of the parameter for parameters that come as an array, such as a surface or a bone.

## AnimationChannelQuat ( AnimationChannelQuat::MODE mode , const char * param , const char * param_name )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *[AnimationChannelQuat::MODE](../../../../api/library/animations/timeline/class.animationchannelquat_cpp.md#MODE)* **mode** - Way the orientation is interpolated between the keys.
- *const char ** **param** - Name of the parameter to be animated by the channel.
- *const char ** **param_name** - Name that addresses the parameter when a number is not enough, such as the name of a property parameter or of a surface.

## void assignFrom ( const Ptr < AnimationChannelQuat > & channel )

Copies the content of the specified channel into this one.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationChannelQuat](../../../../api/library/animations/timeline/class.animationchannelquat_cpp.md)> &* **channel** - Source channel to copy the content from.

## Math:: quat getValueByTime ( float time )

Returns the value the channel holds at the given moment.
### Arguments

- *float* **time** - Moment to be sampled, in seconds.

### Return value

Value the channel holds at the specified moment.
## Math:: quat getValueByNormalizedTime ( float normalized_time )

Returns the value the channel holds at the given moment, addressed as a share of its time span rather than in seconds.
### Arguments

- *float* **normalized_time** - Moment to be sampled, given as a share of the channel time span in the [0.0f, 1.0f] range.

### Return value

Value the channel holds at the specified moment.
## void addQuatValue ( float time , const Math:: quat & value )

Adds a key holding an orientation given as a quaternion.
### Arguments

- *float* **time** - Moment the key is to sit at, in seconds.
- *const  Math::[quat](../../../../api/library/math/class.quat_cpp.md) &* **value** - Orientation to be held by the key.

## void addAnglesValue ( float time , const Math:: vec3 & value , AnimationCurve::KEY_TYPE type = AnimationCurve::KEY_TYPE_LINEAR )

Adds a key holding an orientation given as Euler angles.
### Arguments

- *float* **time** - Moment the key is to sit at, in seconds.
- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **value** - Orientation to be held by the key, given as Euler angles.
- *[AnimationCurve::KEY_TYPE](../../../../api/library/animations/timeline/class.animationcurve_cpp.md#KEY_TYPE)* **type** - Interpolation type of the key. The default value is [KEY_TYPE_LINEAR](../../../../api/library/animations/timeline/class.animationcurve_cpp.md#KEY_TYPE_LINEAR).
