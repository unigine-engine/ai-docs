# Unigine::InputEventMouseButton Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** InputEvent


This class controls mouse button event information.


## InputEventMouseButton Class

### Members

---

## InputEventMouseButton ( )

Default constructor.
## InputEventMouseButton ( long timestamp , ivec2 mouse_pos )

Mouse button input event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.

## InputEventMouseButton ( long timestamp , ivec2 mouse_pos , int action , int button )

Mouse button input event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
- *int* **action** - Action performed.
- *int* **button** - Mouse button.

## void setAction ( int action )

Sets the action to be performed by the mouse button.
### Arguments

- *int* **action** - Action performed by the mouse button.

## int getAction ( )

Returns the action performed by the mouse button.
### Return value

Action performed by the mouse button.
## void setButton ( int button )

Sets the mouse button for the input event.
### Arguments

- *int* **button** - Mouse button, one of the [INPUT_MOUSE_BUTTON](../../../api/library/controls/class.input_usc.md#MOUSE_BUTTON_UNKNOWN) values.

## int getButton ( )

Returns the mouse button for the input event.
### Return value

Mouse button, one of the [INPUT_MOUSE_BUTTON](../../../api/library/controls/class.input_usc.md#MOUSE_BUTTON_UNKNOWN) values.
