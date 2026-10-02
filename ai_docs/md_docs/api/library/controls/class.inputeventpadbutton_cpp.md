# Unigine::InputEventPadButton Class (CPP)

**Header:** #include <UnigineInput.h>

**Inherits from:** InputEvent


This class controls the game pad button event information.


Events of this type are created by the engine and passed to your handlers. You can also construct one yourself and dispatch it via *[Input::sendEvent()](../../../api/library/controls/class.input_cpp.md#sendEvent_InputEvent_void)*, which is what a custom SystemProxy implementation or a device emulator does.


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

Sets the action the event represents. See *[getAction()](../../...md#getAction_int)*.
### Arguments

- *[InputEventPadButton::ACTION](../../../api/library/controls/class.inputeventpadbutton_cpp.md#ACTION)* **action** - Type of the game pad button input event, one of the *[ACTION_*](../../...md#ACTION_DOWN)* values.

## InputEventPadButton::ACTION getAction ( ) const

Returns the action the event represents: one of the [ACTION](#ACTION) values � the button was pressed or released.
### Return value

Type of the game pad button input event, one of the *[ACTION_*](../../...md#ACTION_DOWN)* values.
## void setConnectionID ( int id )

Sets the identifier of the device connection the event comes from. See *[getConnectionID()](../../...md#getConnectionID_int)*.
### Arguments

- *int* **id** - Connection identifier.

## int getConnectionID ( ) const

Returns the identifier of the device connection the event comes from � the value assigned by the OS when the device was connected. The engine uses it to match the event against a device slot; it is not the slot index itself.
### Return value

Connection identifier.
## void setButton ( Input::GAMEPAD_BUTTON button )

Sets the gamepad button the event refers to. See *[getButton()](../../...md#getButton_int)*.
### Arguments

- *[Input::GAMEPAD_BUTTON](../../../api/library/controls/class.input_cpp.md#GAMEPAD_BUTTON)* **button** - Game pad button, one of the *[Input::GAMEPAD_BUTTON_*](../../../api/library/controls/class.input_cpp.md#GAMEPAD_BUTTON_A)* values.

## Input::GAMEPAD_BUTTON getButton ( ) const

Returns the gamepad button the event refers to � one of the [Input::GAMEPAD_BUTTON](../../../api/library/controls/class.input_cpp.md#GAMEPAD_BUTTON) values.
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
