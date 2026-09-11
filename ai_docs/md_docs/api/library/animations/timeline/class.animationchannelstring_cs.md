# Unigine::AnimationChannelString Class (CS)

**Inherits from:** AnimationChannel


This channel animates a text parameter over time. It is one row of a [sequence](../../../../api/library/animations/timeline/class.animationsequence_cs.md), while everything the channels share, such as the animated parameter, the binding and the clips, comes from the [AnimationChannel](../../../../api/library/animations/timeline/class.animationchannel_cs.md) base class.


Text has nothing in between, so the channel holds the value of a key until the next one is reached.


## AnimationChannelString Class

### Properties

## 🔒︎ string DefaultValue

The value the channel falls back to where it has no keys of its own.
## AnimationCurveString Curve

The curve that holds the keys of the channel.
### Members

---

## AnimationChannelString ( AnimParams.PARAM param )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be animated by the channel. Identifiers are looked up through the [Animations](../../../../api/library/animations/class.animations_cs.md) class rather than written out by hand.

## AnimationChannelString ( AnimParams.PARAM param , int param_index )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be animated by the channel. Identifiers are looked up through the [Animations](../../../../api/library/animations/class.animations_cs.md) class rather than written out by hand.
- *int* **param_index** - Slot of the parameter for parameters that come as an array, such as a surface or a bone.

## AnimationChannelString ( AnimParams.PARAM param , string param_name )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be animated by the channel. Identifiers are looked up through the [Animations](../../../../api/library/animations/class.animations_cs.md) class rather than written out by hand.
- *string* **param_name** - Name that addresses the parameter when a number is not enough, such as the name of a property parameter or of a surface.

## AnimationChannelString ( string param )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *string* **param** - Name of the parameter to be animated by the channel.

## AnimationChannelString ( string param , int param_index )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *string* **param** - Name of the parameter to be animated by the channel.
- *int* **param_index** - Slot of the parameter for parameters that come as an array, such as a surface or a bone.

## AnimationChannelString ( string param , string param_name )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *string* **param** - Name of the parameter to be animated by the channel.
- *string* **param_name** - Name that addresses the parameter when a number is not enough, such as the name of a property parameter or of a surface.

## void AssignFrom ( AnimationChannelString channel )

Copies the content of the specified channel into this one.
### Arguments

- *[AnimationChannelString](../../../../api/library/animations/timeline/class.animationchannelstring_cs.md)* **channel** - Source channel to copy the content from.

## string GetValueByTime ( float time )

Returns the value the channel holds at the given moment.
### Arguments

- *float* **time** - Moment to be sampled, in seconds.

### Return value

Value the channel holds at the specified moment.
## string GetValueByNormalizedTime ( float normalized_time )

Returns the value the channel holds at the given moment, addressed as a share of its time span rather than in seconds.
### Arguments

- *float* **normalized_time** - Moment to be sampled, given as a share of the channel time span in the [0.0f, 1.0f] range.

### Return value

Value the channel holds at the specified moment.
## void AddValue ( float time , string value )

Adds a key holding the specified value.
### Arguments

- *float* **time** - Moment the key is to sit at, in seconds.
- *string* **value** - Value to be held by the key.
