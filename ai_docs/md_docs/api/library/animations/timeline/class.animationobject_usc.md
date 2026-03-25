# Unigine::AnimationObject Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is used to manage [animation objects](../../../../principles/animations/index.md#animation_object) via code.


## AnimationObject Class

### Members

## int getType () const

Returns the current type of the animation object.
### Return value

Current animation object type.
## const char * getTypeName () const

Returns the current name of the animation object's type.
### Return value

Current animation object type name.
## getID () const

Returns the current identifier of the animation object.
### Return value

Current animation object identifier.
## void setName ( string name )

Sets a new name of the animation object.
### Arguments

- *string* **name** - The animation object name.

## const char * getName () const

Returns the current name of the animation object.
### Return value

Current animation object name.
