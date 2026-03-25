# Unigine::InputEventVRDevice Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** InputEvent


This class controls VR device event information.


## InputEventVRDevice Class

### Members

---

## InputEventVRDevice ( )

Default constructor.
## InputEventVRDevice ( long timestamp , ivec2 mouse_pos )

VR device input event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.

## InputEventVRDevice ( long timestamp , ivec2 mouse_pos , int action , int connection_id , int type )

VR device input event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
- *int* **action** - Type of the VR device input event, one of the [INPUT_EVENT_VR_DEVICE_ACTION_*](#ACTION_CONNECTED) values.
- *int* **connection_id** - Connection identifier.
- *int* **type** - VR device type.

## void setAction ( int action )

Sets the type of the VR device input event.
### Arguments

- *int* **action** - Type of the VR controller button input event, one of the [INPUT_EVENT_VR_DEVICE_ACTION_*](#ACTION_CONNECTED) values.

## int getAction ( )

Returns the type of the VR device input event.
### Return value

Type of the VR controller button input event, one of the [INPUT_EVENT_VR_DEVICE_ACTION_*](#ACTION_CONNECTED) values.
## void setConnectionID ( int connectionid )

Sets the connection identifier.
### Arguments

- *int* **connectionid** - Connection identifier.

## int getConnectionID ( )

Returns the current connection identifier.
### Return value

Connection identifier.
## void setType ( int type )

Sets the VR device type.
### Arguments

- *int* **type** - VR device type.

## int getType ( )

Returns the VR device type.
### Return value

VR device type.
