# Unigine::AnimationChannelSound Class (CS)

**Inherits from:** AnimationChannel


This channel plays a sound on the sound source it is bound to. Each key names a sound file, and the playback starts at the moment of the key, so the time inside the sound is counted from there.


Pitch, trimming and fades are shaped by the playback property curves of the [AnimationChannel](../../../../api/library/animations/timeline/class.animationchannel_cs.md) base class rather than by a value curve of this one.


## AnimationChannelSound Class

### Members

---

## AnimationChannelSound ( AnimParams.PARAM param )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be animated by the channel. Identifiers are looked up through the [Animations](../../../../api/library/animations/class.animations_cs.md) class rather than written out by hand.

## AnimationChannelSound ( AnimParams.PARAM param , int param_index )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be animated by the channel. Identifiers are looked up through the [Animations](../../../../api/library/animations/class.animations_cs.md) class rather than written out by hand.
- *int* **param_index** - Slot of the parameter for parameters that come as an array, such as a surface or a bone.

## AnimationChannelSound ( AnimParams.PARAM param , string param_name )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be animated by the channel. Identifiers are looked up through the [Animations](../../../../api/library/animations/class.animations_cs.md) class rather than written out by hand.
- *string* **param_name** - Name that addresses the parameter when a number is not enough, such as the name of a property parameter or of a surface.

## AnimationChannelSound ( string param )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *string* **param** - Name of the parameter to be animated by the channel.

## AnimationChannelSound ( string param , int param_index )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *string* **param** - Name of the parameter to be animated by the channel.
- *int* **param_index** - Slot of the parameter for parameters that come as an array, such as a surface or a bone.

## AnimationChannelSound ( string param , string param_name )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *string* **param** - Name of the parameter to be animated by the channel.
- *string* **param_name** - Name that addresses the parameter when a number is not enough, such as the name of a property parameter or of a surface.

## void AssignFrom ( AnimationChannelSound channel )

Copies the content of the specified channel into this one.
### Arguments

- *[AnimationChannelSound](../../../../api/library/animations/timeline/class.animationchannelsound_cs.md)* **channel** - Source channel to copy the content from.
