# Unigine::InputJoystick Class (CPP)

**Header:** #include <UnigineInput.h>


This class handles joystick input. Generic joysticks can be hot-plugged. So, you can connect your joystick before or after create an instance of this class.


The *InputJoystick* class provides access to the following controller input:


- **Axes** detect movement along X and Y axes (if a joystick is two-axis, which is the most typical case) and along Z axis (if it is three-axis one). Two-axis joysticks are configured in such a way that left-to-right movement of the stick is mapped to the movement along the X axis, while movement from backward to forward (down-up) indicates movement along the Y axis. In case of 3D joystick, twisting the stick to the left (counter-clockwise) or to the right (clockwise) corresponds to movement along the Z axis. Axes are quired for their states via *[getAxis()](#getAxis_uint_float)*. To provide smooth interpolation between frames and avoid jerks, axis values can be filtered via *[setFilter()](#setFilter_float_void)*.
- **Buttons** correspond to the controller's buttons and can be either pressed or released in the current frame, or continuously pressed for multiple frames in a row including the current one.
- **POV (Point-Of-View) hat switches** indicate the direction of view and support a number of positions such as left, right, up and down (similar to a D-pad).


### See Also


- C++ sample
- C# Component sample


## InputJoystick Class

### Members

---

## int getPlayerIndex ( ) const

Returns the index of player for the joystick. Some devices support connection of multiple players (e.g., XBox 360 supports up to four players connected through XBox 360 gamepads). This method enables you to get this index.
### Return value

Player index for the joystick.
## bool isAvailable ( ) const

Returns a value indicating if the joystick is available.
### Return value

true if the joystick is available; otherwise, false.
## const char * getName ( ) const

Returns the name of the joystick.
### Return value

Joystick name.
## int getNumber ( ) const

Returns the joystick number.
### Return value

Joystick number.
## Input::DEVICE getDeviceType ( ) const

Returns a value indicating the type of the device (wheel, throttle, etc.).
### Return value

Device type. One of the *[DEVICE_*](../../../api/library/controls/class.input_cpp.md#DEVICE_UNKNOWN)*values of the *Input* class.
## void setFilter ( float filter )

Sets a filter value used to correct the current state of the joystick axis relative to the previous one.
### Arguments

- *float* **filter** - Filter value for interpolation between axis states. The provided value is clamped to a range **[0;1]**.

  - Filter value of **0** means there is no interpolation and the current value is not corrected.
  - Filter value of **1** means the previous state is used instead of the current one.

## float getFilter ( ) const

Returns a filter value used to correct the current state of the joystick axis relative to the previous one:
- Filter value of **0** means there is no interpolation and the current value is not corrected.
- Filter value of **1** means the previous state is used instead of the current one.


### Return value

Filter value for interpolation between axis states.
## int getNumAxes ( ) const

Returns the number of axes supported by the joystick.
### Return value

Number of axes for the joystick.
## float getAxis ( unsigned int axis ) const

Returns a state value for the axis win the specified number. It includes position of the joystick along the following axes: X, Y (two-axis joystick) and Z (three-axis joystick). When a joystick is in the center position, X and Y axes values are zero. Negative values indicate left or down; positive values indicate right or up.
### Arguments

- *unsigned int* **axis** - Axis number.

### Return value

Value in range **[-1; 1]**.
## float getAxisDelta ( unsigned int axis ) const

Returns a delta value (change since the previous frame) for the axis with the specified number.
### Arguments

- *unsigned int* **axis** - Axis number.

### Return value

Axis delta value.
## const char * getAxisName ( unsigned int axis ) const

Returns the name of a given axis by its number.
### Arguments

- *unsigned int* **axis** - Axis number.

### Return value

Axis name.
## int getNumPovs ( ) const

Returns the number of POV hat switches supported by the joystick.
### Return value

Number of POV hats.
## Input::JOYSTICK_POV getPov ( unsigned int pov ) const

Returns a POV hat switch state. POV hats support the following positions: left, right, up and down.
### Arguments

- *unsigned int* **pov** - POV hat number.

### Return value

POV hat state. One of the *[JOYSTICK_POV](../../../api/library/controls/class.input_cpp.md#JOYSTICK_POV)* values of the *Input* class.
## const char * getPovName ( unsigned int pov ) const

Returns the name of a given POV hat switch.
### Arguments

- *unsigned int* **pov** - POV hat number.

### Return value

POV hat name.
## int getNumButtons ( ) const

Returns the number of buttons supported by the joystick.
### Return value

Number of buttons.
## bool isButtonPressed ( unsigned int key ) const

Returns a value indicating if the button with the specified number is pressed. Check this value to perform continuous actions.
### Arguments

- *unsigned int* **key** - Button number.

### Return value

true if the button with the specified number is pressed; otherwise - false (pressed).
## bool isButtonDown ( unsigned int key ) const

Returns a value indicating if the button with the specified number was pressed during the current frame.
### Arguments

- *unsigned int* **key** - Button number.

### Return value

true if the button with the specified number was pressed during the current frame; otherwise - false (pressed).
## bool isButtonUp ( unsigned int key ) const

Returns a value indicating if the button with the specified number was released during the current frame.
### Arguments

- *unsigned int* **key** - Button number.

### Return value

true if the button with the specified number was released during the current frame; otherwise - false.
## const char * getButtonName ( unsigned int button ) const

Returns the name of the button with the specified number.
### Arguments

- *unsigned int* **button** - Button number.

### Return value

Button name.
## Ptr < InputEventJoyButton > getButtonEvent ( int button ) const

Returns the currently processed joystick button input event.
### Arguments

- *int* **button** - Button number.

### Return value

Joystick button input event, or nullptr if there are no events for the specified joystick button in the current frame.
## int getButtonEvents ( int button , Vector < Ptr < InputEventJoyButton >> & OUT_events ) const

Returns the number of input events for the specified joystick button and puts the events to the specified output buffer.
### Arguments

- *int* **button** - Button number.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[InputEventJoyButton](../../../api/library/controls/class.inputeventjoybutton_cpp.md)>> &* **OUT_events** - Buffer with button input events. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of input events for the specified joystick button.
## Ptr < InputEventJoyPovMotion > getPovEvent ( int pov ) const

Returns the currently processed joystick POV hat input event.
### Arguments

- *int* **pov** - POV hat number.

### Return value

Joystick POV hat input event, or nullptr if there are no events for the specified joystick POV hat in the current frame.
## int getPovEvents ( int pov , Vector < Ptr < InputEventJoyPovMotion >> & OUT_events ) const

Returns the number of input events for the specified joystick POV hat and puts the events to the specified output buffer.
### Arguments

- *int* **pov** - POV hat number.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[InputEventJoyPovMotion](../../../api/library/controls/class.inputeventjoypovmotion_cpp.md)>> &* **OUT_events** - Buffer with POV input events. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of input events for the specified joystick POV hat.
## const char * getGuid ( ) const

Returns the GUID created on the basis of [vendor](#getVendor_int) and [product](#getProduct_int) identifiers and [product version number](#getProduct_int). It enables you to identify device model (*Controller XBox One*, etc.), however, it will be the same for two identical models.
### Return value

Device model GUID.
## int getVendor ( ) const

Returns a unique identifier of the device manufacturer (vendor). This can be very useful in case your application uses non-standard custom input devices to ensure proper configuration (dead zones, inverse flags, correction curves, etc.).
### Return value

Unique identifier of the device manufacturer (vendor).
## int getProduct ( ) const

Returns a unique identifier for the product (GUID). This identifier is established by the manufacturer of the device. This can be very useful in case your application uses non-standard custom input devices to ensure proper configuration (dead zones, inverse flags, correction curves, etc.).
### Return value

Unique identifier for the product (GUID).
## int getProductVersion ( ) const

Returns the version of the product established by the manufacturer of the device. This can be very useful in case your application uses non-standard custom input devices to ensure proper configuration (dead zones, inverse flags, correction curves, etc.).
### Return value

Version of the product established by the manufacturer of the device.
## bool isForceFeedbackEffectSupported ( Input::JOYSTICK_FORCE_FEEDBACK_EFFECT effect ) const

Returns the value indicating of the specified force feedback effect is supported by the joystick.
### Arguments

- *[Input::JOYSTICK_FORCE_FEEDBACK_EFFECT](../../../api/library/controls/class.input_cpp.md#JOYSTICK_FORCE_FEEDBACK_EFFECT)* **effect** - Force feedback effect.

### Return value

true if the specified force feedback effect is supported, otherwise false.
## void playForceFeedbackEffectConstant ( float force )

Applies the constant force-feedback effect with the specified parameters to the joystick. Force is applied at a constant level for the duration of the effect.
### Arguments

- *float* **force** - Amount of force being applied by a force-feedback effect. The value in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.

## void playForceFeedbackEffectRamp ( float force , unsigned long long duration_us )

Applies the ramp force-feedback effect with the specified parameters to the joystick. Force is applied gradually by being increased or decreased over the duration of the effect.
### Arguments

- *float* **force** - Amount of force being applied by a force-feedback effect. The value in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.
- *unsigned long long* **duration_us** - Force-feedback effect duration, in microseconds.

## void playForceFeedbackEffectSineWave ( float force , unsigned int period_ms )

Applies the sine-wave force-feedback effect with the specified parameters to the joystick. Force is applied in a sine-wave pattern.
### Arguments

- *float* **force** - Amount of force being applied by a force-feedback effect. The value in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.
- *unsigned int* **period_ms** - Force-feedback effect duration, in microseconds.

## void playForceFeedbackEffectSineWave ( float force , float attack_force , float fade_force , int phase , unsigned int period_ms , unsigned int attack_length_ms , unsigned int fade_length_ms , unsigned int effect_duration_ms )

Applies the sine-wave force-feedback effect with the specified parameters to the joystick. Force is applied in a sine-wave pattern.
### Arguments

- *float* **force** - Sustain value � the force value in the middle of the force-feedback effect in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.
- *float* **attack_force** - Value at the start of the attack, in range [0, 1].
- *float* **fade_force** - Value at the end of the fade, in range [0, 1].
- *int* **phase** - Positive phase shift, in degrees in range [0, 360].
- *unsigned int* **period_ms** - Period of the wave, in ms.
- *unsigned int* **attack_length_ms** - Duration of the attack � time period in ms defining how long it takes to reach the force value (the value in the middle of the effect).
- *unsigned int* **fade_length_ms** - Duration of the fade out � time period in ms defining how long it takes to fall away from the force value (the value in the middle of the effect).
- *unsigned int* **effect_duration_ms** - Duration of the effect, in ms.

## void playForceFeedbackEffectSquareWave ( float force , unsigned int period_ms )

Applies the square-wave force-feedback effect with the specified parameters to the joystick. Force is applied in a square-wave pattern.
### Arguments

- *float* **force** - Amount of force being applied by a force-feedback effect. The value in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.
- *unsigned int* **period_ms** - Period of the wave, in ms.

## void playForceFeedbackEffectSquareWave ( float force , float attack_force , float fade_force , int phase , unsigned int period_ms , unsigned int attack_length_ms , unsigned int fade_length_ms , unsigned int effect_duration_ms )

Applies the square-wave force-feedback effect with the specified parameters to the joystick. Force is applied in a square-wave pattern.
### Arguments

- *float* **force** - Sustain value � the force value in the middle of the force-feedback effect in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.
- *float* **attack_force** - Value at the start of the attack, in range [0, 1].
- *float* **fade_force** - Value at the end of the fade, in range [0, 1].
- *int* **phase** - Positive phase shift, in degrees in range [0, 360].
- *unsigned int* **period_ms** - Period of the wave, in ms.
- *unsigned int* **attack_length_ms** - Duration of the attack � time period in ms defining how long it takes to reach the force value (the value in the middle of the effect).
- *unsigned int* **fade_length_ms** - Duration of the fade out � time period in ms defining how long it takes to fall away from the force value (the value in the middle of the effect).
- *unsigned int* **effect_duration_ms** - Duration of the effect, in ms.

## void playForceFeedbackEffectTriangleWave ( float force , unsigned int period_ms )

Applies the triangle-wave force-feedback effect with the specified parameters to the joystick. Force is applied in a triangle-wave pattern.
### Arguments

- *float* **force** - Amount of force being applied by a force-feedback effect. The value in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.
- *unsigned int* **period_ms** - Period of the wave, in ms.

## void playForceFeedbackEffectTriangleWave ( float force , float attack_force , float fade_force , int phase , unsigned int period_ms , unsigned int attack_length_ms , unsigned int fade_length_ms , unsigned int effect_duration_ms )

Applies the triangle-wave force-feedback effect with the specified parameters to the joystick. Force is applied in a triangle-wave pattern.
### Arguments

- *float* **force** - Sustain value � the force value in the middle of the force-feedback effect in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.
- *float* **attack_force** - Value at the start of the attack. Value in range [0, 1].
- *float* **fade_force** - Value at the end of the fade. Value in range [0, 1].
- *int* **phase** - Positive phase shift, in degrees in range [0, 360].
- *unsigned int* **period_ms** - Period of the wave, in ms.
- *unsigned int* **attack_length_ms** - Duration of the attack � time period in ms defining how long it takes to reach the force value (the value in the middle of the effect).
- *unsigned int* **fade_length_ms** - Duration of the fade out � time period in ms defining how long it takes to fall away from the force value (the value in the middle of the effect).
- *unsigned int* **effect_duration_ms** - Duration of the effect, in ms.

## void playForceFeedbackEffectSawtoothUpWave ( float force , unsigned int period_ms )

Applies the upward-sawtooth-wave force-feedback effect with the specified parameters to the joystick. Force is applied in a upward-sawtooth-wave pattern.
### Arguments

- *float* **force** - Amount of force being applied by a force-feedback effect. The value in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.
- *unsigned int* **period_ms** - Period of the wave, in ms.

## void playForceFeedbackEffectSawtoothUpWave ( float force , float attack_force , float fade_force , int phase , unsigned int period_ms , unsigned int attack_length_ms , unsigned int fade_length_ms , unsigned int effect_duration_ms )

Applies the upward-sawtooth-wave force-feedback effect with the specified parameters to the joystick. Force is applied in a upward-sawtooth-wave pattern.
### Arguments

- *float* **force** - Sustain value � the force value in the middle of the force-feedback effect in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.
- *float* **attack_force** - Value at the start of the attack. Value in range [0, 1].
- *float* **fade_force** - Value at the end of the fade. Value in range [0, 1].
- *int* **phase** - Positive phase shift, in degrees in range [0, 360].
- *unsigned int* **period_ms** - Period of the wave, in ms.
- *unsigned int* **attack_length_ms** - Duration of the attack � time period in ms defining how long it takes to reach the force value (the value in the middle of the effect).
- *unsigned int* **fade_length_ms** - Duration of the fade out � time period in ms defining how long it takes to fall away from the force value (the value in the middle of the effect).
- *unsigned int* **effect_duration_ms** - Duration of the effect, in ms.

## void playForceFeedbackEffectSawtoothDownWave ( float force , unsigned int period_ms )

Applies the downward-sawtooth-wave force-feedback effect with the specified parameters to the joystick. Force is applied in a downward-sawtooth-wave pattern.
### Arguments

- *float* **force** - Amount of force being applied by a force-feedback effect. The value in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.
- *unsigned int* **period_ms** - Force-feedback effect duration, in microseconds.

## void playForceFeedbackEffectSawtoothDownWave ( float force , float attack_force , float fade_force , int phase , unsigned int period_ms , unsigned int attack_length_ms , unsigned int fade_length_ms , unsigned int effect_duration_ms )

Applies the downward-sawtooth-wave force-feedback effect with the specified parameters to the joystick. Force is applied in a downward-sawtooth-wave pattern.
### Arguments

- *float* **force** - Sustain value � the force value in the middle of the force-feedback effect in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.
- *float* **attack_force** - Value at the start of the attack. Value in range [0, 1].
- *float* **fade_force** - Value at the end of the fade. Value in range [0, 1].
- *int* **phase** - Positive phase shift, in degrees in range [0, 360].
- *unsigned int* **period_ms** - Period of the wave, in ms.
- *unsigned int* **attack_length_ms** - Duration of the attack � time period in ms defining how long it takes to reach the force value (the value in the middle of the effect).
- *unsigned int* **fade_length_ms** - Duration of the fade out � time period in ms defining how long it takes to fall away from the force value (the value in the middle of the effect).
- *unsigned int* **effect_duration_ms** - Duration of the effect, in ms.

## void playForceFeedbackEffectSpring ( float force )

Applies the spring force-feedback effect with the specified force to the joystick. Force is applied in opposition to a set state.
### Arguments

- *float* **force** - Amount of force being applied by a force-feedback effect. The value in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.

## void playForceFeedbackEffectSpring ( float left_force , float left_saturation , float right_force , float right_saturation , float offset , float deadband )

Applies the spring force-feedback effect with the specified parameters to the joystick. Force is applied in opposition to a set state.
### Arguments

- *float* **left_force** - Strength of the force-feedback effect that occurs when turning to the left. Value in range [0, 1].
- *float* **left_saturation** - Maximum possible force for the force-feedback effect on turning left. Value in range [0, 1]. Not all devices support saturation.
- *float* **right_force** - Strength of the force-feedback effect that occurs when turning to the right. Value in range [0, 1].
- *float* **right_saturation** - Maximum possible force for the force-feedback effect on turning right. Value in range [0, 1]. Not all devices support saturation.
- *float* **offset** - The offset from the zero reading of the appropriate sensor value at which the condition begins to be applied. For a spring effect, the neutral point - that is, the point along the axis at which the spring would be considered at rest - would be defined by the offset for the condition.
- *float* **deadband** - Zone around the offset of an axis at which the condition is not active. In the case of a spring that is at rest in the middle of an axis, the deadband enlarges this area of rest. Not all devices support deadband.

## void playForceFeedbackEffectFriction ( float force )

Applies the friction force-feedback effect with the specified force to the joystick. Force is applied to mimic friction.
### Arguments

- *float* **force** - Amount of force being applied by a force-feedback effect. The value in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.

## void playForceFeedbackEffectFriction ( float left_force , float left_saturation , float right_force , float right_saturation )

Applies the friction force-feedback effect with the specified parameters to the joystick. Force is applied to mimic friction.
### Arguments

- *float* **left_force** - Strength of the force-feedback effect that occurs when turning to the left. Value in range [0, 1].
- *float* **left_saturation** - Maximum possible force for the force-feedback effect on turning left. Value in range [0, 1]. Not all devices support saturation.
- *float* **right_force** - Strength of the force-feedback effect that occurs when turning to the right. Value in range [0, 1].
- *float* **right_saturation** - Maximum possible force for the force-feedback effect on turning right. Value in range [0, 1]. Not all devices support saturation.

## void playForceFeedbackEffectDamper ( float force )

Applies the damper force-feedback effect with the specified force to the joystick. Force is applied to mimic a damper effect.
### Arguments

- *float* **force** - Amount of force being applied by a force-feedback effect. The value in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.

## void playForceFeedbackEffectDamper ( float left_force , float left_saturation , float right_force , float right_saturation )

Applies the damper force-feedback effect with the specified parameters to the joystick. Force is applied to mimic a damper effect.
### Arguments

- *float* **left_force** - Strength of the force-feedback effect that occurs when turning to the left. Value in range [0, 1].
- *float* **left_saturation** - Maximum possible force for the force-feedback effect on turning left. Value in range [0, 1]. Not all devices support saturation.
- *float* **right_force** - Strength of the force-feedback effect that occurs when turning to the right. Value in range [0, 1].
- *float* **right_saturation** - Maximum possible force for the force-feedback effect on turning right. Value in range [0, 1]. Not all devices support saturation.

## void playForceFeedbackEffectInertia ( float force )

Applies the inertia force-feedback effect with the specified force to the joystick. Force is applied to mimic an inertia effect.
### Arguments

- *float* **force** - Amount of force being applied by a force-feedback effect. The value in range [-1, 1]. Negative values mean that the initial direction of the force-feedback effect is towards the left, positive values � to the right.

## void stopForceFeedbackEffect ( Input::JOYSTICK_FORCE_FEEDBACK_EFFECT effect )

Stops application of the specified type of force-feedback effect to the joystick.
### Arguments

- *[Input::JOYSTICK_FORCE_FEEDBACK_EFFECT](../../../api/library/controls/class.input_cpp.md#JOYSTICK_FORCE_FEEDBACK_EFFECT)* **effect** - Type of a force-feedback effect.

## bool isForceFeedbackEffectPlaying ( Input::JOYSTICK_FORCE_FEEDBACK_EFFECT effect ) const

Returns the value indicating if the specified type of force-feedback effect is currently being applied.
### Arguments

- *[Input::JOYSTICK_FORCE_FEEDBACK_EFFECT](../../../api/library/controls/class.input_cpp.md#JOYSTICK_FORCE_FEEDBACK_EFFECT)* **effect** - Type of a force-feedback effect.

### Return value

true if the specified type of force-feedback effect is currently being applied, otherwise false.
