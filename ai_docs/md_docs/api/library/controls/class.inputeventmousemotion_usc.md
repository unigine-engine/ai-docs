# Unigine::InputEventMouseMotion Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** InputEvent


This class controls mouse motion event information.


## InputEventMouseMotion Class

### Members

---

## InputEventMouseMotion ( )

Default constructor.
## InputEventMouseMotion ( long timestamp , ivec2 mouse_pos , ivec2 delta )

Mouse motion input event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
- *ivec2* **delta** - Delta of the mouse position from the previous event.

## InputEventMouseMotion ( long timestamp , ivec2 mouse_pos )

Mouse motion input event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.

## void setDelta ( ivec2 delta )

Sets the delta of the mouse position from the previous event.
### Arguments

- *ivec2* **delta** - Delta of the mouse position from the previous event.

## ivec2 getDelta ( )

Returns the delta of the mouse position from the previous event.
### Return value

Delta of the mouse position from the previous event.
