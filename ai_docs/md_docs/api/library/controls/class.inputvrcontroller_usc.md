# Unigine::InputVRController Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** InputVRDevice


The class manages VR controller input, serving as the primary interface for VR input.


> **Notice:** Each instance of the InputVRController class will contain its own set of values sampled from the controller.


There are *three* types of VR controllers: *left-hand*, *right*-hand controllers, and a *treadmill*. To get the type of the VR controller, you can use the *[getControllerType()](#getControllerType_int)* function.


The class provides access to the following input:


- **Buttons** of the VR controller, including the *touch* buttons. They can be either pressed or released in the current frame or continuously pressed or touched for multiple frames in a row, including the current one.
- **Axes** of the VR controller that detect 1-dimensional movement of the control. Depending on the type of the VR controller, there can be a different number of axes. Usually, there are *3* or *4* axes. An axis can be mapped to a control of one of the supported types, also referred to as an [*axis type*](../../../api/library/controls/class.inputvrcontroller_usc.md#AXIS_TYPE). To identify the supported axes, call *[getNumAxes()](../../../api/library/controls/class.inputvrcontroller_usc.md#getNumAxes_int)*. Additionally, you can get the axis type using *[getAxisType()](../../../api/library/controls/class.inputvrcontroller_usc.md#getAxisType_int_int)*, find the axis index by its type via *[findAxisByType()](../../../api/library/controls/class.inputvrcontroller_usc.md#findAxisByType_int_int)*, or get a state value for the axis via *[getAxisByType()](../../../api/library/controls/class.inputvrcontroller_usc.md#getAxisByType_int_float)*.


> **Notice:** The article on VR Input System provides several [examples of inputs](../../../vr_development/vr_input.md#openvr_input) on different types of OpenVR-supported controllers and information on buttons and axes mapping in UNIGINE.


## InputVRController Class

### Members

## int getModelType () const

Returns the current model type of the VR controller.
### Return value

Current controller model type.
## void setFilter ( float filter )

Sets a new filter value used to correct the current state of the analog axis relative to the previous one. Axis states are interpolated for thumbsticks and triggers.
### Arguments

- *float* **filter** - The filter value for interpolation between axis states. The provided value is clamped to a range [0.0;1.0].

  - Filter value of 0.0 means there is no interpolation and the current value is not corrected.
  - Filter value of 1.0 means the previous state is used instead of the current one.

## float getFilter () const

Returns the current filter value used to correct the current state of the analog axis relative to the previous one. Axis states are interpolated for thumbsticks and triggers.
### Return value

Current filter value for interpolation between axis states. The provided value is clamped to a range [0.0;1.0].
- Filter value of 0.0 means there is no interpolation and the current value is not corrected.
- Filter value of 1.0 means the previous state is used instead of the current one.


## int getControllerType () const

Returns the current the type of the VR controller.
### Return value

Current Controller type.
## int getNumAxes () const

Returns the current number of axes supported by the VR controller.
### Return value

Current number of axes.
## getSupportedButtonsMask () const

Returns the current
### Return value

Current Supported buttons mask.
## int isUsingHandTracking () const

Returns the current value indicating if the controller uses hand tracking, i.e. hands don't hold controllers and their movements can be tracked.
> **Notice:** For OpenXR devices.


### Return value

Current hand tracking is used (no controllers are held in hands)
---

## int getAxisType ( int axis )

Returns the type of the specified axis.
### Arguments

- *int* **axis** - Axis number.

### Return value

Axis type.
## float getAxis ( int axis )

Returns a state value for the specified axis. It includes position of the VR controller along the following axes: X, Y (two-axis controller) and Z (three-axis controller). When the VR controller is in the center position, X and Y axes values are zero. Negative values indicate left or down; positive values indicate right or up.
### Arguments

- *int* **axis** - Axis number.

### Return value

Value in range [-1.0f; 1.0f].
## float getAxisDelta ( int axis )

Returns the axis delta � the difference between a new and the current state of the specified axis.
### Arguments

- *int* **axis** - Axis number.

### Return value

Value in range [-1.0f; 1.0f].
## int isButtonPressed ( int button )

Returns a value indicating if the specified button is pressed. Check this value to perform continuous actions.
### Arguments

- *int* **button** - Button.

### Return value

true if the button is pressed; otherwise, false.
## int isButtonDown ( int button )

Returns a value indicating if the specified button was pressed during the current frame.
### Arguments

- *int* **button** - Button.

### Return value

true if the button was pressed; otherwise, false.
## int isButtonUp ( int button )

Returns a value indicating if the specified button was released during the current frame.
### Arguments

- *int* **button** - Button.

### Return value

true if the button was released; otherwise, false.
## int isButtonTouchPressed ( int touch )

Returns a value indicating if the specified button is touched.
### Arguments

- *int* **touch** - Button.

### Return value

true if the button is touched; otherwise, false.
## int isButtonTouchDown ( int touch )

Returns a value indicating if the specified touch button was "pressed" in the currect frame.
### Arguments

- *int* **touch** -

### Return value

true if the touch button was "pressed"; otherwise, false.
## int isButtonTouchUp ( int touch )

Returns a value indicating if the specified touch button was "released" in the currect frame.
### Arguments

- *int* **touch** -

### Return value

true if the touch button was "released"; otherwise, false.
## InputEventVRButton getButtonEvent ( int button )

Returns the currently processed VR controller button input event.
### Arguments

- *int* **button** - Button.

### Return value

## InputEventVRButtonTouch getButtonTouchEvent ( int button )

Returns the currently processed VR controller button touch event.
### Arguments

- *int* **button** - Button.

### Return value

## void stopHaptic ( )

Stops the vibration feedback.
## void applyHaptic ( float amplitude = -1 , double duration_ms = -1 , float frequency_hz = -1 )

Applies the vibration feedback with the specified amplitude, duration and frequency parameters.
### Arguments

- *float* **amplitude** - Amplitude of vibration between 0.0 and 1.0.
- *double* **duration_ms** - Duration of the vibration, in milliseconds.
- *float* **frequency_hz** - Frequency of the vibration in Hz.

## float getAxisByType ( int axis_type )

Returns a state value for the axis of the specified type. It includes position of the VR controller along the X and Y axes (a two-axis controller). The return value depends on the [axis type](#AXIS_TYPE).
### Arguments

- *int* **axis_type** - Axis type.

### Return value

Value in range [-1.0f;1.0f].
## int findAxisByType ( int axis_type )

Returns the index of the axis by its type.
### Arguments

- *int* **axis_type** - Axis type.

### Return value

Axis index.
