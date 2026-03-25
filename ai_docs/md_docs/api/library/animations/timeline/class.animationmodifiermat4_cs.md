# Unigine::AnimationModifierMat4 Class (CS)

**Inherits from:** AnimationModifier


## AnimationModifierMat4 Class

### Enums

## FOLLOW_MODE

| Name | Description |
|---|---|
| **NONE** = 0 | The modified object is rotated using the result of interpolation between the keys. |
| **X** = 1 | The modified object's X axis follows the transformation curve. |
| **Y** = 2 | The modified object's Y axis follows the transformation curve. |
| **Z** = 3 | The modified object's Z axis follows the transformation curve. |

### Properties

## AnimationModifierMat4.FOLLOW_MODE FollowMode

The transformation mode for the modified object.
## float FollowPositionOffset

The position offset along the follow axis.
## 🔒︎ bool IsUniformTime

The value showing if the modifier values are changed uniformly along the timeline.
### Members

---

## AnimationModifierMat4 ( AnimParams.PARAM param )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be animated by the modifier.

## AnimationModifierMat4 ( AnimParams.PARAM param , int param_index )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be animated by the modifier.
- *int* **param_index** - Index of the parameter.

## AnimationModifierMat4 ( AnimParams.PARAM param , string param_name )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be animated by the modifier.
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

## void Copy ( AnimationModifierMat4 modifier )

Copies all data from the specified source animation modifier.
### Arguments

- *[AnimationModifierMat4](../../../../api/library/animations/timeline/class.animationmodifiermat4_cs.md)* **modifier** - Source animation modifier.

## void AddValue ( float time , mat4 value )

Adds the value to the modifier at the specified time.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.
- *mat4* **value** - The modifier value at the specified time.

## void UpdateUniformTime ( bool enabled , bool force_update = false )

Changes the value that defines if the modifier values are changed uniformly along the timeline. Enabling the uniform time allows avoiding such cases as speeding up or slowing down due to the curve shape.
### Arguments

- *bool* **enabled** - The current value.
- *bool* **force_update** - The target value.
