# Unigine::InputEventVRAxisMotion Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** InputEvent


This class controls the VR controller axis motion event information.


## InputEventVRAxisMotion Class

### Members

---

## InputEventVRAxisMotion ( )

Default constructor.
## InputEventVRAxisMotion ( long timestamp , ivec2 mouse_pos )

VR controller axis motion event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.

## InputEventVRAxisMotion ( long timestamp , ivec2 mouse_pos , int connection_id , int axis , float value )

VR controller axis motion event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
- *int* **connection_id** - Connection identifier.
- *int* **axis** - VR controller axis index.
- *float* **value** - Axis position value.

## void setConnectionID ( int connectionid )

Sets the connection identifier.
### Arguments

- *int* **connectionid** - Connection identifier to be set.

## int getConnectionID ( )

Returns the current connection identifier.
### Return value

Connection identifier.
## void setAxis ( int axis )

Sets the VR controller axis.
### Arguments

- *int* **axis** - The VR controller axis.

## int getAxis ( )

Returns the VR controller axis.
### Return value

The VR controller axis.
## void setValue ( float value )

Sets the axis position value.
### Arguments

- *float* **value** - The axis position value.

## float getValue ( )

Returns the axis position value.
### Return value

The axis position value.
