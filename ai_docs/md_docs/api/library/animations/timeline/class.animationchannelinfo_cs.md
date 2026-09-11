# Unigine::AnimationChannelInfo Class (CS)


This class is the compact description of what a channel animates: its type, its parameter and the slot or the name that addresses that parameter. It carries no keys and no timing.


A frame produced by a playing sequence is described by these records rather than by the channels themselves, which is what lets a value be matched to its target without holding the whole [channel](../../../../api/library/animations/timeline/class.animationchannel_cs.md).


## AnimationChannelInfo Class

### Properties

## 🔒︎ AnimationChannel.TYPE Type

The type of the channel the description belongs to.
## AnimParams.PARAM Param

The parameter animated by the channel. The identifier comes from the registry of animatable parameters, which is looked up through the [Animations](../../../../api/library/animations/class.animations_cs.md) class.
## int ParamIndex

The slot of the animated parameter for parameters that come as an array, such as a surface or a bone. A parameter that has no slots reports -1.
## string ParamName

The name that addresses the animated parameter when a number is not enough, such as the name of a property parameter or of a surface.
## AnimationChannel.SLOT_ACCESS SlotAccess

The way the parameter slot is addressed: by the position it takes in the list of slots, or by its name. See [SLOT_ACCESS_*](../../../../api/library/animations/timeline/class.animationchannel_cs.md#SLOT_ACCESS_BY_INDEX) for the values and the difference between them.
