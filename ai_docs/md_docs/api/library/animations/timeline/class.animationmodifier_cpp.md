# Unigine::AnimationModifier Class (CPP)

**Header:** #include <UnigineAnimation.h>


Animation modifiers store the description of the parameter to be animated and a set of curves to change the values.


## AnimationModifier Class

### Enums

## TYPE

| Name | Description |
|---|---|
| **ANIMATION_MODIFIER** = 0 | The animation modifier. |
| **ANIMATION_MODIFIER_INT** = 1 | The animation modifier using integer values. |
| **ANIMATION_MODIFIER_BOOL** = 2 | The animation modifier using boolean values. |
| **ANIMATION_MODIFIER_QUAT** = 3 | The animation modifier using quaternions. |
| **ANIMATION_MODIFIER_SCALAR** = 4 | The animation modifier using scalar values. |
| **ANIMATION_MODIFIER_FLOAT** = 5 | The animation modifier using floating point values. |
| **ANIMATION_MODIFIER_DOUBLE** = 6 | The animation modifier using double precision values. |
| **ANIMATION_MODIFIER_STRING** = 7 | The animation modifier using strings. |
| **ANIMATION_MODIFIER_UGUID** = 8 | The animation modifier using UGUIDs. |
| **ANIMATION_MODIFIER_IVEC2** = 9 | The animation modifier using 2-component vectors of integer values. |
| **ANIMATION_MODIFIER_IVEC3** = 10 | The animation modifier using 3-component vectors of integer values. |
| **ANIMATION_MODIFIER_IVEC4** = 11 | The animation modifier using 4-component vectors of integer values. |
| **ANIMATION_MODIFIER_VEC2** = 12 | The animation modifier using 2-component vectors. |
| **ANIMATION_MODIFIER_FVEC2** = 13 | The animation modifier using 2-component vectors of floating point values. |
| **ANIMATION_MODIFIER_DVEC2** = 14 | The animation modifier using 2-component vectors of double precision values. |
| **ANIMATION_MODIFIER_VEC3** = 15 | The animation modifier using 3-component vectors. |
| **ANIMATION_MODIFIER_FVEC3** = 16 | The animation modifier using 3-component vectors of floating point values. |
| **ANIMATION_MODIFIER_DVEC3** = 17 | The animation modifier using 3-component vectors of double precision values. |
| **ANIMATION_MODIFIER_VEC4** = 18 | The animation modifier using 4-component vectors. |
| **ANIMATION_MODIFIER_FVEC4** = 19 | The animation modifier using 4-component vectors of floating point values. |
| **ANIMATION_MODIFIER_DVEC4** = 20 | The animation modifier using 4-component vectors of double precision values. |
| **ANIMATION_MODIFIER_MAT4** = 21 | The animation modifier using 4x4 matrices. |
| **ANIMATION_MODIFIER_NODE** = 22 | The animation modifier animating nodes. |
| **ANIMATION_MODIFIER_BONES** = 23 | The animation modifier animating [ObjectMeshSkinnedLegacy](../../../../api/library/objects/class.objectmeshskinnedlegacy_cpp.md) bones. |
| **ANIMATION_MODIFIER_TRACK** = 24 | The animation modifier using tracks. |

### Members

## Ptr < AnimationModifierInfo > getInfo () const

Returns the current information on the animation modifier.
### Return value

Current information on the animation modifier.
## AnimationModifier::TYPE getType () const

Returns the current type of the animation modifier.
### Return value

Current type of the animation modifier.
## const char * getTypeName () const

Returns the current name of the animation modifier type.
### Return value

Current name of the animation modifier type.
## AnimParams::PARAM getParam () const

Returns the current parameter animated by the modifier.
### Return value

Current parameter animated by the modifier.
## getParamIndex () const

Returns the current index of the parameter animated by the modifier.
### Return value

Current index of the parameter animated by the modifier.
## const char * getParamName () const

Returns the current name of the parameter animated by the modifier.
### Return value

Current name of the parameter animated by the modifier.
## void setObjID ( )

Sets a new ID of the animation object to which the modifier is applied.
### Arguments

- **id** - The ID of the animation object to which the modifier is applied.

## getObjID () const

Returns the current ID of the animation object to which the modifier is applied.
### Return value

Current ID of the animation object to which the modifier is applied.
## getMinTime () const

Returns the current point of the whole animation timeline where this modifier starts being applied, in units.
### Return value

Current point of the whole animation timeline where this modifier starts being applied, in units.
## getMaxTime () const

Returns the current point of the whole animation timeline up to which this modifier is applied, in units.
### Return value

Current point of the whole animation timeline up to which this modifier is applied, in units.
## getDuration () const

Returns the current duration of the period when the modifier affects the animation, in units.
### Return value

Current duration of the period when the modifier affects the animation, in units.
---

## void save ( const Ptr < Blob > & blob ) const

Saves the animation modifier data to a blob.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Blob](../../../../api/library/common/class.blob_cpp.md)> &* **blob** - Blob to which the animation modifier data will be saved.

## void load ( const Ptr < Blob > & blob )

Loads the animation modifier data from the blob.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Blob](../../../../api/library/common/class.blob_cpp.md)> &* **blob** - Blob storing the animation modifier data.
