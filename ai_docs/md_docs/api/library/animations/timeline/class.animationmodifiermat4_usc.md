# Unigine::AnimationModifierMat4 Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** AnimationModifier


## AnimationModifierMat4 Class

### Members

## void setFollowMode ( )

Sets a new transformation mode for the modified object.
### Arguments

- **mode** - The transformation mode for the modified object.

## getFollowMode () const

Returns the current transformation mode for the modified object.
### Return value

Current transformation mode for the modified object.
## void setFollowPositionOffset ( )

Sets a new position offset along the follow axis.
### Arguments

- **offset** - The position offset along the follow axis.

## getFollowPositionOffset () const

Returns the current position offset along the follow axis.
### Return value

Current position offset along the follow axis.
## int isUniformTime () const

Returns the current value showing if the modifier values are changed uniformly along the timeline.
### Return value

Current value showing if the modifier values are changed uniformly along the timeline.
---

## AnimationModifierMat4 ( int param )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *int* **param** - Parameter to be animated by the modifier.

## AnimationModifierMat4 ( int param , int param_index )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *int* **param** - Parameter to be animated by the modifier.
- *int* **param_index** - Index of the parameter.

## AnimationModifierMat4 ( int param , string param_name )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *int* **param** - Parameter to be animated by the modifier.
- *string* **param_name** - Name of the parameter.

## AnimationModifierMat4 ( string param )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *string* **param** - Parameter to be animated by the modifier.

## AnimationModifierMat4 ( string param , int param_index )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *string* **param** - Parameter to be animated by the modifier.
- *int* **param_index** - Index of the parameter.

## AnimationModifierMat4 ( string param , string param_name )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *string* **param** - Parameter to be animated by the modifier.
- *string* **param_name** - Name of the parameter.

## void copy ( AnimationModifierMat4 modifier )

Copies all data from the specified source animation modifier.
### Arguments

- *[AnimationModifierMat4](../../../../api/library/animations/timeline/class.animationmodifiermat4_usc.md)* **modifier** - Source animation modifier.

## void addValue ( float time , Mat4 value )

Adds the value to the modifier at the specified time.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.
- *Mat4* **value** - The modifier value at the specified time.

## void updateUniformTime ( int enabled , int force_update = false )

Changes the value that defines if the modifier values are changed uniformly along the timeline. Enabling the uniform time allows avoiding such cases as speeding up or slowing down due to the curve shape.
### Arguments

- *int* **enabled** - The current value.
- *int* **force_update** - The target value.
