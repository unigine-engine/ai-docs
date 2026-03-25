# Unigine::AnimationMask Class (CPP)

**Header:** #include <UnigineAnimation.h>


This class enables you to manage [animation masks](../../../../principles/animations/index.md#animation_mask). A mask is a set of [objects](../../../../principles/animations/index.md#animation_object) and modifiers operated by a track.


## AnimationMask Class

### Members

## bool isEmpty () const

Returns the current value indicating if the mask is empty.
### Return value

**true** if the mask is empty; otherwise **false**.
## getNumModifiers () const

Returns the current number of modifiers that belong to the mask.
### Return value

Current number of modifiers that belong to the mask.
---

## AnimationMask ( )

Constructor. Creates an empty *AnimationMask* with default parameters.
## void addInfo ( const Ptr < AnimationModifierInfo > & info )

Adds a new animation modifier description to the mask.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationModifierInfo](../../../../api/library/animations/timeline/class.animationmodifierinfo_cpp.md)> &* **info** - Description of an animation modifier.

## void removeInfo ( const Ptr < AnimationModifierInfo > & info )

Removes the specified animation modifier description from the mask.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationModifierInfo](../../../../api/library/animations/timeline/class.animationmodifierinfo_cpp.md)> &* **info** - Description of an animation modifier to be removed.

## bool containsInfo ( const Ptr < AnimationModifierInfo > & info ) const

Returns a value indicating if the mask contains the specified animation modifier description.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationModifierInfo](../../../../api/library/animations/timeline/class.animationmodifierinfo_cpp.md)> &* **info** - Description of an animation modifier to be checked.

### Return value

true if the mask contains the specified animation modifier description; otherwise, false.
## Ptr < AnimationModifierInfo > getInfoByIndex ( int index ) const

Returns a description of the [animation modifier](../../../../principles/animations/index.md#animation_modifier) with the specified index.
### Arguments

- *int* **index** - Animation modifier description index.

### Return value

Description of an animation modifier with the specified index.
