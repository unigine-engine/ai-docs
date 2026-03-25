# Unigine::InputEventMouseWheel Class (CS)

**Inherits from:** InputEvent


This class controls mouse wheel event information.


## InputEventMouseWheel Class

### Properties

## int WheelHorizontal

The amount scrolled horizontally, positive to the right and negative to the left.
## int Wheel

The amount scrolled vertically, positive away from the user and negative towards the user.
### Members

---

## InputEventMouseWheel ( )

Default constructor.
## InputEventMouseWheel ( ulong timestamp , ivec2 mouse_pos )

Mouse wheel input event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.

## InputEventMouseWheel ( ulong timestamp , ivec2 mouse_pos , int wheel , int wheel_h )

Mouse wheel input event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
- *int* **wheel** - Delta amount scrolled vertically (positive value - away from the user, negative - towards the user.
- *int* **wheel_h** - Delta amount scrolled horizontally (positive value - to the right, negative - to the left).
