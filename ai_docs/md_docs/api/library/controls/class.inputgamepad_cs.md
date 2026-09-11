# Unigine::InputGamePad Class (CS)


The InputGamePad class represents a gamepad and contains a set of functions for handling user inputs.


## InputGamePad Class

### Enums

## MODEL_TYPE

| Name | Description |
|---|---|
| **UNKNOWN** = 0 | Unknown model. |
| **XBOX_360** = 1 | Xbox 360. |
| **XBOX_ONE** = 2 | Xbox One. |
| **PS3** = 3 | PlayStation 3. |
| **PS4** = 4 | PlayStation 4. |
| **PS5** = 5 | PlayStation 5. |

### Properties

## 🔒︎ float TriggerRightDelta

The delta value of the right trigger � the difference between the values in the previous and the current frame.
## 🔒︎ float TriggerRight

The axis state value (the position) of the right trigger. 0 means the trigger is not pressed; 1 means the trigger is pressed to the maximum.
## 🔒︎ float TriggerLeftDelta

The delta value of the left trigger � the difference between the values in the previous and the current frame.
## 🔒︎ float TriggerLeft

The axis state value (the position) of the left trigger. 0 means the trigger is not pressed; 1 means the trigger is pressed to the maximum.
## 🔒︎ vec2 AxesRightDelta

The vector of delta values of the [right thumbstick axes](../../../api/library/controls/class.inputgamepad_cs.md#getAxesRight_vec2) � the difference between the values in the previous and the current frames.
## 🔒︎ vec2 AxesRight

The vector of axes of the right thumbstick. when a thumbstick is in the center position, this value is [0,0]. The values correspond to the following thumbstick positions:
- **First value** corresponds to the **X** axis. Negative values indicate the left position; positive values indicate right.
- **Second value** corresponds to the **Y** axis. Negative values indicate the down position; positive values indicate up.


## 🔒︎ vec2 AxesLeftDelta

The vector of delta values of the [left thumbstick axes](../../../api/library/controls/class.inputgamepad_cs.md#getAxesLeft_vec2) � the difference between the values in the previous and the current frames.
## 🔒︎ vec2 AxesLeft

The vector of axes of the left thumbstick. when a thumbstick is in the center position, this value is [0,0]. The values correspond to the following thumbstick positions:
- **First value** corresponds to the **X** axis. Negative values indicate the left position; positive values indicate right.
- **Second value** corresponds to the **Y** axis. Negative values indicate the down position; positive values indicate up.


## float Filter

The filter value used to correct the current state of the analog axis (thumbsticks and triggers) relative to the previous one:
- Filter value of 0 means there is no interpolation and the current value is not corrected.
- Filter value of 1 means the previous state is used instead of the current one.


## 🔒︎ string Name

The user-friendly name of the gamepad.
## 🔒︎ int Number

The gamepad number.
## 🔒︎ bool IsAvailable

The value indicating if the gamepad is available.
## 🔒︎ InputGamePad.MODEL_TYPE ModelType

The gamepad model type identifier.
## 🔒︎ Input.DEVICE DeviceType

The device type. One of the *[Input.DEVICE_*](../../../api/library/controls/class.input_cs.md#DEVICE_UNKNOWN)* values indicating whether it is a wheel, throttle, or other device.
## 🔒︎ int PlayerIndex

The index of player for the gamepad. Some devices support connection of multiple players (e.g., XBox 360 supports up to four players connected through XBox 360 gamepads).
## 🔒︎ int NumTouches

The total number of the gamepad touch panels.
## 🔒︎ string Guid

The Device model GUID.
## 🔒︎ vec3 Acceleration

The last acceleration vector reported by the game pad accelerometer, in meters per second squared. The value includes the gravity vector while the controller is at rest and is updated from *[InputEventPadAccelerometerMotion](../../../api/library/controls/class.inputeventpadaccelerometermotion_cs.md)* events.
## 🔒︎ vec3 AngularVelocity

The last angular velocity reported by the game pad gyroscope, in degrees per second. The value is updated from *[InputEventPadGyroscopeMotion](../../../api/library/controls/class.inputeventpadgyroscopemotion_cs.md)* events.
## 🔒︎ bool IsAccelerationSupported

The value indicating if the connected controller has an accelerometer the engine can read.
## 🔒︎ bool IsAngularVelocitySupported

The value indicating if the connected controller has a gyroscope the engine can read.
## 🔒︎ bool IsLightSupported

The value indicating if the controller has a light the application can control (for example, the *DualShock 4* or *DualSense* light bar).
### Members

---

## void SetVibration ( float low_frequency , float high_frequency , float duration_ms = 100.0f )

Sets the amount of vibration for the right (high-frequency) and left (low-frequency) motors for the time period specified in milliseconds.
### Arguments

- *float* **low_frequency** - Vibration value in the [0.0f; 1.0f] range for the left (low-frequency) motor.
- *float* **high_frequency** - Vibration value in the [0.0f; 1.0f] range for the right (high-frequency) motor.
- *float* **duration_ms** - Vibration period duration, in milliseconds.

## bool IsButtonPressed ( Input.GAMEPAD_BUTTON button )

Returns a value indicating if the given button is pressed.
### Arguments

- *[Input.GAMEPAD_BUTTON](../../../api/library/controls/class.input_cs.md#GAMEPAD_BUTTON)* **button** - One of the [Input.GAMEPAD_BUTTON](../../../api/library/controls/class.input_cs.md#GAMEPAD_BUTTON) enum values.

### Return value

true if the button is pressed; otherwise, false.
## bool IsButtonDown ( Input.GAMEPAD_BUTTON button )

Returns a value indicating if the given button was pressed during the current frame.
### Arguments

- *[Input.GAMEPAD_BUTTON](../../../api/library/controls/class.input_cs.md#GAMEPAD_BUTTON)* **button** - One of the [Input.GAMEPAD_BUTTON](../../../api/library/controls/class.input_cs.md#GAMEPAD_BUTTON) enum values.

### Return value

true if the button was pressed during the current frame; otherwise, false.
## bool IsButtonUp ( Input.GAMEPAD_BUTTON button )

Returns a value indicating if the given button was released during the current frame.
### Arguments

- *[Input.GAMEPAD_BUTTON](../../../api/library/controls/class.input_cs.md#GAMEPAD_BUTTON)* **button** - One of the [Input.GAMEPAD_BUTTON](../../../api/library/controls/class.input_cs.md#GAMEPAD_BUTTON) enum values.

### Return value

true if the button was released during the current frame; otherwise, false.
## InputEventPadButton GetButtonEvent ( Input.GAMEPAD_BUTTON button )

Returns the currently processed gamepad button input event.
### Arguments

- *[Input.GAMEPAD_BUTTON](../../../api/library/controls/class.input_cs.md#GAMEPAD_BUTTON)* **button** - One of the [Input.GAMEPAD_BUTTON](../../../api/library/controls/class.input_cs.md#GAMEPAD_BUTTON) enum values.

### Return value

Gamepad button input event, or null if there are no events for the specified gamepad button in the current frame.
## int GetButtonEvents ( Input.GAMEPAD_BUTTON button , InputEventPadButton [] OUT_events )

Returns the number of input events for the specified gamepad button and puts the events to the specified output buffer.
### Arguments

- *[Input.GAMEPAD_BUTTON](../../../api/library/controls/class.input_cs.md#GAMEPAD_BUTTON)* **button** - One of the [Input.GAMEPAD_BUTTON](../../../api/library/controls/class.input_cs.md#GAMEPAD_BUTTON) enum values.
- *[InputEventPadButton](../../../api/library/controls/class.inputeventpadbutton_cs.md)[]* **OUT_events** - Buffer with input events. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of input events for the specified gamepad button.
## int GetNumTouchFingers ( int touch )

Returns the total number of the fingers supported by the specified gamepad touch panel.
### Arguments

- *int* **touch** - The index of the gamepad touch panel, the number from 0 to the [total number](#getNumTouches_int) of touch panels.

### Return value

The total number of the fingers supported by the gamepad touch panel.
## bool IsTouchPressed ( int touch , int finger )

Returns the value indicating if the given touch panel has been pressed.
### Arguments

- *int* **touch** - The index of the gamepad touch panel, the number from 0 to the [total number](#getNumTouches_int) of touch panels.
- *int* **finger** - The index of the finger, the number from 0 to the [total number](#getNumTouchFingers_int_int) of supported fingers.

### Return value

true if the touch panel is pressed, otherwise false.
## bool IsTouchDown ( int touch , int finger )

Returns a value indicating if the given touch panel has been touched during the current frame.
### Arguments

- *int* **touch** - The index of the gamepad touch panel, the number from 0 to the [total number](#getNumTouches_int) of touch panels.
- *int* **finger** - The index of the finger, the number from 0 to the [total number](#getNumTouchFingers_int_int) of supported fingers.

### Return value

true if the touch panel has been touched during the current frame, otherwise false.
## bool IsTouchUp ( int touch , int finger )

Returns a value indicating if the given touch panel has been released during the current frame.
### Arguments

- *int* **touch** - The index of the gamepad touch panel, the number from 0 to the [total number](#getNumTouches_int) of touch panels.
- *int* **finger** - The index of the finger, the number from 0 to the [total number](#getNumTouchFingers_int_int) of supported fingers.

### Return value

true if the touch panel has been released during the current frame, otherwise false.
## vec2 GetTouchPosition ( int touch , int finger )

Returns the normalized position of the touch along the axes.
### Arguments

- *int* **touch** - The index of the gamepad touch panel, the number from 0 to the [total number](#getNumTouches_int) of touch panels.
- *int* **finger** - The index of the finger, the number from 0 to the [total number](#getNumTouchFingers_int_int) of supported fingers.

### Return value

The normalized position of the touch along the axes from (0,0) to (1,1).
## vec2 GetTouchDelta ( int touch , int finger )

Returns the delta of the touch position from the previous event.
### Arguments

- *int* **touch** - The index of the gamepad touch panel, the number from 0 to the [total number](#getNumTouches_int) of touch panels.
- *int* **finger** - The index of the finger, the number from 0 to the [total number](#getNumTouchFingers_int_int) of supported fingers.

### Return value

The delta of the touch position from the previous event.
## float GetTouchPressure ( int touch , int finger )

Returns the pressure with which the finger is currently pressed against the touch panel.
### Arguments

- *int* **touch** - The index of the gamepad touch panel, the number from 0 to the [total number](#getNumTouches_int) of touch panels.
- *int* **finger** - The index of the finger, the number from 0 to the [total number](#getNumTouchFingers_int_int) of supported fingers.

### Return value

The pressure with which the finger is currently pressed, a value from 0 (not pressed) to 1 (fully pressed).
## string GetGuid ( )

Returns the GUID created on the basis of vendor and product identifiers and product version number. It enables you to identify device model (*Controller XBox One*, etc.), however, it will be the same for two identical models.
### Return value

Device model GUID.
## void SetLightColor ( vec3 color )

Sets the color of the controller's light. Has no effect if the controller has no application-controllable light (check the **[IsLightSupported](../../...md#isLightSupported_int)** property).
### Arguments

- *vec3* **color** - RGB color of the light, with components in the [0; 1] range.
