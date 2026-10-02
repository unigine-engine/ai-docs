# Unigine::InputEventMouseButton Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** InputEvent


This class controls mouse button event information.


Events of this type are created by the engine and passed to your handlers. You can also construct one yourself and dispatch it via *[engine.input.sendEvent()()](../../../api/library/controls/class.input_usc.md#sendEvent_InputEvent_void)*, which is what a custom SystemProxy implementation or a device emulator does.


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

Sets the action the event represents. See *[getAction()()](../../...md#getAction_int)*.
### Arguments

- *int* **action** - Action performed by the mouse button.

## int getAction ( )

Returns the action the event represents: one of the [ACTION](#ACTION) values � the button was pressed or released.
### Return value

Action performed by the mouse button.
## void setButton ( int button )

Sets the mouse button the event refers to. See *[getButton()()](../../...md#getButton_int)*.
### Arguments

- *int* **button** - Mouse button, one of the [INPUT_MOUSE_BUTTON](../../../api/library/controls/class.input_usc.md#MOUSE_BUTTON_UNKNOWN) values.

## int getButton ( )

Returns the mouse button the event refers to � one of the [Input::MOUSE_BUTTON](../../../api/library/controls/class.input_usc.md#MOUSE_BUTTON) values.
### Return value

Mouse button, one of the [INPUT_MOUSE_BUTTON](../../../api/library/controls/class.input_usc.md#MOUSE_BUTTON_UNKNOWN) values.
