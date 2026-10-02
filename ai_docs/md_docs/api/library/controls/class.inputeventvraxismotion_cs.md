# Unigine::InputEventVRAxisMotion Class (CS)

**Inherits from:** InputEvent


This class controls the VR controller axis motion event information.


Events of this type are created by the engine and passed to your handlers. You can also construct one yourself and dispatch it via *[Input.SendEvent()](../../../api/library/controls/class.input_cs.md#sendEvent_InputEvent_void)*, which is what a custom SystemProxy implementation or a device emulator does.


## InputEventVRAxisMotion Class

### Properties

## int ConnectionID

The Connection identifier.
## int Axis

The VR controller axis.
## float Value

The axis position value.
### Members

---

## InputEventVRAxisMotion ( )

Default constructor.
## InputEventVRAxisMotion ( ulong timestamp , ivec2 mouse_pos )

VR controller axis motion event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.

## InputEventVRAxisMotion ( ulong timestamp , ivec2 mouse_pos , int connection_id , int axis , float value )

VR controller axis motion event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
- *int* **connection_id** - Connection identifier.
- *int* **axis** - VR controller axis index.
- *float* **value** - Axis position value.
