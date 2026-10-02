# Unigine::InputEventMouseMotion Class (CS)

**Inherits from:** InputEvent


This class controls mouse motion event information.


Events of this type are created by the engine and passed to your handlers. You can also construct one yourself and dispatch it via *[Input.SendEvent()](../../../api/library/controls/class.input_cs.md#sendEvent_InputEvent_void)*, which is what a custom SystemProxy implementation or a device emulator does.


## InputEventMouseMotion Class

### Properties

## ivec2 Delta

The Delta of the mouse position from the previous event.
### Members

---

## InputEventMouseMotion ( )

Default constructor.
## InputEventMouseMotion ( ulong timestamp , ivec2 mouse_pos , ivec2 delta )

Mouse motion input event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
- *ivec2* **delta** - Delta of the mouse position from the previous event.

## InputEventMouseMotion ( ulong timestamp , ivec2 mouse_pos )

Mouse motion input event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
