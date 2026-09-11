# Unigine::InputJoystick Class (CS)


This class handles joystick input. Generic joysticks can be hot-plugged. So, you can connect your joystick before or after create an instance of this class.


The *InputJoystick* class provides access to the following controller input:


- **Axes** detect movement along X and Y axes (if a joystick is two-axis, which is the most typical case) and along Z axis (if it is three-axis one). Two-axis joysticks are configured in such a way that left-to-right movement of the stick is mapped to the movement along the X axis, while movement from backward to forward (down-up) indicates movement along the Y axis. In case of 3D joystick, twisting the stick to the left (counter-clockwise) or to the right (clockwise) corresponds to movement along the Z axis. Axes are quired for their states via *[getAxis()](#getAxis_uint_float)*. To provide smooth interpolation between frames and avoid jerks, axis values can be filtered via *[setFilter()](#setFilter_float_void)*.
- **Buttons** correspond to the controller's buttons and can be either pressed or released in the current frame, or continuously pressed for multiple frames in a row including the current one.
- **POV (Point-Of-View) hat switches** indicate the direction of view and support a number of positions such as left, right, up and down (similar to a D-pad).


## InputJoystick Class

### Properties

## 🔒︎ int PlayerIndex

The index of player for the joystick. Some devices support connection of multiple players (e.g., XBox 360 supports up to four players connected through XBox 360 gamepads).
## 🔒︎ bool IsAvailable

The value indicating if the joystick is available.
## 🔒︎ string Name

The name of the joystick.
## 🔒︎ int Number

The joystick number.
## 🔒︎ Input.DEVICE DeviceType

The device type. One of the *[Input.DEVICE_*](../../../api/library/controls/class.input_cs.md#DEVICE_UNKNOWN)*values indicating whether it is a wheel, throttle, or other device.
## float Filter

The filter value used to correct the current state of the joystick axis relative to the previous one:
- Filter value of **0** means there is no interpolation and the current value is not corrected.
- Filter value of **1** means the previous state is used instead of the current one.


## 🔒︎ int NumAxes

The number of axes supported by the joystick.
## 🔒︎ int NumPovs

The number of POV hat switches supported by the joystick.
## 🔒︎ int NumButtons

The number of buttons supported by the joystick.
## 🔒︎ string Guid

The GUID created on the basis of [vendor](#getVendor_int) and [product](#getProduct_int) identifiers and [product version number](#getProduct_int). It enables you to identify device model (Controller XBox One, etc.), however, it will be the same for two identical models.
## 🔒︎ int Vendor

The unique identifier of the device manufacturer (vendor). This can be very useful in case your application uses non-standard custom input devices to ensure proper configuration (dead zones, inverse flags, correction curves, etc.).
## 🔒︎ int Product

The unique identifier for the product (GUID). This identifier is established by the manufacturer of the device. This can be very useful in case your application uses non-standard custom input devices to ensure proper configuration (dead zones, inverse flags, correction curves, etc.).
## 🔒︎ int ProductVersion

The version of the product established by the manufacturer of the device. This can be very useful in case your application uses non-standard custom input devices to ensure proper configuration (dead zones, inverse flags, correction curves, etc.).
### Members

---

## float GetAxis ( uint axis )

Returns a state value for the axis win the specified number. It includes position of the joystick along the following axes: X, Y (two-axis joystick) and Z (three-axis joystick). When a joystick is in the center position, X and Y axes values are zero. Negative values indicate left or down; positive values indicate right or up.
### Arguments

- *uint* **axis** - Axis number.

### Return value

Value in range **[-1; 1]**.
## float GetAxisDelta ( uint axis )

Returns a delta value (change since the previous frame) for the axis with the specified number.
### Arguments

- *uint* **axis** - Axis number.

### Return value

Axis delta value.
## string GetAxisName ( uint axis )

Returns the name of a given axis by its number.
### Arguments

- *uint* **axis** - Axis number.

### Return value

Axis name.
## Input.JOYSTICK_POV GetPov ( uint pov )

Returns a POV hat switch state. POV hats support the following positions: left, right, up and down.
### Arguments

- *uint* **pov** - POV hat number.

### Return value

POV hat state. One of the *[JOYSTICK_POV](../../../api/library/controls/class.input_cs.md#JOYSTICK_POV)* values of the *Input* class.
## string GetPovName ( uint pov )

Returns the name of a given POV hat switch.
### Arguments

- *uint* **pov** - POV hat number.

### Return value

POV hat name.
## bool IsButtonPressed ( uint key )

Returns a value indicating if the button with the specified number is pressed. Check this value to perform continuous actions.
### Arguments

- *uint* **key** - Button number.

### Return value

true if the button with the specified number is pressed; otherwise - false (pressed).
## bool IsButtonDown ( uint key )

Returns a value indicating if the button with the specified number was pressed during the current frame.
### Arguments

- *uint* **key** - Button number.

### Return value

true if the button with the specified number was pressed during the current frame; otherwise - false (pressed).
## bool IsButtonUp ( uint key )

Returns a value indicating if the button with the specified number was released during the current frame.
### Arguments

- *uint* **key** - Button number.

### Return value

true if the button with the specified number was released during the current frame; otherwise - false.
## string GetButtonName ( uint button )

Returns the name of the button with the specified number.
### Arguments

- *uint* **button** - Button number.

### Return value

Button name.
## InputEventJoyButton GetButtonEvent ( int button )

Returns the currently processed joystick button input event.
### Arguments

- *int* **button** - Button number.

### Return value

Joystick button input event, or null if there are no events for the specified joystick button in the current frame.
## int GetButtonEvents ( int button , InputEventJoyButton [] OUT_events )

Returns the number of input events for the specified joystick button and puts the events to the specified output buffer.
### Arguments

- *int* **button** - Button number.
- *[InputEventJoyButton](../../../api/library/controls/class.inputeventjoybutton_cs.md)[]* **OUT_events** - Buffer with button input events. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of input events for the specified joystick button.
## InputEventJoyPovMotion GetPovEvent ( int pov )

Returns the currently processed joystick POV hat input event.
### Arguments

- *int* **pov** - POV hat number.

### Return value

Joystick POV hat input event, or null if there are no events for the specified joystick POV hat in the current frame.
## int GetPovEvents ( int pov , InputEventJoyPovMotion [] OUT_events )

Returns the number of input events for the specified joystick POV hat and puts the events to the specified output buffer.
### Arguments

- *int* **pov** - POV hat number.
- *[InputEventJoyPovMotion](../../../api/library/controls/class.inputeventjoypovmotion_cs.md)[]* **OUT_events** - Buffer with POV input events. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of input events for the specified joystick POV hat.
## bool IsForceFeedbackEffectSupported ( Input.JOYSTICK_FORCE_FEEDBACK_EFFECT effect )

Returns the value indicating of the specified force feedback effect is supported by the joystick.
### Arguments

- *[Input.JOYSTICK_FORCE_FEEDBACK_EFFECT](../../../api/library/controls/class.input_cs.md#JOYSTICK_FORCE_FEEDBACK_EFFECT)* **effect** - Force feedback effect.

### Return value

true if the specified force feedback effect is supported, otherwise false.
## void PlayForceFeedbackEffectConstant ( float force )

Applies the constant force-feedback effect with the specified parameters to the joystick. Force is applied at a constant level for the duration of the effect.
### Arguments

- *float* **force** - Amount of force being applied by a force-feedback effect. The value in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.

## void PlayForceFeedbackEffectRamp ( float force , ulong duration_us )

Applies the ramp force-feedback effect with the specified parameters to the joystick. Force is applied gradually by being increased or decreased over the duration of the effect.
### Arguments

- *float* **force** - Amount of force being applied by a force-feedback effect. The value in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.
- *ulong* **duration_us** - Force-feedback effect duration, in microseconds.

## void PlayForceFeedbackEffectSineWave ( float force , uint period_ms )

Applies the sine-wave force-feedback effect with the specified parameters to the joystick. Force is applied in a sine-wave pattern.
### Arguments

- *float* **force** - Amount of force being applied by a force-feedback effect. The value in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.
- *uint* **period_ms** - Force-feedback effect duration, in microseconds.

## void PlayForceFeedbackEffectSineWave ( float force , float attack_force , float fade_force , int phase , uint period_ms , uint attack_length_ms , uint fade_length_ms , uint effect_duration_ms )

Applies the sine-wave force-feedback effect with the specified parameters to the joystick. Force is applied in a sine-wave pattern.
### Arguments

- *float* **force** - Sustain value � the force value in the middle of the force-feedback effect in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.
- *float* **attack_force** - Value at the start of the attack, in range [0, 1].
- *float* **fade_force** - Value at the end of the fade, in range [0, 1].
- *int* **phase** - Positive phase shift, in degrees in range [0, 360].
- *uint* **period_ms** - Period of the wave, in ms.
- *uint* **attack_length_ms** - Duration of the attack � time period in ms defining how long it takes to reach the force value (the value in the middle of the effect).
- *uint* **fade_length_ms** - Duration of the fade out � time period in ms defining how long it takes to fall away from the force value (the value in the middle of the effect).
- *uint* **effect_duration_ms** - Duration of the effect, in ms.

## void PlayForceFeedbackEffectSquareWave ( float force , uint period_ms )

Applies the square-wave force-feedback effect with the specified parameters to the joystick. Force is applied in a square-wave pattern.
### Arguments

- *float* **force** - Amount of force being applied by a force-feedback effect. The value in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.
- *uint* **period_ms** - Period of the wave, in ms.

## void PlayForceFeedbackEffectSquareWave ( float force , float attack_force , float fade_force , int phase , uint period_ms , uint attack_length_ms , uint fade_length_ms , uint effect_duration_ms )

Applies the square-wave force-feedback effect with the specified parameters to the joystick. Force is applied in a square-wave pattern.
### Arguments

- *float* **force** - Sustain value � the force value in the middle of the force-feedback effect in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.
- *float* **attack_force** - Value at the start of the attack, in range [0, 1].
- *float* **fade_force** - Value at the end of the fade, in range [0, 1].
- *int* **phase** - Positive phase shift, in degrees in range [0, 360].
- *uint* **period_ms** - Period of the wave, in ms.
- *uint* **attack_length_ms** - Duration of the attack � time period in ms defining how long it takes to reach the force value (the value in the middle of the effect).
- *uint* **fade_length_ms** - Duration of the fade out � time period in ms defining how long it takes to fall away from the force value (the value in the middle of the effect).
- *uint* **effect_duration_ms** - Duration of the effect, in ms.

## void PlayForceFeedbackEffectTriangleWave ( float force , uint period_ms )

Applies the triangle-wave force-feedback effect with the specified parameters to the joystick. Force is applied in a triangle-wave pattern.
### Arguments

- *float* **force** - Amount of force being applied by a force-feedback effect. The value in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.
- *uint* **period_ms** - Period of the wave, in ms.

## void PlayForceFeedbackEffectTriangleWave ( float force , float attack_force , float fade_force , int phase , uint period_ms , uint attack_length_ms , uint fade_length_ms , uint effect_duration_ms )

Applies the triangle-wave force-feedback effect with the specified parameters to the joystick. Force is applied in a triangle-wave pattern.
### Arguments

- *float* **force** - Sustain value � the force value in the middle of the force-feedback effect in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.
- *float* **attack_force** - Value at the start of the attack. Value in range [0, 1].
- *float* **fade_force** - Value at the end of the fade. Value in range [0, 1].
- *int* **phase** - Positive phase shift, in degrees in range [0, 360].
- *uint* **period_ms** - Period of the wave, in ms.
- *uint* **attack_length_ms** - Duration of the attack � time period in ms defining how long it takes to reach the force value (the value in the middle of the effect).
- *uint* **fade_length_ms** - Duration of the fade out � time period in ms defining how long it takes to fall away from the force value (the value in the middle of the effect).
- *uint* **effect_duration_ms** - Duration of the effect, in ms.

## void PlayForceFeedbackEffectSawtoothUpWave ( float force , uint period_ms )

Applies the upward-sawtooth-wave force-feedback effect with the specified parameters to the joystick. Force is applied in a upward-sawtooth-wave pattern.
### Arguments

- *float* **force** - Amount of force being applied by a force-feedback effect. The value in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.
- *uint* **period_ms** - Period of the wave, in ms.

## void PlayForceFeedbackEffectSawtoothUpWave ( float force , float attack_force , float fade_force , int phase , uint period_ms , uint attack_length_ms , uint fade_length_ms , uint effect_duration_ms )

Applies the upward-sawtooth-wave force-feedback effect with the specified parameters to the joystick. Force is applied in a upward-sawtooth-wave pattern.
### Arguments

- *float* **force** - Sustain value � the force value in the middle of the force-feedback effect in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.
- *float* **attack_force** - Value at the start of the attack. Value in range [0, 1].
- *float* **fade_force** - Value at the end of the fade. Value in range [0, 1].
- *int* **phase** - Positive phase shift, in degrees in range [0, 360].
- *uint* **period_ms** - Period of the wave, in ms.
- *uint* **attack_length_ms** - Duration of the attack � time period in ms defining how long it takes to reach the force value (the value in the middle of the effect).
- *uint* **fade_length_ms** - Duration of the fade out � time period in ms defining how long it takes to fall away from the force value (the value in the middle of the effect).
- *uint* **effect_duration_ms** - Duration of the effect, in ms.

## void PlayForceFeedbackEffectSawtoothDownWave ( float force , uint period_ms )

Applies the downward-sawtooth-wave force-feedback effect with the specified parameters to the joystick. Force is applied in a downward-sawtooth-wave pattern.
### Arguments

- *float* **force** - Amount of force being applied by a force-feedback effect. The value in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.
- *uint* **period_ms** - Force-feedback effect duration, in microseconds.

## void PlayForceFeedbackEffectSawtoothDownWave ( float force , float attack_force , float fade_force , int phase , uint period_ms , uint attack_length_ms , uint fade_length_ms , uint effect_duration_ms )

Applies the downward-sawtooth-wave force-feedback effect with the specified parameters to the joystick. Force is applied in a downward-sawtooth-wave pattern.
### Arguments

- *float* **force** - Sustain value � the force value in the middle of the force-feedback effect in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.
- *float* **attack_force** - Value at the start of the attack. Value in range [0, 1].
- *float* **fade_force** - Value at the end of the fade. Value in range [0, 1].
- *int* **phase** - Positive phase shift, in degrees in range [0, 360].
- *uint* **period_ms** - Period of the wave, in ms.
- *uint* **attack_length_ms** - Duration of the attack � time period in ms defining how long it takes to reach the force value (the value in the middle of the effect).
- *uint* **fade_length_ms** - Duration of the fade out � time period in ms defining how long it takes to fall away from the force value (the value in the middle of the effect).
- *uint* **effect_duration_ms** - Duration of the effect, in ms.

## void PlayForceFeedbackEffectSpring ( float force )

Applies the spring force-feedback effect with the specified force to the joystick. Force is applied in opposition to a set state.
### Arguments

- *float* **force** - Amount of force being applied by a force-feedback effect. The value in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.

## void PlayForceFeedbackEffectSpring ( float left_force , float left_saturation , float right_force , float right_saturation , float offset , float deadband )

Applies the spring force-feedback effect with the specified parameters to the joystick. Force is applied in opposition to a set state.
### Arguments

- *float* **left_force** - Strength of the force-feedback effect that occurs when turning to the left. Value in range [0, 1].
- *float* **left_saturation** - Maximum possible force for the force-feedback effect on turning left. Value in range [0, 1]. Not all devices support saturation.
- *float* **right_force** - Strength of the force-feedback effect that occurs when turning to the right. Value in range [0, 1].
- *float* **right_saturation** - Maximum possible force for the force-feedback effect on turning right. Value in range [0, 1]. Not all devices support saturation.
- *float* **offset** - The offset from the zero reading of the appropriate sensor value at which the condition begins to be applied. For a spring effect, the neutral point - that is, the point along the axis at which the spring would be considered at rest - would be defined by the offset for the condition.
- *float* **deadband** - Zone around the offset of an axis at which the condition is not active. In the case of a spring that is at rest in the middle of an axis, the deadband enlarges this area of rest. Not all devices support deadband.

## void PlayForceFeedbackEffectFriction ( float force )

Applies the friction force-feedback effect with the specified force to the joystick. Force is applied to mimic friction.
### Arguments

- *float* **force** - Amount of force being applied by a force-feedback effect. The value in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.

## void PlayForceFeedbackEffectFriction ( float left_force , float left_saturation , float right_force , float right_saturation )

Applies the friction force-feedback effect with the specified parameters to the joystick. Force is applied to mimic friction.
### Arguments

- *float* **left_force** - Strength of the force-feedback effect that occurs when turning to the left. Value in range [0, 1].
- *float* **left_saturation** - Maximum possible force for the force-feedback effect on turning left. Value in range [0, 1]. Not all devices support saturation.
- *float* **right_force** - Strength of the force-feedback effect that occurs when turning to the right. Value in range [0, 1].
- *float* **right_saturation** - Maximum possible force for the force-feedback effect on turning right. Value in range [0, 1]. Not all devices support saturation.

## void PlayForceFeedbackEffectDamper ( float force )

Applies the damper force-feedback effect with the specified force to the joystick. Force is applied to mimic a damper effect.
### Arguments

- *float* **force** - Amount of force being applied by a force-feedback effect. The value in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.

## void PlayForceFeedbackEffectDamper ( float left_force , float left_saturation , float right_force , float right_saturation )

Applies the damper force-feedback effect with the specified parameters to the joystick. Force is applied to mimic a damper effect.
### Arguments

- *float* **left_force** - Strength of the force-feedback effect that occurs when turning to the left. Value in range [0, 1].
- *float* **left_saturation** - Maximum possible force for the force-feedback effect on turning left. Value in range [0, 1]. Not all devices support saturation.
- *float* **right_force** - Strength of the force-feedback effect that occurs when turning to the right. Value in range [0, 1].
- *float* **right_saturation** - Maximum possible force for the force-feedback effect on turning right. Value in range [0, 1]. Not all devices support saturation.

## void PlayForceFeedbackEffectInertia ( float force )

Applies the inertia force-feedback effect with the specified force to the joystick. Force is applied to mimic an inertia effect.
### Arguments

- *float* **force** - Amount of force being applied by a force-feedback effect. The value in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.

## void StopForceFeedbackEffect ( Input.JOYSTICK_FORCE_FEEDBACK_EFFECT effect )

Stops application of the specified type of force-feedback effect to the joystick.
### Arguments

- *[Input.JOYSTICK_FORCE_FEEDBACK_EFFECT](../../../api/library/controls/class.input_cs.md#JOYSTICK_FORCE_FEEDBACK_EFFECT)* **effect** - Type of a force-feedback effect.

## bool IsForceFeedbackEffectPlaying ( Input.JOYSTICK_FORCE_FEEDBACK_EFFECT effect )

Returns the value indicating if the specified type of force-feedback effect is currently being applied.
### Arguments

- *[Input.JOYSTICK_FORCE_FEEDBACK_EFFECT](../../../api/library/controls/class.input_cs.md#JOYSTICK_FORCE_FEEDBACK_EFFECT)* **effect** - Type of a force-feedback effect.

### Return value

true if the specified type of force-feedback effect is currently being applied, otherwise false.
