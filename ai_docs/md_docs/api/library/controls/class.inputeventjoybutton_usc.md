# Unigine::InputEventJoyButton Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** InputEvent


This class controls joystick button event information.


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
- *int* **button** - Joystick button index.

## void setAction ( int action )

Sets the type of the joystick button input event.
### Arguments

- *int* **action** - Type of the joystick button input event, one of the [INPUT_EVENT_JOY_BUTTON_ACTION_*](#ACTION_DOWN) values.

## int getAction ( )

Returns the type of the joystick button input event.
### Return value

Type of the joystick button input event, one of the [INPUT_EVENT_JOY_BUTTON_ACTION_*](#ACTION_DOWN) values.
## void setConnectionID ( int id )

Sets the connection identifier.
### Arguments

- *int* **id** - Connection identifier.

## int getConnectionID ( )

Returns the current connection identifier.
### Return value

Connection identifier.
## void setButton ( int button )

Sets the joystick button index.
### Arguments

- *int* **button** - Joystick button index.

## int getButton ( )

Returns the joystick button index.
### Return value

Joystick button index.
