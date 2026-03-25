# Unigine::InputEventMouseWheel Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** InputEvent


This class controls mouse wheel event information.


## InputEventMouseWheel Class

### Members

---

## static InputEventMouseWheel ( )

Default constructor.
## InputEventMouseWheel ( long timestamp , ivec2 mouse_pos )

Mouse wheel input event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.

## InputEventMouseWheel ( long timestamp , ivec2 mouse_pos , int wheel , int wheel_h )

Mouse wheel input event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
- *int* **wheel** - Delta amount scrolled vertically (positive value - away from the user, negative - towards the user.
- *int* **wheel_h** - Delta amount scrolled horizontally (positive value - to the right, negative - to the left).

## void setWheel ( int wheel )

Sets the delta of the vertical mouse scroll movement.
### Arguments

- *int* **wheel** - The amount scrolled vertically, positive away from the user and negative towards the user.

## int getWheel ( )

Returns the delta of the vertical mouse scroll movement.
### Return value

The amount scrolled vertically, positive away from the user and negative towards the user.
## void setWheelHorizontal ( int horizontal )

Sets the delta of the horizontal mouse scroll movement.
### Arguments

- *int* **horizontal** - The amount scrolled horizontally, positive to the right and negative to the left.

## int getWheelHorizontal ( )

Returns the delta of the horizontal mouse scroll movement.
### Return value

The amount scrolled horizontally, positive to the right and negative to the left.
