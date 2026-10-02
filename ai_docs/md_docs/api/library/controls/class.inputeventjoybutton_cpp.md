# Unigine::InputEventJoyButton Class (CPP)

**Header:** #include <UnigineInput.h>

**Inherits from:** InputEvent


This class controls joystick button event information.


Events of this type are created by the engine and passed to your handlers. You can also construct one yourself and dispatch it via *[Input::sendEvent()](../../../api/library/controls/class.input_cpp.md#sendEvent_InputEvent_void)*, which is what a custom SystemProxy implementation or a device emulator does.


### See Also


- C++ sample
- C# Component sample


## InputEventJoyButton Class

### Enums

## ACTION

| Name | Description |
|---|---|
| **ACTION_DOWN** = 0 | Button state is "pressed". |
| **ACTION_UP** = 1 | Button state is "released". |

### Members

---

## InputEventJoyButton ( )

Default constructor.
## InputEventJoyButton ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos )

Joystick button input event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.

## InputEventJoyButton ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos , InputEventJoyButton::ACTION action , int connection_id , Input::JOYSTICK_POV button )

Joystick button input event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.
- *[InputEventJoyButton::ACTION](../../../api/library/controls/class.inputeventjoybutton_cpp.md#ACTION)* **action** - Type of the joystick button input event, one of the [ACTION_*](#ACTION_DOWN) values.
- *int* **connection_id** - Connection identifier.
- *[Input::JOYSTICK_POV](../../../api/library/controls/class.input_cpp.md#JOYSTICK_POV)* **button** - POV hat direction, one of the *[Input::JOYSTICK_POV_*](../../../api/library/controls/class.input_cpp.md#JOYSTICK_POV_NOT_PRESSED)* values.

## void setAction ( InputEventJoyButton::ACTION action )

Sets the action the event represents. See *[getAction()](../../...md#getAction_int)*.
### Arguments

- *[InputEventJoyButton::ACTION](../../../api/library/controls/class.inputeventjoybutton_cpp.md#ACTION)* **action** - Type of the joystick button input event, one of the [ACTION_*](#ACTION_DOWN) values.

## InputEventJoyButton::ACTION getAction ( ) const

Returns the action the event represents: one of the [ACTION](#ACTION) values � the button was pressed or released.
### Return value

Type of the joystick button input event, one of the [ACTION_*](#ACTION_DOWN) values.
## void setConnectionID ( int id )

Sets the identifier of the device connection the event comes from. See *[getConnectionID()](../../...md#getConnectionID_int)*.
### Arguments

- *int* **id** - Connection identifier.

## int getConnectionID ( ) const

Returns the identifier of the device connection the event comes from � the value assigned by the OS when the device was connected. The engine uses it to match the event against a device slot; it is not the slot index itself.
### Return value

Connection identifier.
## void setButton ( Input::JOYSTICK_POV button )

Sets the POV hat direction carried by the event. See *[getButton()](../../...md#getButton_int)*.
### Arguments

- *[Input::JOYSTICK_POV](../../../api/library/controls/class.input_cpp.md#JOYSTICK_POV)* **button** - POV hat direction, one of the *[Input::JOYSTICK_POV_*](../../../api/library/controls/class.input_cpp.md#JOYSTICK_POV_NOT_PRESSED)* values.

## Input::JOYSTICK_POV getButton ( ) const

Returns the direction the POV hat points at � one of the [Input::JOYSTICK_POV](../../../api/library/controls/class.input_cpp.md#JOYSTICK_POV) values.
### Return value

POV hat direction, one of the *[Input::JOYSTICK_POV_*](../../../api/library/controls/class.input_cpp.md#JOYSTICK_POV_NOT_PRESSED)* values.
