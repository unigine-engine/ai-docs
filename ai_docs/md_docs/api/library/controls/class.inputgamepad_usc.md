# Unigine::InputGamePad Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


The InputGamePad class represents a gamepad and contains a set of functions for handling user inputs.


## InputGamePad Class

### Members

---

## int getNumber ( )

Returns the gamepad number (up to four gamepads are supported).
### Return value

Gamepad number.
## string getName ( )

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

## float getFilter ( )

A filter value used to correct the current state of the analog axis (thumbsticks and triggers) relative to the previous one:
- Filter value of 0 means there is no interpolation and the current value is not corrected.
- Filter value of 1 means the previous state is used instead of the current one.


### Return value

The filter of the gamepad.
## vec2 getAxesLeft ( )

Returns a vector of axes of the left thumbstick. When a thumbstick is in the center position, this value is [0,0]. The values correspond to the following thumbstick positions:
- **First value** corresponds to the **X** axis. Negative values indicate the left position; positive values indicate right.
- **Second value** corresponds to the **Y** axis. Negative values indicate the down position; positive values indicate up.


### Return value

A vector of two values in the [-1;1] range.
## vec2 getAxesLeftDelta ( )

Returns a vector of delta values of the [left thumbstick axes](../../../api/library/controls/class.inputgamepad_usc.md#getAxesLeft_vec2) � the difference between the values in the previous and the current frames.
### Return value

Vector of delta axes.
## vec2 getAxesRight ( )

Returns a vector of axes of the right thumbstick. When a thumbstick is in the center position, this value is [0,0]. The values correspond to the following thumbstick positions:
- **First value** corresponds to the **X** axis. Negative values indicate the left position; positive values indicate right.
- **Second value** corresponds to the **Y** axis. Negative values indicate the down position; positive values indicate up.


### Return value

A vector of two values in the [-1;1] range.
## vec2 getAxesRightDelta ( )

Returns a vector of delta values of the [right thumbstick axes](../../../api/library/controls/class.inputgamepad_usc.md#getAxesRight_vec2) � the difference between the values in the previous and the current frames.
### Return value

Vector of delta axes.
## float getTriggerLeft ( )

Returns an axis state value (the position) of the left trigger. 0 means the trigger is not pressed; 1 means the trigger is pressed to the maximum.
### Return value

Value in range [0; 1].
## float getTriggerLeftDelta ( )

Returns the delta value of the left trigger � the difference between the values in the previous and the current frame.
### Return value

Left trigger delta.
## float getTriggerRight ( )

Returns an axis state value (the position) of the right trigger. 0 means the trigger is not pressed; 1 means the trigger is pressed to the maximum.
### Return value

Value in range [0; 1].
## float getTriggerRightDelta ( )

Returns the delta value of the right trigger � the difference between the values in the previous and the current frame.
### Return value

Right trigger delta.
## void setVibration ( float low_frequency , float high_frequency , float duration_ms = 100.0f )

Sets the amount of vibration for the right (high-frequency) and left (low-frequency) motors for the time period specified in milliseconds.
### Arguments

- *float* **low_frequency** - Vibration value in the [0.0f; 1.0f] range for the left (low-frequency) motor.
- *float* **high_frequency** - Vibration value in the [0.0f; 1.0f] range for the right (high-frequency) motor.
- *float* **duration_ms** - Vibration period duration, in milliseconds.

## int isAvailable ( )

Checks if the gamepad is available.
### Return value

**1** if the gamepad is available; otherwise, **0**.
## int isButtonPressed ( int button )

Returns a value indicating if the given button is pressed.
### Arguments

- *int* **button** - One of the [INPUT_GAME_PAD_BUTTON_](../../../api/library/controls/class.input_usc.md#GAMEPAD_BUTTON_A) codes.

### Return value

**1** if the button is pressed; otherwise, **0**.
## int isButtonDown ( int button )

Returns a value indicating if the given button was pressed during the current frame.
### Arguments

- *int* **button** - One of the [INPUT_GAME_PAD_BUTTON_](../../../api/library/controls/class.input_usc.md#GAMEPAD_BUTTON_A) codes.

### Return value

**1** if the button was pressed during the current frame; otherwise, **0**.
## int isButtonUp ( int button )

Returns a value indicating if the given button was released during the current frame.
### Arguments

- *int* **button** - One of the [INPUT_GAME_PAD_BUTTON_](../../../api/library/controls/class.input_usc.md#GAMEPAD_BUTTON_A) codes.

### Return value

**1** if the button was released during the current frame; otherwise, **0**.
## InputEventPadButton getButtonEvent ( int button )

Returns the currently processed gamepad button input event.
### Arguments

- *int* **button** - One of the [INPUT_GAME_PAD_BUTTON_](../../../api/library/controls/class.input_usc.md#GAMEPAD_BUTTON_A) codes.

### Return value

Gamepad button input event, or null if there are no events for the specified gamepad button in the current frame.
## int getPlayerIndex ( )

Returns the index of player for the gamepad. Some devices support connection of multiple players (e.g., XBox 360 supports up to four players connected through XBox 360 gamepads). This method enables you to get this index.
### Return value

Player index for the gamepad.
## int getDeviceType ( )

Returns a value indicating the type of the device (wheel, throttle, etc.).
### Return value

Device type. One of the *[Input::DEVICE_*](../../../api/library/controls/class.input_usc.md#DEVICE_UNKNOWN)* values.
## int getModelType ( )

Returns a value indicating the gamepad model type.
### Return value

Gamepad model type identifier.
## int getNumTouches ( )

Returns the total number of the gamepad touch panels.
### Return value

The total number of the gamepad touch panels.
## int getNumTouchFingers ( int touch )

Returns the total number of the fingers supported by the specified gamepad touch panel.
### Arguments

- *int* **touch** - The index of the gamepad touch panel, the number from 0 to the [total number](#getNumTouches_int) of touch panels.

### Return value

The total number of the fingers supported by the gamepad touch panel.
## int isTouchPressed ( int touch , int finger )

Returns the value indicating if the given touch panel has been pressed.
### Arguments

- *int* **touch** - The index of the gamepad touch panel, the number from 0 to the [total number](#getNumTouches_int) of touch panels.
- *int* **finger** - The index of the finger, the number from 0 to the [total number](#getNumTouchFingers_int_int) of supported fingers.

### Return value

**1** if the touch panel is pressed, otherwise **0**.
## int isTouchDown ( int touch , int finger )

Returns a value indicating if the given touch panel has been touched during the current frame.
### Arguments

- *int* **touch** - The index of the gamepad touch panel, the number from 0 to the [total number](#getNumTouches_int) of touch panels.
- *int* **finger** - The index of the finger, the number from 0 to the [total number](#getNumTouchFingers_int_int) of supported fingers.

### Return value

**1** if the touch panel has been touched during the current frame, otherwise **0**.
## int isTouchUp ( int touch , int finger )

Returns a value indicating if the given touch panel has been released during the current frame.
### Arguments

- *int* **touch** - The index of the gamepad touch panel, the number from 0 to the [total number](#getNumTouches_int) of touch panels.
- *int* **finger** - The index of the finger, the number from 0 to the [total number](#getNumTouchFingers_int_int) of supported fingers.

### Return value

**1** if the touch panel has been released during the current frame, otherwise **0**.
## vec2 getTouchPosition ( int touch , int finger )

Returns the normalized position of the touch along the axes.
### Arguments

- *int* **touch** - The index of the gamepad touch panel, the number from 0 to the [total number](#getNumTouches_int) of touch panels.
- *int* **finger** - The index of the finger, the number from 0 to the [total number](#getNumTouchFingers_int_int) of supported fingers.

### Return value

The normalized position of the touch along the axes from (0,0) to (1,1).
## vec2 getTouchDelta ( int touch , int finger )

Returns the delta of the touch position from the previous event.
### Arguments

- *int* **touch** - The index of the gamepad touch panel, the number from 0 to the [total number](#getNumTouches_int) of touch panels.
- *int* **finger** - The index of the finger, the number from 0 to the [total number](#getNumTouchFingers_int_int) of supported fingers.

### Return value

The delta of the touch position from the previous event.
## float getTouchPressure ( int touch , int finger )

Returns the pressure with which the finger is currently pressed against the touch panel.
### Arguments

- *int* **touch** - The index of the gamepad touch panel, the number from 0 to the [total number](#getNumTouches_int) of touch panels.
- *int* **finger** - The index of the finger, the number from 0 to the [total number](#getNumTouchFingers_int_int) of supported fingers.

### Return value

The pressure with which the finger is currently pressed, a value from 0 (not pressed) to 1 (fully pressed).
## string getGuid ( )

Returns the GUID created on the basis of vendor and product identifiers and product version number. It enables you to identify device model (*Controller XBox One*, etc.), however, it will be the same for two identical models.
### Return value

Device model GUID.
## void setLightColor ( vec3 color )

Sets the color of the controller's light. Has no effect if the controller has no application-controllable light (check the **[isLightSupported()()](../../...md#isLightSupported_int)** property).
### Arguments

- *vec3* **color** - RGB color of the light, with components in the [0; 1] range.
