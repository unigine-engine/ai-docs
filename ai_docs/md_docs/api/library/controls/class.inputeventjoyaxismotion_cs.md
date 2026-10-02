# Unigine::InputEventJoyAxisMotion Class (CS)

**Inherits from:** InputEvent


This class controls joystick axis motion event information.


Events of this type are created by the engine and passed to your handlers. You can also construct one yourself and dispatch it via *[Input.SendEvent()](../../../api/library/controls/class.input_cs.md#sendEvent_InputEvent_void)*, which is what a custom SystemProxy implementation or a device emulator does.


## InputEventJoyAxisMotion Class

### Properties

## int ConnectionID

The Connection identifier.
## int Axis

The Joystick axis index.
## float Value

The Axis position value.
### Members

---

## InputEventJoyAxisMotion ( )

Default constructor.
## InputEventJoyAxisMotion ( ulong timestamp , ivec2 mouse_pos )

Joystick axis motion event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.

## InputEventJoyAxisMotion ( ulong timestamp , ivec2 mouse_pos , int connection_id , int axis , float value )

Joystick axis motion event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
- *int* **connection_id** - Connection identifier.
- *int* **axis** - Joystick axis index.
- *float* **value** - Axis position value.
