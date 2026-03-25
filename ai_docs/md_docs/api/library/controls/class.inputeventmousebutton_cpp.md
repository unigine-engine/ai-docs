# Unigine::InputEventMouseButton Class (CPP)

**Header:** #include <UnigineInput.h>

**Inherits from:** InputEvent


This class controls mouse button event information.


### See Also


- C++ sample
- C# Component sample


## InputEventMouseButton Class

### Enums

## ACTION

| Name | Description |
|---|---|
| **ACTION_DOWN** = 0 | Mouse button has been pressed. |
| **ACTION_UP** = 1 | Mouse button has been released. |

### Members

---

## InputEventMouseButton ( )

Default constructor.
## InputEventMouseButton ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos )

Mouse button input event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.

## InputEventMouseButton ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos , InputEventMouseButton::ACTION action , Input::MOUSE_BUTTON button )

Mouse button input event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.
- *[InputEventMouseButton::ACTION](../../../api/library/controls/class.inputeventmousebutton_cpp.md#ACTION)* **action** - Action performed.
- *[Input::MOUSE_BUTTON](../../../api/library/controls/class.input_cpp.md#MOUSE_BUTTON)* **button** - Mouse button.

## void setAction ( InputEventMouseButton::ACTION action )

Sets the action to be performed by the mouse button.
### Arguments

- *[InputEventMouseButton::ACTION](../../../api/library/controls/class.inputeventmousebutton_cpp.md#ACTION)* **action** - Action performed by the mouse button.

## InputEventMouseButton::ACTION getAction ( ) const

Returns the action performed by the mouse button.
### Return value

Action performed by the mouse button.
## void setButton ( Input::MOUSE_BUTTON button )

Sets the mouse button for the input event.
### Arguments

- *[Input::MOUSE_BUTTON](../../../api/library/controls/class.input_cpp.md#MOUSE_BUTTON)* **button** - Mouse button, one of the [MOUSE_BUTTON_*](../../../api/library/controls/class.input_cpp.md#MOUSE_BUTTON) values.

## Input::MOUSE_BUTTON getButton ( ) const

Returns the mouse button for the input event.
### Return value

Mouse button, one of the [MOUSE_BUTTON_*](../../../api/library/controls/class.input_cpp.md#MOUSE_BUTTON) values.
