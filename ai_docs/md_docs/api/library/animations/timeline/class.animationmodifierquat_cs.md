# Unigine::AnimationModifierQuat Class (CS)

**Inherits from:** AnimationModifier


## AnimationModifierQuat Class

### Enums

## MODE

| Name | Description |
|---|---|
| **QUAT** = 0 | Rotation value is obtained from *AnimationCurveQuat*. |
| **ANGLES_XYZ** = 1 | Three *AnimationCurveFloat* curves are used for each angle, and their data are used to compose a quaternion with the {X, Y, Z} order of coordinates. |
| **ANGLES_ZYX** = 2 | Three *AnimationCurveFloat* curves are used for each angle, and their data are used to compose a quaternion with the {Z, Y, X} order of coordinates. |

### Properties

## 🔒︎ AnimationModifierQuat.MODE Mode

The mode of obtaining the rotation data.
## 🔒︎ quat DefaultValue

The default value of all modifier elements.
## AnimationCurveQuat QuatCurve

The curve storing the values used by the modifier.
## AnimationCurveFloat CurveX

The curve storing the values used by the modifier for the X axis.
## AnimationCurveFloat CurveY

The curve storing the values used by the modifier for the Y axis.
## AnimationCurveFloat CurveZ

The curve storing the values used by the modifier for the Z axis.
## 🔒︎ bool IsUniformTime

The value showing if the modifier values are changed uniformly along the timeline.
### Members

---

## AnimationModifierQuat ( AnimationModifierQuat.MODE mode , AnimParams.PARAM param )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *[AnimationModifierQuat.MODE](../../../../api/library/animations/timeline/class.animationmodifierquat_cs.md#MODE)* **mode** - The mode of obtaining the rotation data.
- *AnimParams.PARAM* **param** - Parameter to be animated by the modifier.

## AnimationModifierQuat ( AnimationModifierQuat.MODE mode , AnimParams.PARAM param , int param_index )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *[AnimationModifierQuat.MODE](../../../../api/library/animations/timeline/class.animationmodifierquat_cs.md#MODE)* **mode** - The mode of obtaining the rotation data.
- *AnimParams.PARAM* **param** - Parameter to be animated by the modifier.
- *int* **param_index** - Index of the parameter.

## AnimationModifierQuat ( AnimationModifierQuat.MODE mode , AnimParams.PARAM param , string param_name )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *[AnimationModifierQuat.MODE](../../../../api/library/animations/timeline/class.animationmodifierquat_cs.md#MODE)* **mode** - The mode of obtaining the rotation data.
- *AnimParams.PARAM* **param** - Parameter to be animated by the modifier.
- *string* **param_name** - Name of the parameter.

## AnimationModifierQuat ( AnimationModifierQuat.MODE mode , string param )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *[AnimationModifierQuat.MODE](../../../../api/library/animations/timeline/class.animationmodifierquat_cs.md#MODE)* **mode** - The mode of obtaining the rotation data.
- *string* **param** - Parameter to be animated by the modifier.

## AnimationModifierQuat ( AnimationModifierQuat.MODE mode , string param , int param_index )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *[AnimationModifierQuat.MODE](../../../../api/library/animations/timeline/class.animationmodifierquat_cs.md#MODE)* **mode** - The mode of obtaining the rotation data.
- *string* **param** - Parameter to be animated by the modifier.
- *int* **param_index** - Index of the parameter.

## AnimationModifierQuat ( AnimationModifierQuat.MODE mode , string param , string param_name )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *[AnimationModifierQuat.MODE](../../../../api/library/animations/timeline/class.animationmodifierquat_cs.md#MODE)* **mode** - The mode of obtaining the rotation data.
- *string* **param** - Parameter to be animated by the modifier.
- *string* **param_name** - Name of the parameter.

## void Copy ( AnimationModifierQuat modifier )

Copies all data from the specified source animation modifier.
### Arguments

- *[AnimationModifierQuat](../../../../api/library/animations/timeline/class.animationmodifierquat_cs.md)* **modifier** - Source animation modifier.

## quat GetValueByTime ( float time )

Returns the value of the modifier at the specified time.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.

### Return value

The modifier value at the specified time.
## quat GetValueByNormalizedTime ( float normalized_time )

Returns the normalized value of the modifier at the specified time.
### Arguments

- *float* **normalized_time** - The normalized time value.

### Return value

The modifier value at the specified time.
## void AddQuatValue ( float time , quat value )

Adds the quaternion value to the modifier at the specified time.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.
- *quat* **value** - The modifier value at the specified time.

## void AddAnglesValue ( float time , vec3 value , AnimationCurve.KEY_TYPE type = Enum.AnimationCurve.KEY_TYPE.LINEAR )

Adds the angles value to the modifier at the specified time.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.
- *vec3* **value** - The modifier value at the specified time.
- *[AnimationCurve.KEY_TYPE](../../../../api/library/animations/timeline/class.animationcurve_cs.md#KEY_TYPE)* **type** - Interpolation type set for the key, one of the [KEY_TYPE](../../../../api/library/animations/timeline/class.animationcurve_cs.md#KEY_TYPE) values.

## void UpdateUniformTime ( bool enabled , bool force_update = false )

Changes the value that defines if the modifier values are changed uniformly along the timeline. Enabling the uniform time allows avoiding such cases as speeding up or slowing down due to the curve shape.
### Arguments

- *bool* **enabled** - The current value.
- *bool* **force_update** - The target value.
