# Unigine::AnimationChannelInfo Class (CPP)

**Header:** #include <UnigineAnimation.h>


This class is the compact description of what a channel animates: its type, its parameter and the slot or the name that addresses that parameter. It carries no keys and no timing.


A frame produced by a playing sequence is described by these records rather than by the channels themselves, which is what lets a value be matched to its target without holding the whole [channel](../../../../api/library/animations/timeline/class.animationchannel_cpp.md).


## AnimationChannelInfo Class

### Members

## AnimationChannel::TYPE getType () const

Returns the current type of the channel the description belongs to.
### Return value

Current type of the channel the description belongs to
## void setParam ( AnimParams::PARAM param )

Sets a new parameter animated by the channel. The identifier comes from the registry of animatable parameters, which is looked up through the [Animations](../../../../api/library/animations/class.animations_cpp.md) class.
### Arguments

- *AnimParams::PARAM* **param** - The parameter animated by the channel

## AnimParams::PARAM getParam () const

Returns the current parameter animated by the channel. The identifier comes from the registry of animatable parameters, which is looked up through the [Animations](../../../../api/library/animations/class.animations_cpp.md) class.
### Return value

Current parameter animated by the channel
## void setParamIndex ( int index )

Sets a new slot of the animated parameter for parameters that come as an array, such as a surface or a bone. A parameter that has no slots reports -1.
### Arguments

- *int* **index** - The slot of the animated parameter

## int getParamIndex () const

Returns the current slot of the animated parameter for parameters that come as an array, such as a surface or a bone. A parameter that has no slots reports -1.
### Return value

Current slot of the animated parameter
## void setParamName ( const char * name )

Sets a new name that addresses the animated parameter when a number is not enough, such as the name of a property parameter or of a surface.
### Arguments

- *const char ** **name** - The name that addresses the animated parameter

## const char * getParamName () const

Returns the current name that addresses the animated parameter when a number is not enough, such as the name of a property parameter or of a surface.
### Return value

Current name that addresses the animated parameter
## void setSlotAccess ( AnimationChannel::SLOT_ACCESS access )

Sets a new way the parameter slot is addressed: by the position it takes in the list of slots, or by its name. See [SLOT_ACCESS_*](../../../../api/library/animations/timeline/class.animationchannel_cpp.md#SLOT_ACCESS_BY_INDEX) for the values and the difference between them.
### Arguments

- *[AnimationChannel::SLOT_ACCESS](../../../../api/library/animations/timeline/class.animationchannel_cpp.md#SLOT_ACCESS)* **access** - The way the parameter slot is addressed

## AnimationChannel::SLOT_ACCESS getSlotAccess () const

Returns the current way the parameter slot is addressed: by the position it takes in the list of slots, or by its name. See [SLOT_ACCESS_*](../../../../api/library/animations/timeline/class.animationchannel_cpp.md#SLOT_ACCESS_BY_INDEX) for the values and the difference between them.
### Return value

Current way the parameter slot is addressed
