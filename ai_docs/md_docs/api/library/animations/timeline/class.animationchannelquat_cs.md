# Unigine::AnimationChannelQuat Class (CS)

**Inherits from:** AnimationChannel


This channel animates an orientation over time. It is one row of a [sequence](../../../../api/library/animations/timeline/class.animationsequence_cs.md), while everything the channels share, such as the animated parameter, the binding and the clips, comes from the [AnimationChannel](../../../../api/library/animations/timeline/class.animationchannel_cs.md) base class.


Every mode stores the orientation as three Euler curves and only picks the way the segments between the keys are interpolated, so switching the mode remaps no key.


## AnimationChannelQuat Class

### Enums

## MODE

Way the orientation is interpolated between the keys.
| Name | Description |
|---|---|
| **QUAT** = 0 | The key quaternions are interpolated along the shortest arc between them, and the tangents of the keys act as an ease of the timing rather than of the path. |
| **ANGLES_XYZ** = 1 | Each Euler axis is interpolated on its own and the result is composed in the XYZ order. |
| **ANGLES_ZYX** = 2 | Each Euler axis is interpolated on its own and the result is composed in the ZYX order. |

### Properties

## AnimationChannelQuat.MODE Mode

The way the orientation is interpolated between the keys. Every mode keeps the same three Euler curves, so switching between them remaps no key.
## 🔒︎ quat DefaultValue

The value the channel falls back to where it has no keys of its own.
## AnimationCurveQuat QuatCurve

The curve that holds the orientation keys.
## AnimationCurveFloat CurveX

The curve of the X component.
## AnimationCurveFloat CurveY

The curve of the Y component.
## AnimationCurveFloat CurveZ

The curve of the Z component.
### Members

---

## AnimationChannelQuat ( AnimationChannelQuat.MODE mode , AnimParams.PARAM param )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *[AnimationChannelQuat.MODE](../../../../api/library/animations/timeline/class.animationchannelquat_cs.md#MODE)* **mode** - Way the orientation is interpolated between the keys.
- *AnimParams.PARAM* **param** - Parameter to be animated by the channel. Identifiers are looked up through the [Animations](../../../../api/library/animations/class.animations_cs.md) class rather than written out by hand.

## AnimationChannelQuat ( AnimationChannelQuat.MODE mode , AnimParams.PARAM param , int param_index )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *[AnimationChannelQuat.MODE](../../../../api/library/animations/timeline/class.animationchannelquat_cs.md#MODE)* **mode** - Way the orientation is interpolated between the keys.
- *AnimParams.PARAM* **param** - Parameter to be animated by the channel. Identifiers are looked up through the [Animations](../../../../api/library/animations/class.animations_cs.md) class rather than written out by hand.
- *int* **param_index** - Slot of the parameter for parameters that come as an array, such as a surface or a bone.

## AnimationChannelQuat ( AnimationChannelQuat.MODE mode , AnimParams.PARAM param , string param_name )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *[AnimationChannelQuat.MODE](../../../../api/library/animations/timeline/class.animationchannelquat_cs.md#MODE)* **mode** - Way the orientation is interpolated between the keys.
- *AnimParams.PARAM* **param** - Parameter to be animated by the channel. Identifiers are looked up through the [Animations](../../../../api/library/animations/class.animations_cs.md) class rather than written out by hand.
- *string* **param_name** - Name that addresses the parameter when a number is not enough, such as the name of a property parameter or of a surface.

## AnimationChannelQuat ( AnimationChannelQuat.MODE mode , string param )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *[AnimationChannelQuat.MODE](../../../../api/library/animations/timeline/class.animationchannelquat_cs.md#MODE)* **mode** - Way the orientation is interpolated between the keys.
- *string* **param** - Name of the parameter to be animated by the channel.

## AnimationChannelQuat ( AnimationChannelQuat.MODE mode , string param , int param_index )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *[AnimationChannelQuat.MODE](../../../../api/library/animations/timeline/class.animationchannelquat_cs.md#MODE)* **mode** - Way the orientation is interpolated between the keys.
- *string* **param** - Name of the parameter to be animated by the channel.
- *int* **param_index** - Slot of the parameter for parameters that come as an array, such as a surface or a bone.

## AnimationChannelQuat ( AnimationChannelQuat.MODE mode , string param , string param_name )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *[AnimationChannelQuat.MODE](../../../../api/library/animations/timeline/class.animationchannelquat_cs.md#MODE)* **mode** - Way the orientation is interpolated between the keys.
- *string* **param** - Name of the parameter to be animated by the channel.
- *string* **param_name** - Name that addresses the parameter when a number is not enough, such as the name of a property parameter or of a surface.

## void AssignFrom ( AnimationChannelQuat channel )

Copies the content of the specified channel into this one.
### Arguments

- *[AnimationChannelQuat](../../../../api/library/animations/timeline/class.animationchannelquat_cs.md)* **channel** - Source channel to copy the content from.

## quat GetValueByTime ( float time )

Returns the value the channel holds at the given moment.
### Arguments

- *float* **time** - Moment to be sampled, in seconds.

### Return value

Value the channel holds at the specified moment.
## quat GetValueByNormalizedTime ( float normalized_time )

Returns the value the channel holds at the given moment, addressed as a share of its time span rather than in seconds.
### Arguments

- *float* **normalized_time** - Moment to be sampled, given as a share of the channel time span in the [0.0f, 1.0f] range.

### Return value

Value the channel holds at the specified moment.
## void AddQuatValue ( float time , quat value )

Adds a key holding an orientation given as a quaternion.
### Arguments

- *float* **time** - Moment the key is to sit at, in seconds.
- *quat* **value** - Orientation to be held by the key.

## void AddAnglesValue ( float time , vec3 value , AnimationCurve.KEY_TYPE type = AnimationCurve::KEY_TYPE_LINEAR )

Adds a key holding an orientation given as Euler angles.
### Arguments

- *float* **time** - Moment the key is to sit at, in seconds.
- *vec3* **value** - Orientation to be held by the key, given as Euler angles.
- *[AnimationCurve.KEY_TYPE](../../../../api/library/animations/timeline/class.animationcurve_cs.md#KEY_TYPE)* **type** - Interpolation type of the key. The default value is [KEY_TYPE_LINEAR](../../../../api/library/animations/timeline/class.animationcurve_cs.md#KEY_TYPE_LINEAR).
