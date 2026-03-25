# Unigine::AnimationModifierInfo Class (CPP)

**Header:** #include <UnigineAnimation.h>


## AnimationModifierInfo Class

### Members

## AnimationModifier::TYPE getType () const

Returns the current type of the animation modifier.
### Return value

Current type of the animation modifier.
## void setParam ( AnimParams::PARAM param )

Sets a new parameter animated by the modifier.
### Arguments

- *AnimParams::PARAM* **param** - The parameter animated by the modifier.

## AnimParams::PARAM getParam () const

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
## void setParamName ( const char * name )

Sets a new name of the parameter animated by the modifier.
### Arguments

- *const char ** **name** - The name of the parameter animated by the modifier.

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
