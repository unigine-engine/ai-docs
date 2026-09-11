# Unigine::AnimationChannelVec3 Class (CS)

**Inherits from:** AnimationChannel


This channel animates a three-component scalar vector, such as a position over time. It is one row of a [sequence](../../../../api/library/animations/timeline/class.animationsequence_cs.md), while everything the channels share, such as the animated parameter, the binding and the clips, comes from the [AnimationChannel](../../../../api/library/animations/timeline/class.animationchannel_cs.md) base class.


## AnimationChannelVec3 Class

### Properties

## 🔒︎ vec3 DefaultValue

The value the channel falls back to where it has no keys of its own.
## AnimationCurveScalar CurveX

The curve of the X component.
## AnimationCurveScalar CurveY

The curve of the Y component.
## AnimationCurveScalar CurveZ

The curve of the Z component.
### Members

---

## AnimationChannelVec3 ( AnimParams.PARAM param )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be animated by the channel. Identifiers are looked up through the [Animations](../../../../api/library/animations/class.animations_cs.md) class rather than written out by hand.

## AnimationChannelVec3 ( AnimParams.PARAM param , int param_index )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be animated by the channel. Identifiers are looked up through the [Animations](../../../../api/library/animations/class.animations_cs.md) class rather than written out by hand.
- *int* **param_index** - Slot of the parameter for parameters that come as an array, such as a surface or a bone.

## AnimationChannelVec3 ( AnimParams.PARAM param , string param_name )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be animated by the channel. Identifiers are looked up through the [Animations](../../../../api/library/animations/class.animations_cs.md) class rather than written out by hand.
- *string* **param_name** - Name that addresses the parameter when a number is not enough, such as the name of a property parameter or of a surface.

## AnimationChannelVec3 ( string param )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *string* **param** - Name of the parameter to be animated by the channel.

## AnimationChannelVec3 ( string param , int param_index )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *string* **param** - Name of the parameter to be animated by the channel.
- *int* **param_index** - Slot of the parameter for parameters that come as an array, such as a surface or a bone.

## AnimationChannelVec3 ( string param , string param_name )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *string* **param** - Name of the parameter to be animated by the channel.
- *string* **param_name** - Name that addresses the parameter when a number is not enough, such as the name of a property parameter or of a surface.

## void AssignFrom ( AnimationChannelVec3 channel )

Copies the content of the specified channel into this one.
### Arguments

- *[AnimationChannelVec3](../../../../api/library/animations/timeline/class.animationchannelvec3_cs.md)* **channel** - Source channel to copy the content from.

## vec3 GetValueByTime ( float time )

Returns the value the channel holds at the given moment.
### Arguments

- *float* **time** - Moment to be sampled, in seconds.

### Return value

Value the channel holds at the specified moment.
## vec3 GetValueByNormalizedTime ( float normalized_time )

Returns the value the channel holds at the given moment, addressed as a share of its time span rather than in seconds.
### Arguments

- *float* **normalized_time** - Moment to be sampled, given as a share of the channel time span in the [0.0f, 1.0f] range.

### Return value

Value the channel holds at the specified moment.
## void AddValue ( float time , vec3 value , AnimationCurve.KEY_TYPE type = AnimationCurve::KEY_TYPE_LINEAR )

Adds a key holding the specified value.
### Arguments

- *float* **time** - Moment the key is to sit at, in seconds.
- *vec3* **value** - Value to be held by the key.
- *[AnimationCurve.KEY_TYPE](../../../../api/library/animations/timeline/class.animationcurve_cs.md#KEY_TYPE)* **type** - Interpolation type of the key. The default value is [KEY_TYPE_LINEAR](../../../../api/library/animations/timeline/class.animationcurve_cs.md#KEY_TYPE_LINEAR).
