# Unigine::InputEventVRButtonTouch Class (CPP)

**Header:** #include <UnigineInput.h>

**Inherits from:** InputEvent


This class controls VR controller button touch event information.


Events of this type are created by the engine and passed to your handlers. You can also construct one yourself and dispatch it via *[Input::sendEvent()](../../../api/library/controls/class.input_cpp.md#sendEvent_InputEvent_void)*, which is what a custom SystemProxy implementation or a device emulator does.


## InputEventVRButtonTouch Class

### Enums

## ACTION

| Name | Description |
|---|---|
| **ACTION_DOWN** = 0 | The button is being touched. |
| **ACTION_UP** = 1 | The button is no longer touched. |

### Members

---

## InputEventVRButtonTouch ( )

Default constructor.
## InputEventVRButtonTouch ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos )

VR controller button touch input event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.

## InputEventVRButtonTouch ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos , InputEventVRButtonTouch::ACTION action , int connection_id , Input::VR_BUTTON button )

VR controller button touch input event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.
- *[InputEventVRButtonTouch::ACTION](../../../api/library/controls/class.inputeventvrbuttontouch_cpp.md#ACTION)* **action** - Type of the VR controller button touch input event, one of the [ACTION_*](#ACTION_DOWN) values.
- *int* **connection_id** - Connection identifier.
- *[Input::VR_BUTTON](../../../api/library/controls/class.input_cpp.md#VR_BUTTON)* **button** - VR controller button touch index.

## void setAction ( InputEventVRButtonTouch::ACTION action )

Sets the action the event represents. See *[getAction()](../../...md#getAction_int)*.
### Arguments

- *[InputEventVRButtonTouch::ACTION](../../../api/library/controls/class.inputeventvrbuttontouch_cpp.md#ACTION)* **action** - Type of the VR controller button touch input event, one of the [ACTION_*](#ACTION_DOWN) values.

## InputEventVRButtonTouch::ACTION getAction ( ) const

Returns the action the event represents: one of the [ACTION](#ACTION) values � the button was touched or the touch ended. This event reports capacitive touch, which the hardware detects before the button is actually pressed; presses are reported by [InputEventVRButton](../../../api/library/controls/class.inputeventvrbutton_cpp.md).
### Return value

Type of the VR controller button touch input event, one of the [ACTION_*](#ACTION_DOWN) values.
## void setConnectionID ( int connectionid )

Sets the identifier of the device connection the event comes from. See *[getConnectionID()](../../...md#getConnectionID_int)*.
### Arguments

- *int* **connectionid** - Connection identifier.

## int getConnectionID ( ) const

Returns the identifier of the device connection the event comes from � the value assigned by the OS when the device was connected. The engine uses it to match the event against a device slot; it is not the slot index itself.
### Return value

Connection identifier.
## void setButton ( Input::VR_BUTTON button )

Sets the VR controller button the event refers to. See *[getButton()](../../...md#getButton_int)*.
### Arguments

- *[Input::VR_BUTTON](../../../api/library/controls/class.input_cpp.md#VR_BUTTON)* **button** - VR controller button index.

## Input::VR_BUTTON getButton ( ) const

Returns the VR controller button the event refers to � one of the [Input::VR_BUTTON](../../../api/library/controls/class.input_cpp.md#VR_BUTTON) values. Not every button reports touch: it is available only for the components the hardware exposes a touch sensor for.
### Return value

VR controller button index.
