# Unigine::InputEventJoyAxisMotion Class (CS)

**Inherits from:** InputEvent


This class controls joystick axis motion event information.


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
