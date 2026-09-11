# Unigine::InputGamePad Class (CPP)

**Header:** #include <UnigineInput.h>


The InputGamePad class represents a gamepad and contains a set of functions for handling user inputs.


### See Also


- C++ sample
- C# Component sample


## InputGamePad Class

### Enums

## MODEL_TYPE

| Name | Description |
|---|---|
| **MODEL_TYPE_UNKNOWN** = 0 | Unknown model. |
| **MODEL_TYPE_XBOX_360** = 1 | Xbox 360. |
| **MODEL_TYPE_XBOX_ONE** = 2 | Xbox One. |
| **MODEL_TYPE_PS3** = 3 | PlayStation 3. |
| **MODEL_TYPE_PS4** = 4 | PlayStation 4. |
| **MODEL_TYPE_PS5** = 5 | PlayStation 5. |

### Members

---

## int getNumber ( ) const

Returns the gamepad number (up to four gamepads are supported).
### Return value

Gamepad number.
## const char * getName ( ) const

Returns the name of the gamepad.
### Return value

User-friendly name of the gamepad. One of the following:
- GamePad
- Wheel
- Arcade Stick
- Flight Stick
- Dance Pad
- Guitar
- Drum Kit
- Unknown


## void setFilter ( float filter )

Sets a filter value used to correct the current state of the analog axis relative to the previous one. Axis states are interpolated for thumbsticks and triggers.
### Arguments

- *float* **filter** - Filter value for interpolation between axis states. The provided value is clamped to a range [0;1].

  - Filter value of 0 means there is no interpolation and the current value is not corrected.
  - Filter value of 1 means the previous state is used instead of the current one.

## float getFilter ( ) const

A filter value used to correct the current state of the analog axis (thumbsticks and triggers) relative to the previous one:
- Filter value of 0 means there is no interpolation and the current value is not corrected.
- Filter value of 1 means the previous state is used instead of the current one.


### Return value

The filter of the gamepad.
## Math:: vec2 getAxesLeft ( ) const

Returns a vector of axes of the left thumbstick. When a thumbstick is in the center position, this value is [0,0]. The values correspond to the following thumbstick positions:
- **First value** corresponds to the **X** axis. Negative values indicate the left position; positive values indicate right.
- **Second value** corresponds to the **Y** axis. Negative values indicate the down position; positive values indicate up.


### Return value

A vector of two values in the [-1;1] range.
## Math:: vec2 getAxesLeftDelta ( ) const

Returns a vector of delta values of the [left thumbstick axes](../../../api/library/controls/class.inputgamepad_cpp.md#getAxesLeft_vec2) � the difference between the values in the previous and the current frames.
### Return value

Vector of delta axes.
## Math:: vec2 getAxesRight ( ) const

Returns a vector of axes of the right thumbstick. When a thumbstick is in the center position, this value is [0,0]. The values correspond to the following thumbstick positions:
- **First value** corresponds to the **X** axis. Negative values indicate the left position; positive values indicate right.
- **Second value** corresponds to the **Y** axis. Negative values indicate the down position; positive values indicate up.


### Return value

A vector of two values in the [-1;1] range.
## Math:: vec2 getAxesRightDelta ( ) const

Returns a vector of delta values of the [right thumbstick axes](../../../api/library/controls/class.inputgamepad_cpp.md#getAxesRight_vec2) � the difference between the values in the previous and the current frames.
### Return value

Vector of delta axes.
## float getTriggerLeft ( ) const

Returns an axis state value (the position) of the left trigger. 0 means the trigger is not pressed; 1 means the trigger is pressed to the maximum.
### Return value

Value in range [0; 1].
## float getTriggerLeftDelta ( ) const

Returns the delta value of the left trigger � the difference between the values in the previous and the current frame.
### Return value

Left trigger delta.
## float getTriggerRight ( ) const

Returns an axis state value (the position) of the right trigger. 0 means the trigger is not pressed; 1 means the trigger is pressed to the maximum.
### Return value

Value in range [0; 1].
## float getTriggerRightDelta ( ) const

Returns the delta value of the right trigger � the difference between the values in the previous and the current frame.
### Return value

Right trigger delta.
## void setVibration ( float low_frequency , float high_frequency , float duration_ms = 100.0f )

Sets the amount of vibration for the right (high-frequency) and left (low-frequency) motors for the time period specified in milliseconds.
### Arguments

- *float* **low_frequency** - Vibration value in the [0.0f; 1.0f] range for the left (low-frequency) motor.
- *float* **high_frequency** - Vibration value in the [0.0f; 1.0f] range for the right (high-frequency) motor.
- *float* **duration_ms** - Vibration period duration, in milliseconds.

## bool isAvailable ( ) const

Checks if the gamepad is available.
### Return value

true if the gamepad is available; otherwise, false.
## bool isButtonPressed ( Input::GAMEPAD_BUTTON button ) const

Returns a value indicating if the given button is pressed.
### Arguments

- *[Input::GAMEPAD_BUTTON](../../../api/library/controls/class.input_cpp.md#GAMEPAD_BUTTON)* **button** - One of the preset [Input::GAMEPAD_BUTTON_](../../../api/library/controls/class.input_cpp.md#GAMEPAD_BUTTON_A) codes.

### Return value

true if the button is pressed; otherwise, false.
## bool isButtonDown ( Input::GAMEPAD_BUTTON button ) const

Returns a value indicating if the given button was pressed during the current frame.
### Arguments

- *[Input::GAMEPAD_BUTTON](../../../api/library/controls/class.input_cpp.md#GAMEPAD_BUTTON)* **button** - One of the preset [Input::GAMEPAD_BUTTON_](../../../api/library/controls/class.input_cpp.md#GAMEPAD_BUTTON_A) codes.

### Return value

true if the button was pressed during the current frame; otherwise, false.
## bool isButtonUp ( Input::GAMEPAD_BUTTON button ) const

Returns a value indicating if the given button was released during the current frame.
### Arguments

- *[Input::GAMEPAD_BUTTON](../../../api/library/controls/class.input_cpp.md#GAMEPAD_BUTTON)* **button** - One of the preset [Input::GAMEPAD_BUTTON_](../../../api/library/controls/class.input_cpp.md#GAMEPAD_BUTTON_A) codes.

### Return value

true if the button was released during the current frame; otherwise, false.
## Ptr < InputEventPadButton > getButtonEvent ( Input::GAMEPAD_BUTTON button ) const

Returns the currently processed gamepad button input event.
### Arguments

- *[Input::GAMEPAD_BUTTON](../../../api/library/controls/class.input_cpp.md#GAMEPAD_BUTTON)* **button** - One of the preset [Input::GAMEPAD_BUTTON_](../../../api/library/controls/class.input_cpp.md#GAMEPAD_BUTTON_A) codes.

### Return value

Gamepad button input event, or nullptr if there are no events for the specified gamepad button in the current frame.
## int getButtonEvents ( Input::GAMEPAD_BUTTON button , Vector < Ptr < InputEventPadButton >> & OUT_events )

Returns the number of input events for the specified gamepad button and puts the events to the specified output buffer.
### Arguments

- *[Input::GAMEPAD_BUTTON](../../../api/library/controls/class.input_cpp.md#GAMEPAD_BUTTON)* **button** - One of the preset [Input::GAMEPAD_BUTTON_](../../../api/library/controls/class.input_cpp.md#GAMEPAD_BUTTON_A) codes.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[InputEventPadButton](../../../api/library/controls/class.inputeventpadbutton_cpp.md)>> &* **OUT_events** - Buffer with input events. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of input events for the specified gamepad button.
## int getPlayerIndex ( ) const

Returns the index of player for the gamepad. Some devices support connection of multiple players (e.g., XBox 360 supports up to four players connected through XBox 360 gamepads). This method enables you to get this index.
### Return value

Player index for the gamepad.
## Input::DEVICE getDeviceType ( ) const

Returns a value indicating the type of the device (wheel, throttle, etc.).
### Return value

Device type. One of the *[Input::DEVICE_*](../../../api/library/controls/class.input_cpp.md#DEVICE_UNKNOWN)* values.
## InputGamePad::MODEL_TYPE getModelType ( ) const

Returns a value indicating the gamepad model type.
### Return value

Gamepad model type identifier.
## int getNumTouches ( ) const

Returns the total number of the gamepad touch panels.
### Return value

The total number of the gamepad touch panels.
## int getNumTouchFingers ( int touch ) const

Returns the total number of the fingers supported by the specified gamepad touch panel.
### Arguments

- *int* **touch** - The index of the gamepad touch panel, the number from 0 to the [total number](#getNumTouches_int) of touch panels.

### Return value

The total number of the fingers supported by the gamepad touch panel.
## bool isTouchPressed ( int touch , int finger ) const

Returns the value indicating if the given touch panel has been pressed.
### Arguments

- *int* **touch** - The index of the gamepad touch panel, the number from 0 to the [total number](#getNumTouches_int) of touch panels.
- *int* **finger** - The index of the finger, the number from 0 to the [total number](#getNumTouchFingers_int_int) of supported fingers.

### Return value

true if the touch panel is pressed, otherwise false.
## bool isTouchDown ( int touch , int finger ) const

Returns a value indicating if the given touch panel has been touched during the current frame.
### Arguments

- *int* **touch** - The index of the gamepad touch panel, the number from 0 to the [total number](#getNumTouches_int) of touch panels.
- *int* **finger** - The index of the finger, the number from 0 to the [total number](#getNumTouchFingers_int_int) of supported fingers.

### Return value

true if the touch panel has been touched during the current frame, otherwise false.
## bool isTouchUp ( int touch , int finger ) const

Returns a value indicating if the given touch panel has been released during the current frame.
### Arguments

- *int* **touch** - The index of the gamepad touch panel, the number from 0 to the [total number](#getNumTouches_int) of touch panels.
- *int* **finger** - The index of the finger, the number from 0 to the [total number](#getNumTouchFingers_int_int) of supported fingers.

### Return value

true if the touch panel has been released during the current frame, otherwise false.
## Math:: vec2 getTouchPosition ( int touch , int finger ) const

Returns the normalized position of the touch along the axes.
### Arguments

- *int* **touch** - The index of the gamepad touch panel, the number from 0 to the [total number](#getNumTouches_int) of touch panels.
- *int* **finger** - The index of the finger, the number from 0 to the [total number](#getNumTouchFingers_int_int) of supported fingers.

### Return value

The normalized position of the touch along the axes from (0,0) to (1,1).
## Math:: vec2 getTouchDelta ( int touch , int finger ) const

Returns the delta of the touch position from the previous event.
### Arguments

- *int* **touch** - The index of the gamepad touch panel, the number from 0 to the [total number](#getNumTouches_int) of touch panels.
- *int* **finger** - The index of the finger, the number from 0 to the [total number](#getNumTouchFingers_int_int) of supported fingers.

### Return value

The delta of the touch position from the previous event.
## float getTouchPressure ( int touch , int finger ) const

Returns the pressure with which the finger is currently pressed against the touch panel.
### Arguments

- *int* **touch** - The index of the gamepad touch panel, the number from 0 to the [total number](#getNumTouches_int) of touch panels.
- *int* **finger** - The index of the finger, the number from 0 to the [total number](#getNumTouchFingers_int_int) of supported fingers.

### Return value

The pressure with which the finger is currently pressed, a value from 0 (not pressed) to 1 (fully pressed).
## const char * getGuid ( ) const

Returns the GUID created on the basis of vendor and product identifiers and product version number. It enables you to identify device model (*Controller XBox One*, etc.), however, it will be the same for two identical models.
### Return value

Device model GUID.
## void setLightColor ( const Math:: vec3 & color )

Sets the color of the controller's light. Has no effect if the controller has no application-controllable light (check the **[isLightSupported()](../../...md#isLightSupported_int)** property).
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **color** - RGB color of the light, with components in the [0; 1] range.
