# Unigine::AnimationMask Class (CS)


This class enables you to manage [animation masks](../../../../principles/animations/index.md#animation_mask). A mask is a set of [objects](../../../../principles/animations/index.md#animation_object) and modifiers operated by a track.


## AnimationMask Class

### Properties

## 🔒︎ bool IsEmpty

The value indicating if the mask is empty.
## 🔒︎ int NumModifiers

The number of modifiers that belong to the mask.
### Members

---

## AnimationMask ( )

Constructor. Creates an empty *AnimationMask* with default parameters.
## void AddInfo ( AnimationModifierInfo info )

Adds a new animation modifier description to the mask.
### Arguments

- *[AnimationModifierInfo](../../../../api/library/animations/timeline/class.animationmodifierinfo_cs.md)* **info** - Description of an animation modifier.

## void RemoveInfo ( AnimationModifierInfo info )

Removes the specified animation modifier description from the mask.
### Arguments

- *[AnimationModifierInfo](../../../../api/library/animations/timeline/class.animationmodifierinfo_cs.md)* **info** - Description of an animation modifier to be removed.

## bool ContainsInfo ( AnimationModifierInfo info )

Returns a value indicating if the mask contains the specified animation modifier description.
### Arguments

- *[AnimationModifierInfo](../../../../api/library/animations/timeline/class.animationmodifierinfo_cs.md)* **info** - Description of an animation modifier to be checked.

### Return value

true if the mask contains the specified animation modifier description; otherwise, false.
## AnimationModifierInfo GetInfoByIndex ( int index )

Returns a description of the [animation modifier](../../../../principles/animations/index.md#animation_modifier) with the specified index.
### Arguments

- *int* **index** - Animation modifier description index.

### Return value

Description of an animation modifier with the specified index.
