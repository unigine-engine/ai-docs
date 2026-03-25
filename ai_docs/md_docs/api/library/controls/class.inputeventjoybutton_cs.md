# Unigine::InputEventJoyButton Class (CS)

**Inherits from:** InputEvent


This class controls joystick button event information.


## InputEventJoyButton Class

### Enums

## ACTION

| Name | Description |
|---|---|
| **DOWN** = 0 | Button state is "pressed". |
| **UP** = 1 | Button state is "released". |

### Properties

## InputEventJoyButton.ACTION Action

The Type of the joystick input event, one of the [ACTION](#ACTION) values.
## int ConnectionID

The Connection identifier.
## int Button

The Joystick button index.
### Members

---

## InputEventJoyButton ( )

Default constructor.
## InputEventJoyButton ( ulong timestamp , ivec2 mouse_pos )

Joystick button input event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.

## InputEventJoyButton ( ulong timestamp , ivec2 mouse_pos , InputEventJoyButton.ACTION action , int connection_id , int button )

Joystick button input event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
- *[InputEventJoyButton.ACTION](../../../api/library/controls/class.inputeventjoybutton_cs.md#ACTION)* **action** - Type of the joystick button input event, one of the [ACTION](#ACTION) values.
- *int* **connection_id** - Connection identifier.
- *int* **button** - Joystick button index.
