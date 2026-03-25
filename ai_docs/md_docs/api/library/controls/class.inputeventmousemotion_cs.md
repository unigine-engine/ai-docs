# Unigine::InputEventMouseMotion Class (CS)

**Inherits from:** InputEvent


This class controls mouse motion event information.


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
