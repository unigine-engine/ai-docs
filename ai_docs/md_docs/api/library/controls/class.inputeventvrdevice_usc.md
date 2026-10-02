# Unigine::InputEventVRDevice Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** InputEvent


This class controls VR device event information.


Events of this type are created by the engine and passed to your handlers. You can also construct one yourself and dispatch it via *[engine.input.sendEvent()()](../../../api/library/controls/class.input_usc.md#sendEvent_InputEvent_void)*, which is what a custom SystemProxy implementation or a device emulator does.


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
- *int* **type** - VR device type, one of the [InputVRDevice::TYPE](../../../api/library/controls/class.inputvrdevice_usc.md#TYPE) values.

## void setAction ( int action )

Sets the action the event represents. See *[getAction()()](../../...md#getAction_int)*.
### Arguments

- *int* **action** - Type of the VR device input event, one of the [INPUT_EVENT_VR_DEVICE_ACTION_*](#ACTION_CONNECTED) values.

## int getAction ( )

Returns the action the event represents: one of the [ACTION](#ACTION) values � the VR device was connected or disconnected.
### Return value

Type of the VR device input event, one of the [INPUT_EVENT_VR_DEVICE_ACTION_*](#ACTION_CONNECTED) values.
## void setConnectionID ( int connectionid )

Sets the identifier of the device connection the event comes from. See *[getConnectionID()()](../../...md#getConnectionID_int)*.
### Arguments

- *int* **connectionid** - Connection identifier.

## int getConnectionID ( )

Returns the identifier of the device connection the event comes from � the value assigned by the OS when the device was connected. The engine uses it to match the event against a device slot; it is not the slot index itself.
### Return value

Connection identifier.
## void setType ( int type )

Sets the type of the VR device the event refers to. See *[getType()()](../../...md#getType_int)*.
### Arguments

- *int* **type** - VR device type, one of the [InputVRDevice::TYPE](../../../api/library/controls/class.inputvrdevice_usc.md#TYPE) values.

## int getType ( )

Returns the type of the VR device the event refers to � one of the [InputVRDevice::TYPE](../../../api/library/controls/class.inputvrdevice_usc.md#TYPE) values. The type is filled in only for a connection event: on disconnection it carries a placeholder value, so identify the device by [ConnectionID](#ConnectionID) instead.
### Return value

VR device type, one of the [InputVRDevice::TYPE](../../../api/library/controls/class.inputvrdevice_usc.md#TYPE) values.
