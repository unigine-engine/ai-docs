# Unigine::InputEventPadButton Class (CS)

**Inherits from:** InputEvent


This class controls the game pad button event information.


## InputEventPadButton Class

### Enums

## ACTION

| Name | Description |
|---|---|
| **DOWN** = 0 | Button state is "pressed". |
| **UP** = 1 | Button state is "released". |

### Properties

## InputEventPadButton.ACTION Action

The Type of the game pad button input event, one of the *[ACTION](../../...md#ACTION_DOWN)* values.
## int ConnectionID

The Connection identifier.
## Input.GAMEPAD_BUTTON Button

The Game pad button, one of the *[Input.GAMEPAD_BUTTON](../../../api/library/controls/class.input_cs.md#GAMEPAD_BUTTON_A)* values.
### Members

---

## InputEventPadButton ( )

Default constructor.
## InputEventPadButton ( ulong timestamp , ivec2 mouse_pos )

game pad button input event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.

## InputEventPadButton ( ulong timestamp , ivec2 mouse_pos , InputEventJoyButton.ACTION action , int connection_id , int button )

game pad button input event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
- *[InputEventJoyButton.ACTION](../../../api/library/controls/class.inputeventjoybutton_cs.md#ACTION)* **action** - Type of the game pad button input event, one of the *[ACTION](../../...md#ACTION_DOWN)* values.
- *int* **connection_id** - Connection identifier.
- *int* **button** - game pad button index.

## InputEventPadButton ( ulong timestamp , ivec2 mouse_pos , InputEventPadButton.ACTION action , int connection_id , Input.GAMEPAD_BUTTON button )

Constructor. Creates a game pad button event with the given parameters.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse at the moment of the event.
- *[InputEventPadButton.ACTION](../../../api/library/controls/class.inputeventpadbutton_cs.md#ACTION)* **action** - Button action, one of the *ACTION_** values.
- *int* **connection_id** - Connection identifier of the game pad.
- *[Input.GAMEPAD_BUTTON](../../../api/library/controls/class.input_cs.md#GAMEPAD_BUTTON)* **button** - Game pad button, one of the *Input::GAMEPAD_BUTTON_** values.
