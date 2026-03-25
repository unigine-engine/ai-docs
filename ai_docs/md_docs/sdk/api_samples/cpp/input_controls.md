# Input Handling

> **Notice:** The complete sample source code is available on GitHub:
> **[github.com/unigine-engine/cpp-api-samples](https://github.com/unigine-engine/cpp-api-samples)**.


## Gamepad

This sample demostrates the simple usage of Gamepad input.
**SDK Path:***<SAMPLES_PROJECT_PATH>/source/input_handling/gamepad*

## Joystick

This sample demonstrates how to add advanced **[joystick](../../../api/library/controls/class.inputjoystick_cpp.md)** input handling, supporting multiple controllers with real-time axis/button monitoring and force feedback effects in UNIGINE. It features dynamic UI for testing 10+ force feedback types (springs, vibrations, waves) and automatically handles device connection/disconnection events. Ideal for racing/flight simulators or any project requiring precise controller input with haptic feedback.
**SDK Path:***<SAMPLES_PROJECT_PATH>/source/input_handling/joystick*

## Keyboard And Mouse

This sample demonstrates how to add monitoring of keyboard and mouse input, tracking key states, mouse movements, wheel events, and cursor positions across different coordinate systems. It displays real-time input data including key presses, mouse deltas, and text input. The sample shows three mouse handling modes:


- **GRAB** - locks and hides the cursor
- **SOFT** - locks the cursor to the window but keeps it visible
- **USER** - no cursor restrictions.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/input_handling/keyboard_and_mouse*
## Touch

This sample demonstrates how to add multi-touch input from the **[touchscreen](../../../api/library/controls/class.input_cpp.md)**, visualizing finger positions with dynamic circles and displaying real-time coordinates to the project.
**SDK Path:***<SAMPLES_PROJECT_PATH>/source/input_handling/touch*
