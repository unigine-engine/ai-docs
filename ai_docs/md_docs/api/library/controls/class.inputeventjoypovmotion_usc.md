# Unigine::InputEventJoyPovMotion Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** InputEvent


This class controls joystick POV hat motion event information.


## InputEventJoyPovMotion Class

### Members

---

## InputEventJoyPovMotion ( )

Default constructor.
## InputEventJoyPovMotion ( long timestamp , ivec2 mouse_pos )

Joystick POV hat motion event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.

## InputEventJoyPovMotion ( long timestamp , ivec2 mouse_pos , int connection_id , int pov , int value )

Joystick POV hat motion event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
- *int* **connection_id** - Connection identifier.
- *int* **pov** - Index of the POV hat.
- *int* **value** - Position of the POV hat.

## void setConnectionID ( int id )

Sets the connection identifier.
### Arguments

- *int* **id** - Connection identifier to be set.

## int getConnectionID ( )

Returns the connection identifier.
### Return value

Connection identifier.
## void setPov ( int pov )

Sets the index of the POV hat.
### Arguments

- *int* **pov** - Index of the POV hat.

## int getPov ( )

Returns the index of the POV hat.
### Return value

Index of the POV hat.
## void setValue ( int value )

Sets the position of the POV hat.
### Arguments

- *int* **value** - Position of the POV hat.

## int getValue ( )

Returns the position of the POV hat.
### Return value

Position of the POV hat.
