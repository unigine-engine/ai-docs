# Unigine::InputEventJoyAxisMotion Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** InputEvent


This class controls joystick axis motion event information.


## InputEventJoyAxisMotion Class

### Members

---

## InputEventJoyAxisMotion ( )

Default constructor.
## InputEventJoyAxisMotion ( long timestamp , ivec2 mouse_pos )

Joystick axis motion event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.

## InputEventJoyAxisMotion ( long timestamp , ivec2 mouse_pos , int connection_id , int axis , float value )

Joystick axis motion event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
- *int* **connection_id** - Connection identifier.
- *int* **axis** - Joystick axis index.
- *float* **value** - Axis position value.

## void setConnectionID ( int id )

Sets the connection identifier.
### Arguments

- *int* **id** - Connection identifier.

## int getConnectionID ( )

Returns the current connection identifier.
### Return value

Connection identifier.
## void setAxis ( int axis )

Sets the joystick axis index.
### Arguments

- *int* **axis** - Joystick axis index.

## int getAxis ( )

Sets the joystick axis index.
### Return value

Joystick axis index.
## void setValue ( float value )

Sets the axis position value.
### Arguments

- *float* **value** - Axis position value.

## float getValue ( )

Returns the axis position value.
### Return value

Axis position value.
