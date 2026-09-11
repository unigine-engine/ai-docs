# Unigine::AnimationChannelUGUID Class (CPP)

**Header:** #include <UnigineAnimation.h>

**Inherits from:** AnimationChannel


This channel animates a parameter that refers to an asset over time. It is one row of a [sequence](../../../../api/library/animations/timeline/class.animationsequence_cpp.md), while everything the channels share, such as the animated parameter, the binding and the clips, comes from the [AnimationChannel](../../../../api/library/animations/timeline/class.animationchannel_cpp.md) base class.


An asset reference has nothing in between, so the channel holds the value of a key until the next one is reached.


## AnimationChannelUGUID Class

### Members

## UGUID getDefaultValue () const

Returns the current value the channel falls back to where it has no keys of its own.
### Return value

Current value the channel falls back to
## void setCurve ( const Ptr < AnimationCurveUGUID >& curve )

Sets a new curve that holds the keys of the channel.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveUGUID](../../../../api/library/animations/timeline/class.animationcurveuguid_cpp.md)>&* **curve** - The curve that holds the keys of the channel

## Ptr < AnimationCurveUGUID > getCurve () const

Returns the current curve that holds the keys of the channel.
### Return value

Current curve that holds the keys of the channel
---

## AnimationChannelUGUID ( AnimParams::PARAM param )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be animated by the channel. Identifiers are looked up through the [Animations](../../../../api/library/animations/class.animations_cpp.md) class rather than written out by hand.

## AnimationChannelUGUID ( AnimParams::PARAM param , int param_index )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be animated by the channel. Identifiers are looked up through the [Animations](../../../../api/library/animations/class.animations_cpp.md) class rather than written out by hand.
- *int* **param_index** - Slot of the parameter for parameters that come as an array, such as a surface or a bone.

## AnimationChannelUGUID ( AnimParams::PARAM param , const char * param_name )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be animated by the channel. Identifiers are looked up through the [Animations](../../../../api/library/animations/class.animations_cpp.md) class rather than written out by hand.
- *const char ** **param_name** - Name that addresses the parameter when a number is not enough, such as the name of a property parameter or of a surface.

## AnimationChannelUGUID ( const char * param )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *const char ** **param** - Name of the parameter to be animated by the channel.

## AnimationChannelUGUID ( const char * param , int param_index )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *const char ** **param** - Name of the parameter to be animated by the channel.
- *int* **param_index** - Slot of the parameter for parameters that come as an array, such as a surface or a bone.

## AnimationChannelUGUID ( const char * param , const char * param_name )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *const char ** **param** - Name of the parameter to be animated by the channel.
- *const char ** **param_name** - Name that addresses the parameter when a number is not enough, such as the name of a property parameter or of a surface.

## void assignFrom ( const Ptr < AnimationChannelUGUID > & channel )

Copies the content of the specified channel into this one.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationChannelUGUID](../../../../api/library/animations/timeline/class.animationchanneluguid_cpp.md)> &* **channel** - Source channel to copy the content from.

## UGUID getValueByTime ( float time )

Returns the value the channel holds at the given moment.
### Arguments

- *float* **time** - Moment to be sampled, in seconds.

### Return value

Value the channel holds at the specified moment.
## UGUID getValueByNormalizedTime ( float normalized_time )

Returns the value the channel holds at the given moment, addressed as a share of its time span rather than in seconds.
### Arguments

- *float* **normalized_time** - Moment to be sampled, given as a share of the channel time span in the [0.0f, 1.0f] range.

### Return value

Value the channel holds at the specified moment.
## void addValue ( float time , const UGUID & value )

Adds a key holding the specified value.
### Arguments

- *float* **time** - Moment the key is to sit at, in seconds.
- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **value** - Value to be held by the key.
