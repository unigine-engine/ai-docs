# Unigine::InputEvent Class (CS)


This class handles input event information.


## InputEvent Class

### Enums

## TYPE

| Name | Description |
|---|---|
| **INPUT_EVENT** = 0 | Basic type. Cannot be created. |
| **INPUT_EVENT_MOUSE_BUTTON** = 1 | Mouse button has been clicked. |
| **INPUT_EVENT_MOUSE_WHEEL** = 2 | Mouse wheel has been moved. |
| **INPUT_EVENT_MOUSE_MOTION** = 3 | Mouse has been moved. |
| **INPUT_EVENT_KEYBOARD** = 4 | Keyboard button has been pressed. |
| **INPUT_EVENT_TEXT** = 5 | Text has been entered. |
| **INPUT_EVENT_TOUCH** = 6 | Touch device has been touched. |
| **INPUT_EVENT_JOY_DEVICE** = 7 | Joystick has been connected or disconnected. |
| **INPUT_EVENT_JOY_BUTTON** = 8 | Joystick button has been pressed. |
| **INPUT_EVENT_JOY_AXIS_MOTION** = 9 | Joystick axis has been moved. |
| **INPUT_EVENT_JOY_POV_MOTION** = 10 | Joystick POV hat has been moved. |
| **INPUT_EVENT_PAD_DEVICE** = 11 | Game pad has been connected or disconnected. |
| **INPUT_EVENT_PAD_BUTTON** = 12 | Game pad button has been pressed. |
| **INPUT_EVENT_PAD_AXIS_MOTION** = 13 | Game pad axis has been moved. |
| **INPUT_EVENT_PAD_TOUCH_MOTION** = 14 | Touch panel has been touched. |
| **INPUT_EVENT_PAD_ACCELEROMETER_MOTION** = 15 | Game pad accelerometer has reported a new state (see the *[InputEventPadAccelerometerMotion](../../../api/library/controls/class.inputeventpadaccelerometermotion_cs.md)* class). |
| **INPUT_EVENT_PAD_GYROSCOPE_MOTION** = 16 | Game pad gyroscope has reported a new state (see the *[InputEventPadGyroscopeMotion](../../../api/library/controls/class.inputeventpadgyroscopemotion_cs.md)* class). |
| **INPUT_EVENT_VR_DEVICE** = 17 | VR device has been connected or disconnected. |
| **INPUT_EVENT_VR_BUTTON** = 18 | VR device button has been pressed. |
| **INPUT_EVENT_VR_BUTTON_TOUCH** = 19 | VR device button has been touched. |
| **INPUT_EVENT_VR_AXIS_MOTION** = 20 | VR device axis has been moved. |
| **INPUT_EVENT_SYSTEM** = 21 | System event has occurred (keyboard layout or input language has changed). |
| **INPUT_EVENT_TEXT_EDITING** = 22 | IME text composition (preedit) has been updated (see the *[InputEventTextEditing](../../../api/library/controls/class.inputeventtextediting_cs.md)* class). |
| **NUM_INPUT_EVENTS** = 23 | Counter of input events. |

### Properties

## 🔒︎ ulong Frame

The engine frame during which the event has been sent from proxy to Input.
## ivec2 MousePosition

The position of the mouse.
## ulong Timestamp

The timestamp of the event, in milliseconds.
## 🔒︎ InputEvent.TYPE Type

The type of the input event, one of the [INPUT_EVENT](#TYPE) values.
## 🔒︎ string TypeName

The name of the input event type.
### Members

---
