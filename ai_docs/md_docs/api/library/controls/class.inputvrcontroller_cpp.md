# Unigine::InputVRController Class (CPP)

**Header:** #include <UnigineInput.h>

**Inherits from:** InputVRDevice


The class manages VR controller input, serving as the primary interface for VR input.


> **Notice:** Each instance of the InputVRController class will contain its own set of values sampled from the controller.


There are *three* types of VR controllers: *left-hand*, *right*-hand controllers, and a *treadmill*. To get the type of the VR controller, you can use the *[getControllerType()](#getControllerType_int)* function.


The class provides access to the following input:


- **Buttons** of the VR controller, including the *touch* buttons. They can be either pressed or released in the current frame or continuously pressed or touched for multiple frames in a row, including the current one.
- **Axes** of the VR controller that detect 1-dimensional movement of the control. Depending on the type of the VR controller, there can be a different number of axes. Usually, there are *3* or *4* axes. An axis can be mapped to a control of one of the supported types, also referred to as an [*axis type*](../../../api/library/controls/class.inputvrcontroller_cpp.md#AXIS_TYPE). To identify the supported axes, call *[getNumAxes()](../../../api/library/controls/class.inputvrcontroller_cpp.md#getNumAxes_int)*. Additionally, you can get the axis type using *[getAxisType()](../../../api/library/controls/class.inputvrcontroller_cpp.md#getAxisType_int_int)*, find the axis index by its type via *[findAxisByType()](../../../api/library/controls/class.inputvrcontroller_cpp.md#findAxisByType_int_int)*, or get a state value for the axis via *[getAxisByType()](../../../api/library/controls/class.inputvrcontroller_cpp.md#getAxisByType_int_float)*.


> **Notice:** The article on VR Input System provides several [examples of inputs](../../../vr_development/vr_input_cpp.md#openvr_input) on different types of OpenVR-supported controllers and information on buttons and axes mapping in UNIGINE.


## InputVRController Class

### Enums

## MODEL_TYPE

| Name | Description |
|---|---|
| **MODEL_TYPE_UNKNOWN** = 0 | Unknown controller. |
| **MODEL_TYPE_HTC_VIVE** = 1 | HTC Vive |
| **MODEL_TYPE_OCULUS_RIFT** = 2 | Oculus Rift |
| **MODEL_TYPE_VALVE_KNUCKLES** = 3 | Valve Index Knuckles |
| **NUM_MODEL_TYPES** = 4 | Total number of VR controller models. |

## CONTROLLER_TYPE

| Name | Description |
|---|---|
| **CONTROLLER_TYPE_UNKNOWN** = 0 | Unknown controller type |
| **CONTROLLER_TYPE_HAND_LEFT** = 1 | Left hand controller |
| **CONTROLLER_TYPE_HAND_RIGHT** = 2 | Right hand controller |
| **CONTROLLER_TYPE_TREADMILL** = 3 | Treadmill |
| **NUM_CONTROLLER_TYPES** = 4 | Total number of controller types |

## AXIS_TYPE

| Name | Description |
|---|---|
| **AXIS_TYPE_NONE** = 0 | Not specified |
| **AXIS_TYPE_TRACKPAD_X** = 1 | Trackpad X-axis. The axis range is [-1;1]. |
| **AXIS_TYPE_TRACKPAD_Y** = 2 | Trackpad Y-axis. The axis range is [-1;1]. |
| **AXIS_TYPE_TRACKPAD_FORCE** = 3 | Trackpad axis that takes into account the force value of the finger pressure. The axis range is [0;1]. |
| **AXIS_TYPE_JOYSTICK_X** = 4 | Joystick X-axis. The axis range is [-1;1]. |
| **AXIS_TYPE_JOYSTICK_Y** = 5 | Joystick Y-axis. The axis range is [-1;1]. |
| **AXIS_TYPE_JOYSTICK_FORCE** = 6 | Joystick axis that takes into account the force value of the finger pressure. The axis range is [0;1]. |
| **AXIS_TYPE_GRIP_VALUE** = 7 | Grip axis taking the value from 0 to 1. |
| **AXIS_TYPE_GRIP_FORCE** = 8 | Grip axis that takes into account the force value of the finger pressure exceeding 1. |
| **AXIS_TYPE_TRIGGER_VALUE** = 9 | Trigger axis taking the value from 0 to 1. |
| **AXIS_TYPE_TRIGGER_FORCE** = 10 | Trigger axis that takes into account the force value of the finger pressure exceeding 1. |
| **AXIS_TYPE_TRIGGER_CURL_VALUE** = 11 | Trigger curl axis taking the value from 0 to 1. |
| **AXIS_TYPE_TRIGGER_CURL_FORCE** = 12 | Trigger curl axis that takes into account the force value of the finger pressure exceeding 1. |
| **AXIS_TYPE_TRIGGER_SLIDE_VALUE** = 13 | Trigger slide axis taking the value from 0 to 1. |
| **AXIS_TYPE_TRIGGER_SLIDE_FORCE** = 14 | Trigger slide axis that takes into account the force value of the finger pressure exceeding 1. |
| **AXIS_TYPE_PINCH_VALUE** = 15 | 1D analog input component indicating the extent which the user is bringing their finger and thumb together to perform a pinch gesture (supported by WMR). |
| **AXIS_TYPE_GRASP_VALUE** = 16 | 1D analog input component indicating that the user is making a fist (supported by WMR). |
| **AXIS_TYPE_AIM_ACTIVATE_VALUE** = 17 | 1D analog input component indicating that the user activated the action on the target that the user is pointing at with the aim pose (supported by WMR). |
| **NUM_AXIS_TYPES** = 18 | Total number of axis types. |

### Members

## InputVRController::MODEL_TYPE getModelType () const

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


## InputVRController::CONTROLLER_TYPE getControllerType () const

Returns the current the type of the VR controller.
### Return value

Current Controller type.
## int getNumAxes () const

Returns the current number of axes supported by the VR controller.
### Return value

Current number of axes.
## unsigned long long getSupportedButtonsMask () const

Returns the current supported buttons for the controller. For exaple, you can get the supported buttons and check if a specific button is available:
```cpp
InputVRControllerPtr device = Input::getVRControllerLeft();

// check if there is the X button on the controller
if (device->getSupportedButtonsMask() & (1ull << uint64_t(Input::VR_BUTTON_X)))
	return device->isButtonPressed(Input::VR_BUTTON_X);

```


### Return value

Current Supported buttons mask.
## bool isUsingHandTracking () const

Returns the current value indicating if the controller uses hand tracking, i.e. hands don't hold controllers and their movements can be tracked.
> **Notice:** For OpenXR devices.


### Return value

**true** if hand tracking is used (no controllers are held in hands); otherwise **false**.
---

## InputVRController::AXIS_TYPE getAxisType ( int axis ) const

Returns the type of the specified axis.
### Arguments

- *int* **axis** - Axis number.

### Return value

Axis type.
## float getAxis ( int axis ) const

Returns a state value for the specified axis. It includes position of the VR controller along the following axes: X, Y (two-axis controller) and Z (three-axis controller). When the VR controller is in the center position, X and Y axes values are zero. Negative values indicate left or down; positive values indicate right or up.
### Arguments

- *int* **axis** - Axis number.

### Return value

Value in range [-1.0f; 1.0f].
## float getAxisDelta ( int axis ) const

Returns the axis delta � the difference between a new and the current state of the specified axis.
### Arguments

- *int* **axis** - Axis number.

### Return value

Value in range [-1.0f; 1.0f].
## bool isButtonPressed ( Input::VR_BUTTON button ) const

Returns a value indicating if the specified button is pressed. Check this value to perform continuous actions.
### Arguments

- *[Input::VR_BUTTON](../../../api/library/controls/class.input_cpp.md#VR_BUTTON)* **button** - Button.

### Return value

true if the button is pressed; otherwise, false.
## bool isButtonDown ( Input::VR_BUTTON button ) const

Returns a value indicating if the specified button was pressed during the current frame.
### Arguments

- *[Input::VR_BUTTON](../../../api/library/controls/class.input_cpp.md#VR_BUTTON)* **button** - Button.

### Return value

true if the button was pressed; otherwise, false.
## bool isButtonUp ( Input::VR_BUTTON button ) const

Returns a value indicating if the specified button was released during the current frame.
### Arguments

- *[Input::VR_BUTTON](../../../api/library/controls/class.input_cpp.md#VR_BUTTON)* **button** - Button.

### Return value

true if the button was released; otherwise, false.
## bool isButtonTouchPressed ( Input::VR_BUTTON touch ) const

Returns a value indicating if the specified button is touched.
### Arguments

- *[Input::VR_BUTTON](../../../api/library/controls/class.input_cpp.md#VR_BUTTON)* **touch** - Button.

### Return value

true if the button is touched; otherwise, false.
## bool isButtonTouchDown ( Input::VR_BUTTON touch ) const

Returns a value indicating if the specified touch button was "pressed" in the currect frame.
### Arguments

- *[Input::VR_BUTTON](../../../api/library/controls/class.input_cpp.md#VR_BUTTON)* **touch** -

### Return value

true if the touch button was "pressed"; otherwise, false.
## bool isButtonTouchUp ( Input::VR_BUTTON touch ) const

Returns a value indicating if the specified touch button was "released" in the currect frame.
### Arguments

- *[Input::VR_BUTTON](../../../api/library/controls/class.input_cpp.md#VR_BUTTON)* **touch** -

### Return value

true if the touch button was "released"; otherwise, false.
## Ptr < InputEventVRButton > getButtonEvent ( Input::VR_BUTTON button ) const

Returns the currently processed VR controller button input event.
### Arguments

- *[Input::VR_BUTTON](../../../api/library/controls/class.input_cpp.md#VR_BUTTON)* **button** - Button.

### Return value

VR controller button input event, or nullptr if there are no events for the specified button in the current frame.
## int getButtonEvents ( Input::VR_BUTTON button , Vector < Ptr < InputEventVRButton >> & OUT_events )

Returns the number of input events for the specified VR controller button and puts the events to the specified output buffer.
### Arguments

- *[Input::VR_BUTTON](../../../api/library/controls/class.input_cpp.md#VR_BUTTON)* **button** - Button.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[InputEventVRButton](../../../api/library/controls/class.inputeventvrbutton_cpp.md)>> &* **OUT_events** - Buffer with button input events. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of input events for the specified VR controller button.
## Ptr < InputEventVRButtonTouch > getButtonTouchEvent ( Input::VR_BUTTON button ) const

Returns the currently processed VR controller button touch event.
### Arguments

- *[Input::VR_BUTTON](../../../api/library/controls/class.input_cpp.md#VR_BUTTON)* **button** - Button.

### Return value

VR controller button touch event, or nullptr if there are no events for the specified touch button in the current frame.
## int getButtonTouchEvents ( Input::VR_BUTTON button , Vector < Ptr < InputEventVRButtonTouch >> & OUT_events )

Returns the number of touch events for the specified VR controller touch button and puts the events to the specified output buffer.
### Arguments

- *[Input::VR_BUTTON](../../../api/library/controls/class.input_cpp.md#VR_BUTTON)* **button** - Button.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[InputEventVRButtonTouch](../../../api/library/controls/class.inputeventvrbuttontouch_cpp.md)>> &* **OUT_events** - Buffer with button touch events. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of input events for the specified VR controller touch button.
## void stopHaptic ( )

Stops the vibration feedback.
## void applyHaptic ( float amplitude = -1 , double duration_ms = -1 , float frequency_hz = -1 )

Applies the vibration feedback with the specified amplitude, duration and frequency parameters.
### Arguments

- *float* **amplitude** - Amplitude of vibration between 0.0 and 1.0.
- *double* **duration_ms** - Duration of the vibration, in milliseconds.
- *float* **frequency_hz** - Frequency of the vibration in Hz.

## float getAxisByType ( InputVRController::AXIS_TYPE axis_type ) const

Returns a state value for the axis of the specified type. It includes position of the VR controller along the X and Y axes (a two-axis controller). The return value depends on the [axis type](#AXIS_TYPE).
### Arguments

- *[InputVRController::AXIS_TYPE](../../../api/library/controls/class.inputvrcontroller_cpp.md#AXIS_TYPE)* **axis_type** - Axis type.

### Return value

Value in range [-1.0f;1.0f].
## int findAxisByType ( InputVRController::AXIS_TYPE axis_type ) const

Returns the index of the axis by its type.
### Arguments

- *[InputVRController::AXIS_TYPE](../../../api/library/controls/class.inputvrcontroller_cpp.md#AXIS_TYPE)* **axis_type** - Axis type.

### Return value

Axis index.
