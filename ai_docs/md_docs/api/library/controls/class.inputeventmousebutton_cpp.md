# Unigine::InputEventMouseButton Class (CPP)

**Header:** #include <UnigineInput.h>

**Inherits from:** InputEvent


This class controls mouse button event information.


Events of this type are created by the engine and passed to your handlers. You can also construct one yourself and dispatch it via *[Input::sendEvent()](../../../api/library/controls/class.input_cpp.md#sendEvent_InputEvent_void)*, which is what a custom SystemProxy implementation or a device emulator does.


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

Sets the action the event represents. See *[getAction()](../../...md#getAction_int)*.
### Arguments

- *[InputEventMouseButton::ACTION](../../../api/library/controls/class.inputeventmousebutton_cpp.md#ACTION)* **action** - Action performed by the mouse button.

## InputEventMouseButton::ACTION getAction ( ) const

Returns the action the event represents: one of the [ACTION](#ACTION) values � the button was pressed or released.
### Return value

Action performed by the mouse button.
## void setButton ( Input::MOUSE_BUTTON button )

Sets the mouse button the event refers to. See *[getButton()](../../...md#getButton_int)*.
### Arguments

- *[Input::MOUSE_BUTTON](../../../api/library/controls/class.input_cpp.md#MOUSE_BUTTON)* **button** - Mouse button, one of the [MOUSE_BUTTON_*](../../../api/library/controls/class.input_cpp.md#MOUSE_BUTTON) values.

## Input::MOUSE_BUTTON getButton ( ) const

Returns the mouse button the event refers to � one of the [Input::MOUSE_BUTTON](../../../api/library/controls/class.input_cpp.md#MOUSE_BUTTON) values.
### Return value

Mouse button, one of the [MOUSE_BUTTON_*](../../../api/library/controls/class.input_cpp.md#MOUSE_BUTTON) values.
