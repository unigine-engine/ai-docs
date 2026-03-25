# Unigine::InputEventPadAxisMotion Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** InputEvent


This class controls the game pad axis motion event information.


## InputEventPadAxisMotion Class

### Members

---

## InputEventPadAxisMotion ( )

Default constructor.
## InputEventPadAxisMotion ( long timestamp , ivec2 mouse_pos )

Game pad axis motion event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.

## InputEventPadAxisMotion ( long timestamp , ivec2 mouse_pos , int connection_id , int axis , float value )

Game pad axis motion event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
- *int* **connection_id** - Connection identifier.
- *int* **axis** - Game pad axis index.
- *float* **value** - Axis position value.

## void setConnectionID ( int id )

Sets the connection identifier.
### Arguments

- *int* **id** - Connection identifier to be set.

## int getConnectionID ( )

Returns the current connection identifier.
### Return value

Connection identifier.
## void setAxis ( int axis )

Sets the game pad axis.
### Arguments

- *int* **axis** - The game pad axis, one of the *[INPUT_GAME_PAD_AXIS_*()](../../../api/library/controls/class.input_usc.md#GAMEPAD_AXIS_LEFT_X)* values.

## int getAxis ( )

Returns the game pad axis.
### Return value

The game pad axis, one of the *[INPUT_GAME_PAD_AXIS_*()](../../../api/library/controls/class.input_usc.md#GAMEPAD_AXIS_LEFT_X)* values.
## void setValue ( float value )

Sets the axis position value.
### Arguments

- *float* **value** - The axis position value.

## float getValue ( )

Returns the axis position value.
### Return value

The axis position value.
