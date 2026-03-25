# Unigine::InputEventMouseButton Class (CS)

**Inherits from:** InputEvent


This class controls mouse button event information.


## InputEventMouseButton Class

### Enums

## ACTION

| Name | Description |
|---|---|
| **DOWN** = 0 | Mouse button has been pressed. |
| **UP** = 1 | Mouse button has been released. |

### Properties

## InputEventMouseButton.ACTION Action

The Action performed by the mouse button.
## Input.MOUSE_BUTTON Button

The Mouse button, one of the [MOUSE_BUTTON.*](../../../api/library/controls/class.input_cs.md#MOUSE_BUTTON) values.
### Members

---

## InputEventMouseButton ( )

Default constructor.
## InputEventMouseButton ( ulong timestamp , ivec2 mouse_pos )

Mouse button input event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.

## InputEventMouseButton ( ulong timestamp , ivec2 mouse_pos , InputEventMouseButton.ACTION action , Input.MOUSE_BUTTON button )

Mouse button input event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
- *[InputEventMouseButton.ACTION](../../../api/library/controls/class.inputeventmousebutton_cs.md#ACTION)* **action** - Action performed.
- *[Input.MOUSE_BUTTON](../../../api/library/controls/class.input_cs.md#MOUSE_BUTTON)* **button** - Mouse button.
