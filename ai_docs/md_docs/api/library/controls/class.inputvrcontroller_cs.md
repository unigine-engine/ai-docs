# Unigine::InputVRController Class (CS)

**Inherits from:** InputVRDevice


The class manages VR controller input, serving as the primary interface for VR input.


> **Notice:** Each instance of the InputVRController class will contain its own set of values sampled from the controller.


There are *three* types of VR controllers: *left-hand*, *right*-hand controllers, and a *treadmill*. To get the type of the VR controller, you can use the *[getControllerType()](#getControllerType_int)* function.


The class provides access to the following input:


- **Buttons** of the VR controller, including the *touch* buttons. They can be either pressed or released in the current frame or continuously pressed or touched for multiple frames in a row, including the current one.
- **Axes** of the VR controller that detect 1-dimensional movement of the control. Depending on the type of the VR controller, there can be a different number of axes. Usually, there are *3* or *4* axes. An axis can be mapped to a control of one of the supported types, also referred to as an [*axis type*](../../../api/library/controls/class.inputvrcontroller_cs.md#AXIS_TYPE). To identify the supported axes, call *[getNumAxes()](../../../api/library/controls/class.inputvrcontroller_cs.md#getNumAxes_int)*. Additionally, you can get the axis type using *[getAxisType()](../../../api/library/controls/class.inputvrcontroller_cs.md#getAxisType_int_int)*, find the axis index by its type via *[findAxisByType()](../../../api/library/controls/class.inputvrcontroller_cs.md#findAxisByType_int_int)*, or get a state value for the axis via *[getAxisByType()](../../../api/library/controls/class.inputvrcontroller_cs.md#getAxisByType_int_float)*.


> **Notice:** The article on VR Input System provides several [examples of inputs](../../../vr_development/vr_input_cs.md#openvr_input) on different types of OpenVR-supported controllers and information on buttons and axes mapping in UNIGINE.


## InputVRController Class

### Enums

## MODEL_TYPE

| Name | Description |
|---|---|
| **UNKNOWN** = 0 | Unknown controller. |
| **HTC_VIVE** = 1 | HTC Vive |
| **OCULUS_RIFT** = 2 | Oculus Rift |
| **VALVE_KNUCKLES** = 3 | Valve Index Knuckles |
| **NUM_MODEL_TYPES** = 4 | Total number of VR controller models. |

## CONTROLLER_TYPE

| Name | Description |
|---|---|
| **UNKNOWN** = 0 | Unknown controller type |
| **HAND_LEFT** = 1 | Left hand controller |
| **HAND_RIGHT** = 2 | Right hand controller |
| **TREADMILL** = 3 | Treadmill |
| **NUM_CONTROLLER_TYPES** = 4 | Total number of controller types |

## AXIS_TYPE

| Name | Description |
|---|---|
| **NONE** = 0 | Not specified |
| **TRACKPAD_X** = 1 | Trackpad X-axis. The axis range is [-1;1]. |
| **TRACKPAD_Y** = 2 | Trackpad Y-axis. The axis range is [-1;1]. |
| **TRACKPAD_FORCE** = 3 | Trackpad axis that takes into account the force value of the finger pressure. The axis range is [0;1]. |
| **JOYSTICK_X** = 4 | Joystick X-axis. The axis range is [-1;1]. |
| **JOYSTICK_Y** = 5 | Joystick Y-axis. The axis range is [-1;1]. |
| **JOYSTICK_FORCE** = 6 | Joystick axis that takes into account the force value of the finger pressure. The axis range is [0;1]. |
| **GRIP_VALUE** = 7 | Grip axis taking the value from 0 to 1. |
| **GRIP_FORCE** = 8 | Grip axis that takes into account the force value of the finger pressure exceeding 1. |
| **TRIGGER_VALUE** = 9 | Trigger axis taking the value from 0 to 1. |
| **TRIGGER_FORCE** = 10 | Trigger axis that takes into account the force value of the finger pressure exceeding 1. |
| **TRIGGER_CURL_VALUE** = 11 | Trigger curl axis taking the value from 0 to 1. |
| **TRIGGER_CURL_FORCE** = 12 | Trigger curl axis that takes into account the force value of the finger pressure exceeding 1. |
| **TRIGGER_SLIDE_VALUE** = 13 | Trigger slide axis taking the value from 0 to 1. |
| **TRIGGER_SLIDE_FORCE** = 14 | Trigger slide axis that takes into account the force value of the finger pressure exceeding 1. |
| **PINCH_VALUE** = 15 | 1D analog input component indicating the extent which the user is bringing their finger and thumb together to perform a pinch gesture (supported by WMR). |
| **GRASP_VALUE** = 16 | 1D analog input component indicating that the user is making a fist (supported by WMR). |
| **AIM_ACTIVATE_VALUE** = 17 | 1D analog input component indicating that the user activated the action on the target that the user is pointing at with the aim pose (supported by WMR). |
| **NUM_AXIS_TYPES** = 18 | Total number of axis types. |

### Properties

## 🔒︎ InputVRController.MODEL_TYPE ModelType

The model type of the VR controller.
## float Filter

The filter value used to correct the current state of the analog axis relative to the previous one. Axis states are interpolated for thumbsticks and triggers.
## 🔒︎ InputVRController.CONTROLLER_TYPE ControllerType

The the type of the VR controller.
## 🔒︎ int NumAxes

The number of axes supported by the VR controller.
## 🔒︎ ulong SupportedButtonsMask

The supported buttons for the controller.
## 🔒︎ bool IsUsingHandTracking

The value indicating if the controller uses hand tracking, i.e. hands don't hold controllers and their movements can be tracked.
> **Notice:** For OpenXR devices.


### Members

---

## InputVRController.AXIS_TYPE GetAxisType ( int axis )

Returns the type of the specified axis.
### Arguments

- *int* **axis** - Axis number.

### Return value

Axis type.
## float GetAxis ( int axis )

Returns a state value for the specified axis. It includes position of the VR controller along the following axes: X, Y (two-axis controller) and Z (three-axis controller). When the VR controller is in the center position, X and Y axes values are zero. Negative values indicate left or down; positive values indicate right or up.
### Arguments

- *int* **axis** - Axis number.

### Return value

Value in range [-1.0f; 1.0f].
## float GetAxisDelta ( int axis )

Returns the axis delta � the difference between a new and the current state of the specified axis.
### Arguments

- *int* **axis** - Axis number.

### Return value

Value in range [-1.0f; 1.0f].
## bool IsButtonPressed ( Input.VR_BUTTON button )

Returns a value indicating if the specified button is pressed. Check this value to perform continuous actions.
### Arguments

- *[Input.VR_BUTTON](../../../api/library/controls/class.input_cs.md#VR_BUTTON)* **button** - Button.

### Return value

true if the button is pressed; otherwise, false.
## bool IsButtonDown ( Input.VR_BUTTON button )

Returns a value indicating if the specified button was pressed during the current frame.
### Arguments

- *[Input.VR_BUTTON](../../../api/library/controls/class.input_cs.md#VR_BUTTON)* **button** - Button.

### Return value

true if the button was pressed; otherwise, false.
## bool IsButtonUp ( Input.VR_BUTTON button )

Returns a value indicating if the specified button was released during the current frame.
### Arguments

- *[Input.VR_BUTTON](../../../api/library/controls/class.input_cs.md#VR_BUTTON)* **button** - Button.

### Return value

true if the button was released; otherwise, false.
## bool IsButtonTouchPressed ( Input.VR_BUTTON touch )

Returns a value indicating if the specified button is touched.
### Arguments

- *[Input.VR_BUTTON](../../../api/library/controls/class.input_cs.md#VR_BUTTON)* **touch** - Button.

### Return value

true if the button is touched; otherwise, false.
## bool IsButtonTouchDown ( Input.VR_BUTTON touch )

Returns a value indicating if the specified touch button was "pressed" in the currect frame.
### Arguments

- *[Input.VR_BUTTON](../../../api/library/controls/class.input_cs.md#VR_BUTTON)* **touch** -

### Return value

true if the touch button was "pressed"; otherwise, false.
## bool IsButtonTouchUp ( Input.VR_BUTTON touch )

Returns a value indicating if the specified touch button was "released" in the currect frame.
### Arguments

- *[Input.VR_BUTTON](../../../api/library/controls/class.input_cs.md#VR_BUTTON)* **touch** -

### Return value

true if the touch button was "released"; otherwise, false.
## InputEventVRButton GetButtonEvent ( Input.VR_BUTTON button )

Returns the currently processed VR controller button input event.
### Arguments

- *[Input.VR_BUTTON](../../../api/library/controls/class.input_cs.md#VR_BUTTON)* **button** - Button.

### Return value

VR controller button input event, or null if there are no events for the specified button in the current frame.
## int GetButtonEvents ( Input.VR_BUTTON button , InputEventVRButton [] OUT_events )

Returns the number of input events for the specified VR controller button and puts the events to the specified output buffer.
### Arguments

- *[Input.VR_BUTTON](../../../api/library/controls/class.input_cs.md#VR_BUTTON)* **button** - Button.
- *[InputEventVRButton](../../../api/library/controls/class.inputeventvrbutton_cs.md)[]* **OUT_events** - Buffer with button input events. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of input events for the specified VR controller button.
## InputEventVRButtonTouch GetButtonTouchEvent ( Input.VR_BUTTON button )

Returns the currently processed VR controller button touch event.
### Arguments

- *[Input.VR_BUTTON](../../../api/library/controls/class.input_cs.md#VR_BUTTON)* **button** - Button.

### Return value

VR controller button touch event, or null if there are no events for the specified touch button in the current frame.
## int GetButtonTouchEvents ( Input.VR_BUTTON button , InputEventVRButtonTouch [] OUT_events )

Returns the number of touch events for the specified VR controller touch button and puts the events to the specified output buffer.
### Arguments

- *[Input.VR_BUTTON](../../../api/library/controls/class.input_cs.md#VR_BUTTON)* **button** - Button.
- *[InputEventVRButtonTouch](../../../api/library/controls/class.inputeventvrbuttontouch_cs.md)[]* **OUT_events** - Buffer with button touch events. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of input events for the specified VR controller touch button.
## void StopHaptic ( )

Stops the vibration feedback.
## void ApplyHaptic ( float amplitude = -1 , double duration_ms = -1 , float frequency_hz = -1 )

Applies the vibration feedback with the specified amplitude, duration and frequency parameters.
### Arguments

- *float* **amplitude** - Amplitude of vibration between 0.0 and 1.0.
- *double* **duration_ms** - Duration of the vibration, in milliseconds.
- *float* **frequency_hz** - Frequency of the vibration in Hz.

## float GetAxisByType ( InputVRController.AXIS_TYPE axis_type )

Returns a state value for the axis of the specified type. It includes position of the VR controller along the X and Y axes (a two-axis controller). The return value depends on the [axis type](#AXIS_TYPE).
### Arguments

- *[InputVRController.AXIS_TYPE](../../../api/library/controls/class.inputvrcontroller_cs.md#AXIS_TYPE)* **axis_type** - Axis type.

### Return value

Value in range [-1.0f;1.0f].
## int FindAxisByType ( InputVRController.AXIS_TYPE axis_type )

Returns the index of the axis by its type.
### Arguments

- *[InputVRController.AXIS_TYPE](../../../api/library/controls/class.inputvrcontroller_cs.md#AXIS_TYPE)* **axis_type** - Axis type.

### Return value

Axis index.
