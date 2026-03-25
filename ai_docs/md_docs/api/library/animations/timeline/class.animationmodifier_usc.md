# Unigine::AnimationModifier Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


Animation modifiers store the description of the parameter to be animated and a set of curves to change the values.


## AnimationModifier Class

### Members

## AnimationModifierInfo getInfo () const

Returns the current information on the animation modifier.
### Return value

Current information on the animation modifier.
## int getType () const

Returns the current type of the animation modifier.
### Return value

Current type of the animation modifier.
## const char * getTypeName () const

Returns the current name of the animation modifier type.
### Return value

Current name of the animation modifier type.
## int getParam () const

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

## void save ( Blob blob )

Saves the animation modifier data to a blob.
### Arguments

- *[Blob](../../../../api/library/common/class.blob_usc.md)* **blob** - Blob to which the animation modifier data will be saved.

## void load ( const Blob blob )

Loads the animation modifier data from the blob.
### Arguments

- *const [Blob](../../../../api/library/common/class.blob_usc.md)* **blob** - Blob storing the animation modifier data.
