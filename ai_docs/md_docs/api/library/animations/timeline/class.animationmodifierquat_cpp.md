# Unigine::AnimationModifierQuat Class (CPP)

**Header:** #include <UnigineAnimation.h>

**Inherits from:** AnimationModifier


## AnimationModifierQuat Class

### Enums

## MODE

| Name | Description |
|---|---|
| **MODE_QUAT** = 0 | Rotation value is obtained from *AnimationCurveQuat*. |
| **MODE_ANGLES_XYZ** = 1 | Three *AnimationCurveFloat* curves are used for each angle, and their data are used to compose a quaternion with the {X, Y, Z} order of coordinates. |
| **MODE_ANGLES_ZYX** = 2 | Three *AnimationCurveFloat* curves are used for each angle, and their data are used to compose a quaternion with the {Z, Y, X} order of coordinates. |

### Members

## AnimationModifierQuat::MODE getMode () const

Returns the current mode of obtaining the rotation data.
### Return value

Current mode of obtaining the rotation data.
## Math:: quat getDefaultValue () const

Returns the current default value of all modifier elements.
### Return value

Current default value of all modifier elements.
## void setQuatCurve ( const Ptr < AnimationCurveQuat >& curve )

Sets a new curve storing the values used by the modifier.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveQuat](../../../../api/library/animations/timeline/class.animationcurvequat_cpp.md)>&* **curve** - The curve storing the values used by the modifier.

## Ptr < AnimationCurveQuat > getQuatCurve () const

Returns the current curve storing the values used by the modifier.
### Return value

Current curve storing the values used by the modifier.
## void setCurveX ( const Ptr < AnimationCurveFloat >& x )

Sets a new curve storing the values used by the modifier for the X axis.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_cpp.md)>&* **x** - The curve storing the values used by the modifier for the X axis.

## Ptr < AnimationCurveFloat > getCurveX () const

Returns the current curve storing the values used by the modifier for the X axis.
### Return value

Current curve storing the values used by the modifier for the X axis.
## void setCurveY ( const Ptr < AnimationCurveFloat >& y )

Sets a new curve storing the values used by the modifier for the Y axis.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_cpp.md)>&* **y** - The curve storing the values used by the modifier for the Y axis.

## Ptr < AnimationCurveFloat > getCurveY () const

Returns the current curve storing the values used by the modifier for the Y axis.
### Return value

Current curve storing the values used by the modifier for the Y axis.
## void setCurveZ ( const Ptr < AnimationCurveFloat >& z )

Sets a new curve storing the values used by the modifier for the Z axis.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_cpp.md)>&* **z** - The curve storing the values used by the modifier for the Z axis.

## Ptr < AnimationCurveFloat > getCurveZ () const

Returns the current curve storing the values used by the modifier for the Z axis.
### Return value

Current curve storing the values used by the modifier for the Z axis.
## bool isUniformTime () const

Returns the current value showing if the modifier values are changed uniformly along the timeline.
### Return value

**true** if value showing if the modifier values are changed uniformly along the timeline. is enabled; otherwise **false**.
---

## AnimationModifierQuat ( AnimationModifierQuat::MODE mode , AnimParams::PARAM param )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *[AnimationModifierQuat::MODE](../../../../api/library/animations/timeline/class.animationmodifierquat_cpp.md#MODE)* **mode** - The mode of obtaining the rotation data.
- *AnimParams::PARAM* **param** - Parameter to be animated by the modifier.

## AnimationModifierQuat ( AnimationModifierQuat::MODE mode , AnimParams::PARAM param , int param_index )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *[AnimationModifierQuat::MODE](../../../../api/library/animations/timeline/class.animationmodifierquat_cpp.md#MODE)* **mode** - The mode of obtaining the rotation data.
- *AnimParams::PARAM* **param** - Parameter to be animated by the modifier.
- *int* **param_index** - Index of the parameter.

## AnimationModifierQuat ( AnimationModifierQuat::MODE mode , AnimParams::PARAM param , const char * param_name )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *[AnimationModifierQuat::MODE](../../../../api/library/animations/timeline/class.animationmodifierquat_cpp.md#MODE)* **mode** - The mode of obtaining the rotation data.
- *AnimParams::PARAM* **param** - Parameter to be animated by the modifier.
- *const char ** **param_name** - Name of the parameter.

## AnimationModifierQuat ( AnimationModifierQuat::MODE mode , const char * param )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *[AnimationModifierQuat::MODE](../../../../api/library/animations/timeline/class.animationmodifierquat_cpp.md#MODE)* **mode** - The mode of obtaining the rotation data.
- *const char ** **param** - Parameter to be animated by the modifier.

## AnimationModifierQuat ( AnimationModifierQuat::MODE mode , const char * param , int param_index )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *[AnimationModifierQuat::MODE](../../../../api/library/animations/timeline/class.animationmodifierquat_cpp.md#MODE)* **mode** - The mode of obtaining the rotation data.
- *const char ** **param** - Parameter to be animated by the modifier.
- *int* **param_index** - Index of the parameter.

## AnimationModifierQuat ( AnimationModifierQuat::MODE mode , const char * param , const char * param_name )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *[AnimationModifierQuat::MODE](../../../../api/library/animations/timeline/class.animationmodifierquat_cpp.md#MODE)* **mode** - The mode of obtaining the rotation data.
- *const char ** **param** - Parameter to be animated by the modifier.
- *const char ** **param_name** - Name of the parameter.

## void copy ( const Ptr < AnimationModifierQuat > & modifier )

Copies all data from the specified source animation modifier.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationModifierQuat](../../../../api/library/animations/timeline/class.animationmodifierquat_cpp.md)> &* **modifier** - Source animation modifier.

## Math:: quat getValueByTime ( float time )

Returns the value of the modifier at the specified time.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.

### Return value

The modifier value at the specified time.
## Math:: quat getValueByNormalizedTime ( float normalized_time )

Returns the normalized value of the modifier at the specified time.
### Arguments

- *float* **normalized_time** - The normalized time value.

### Return value

The modifier value at the specified time.
## void addQuatValue ( float time , const Math:: quat & value )

Adds the quaternion value to the modifier at the specified time.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.
- *const  Math::[quat](../../../../api/library/math/class.quat_cpp.md) &* **value** - The modifier value at the specified time.

## void addAnglesValue ( float time , const Math:: vec3 & value , AnimationCurve::KEY_TYPE type = Enum.AnimationCurve.KEY_TYPE.LINEAR )

Adds the angles value to the modifier at the specified time.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.
- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **value** - The modifier value at the specified time.
- *[AnimationCurve::KEY_TYPE](../../../../api/library/animations/timeline/class.animationcurve_cpp.md#KEY_TYPE)* **type** - Interpolation type set for the key, one of the [KEY_TYPE_*](../../../../api/library/animations/timeline/class.animationcurve_cpp.md#KEY_TYPE_CONSTANT) values.

## void updateUniformTime ( bool enabled , bool force_update = false )

Changes the value that defines if the modifier values are changed uniformly along the timeline. Enabling the uniform time allows avoiding such cases as speeding up or slowing down due to the curve shape.
### Arguments

- *bool* **enabled** - The current value.
- *bool* **force_update** - The target value.
