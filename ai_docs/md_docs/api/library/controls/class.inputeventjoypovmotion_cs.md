# Unigine::InputEventJoyPovMotion Class (CS)

**Inherits from:** InputEvent


This class controls joystick POV hat motion event information.


## InputEventJoyPovMotion Class

### Properties

## int ConnectionID

The Connection identifier.
## int Pov

The Index of the POV hat.
## int Value

The Position of the POV hat.
### Members

---

## InputEventJoyPovMotion ( )

Default constructor.
## InputEventJoyPovMotion ( ulong timestamp , ivec2 mouse_pos )

Joystick POV hat motion event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.

## InputEventJoyPovMotion ( ulong timestamp , ivec2 mouse_pos , int connection_id , int pov , int value )

Joystick POV hat motion event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
- *int* **connection_id** - Connection identifier.
- *int* **pov** - Index of the POV hat.
- *int* **value** - Position of the POV hat.
