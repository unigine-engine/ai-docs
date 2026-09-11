# Unigine::InputEventPadButton Class (CPP)

**Header:** #include <UnigineInput.h>

**Inherits from:** InputEvent


This class controls the game pad button event information.


### See Also


- C++ sample
- C# Component sample


## InputEventPadButton Class

### Enums

## ACTION

| Name | Description |
|---|---|
| **ACTION_DOWN** = 0 | Button state is "pressed". |
| **ACTION_UP** = 1 | Button state is "released". |

### Members

---

## InputEventPadButton ( )

Default constructor.
## InputEventPadButton ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos )

game pad button input event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.

## InputEventPadButton ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos , InputEventJoyButton::ACTION action , int connection_id , int button )

game pad button input event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.
- *[InputEventJoyButton::ACTION](../../../api/library/controls/class.inputeventjoybutton_cpp.md#ACTION)* **action** - Type of the game pad button input event, one of the *[ACTION_*](../../...md#ACTION_DOWN)* values.
- *int* **connection_id** - Connection identifier.
- *int* **button** - game pad button index.

## void setAction ( InputEventPadButton::ACTION action )

Sets the type of the game pad button input event.
### Arguments

- *[InputEventPadButton::ACTION](../../../api/library/controls/class.inputeventpadbutton_cpp.md#ACTION)* **action** - Type of the game pad button input event, one of the *[ACTION_*](../../...md#ACTION_DOWN)* values.

## InputEventPadButton::ACTION getAction ( ) const

Returns the type of the game pad button input event.
### Return value

Type of the game pad button input event, one of the *[ACTION_*](../../...md#ACTION_DOWN)* values.
## void setConnectionID ( int id )

Sets the connection identifier.
### Arguments

- *int* **id** - Connection identifier.

## int getConnectionID ( ) const

Returns the current connection identifier.
### Return value

Connection identifier.
## void setButton ( Input::GAMEPAD_BUTTON button )

Sets the game pad button.
### Arguments

- *[Input::GAMEPAD_BUTTON](../../../api/library/controls/class.input_cpp.md#GAMEPAD_BUTTON)* **button** - Game pad button, one of the *[Input::GAMEPAD_BUTTON_*](../../../api/library/controls/class.input_cpp.md#GAMEPAD_BUTTON_A)* values.

## Input::GAMEPAD_BUTTON getButton ( ) const

Returns the game pad button.
### Return value

Game pad button, one of the *[Input::GAMEPAD_BUTTON_*](../../../api/library/controls/class.input_cpp.md#GAMEPAD_BUTTON_A)* values.
## InputEventPadButton ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos , InputEventPadButton::ACTION action , int connection_id , Input::GAMEPAD_BUTTON button )

Constructor. Creates a game pad button event with the given parameters.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse at the moment of the event.
- *[InputEventPadButton::ACTION](../../../api/library/controls/class.inputeventpadbutton_cpp.md#ACTION)* **action** - Button action, one of the *ACTION_** values.
- *int* **connection_id** - Connection identifier of the game pad.
- *[Input::GAMEPAD_BUTTON](../../../api/library/controls/class.input_cpp.md#GAMEPAD_BUTTON)* **button** - Game pad button, one of the *Input::GAMEPAD_BUTTON_** values.
