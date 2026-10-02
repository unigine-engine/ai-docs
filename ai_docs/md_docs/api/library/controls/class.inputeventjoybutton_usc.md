# Unigine::InputEventJoyButton Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** InputEvent


This class controls joystick button event information.


Events of this type are created by the engine and passed to your handlers. You can also construct one yourself and dispatch it via *[engine.input.sendEvent()()](../../../api/library/controls/class.input_usc.md#sendEvent_InputEvent_void)*, which is what a custom SystemProxy implementation or a device emulator does.


## InputEventJoyButton Class

### Members

---

## InputEventJoyButton ( )

Default constructor.
## InputEventJoyButton ( long timestamp , ivec2 mouse_pos )

Joystick button input event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.

## InputEventJoyButton ( long timestamp , ivec2 mouse_pos , int action , int connection_id , int button )

Joystick button input event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
- *int* **action** - Type of the joystick button input event, one of the [INPUT_EVENT_JOY_BUTTON_ACTION_*](#ACTION_DOWN) values.
- *int* **connection_id** - Connection identifier.
- *int* **button** - POV hat direction, one of the *[INPUT_JOYSTICK_POV_*()](../../../api/library/controls/class.input_usc.md#JOYSTICK_POV_NOT_PRESSED)* values.

## void setAction ( int action )

Sets the action the event represents. See *[getAction()()](../../...md#getAction_int)*.
### Arguments

- *int* **action** - Type of the joystick button input event, one of the [INPUT_EVENT_JOY_BUTTON_ACTION_*](#ACTION_DOWN) values.

## int getAction ( )

Returns the action the event represents: one of the [ACTION](#ACTION) values � the button was pressed or released.
### Return value

Type of the joystick button input event, one of the [INPUT_EVENT_JOY_BUTTON_ACTION_*](#ACTION_DOWN) values.
## void setConnectionID ( int id )

Sets the identifier of the device connection the event comes from. See *[getConnectionID()()](../../...md#getConnectionID_int)*.
### Arguments

- *int* **id** - Connection identifier.

## int getConnectionID ( )

Returns the identifier of the device connection the event comes from � the value assigned by the OS when the device was connected. The engine uses it to match the event against a device slot; it is not the slot index itself.
### Return value

Connection identifier.
## void setButton ( int button )

Sets the POV hat direction carried by the event. See *[getButton()()](../../...md#getButton_int)*.
### Arguments

- *int* **button** - POV hat direction, one of the *[INPUT_JOYSTICK_POV_*()](../../../api/library/controls/class.input_usc.md#JOYSTICK_POV_NOT_PRESSED)* values.

## int getButton ( )

Returns the direction the POV hat points at � one of the [Input::JOYSTICK_POV](../../../api/library/controls/class.input_usc.md#JOYSTICK_POV) values.
### Return value

POV hat direction, one of the *[INPUT_JOYSTICK_POV_*()](../../../api/library/controls/class.input_usc.md#JOYSTICK_POV_NOT_PRESSED)* values.
