# Unigine::InputEventVRDevice Class (CPP)

**Header:** #include <UnigineInput.h>

**Inherits from:** InputEvent


This class controls VR device event information.


## InputEventVRDevice Class

### Enums

## ACTION

| Name | Description |
|---|---|
| **ACTION_CONNECTED** = 0 | Device state is "connected". |
| **ACTION_DISCONNECTED** = 1 | Device state is "disconnected". |

### Members

---

## InputEventVRDevice ( )

Default constructor.
## InputEventVRDevice ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos )

VR device input event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.

## InputEventVRDevice ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos , InputEventVRDevice::ACTION action , int connection_id , InputVRDevice::TYPE type )

VR device input event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.
- *[InputEventVRDevice::ACTION](../../../api/library/controls/class.inputeventvrdevice_cpp.md#ACTION)* **action** - Type of the VR device input event, one of the [ACTION_*](#ACTION_CONNECTED) values.
- *int* **connection_id** - Connection identifier.
- *[InputVRDevice::TYPE](../../../api/library/controls/class.inputvrdevice_cpp.md#TYPE)* **type** - VR device type.

## void setAction ( InputEventVRDevice::ACTION action )

Sets the type of the VR device input event.
### Arguments

- *[InputEventVRDevice::ACTION](../../../api/library/controls/class.inputeventvrdevice_cpp.md#ACTION)* **action** - Type of the VR device input event, one of the [ACTION_*](#ACTION_CONNECTED) values.

## InputEventVRDevice::ACTION getAction ( ) const

Returns the type of the VR device input event.
### Return value

Type of the VR device input event, one of the [ACTION_*](#ACTION_CONNECTED) values.
## void setConnectionID ( int connectionid )

Sets the connection identifier.
### Arguments

- *int* **connectionid** - Connection identifier.

## int getConnectionID ( ) const

Returns the current connection identifier.
### Return value

Connection identifier.
## void setType ( InputEventVRDevice::TYPE type )

Sets the VR device type.
### Arguments

- *[InputEventVRDevice::TYPE](../../../api/library/controls/class.inputeventvrdevice_cpp.md#TYPE)* **type** - VR device type.

## InputEventVRDevice::TYPE getType ( ) const

Returns the VR device type.
### Return value

VR device type.
