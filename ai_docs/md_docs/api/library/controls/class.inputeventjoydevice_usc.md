# Unigine::InputEventJoyDevice Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** InputEvent


This class controls joystick device event information.


## InputEventJoyDevice Class

### Members

---

## InputEventJoyDevice ( )

Default constructor.
## InputEventJoyDevice ( long timestamp , ivec2 mouse_pos )

Joystick input event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.

## InputEventJoyDevice ( long timestamp , ivec2 mouse_pos , int action , int connection_id , int player_index , string model_guid )

Joystick input event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
- *int* **action** - Type of the joystick input event, one of the [INPUT_EVENT_JOY_DEVICE_ACTION_*](#ACTION_CONNECTED) values.
- *int* **connection_id** - Connection identifier.
- *int* **player_index** - Index of the player.
- *string* **model_guid** - GUID of the joystick model.

## void setAction ( int action )

Sets the type of the joystick input event.
### Arguments

- *int* **action** - Type of the joystick input event, one of the [INPUT_EVENT_JOY_DEVICE_ACTION_*](#ACTION_CONNECTED) values.

## int getAction ( )

Returns the type of the joystick input event.
### Return value

Type of the joystick input event, one of the [INPUT_EVENT_JOY_DEVICE_ACTION_*](#ACTION_CONNECTED) values.
## void setConnectionID ( int id )

Sets the connection identifier.
### Arguments

- *int* **id** - Сonnection identifier to be set.

## int getConnectionID ( )

Returns the connection identifier.
### Return value

Сonnection identifier.
## void setPlayerIndex ( int index )

Sets the player index.
### Arguments

- *int* **index** - Player index.

## int getPlayerIndex ( )

Returns the player index.
### Return value

Player index.
## void setModelGUID ( string modelguid )

Sets the GUID of the joystick model.
### Arguments

- *string* **modelguid** - GUID of the joystick model.

## string getModelGUID ( )

Returns the GUID of the joystick model.
### Return value

GUID of the joystick model.
