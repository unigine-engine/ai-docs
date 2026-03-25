# Unigine::InputEventKeyboard Class (CS)

**Inherits from:** InputEvent


This class controls keyboard event information.


## InputEventKeyboard Class

### Enums

## ACTION

| Name | Description |
|---|---|
| **DOWN** = 0 | Keyboard button is held down. |
| **REPEAT** = 1 | Keyboard button has been pressed repeatedly. |
| **UP** = 2 | Keyboard button has been released. |

### Properties

## InputEventKeyboard.ACTION Action

The Action performed by the keyboard.
## Input.KEY Key

The Virtual keyboard key value (dependent on the keyboard language).
### Members

---

## InputEventKeyboard ( )

Default constructor.
## InputEventKeyboard ( ulong timestamp , ivec2 mouse_pos , InputEventKeyboard.ACTION action , Input.KEY key )

Keyboard input event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
- *[InputEventKeyboard.ACTION](../../../api/library/controls/class.inputeventkeyboard_cs.md#ACTION)* **action** - Action performed.
- *[Input.KEY](../../../api/library/controls/class.input_cs.md#KEY)* **key** - Virtual keyboard key value (dependent on the language).

## InputEventKeyboard ( ulong timestamp , ivec2 mouse_pos )

Keyboard input event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
