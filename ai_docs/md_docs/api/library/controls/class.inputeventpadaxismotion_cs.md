# Unigine::InputEventPadAxisMotion Class (CS)

**Inherits from:** InputEvent


This class controls the game pad axis motion event information.


Events of this type are created by the engine and passed to your handlers. You can also construct one yourself and dispatch it via *[Input.SendEvent()](../../../api/library/controls/class.input_cs.md#sendEvent_InputEvent_void)*, which is what a custom SystemProxy implementation or a device emulator does.


## InputEventPadAxisMotion Class

### Properties

## int ConnectionID

The Connection identifier.
## Input.GAMEPAD_AXIS Axis

The game pad axis, one of the *[Input.GAMEPAD_AXIS](../../../api/library/controls/class.input_cs.md#GAMEPAD_AXIS_LEFT_X)* values.
## float Value

The axis position value.
### Members

---

## InputEventPadAxisMotion ( )

Default constructor.
## InputEventPadAxisMotion ( ulong timestamp , ivec2 mouse_pos )

Game pad axis motion event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.

## InputEventPadAxisMotion ( ulong timestamp , ivec2 mouse_pos , int connection_id , int axis , float value )

Game pad axis motion event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
- *int* **connection_id** - Connection identifier.
- *int* **axis** - Game pad axis index.
- *float* **value** - Axis position value.
