# Unigine::AnimationModifierInfo Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


## AnimationModifierInfo Class

### Members

## int getType () const

Returns the current type of the animation modifier.
### Return value

Current type of the animation modifier.
## void setParam ( int param )

Sets a new parameter animated by the modifier.
### Arguments

- *int* **param** - The parameter animated by the modifier.

## int getParam () const

Returns the current parameter animated by the modifier.
### Return value

Current parameter animated by the modifier.
## void setParamIndex ( )

Sets a new index of the parameter animated by the modifier.
### Arguments

- **index** - The index of the parameter animated by the modifier.

## getParamIndex () const

Returns the current index of the parameter animated by the modifier.
### Return value

Current index of the parameter animated by the modifier.
## void setParamName ( string name )

Sets a new name of the parameter animated by the modifier.
### Arguments

- *string* **name** - The name of the parameter animated by the modifier.

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
