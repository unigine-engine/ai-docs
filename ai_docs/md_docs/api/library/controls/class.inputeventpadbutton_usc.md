# Unigine::InputEventPadButton Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** InputEvent


This class controls the game pad button event information.


Events of this type are created by the engine and passed to your handlers. You can also construct one yourself and dispatch it via *[engine.input.sendEvent()()](../../../api/library/controls/class.input_usc.md#sendEvent_InputEvent_void)*, which is what a custom SystemProxy implementation or a device emulator does.


## InputEventPadButton Class

### Members

---

## InputEventPadButton ( )

Default constructor.
## InputEventPadButton ( long timestamp , ivec2 mouse_pos )

game pad button input event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.

## InputEventPadButton ( long timestamp , ivec2 mouse_pos , int action , int connection_id , int button )

game pad button input event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
- *int* **action** - Type of the game pad button input event, one of the *[INPUT_EVENT_PAD_BUTTON_ACTION_*()](../../...md#ACTION_DOWN)* values.
- *int* **connection_id** - Connection identifier.
- *int* **button** - game pad button index.

## void setAction ( int action )

Sets the action the event represents. See *[getAction()()](../../...md#getAction_int)*.
### Arguments

- *int* **action** - Type of the game pad button input event, one of the *[INPUT_EVENT_PAD_BUTTON_ACTION_*()](../../...md#ACTION_DOWN)* values.

## int getAction ( )

Returns the action the event represents: one of the [ACTION](#ACTION) values � the button was pressed or released.
### Return value

Type of the game pad button input event, one of the *[INPUT_EVENT_PAD_BUTTON_ACTION_*()](../../...md#ACTION_DOWN)* values.
## void setConnectionID ( int id )

Sets the identifier of the device connection the event comes from. See *[getConnectionID()()](../../...md#getConnectionID_int)*.
### Arguments

- *int* **id** - Connection identifier.

## int getConnectionID ( )

Returns the identifier of the device connection the event comes from � the value assigned by the OS when the device was connected. The engine uses it to match the event against a device slot; it is not the slot index itself.
### Return value

Connection identifier.
## void setButton ( int button )

Sets the gamepad button the event refers to. See *[getButton()()](../../...md#getButton_int)*.
### Arguments

- *int* **button** - Game pad button, one of the *[INPUT_GAME_PAD_BUTTON_*()](../../../api/library/controls/class.input_usc.md#GAMEPAD_BUTTON_A)* values.

## int getButton ( )

Returns the gamepad button the event refers to � one of the [Input::GAMEPAD_BUTTON](../../../api/library/controls/class.input_usc.md#GAMEPAD_BUTTON) values.
### Return value

Game pad button, one of the *[INPUT_GAME_PAD_BUTTON_*()](../../../api/library/controls/class.input_usc.md#GAMEPAD_BUTTON_A)* values.
## InputEventPadButton ( long timestamp , ivec2 mouse_pos , int action , int connection_id , int button )

Constructor. Creates a game pad button event with the given parameters.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse at the moment of the event.
- *int* **action** - Button action, one of the *ACTION_** values.
- *int* **connection_id** - Connection identifier of the game pad.
- *int* **button** - Game pad button, one of the *Input::GAMEPAD_BUTTON_** values.
