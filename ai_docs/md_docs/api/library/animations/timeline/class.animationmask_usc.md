# Unigine::AnimationMask Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class enables you to manage [animation masks](../../../../principles/animations/index.md#animation_mask). A mask is a set of [objects](../../../../principles/animations/index.md#animation_object) and modifiers operated by a track.


## AnimationMask Class

### Members

## int isEmpty () const

Returns the current value indicating if the mask is empty.
### Return value

Current the mask is empty
## getNumModifiers () const

Returns the current number of modifiers that belong to the mask.
### Return value

Current number of modifiers that belong to the mask.
---

## AnimationMask ( )

Constructor. Creates an empty *AnimationMask* with default parameters.
## void addInfo ( AnimationModifierInfo info )

Adds a new animation modifier description to the mask.
### Arguments

- *[AnimationModifierInfo](../../../../api/library/animations/timeline/class.animationmodifierinfo_usc.md)* **info** - Description of an animation modifier.

## void removeInfo ( AnimationModifierInfo info )

Removes the specified animation modifier description from the mask.
### Arguments

- *[AnimationModifierInfo](../../../../api/library/animations/timeline/class.animationmodifierinfo_usc.md)* **info** - Description of an animation modifier to be removed.

## int containsInfo ( AnimationModifierInfo info )

Returns a value indicating if the mask contains the specified animation modifier description.
### Arguments

- *[AnimationModifierInfo](../../../../api/library/animations/timeline/class.animationmodifierinfo_usc.md)* **info** - Description of an animation modifier to be checked.

### Return value

**1** if the mask contains the specified animation modifier description; otherwise, **0**.
## AnimationModifierInfo getInfoByIndex ( int index )

Returns a description of the [animation modifier](../../../../principles/animations/index.md#animation_modifier) with the specified index.
### Arguments

- *int* **index** - Animation modifier description index.

### Return value

Description of an animation modifier with the specified index.
