# Unigine::AnimationChannelSkeletonAnimation Class (CPP)

**Header:** #include <UnigineAnimation.h>

**Inherits from:** AnimationChannel


This channel plays a skeletal animation on the node it is bound to. Each key names an animation asset, and the playback of that animation starts at the moment of the key, so the time inside the clip is counted from there.


The channel carries no value curve of its own: what it holds per key is the animation to play, and the way it is trimmed, faded and retimed comes from the clips of the [AnimationChannel](../../../../api/library/animations/timeline/class.animationchannel_cpp.md) base class.


## AnimationChannelSkeletonAnimation Class

---

## AnimationChannelSkeletonAnimation ( AnimParams::PARAM param )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be animated by the channel. Identifiers are looked up through the [Animations](../../../../api/library/animations/class.animations_cpp.md) class rather than written out by hand.

## AnimationChannelSkeletonAnimation ( AnimParams::PARAM param , int param_index )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be animated by the channel. Identifiers are looked up through the [Animations](../../../../api/library/animations/class.animations_cpp.md) class rather than written out by hand.
- *int* **param_index** - Slot of the parameter for parameters that come as an array, such as a surface or a bone.

## AnimationChannelSkeletonAnimation ( AnimParams::PARAM param , const char * param_name )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be animated by the channel. Identifiers are looked up through the [Animations](../../../../api/library/animations/class.animations_cpp.md) class rather than written out by hand.
- *const char ** **param_name** - Name that addresses the parameter when a number is not enough, such as the name of a property parameter or of a surface.

## AnimationChannelSkeletonAnimation ( const char * param )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *const char ** **param** - Name of the parameter to be animated by the channel.

## AnimationChannelSkeletonAnimation ( const char * param , int param_index )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *const char ** **param** - Name of the parameter to be animated by the channel.
- *int* **param_index** - Slot of the parameter for parameters that come as an array, such as a surface or a bone.

## AnimationChannelSkeletonAnimation ( const char * param , const char * param_name )

Constructor. Creates a channel that animates the specified parameter.
### Arguments

- *const char ** **param** - Name of the parameter to be animated by the channel.
- *const char ** **param_name** - Name that addresses the parameter when a number is not enough, such as the name of a property parameter or of a surface.

## void assignFrom ( const Ptr < AnimationChannelSkeletonAnimation > & channel )

Copies the content of the specified channel into this one.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationChannelSkeletonAnimation](../../../../api/library/animations/timeline/class.animationchannelskeletonanimation_cpp.md)> &* **channel** - Source channel to copy the content from.
