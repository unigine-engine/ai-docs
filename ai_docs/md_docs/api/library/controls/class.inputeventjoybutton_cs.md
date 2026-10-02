# Unigine::InputEventJoyButton Class (CS)

**Inherits from:** InputEvent


This class controls joystick button event information.


Events of this type are created by the engine and passed to your handlers. You can also construct one yourself and dispatch it via *[Input.SendEvent()](../../../api/library/controls/class.input_cs.md#sendEvent_InputEvent_void)*, which is what a custom SystemProxy implementation or a device emulator does.


## InputEventJoyButton Class

### Enums

## ACTION

| Name | Description |
|---|---|
| **DOWN** = 0 | Button state is "pressed". |
| **UP** = 1 | Button state is "released". |

### Properties

## InputEventJoyButton.ACTION Action

The Type of the joystick button input event, one of the [ACTION](#ACTION) values.
## int ConnectionID

The Connection identifier.
## Input.JOYSTICK_POV Button

The POV hat direction, one of the *[Input.JOYSTICK_POV](../../../api/library/controls/class.input_cs.md#JOYSTICK_POV_NOT_PRESSED)* values.
### Members

---

## InputEventJoyButton ( )

Default constructor.
## InputEventJoyButton ( ulong timestamp , ivec2 mouse_pos )

Joystick button input event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.

## InputEventJoyButton ( ulong timestamp , ivec2 mouse_pos , InputEventJoyButton.ACTION action , int connection_id , Input.JOYSTICK_POV button )

Joystick button input event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
- *[InputEventJoyButton.ACTION](../../../api/library/controls/class.inputeventjoybutton_cs.md#ACTION)* **action** - Type of the joystick button input event, one of the [ACTION](#ACTION) values.
- *int* **connection_id** - Connection identifier.
- *[Input.JOYSTICK_POV](../../../api/library/controls/class.input_cs.md#JOYSTICK_POV)* **button** - POV hat direction, one of the *[Input.JOYSTICK_POV](../../../api/library/controls/class.input_cs.md#JOYSTICK_POV_NOT_PRESSED)* values.
