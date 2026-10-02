# Unigine::InputEventVRDevice Class (CPP)

**Header:** #include <UnigineInput.h>

**Inherits from:** InputEvent


This class controls VR device event information.


Events of this type are created by the engine and passed to your handlers. You can also construct one yourself and dispatch it via *[Input::sendEvent()](../../../api/library/controls/class.input_cpp.md#sendEvent_InputEvent_void)*, which is what a custom SystemProxy implementation or a device emulator does.


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
- *[InputVRDevice::TYPE](../../../api/library/controls/class.inputvrdevice_cpp.md#TYPE)* **type** - VR device type, one of the [InputVRDevice::TYPE](../../../api/library/controls/class.inputvrdevice_cpp.md#TYPE) values.

## void setAction ( InputEventVRDevice::ACTION action )

Sets the action the event represents. See *[getAction()](../../...md#getAction_int)*.
### Arguments

- *[InputEventVRDevice::ACTION](../../../api/library/controls/class.inputeventvrdevice_cpp.md#ACTION)* **action** - Type of the VR device input event, one of the [ACTION_*](#ACTION_CONNECTED) values.

## InputEventVRDevice::ACTION getAction ( ) const

Returns the action the event represents: one of the [ACTION](#ACTION) values � the VR device was connected or disconnected.
### Return value

Type of the VR device input event, one of the [ACTION_*](#ACTION_CONNECTED) values.
## void setConnectionID ( int connectionid )

Sets the identifier of the device connection the event comes from. See *[getConnectionID()](../../...md#getConnectionID_int)*.
### Arguments

- *int* **connectionid** - Connection identifier.

## int getConnectionID ( ) const

Returns the identifier of the device connection the event comes from � the value assigned by the OS when the device was connected. The engine uses it to match the event against a device slot; it is not the slot index itself.
### Return value

Connection identifier.
## void setType ( InputEventVRDevice::TYPE type )

Sets the type of the VR device the event refers to. See *[getType()](../../...md#getType_int)*.
### Arguments

- *[InputEventVRDevice::TYPE](../../../api/library/controls/class.inputeventvrdevice_cpp.md#TYPE)* **type** - VR device type, one of the [InputVRDevice::TYPE](../../../api/library/controls/class.inputvrdevice_cpp.md#TYPE) values.

## InputEventVRDevice::TYPE getType ( ) const

Returns the type of the VR device the event refers to � one of the [InputVRDevice::TYPE](../../../api/library/controls/class.inputvrdevice_cpp.md#TYPE) values. The type is filled in only for a connection event: on disconnection it carries a placeholder value, so identify the device by [ConnectionID](#ConnectionID) instead.
### Return value

VR device type, one of the [InputVRDevice::TYPE](../../../api/library/controls/class.inputvrdevice_cpp.md#TYPE) values.
