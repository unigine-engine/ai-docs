# Unigine::AnimationModifierQuat Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** AnimationModifier


## AnimationModifierQuat Class

### Members

## int getMode () const

Returns the current mode of obtaining the rotation data.
### Return value

Current mode of obtaining the rotation data.
## quat getDefaultValue () const

Returns the current default value of all modifier elements.
### Return value

Current default value of all modifier elements.
## void setQuatCurve ( AnimationCurveQuat curve )

Sets a new curve storing the values used by the modifier.
### Arguments

- *[AnimationCurveQuat](../../../../api/library/animations/timeline/class.animationcurvequat_usc.md)* **curve** - The curve storing the values used by the modifier.

## AnimationCurveQuat getQuatCurve () const

Returns the current curve storing the values used by the modifier.
### Return value

Current curve storing the values used by the modifier.
## void setCurveX ( AnimationCurveFloat x )

Sets a new curve storing the values used by the modifier for the X axis.
### Arguments

- *[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_usc.md)* **x** - The curve storing the values used by the modifier for the X axis.

## AnimationCurveFloat getCurveX () const

Returns the current curve storing the values used by the modifier for the X axis.
### Return value

Current curve storing the values used by the modifier for the X axis.
## void setCurveY ( AnimationCurveFloat y )

Sets a new curve storing the values used by the modifier for the Y axis.
### Arguments

- *[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_usc.md)* **y** - The curve storing the values used by the modifier for the Y axis.

## AnimationCurveFloat getCurveY () const

Returns the current curve storing the values used by the modifier for the Y axis.
### Return value

Current curve storing the values used by the modifier for the Y axis.
## void setCurveZ ( AnimationCurveFloat z )

Sets a new curve storing the values used by the modifier for the Z axis.
### Arguments

- *[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_usc.md)* **z** - The curve storing the values used by the modifier for the Z axis.

## AnimationCurveFloat getCurveZ () const

Returns the current curve storing the values used by the modifier for the Z axis.
### Return value

Current curve storing the values used by the modifier for the Z axis.
## int isUniformTime () const

Returns the current value showing if the modifier values are changed uniformly along the timeline.
### Return value

Current value showing if the modifier values are changed uniformly along the timeline.
---

## AnimationModifierQuat ( int mode , int param )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *int* **mode** - The mode of obtaining the rotation data.
- *int* **param** - Parameter to be animated by the modifier.

## AnimationModifierQuat ( int mode , int param , int param_index )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *int* **mode** - The mode of obtaining the rotation data.
- *int* **param** - Parameter to be animated by the modifier.
- *int* **param_index** - Index of the parameter.

## AnimationModifierQuat ( int mode , int param , string param_name )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *int* **mode** - The mode of obtaining the rotation data.
- *int* **param** - Parameter to be animated by the modifier.
- *string* **param_name** - Name of the parameter.

## AnimationModifierQuat ( int mode , string param )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *int* **mode** - The mode of obtaining the rotation data.
- *string* **param** - Parameter to be animated by the modifier.

## AnimationModifierQuat ( int mode , string param , int param_index )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *int* **mode** - The mode of obtaining the rotation data.
- *string* **param** - Parameter to be animated by the modifier.
- *int* **param_index** - Index of the parameter.

## AnimationModifierQuat ( int mode , string param , string param_name )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *int* **mode** - The mode of obtaining the rotation data.
- *string* **param** - Parameter to be animated by the modifier.
- *string* **param_name** - Name of the parameter.

## void copy ( AnimationModifierQuat modifier )

Copies all data from the specified source animation modifier.
### Arguments

- *[AnimationModifierQuat](../../../../api/library/animations/timeline/class.animationmodifierquat_usc.md)* **modifier** - Source animation modifier.

## quat getValueByTime ( float time )

Returns the value of the modifier at the specified time.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.

### Return value

The modifier value at the specified time.
## quat getValueByNormalizedTime ( float normalized_time )

Returns the normalized value of the modifier at the specified time.
### Arguments

- *float* **normalized_time** - The normalized time value.

### Return value

The modifier value at the specified time.
## void addQuatValue ( float time , quat value )

Adds the quaternion value to the modifier at the specified time.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.
- *quat* **value** - The modifier value at the specified time.

## void addAnglesValue ( float time , vec3 value , int type = Enum.AnimationCurve.KEY_TYPE.LINEAR )

Adds the angles value to the modifier at the specified time.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.
- *vec3* **value** - The modifier value at the specified time.
- *int* **type** - Interpolation type set for the key, one of the [ANIMATION_CURVE_KEY_TYPE_*](../../../../api/library/animations/timeline/class.animationcurve_usc.md#KEY_TYPE_CONSTANT) values.

## void updateUniformTime ( int enabled , int force_update = false )

Changes the value that defines if the modifier values are changed uniformly along the timeline. Enabling the uniform time allows avoiding such cases as speeding up or slowing down due to the curve shape.
### Arguments

- *int* **enabled** - The current value.
- *int* **force_update** - The target value.
