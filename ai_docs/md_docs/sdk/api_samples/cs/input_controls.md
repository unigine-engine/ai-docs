# Input Handling

> **Notice:** The complete sample source code is available on GitHub:
> **[github.com/unigine-engine/csharp-component-samples](https://github.com/unigine-engine/csharp-component-samples)**.


## Input Gamepad

This sample demonstrates how to add input from the gamepad to the project.
**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/input_handling/input_gamepad*

## Input Joystick

This sample demonstrates how to add advanced joystick input handling to a project using the *InputJoystick.cs* component assigned to **[NodeDummy](../../../objects/nodes/dummy/index.md)**, supporting multiple controllers with real-time axis/button monitoring and force feedback effects in UNIGINE.


It features a **dynamic UI for testing 10+ force feedback types** (springs, vibrations, waves) and automatically handles device connection/disconnection events.


**Use Cases:**


Ideal for racing/flight simulators or any project requiring precise controller input with haptic feedback.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/input_handling/input_joystick*
## Input Keyboard And Mouse

This sample demonstrates how to add monitoring of keyboard and mouse input, tracking key states, mouse movements, wheel events, and cursor positions across different coordinate systems using the *InputKeyboardAndMouse.cs* component assigned to **[NodeDummy](../../../objects/nodes/dummy/index.md)**. It displays real-time input data including key presses, mouse deltas, and text input.


The sample shows three mouse handling modes:


- **GRAB** - locks and hides the cursor
- **SOFT** - locks the cursor to the window but keeps it visible
- **USER** - leaves mouse behavior completely under user control.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/input_handling/input_keyboard_mouse*
## Touch

This sample demonstrates how to add multi-touch input from the ***[touchscreen](../../../api/library/controls/class.input_cpp.md)***, visualizing finger positions with dynamic circles and displaying real-time coordinates to the project using the *InputTouches.cs* component assigned to **[NodeDummy](../../../objects/nodes/dummy/index.md)**.
**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/input_handling/touch*
