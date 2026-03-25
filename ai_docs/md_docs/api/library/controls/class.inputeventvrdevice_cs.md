# Unigine::InputEventVRDevice Class (CS)

**Inherits from:** InputEvent


This class controls VR device event information.


## InputEventVRDevice Class

### Enums

## ACTION

| Name | Description |
|---|---|
| **CONNECTED** = 0 | Device state is "connected". |
| **DISCONNECTED** = 1 | Device state is "disconnected". |

### Properties

## InputEventVRDevice.ACTION Action

The Type of the VR device input event, one of the [ACTION](#ACTION) values.
## int ConnectionID

The Connection identifier.
## InputEventVRDevice.TYPE Type

The VR device type.
### Members

---

## InputEventVRDevice ( )

Default constructor.
## InputEventVRDevice ( ulong timestamp , ivec2 mouse_pos )

VR device input event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.

## InputEventVRDevice ( ulong timestamp , ivec2 mouse_pos , InputEventVRDevice.ACTION action , int connection_id , InputVRDevice.TYPE type )

VR device input event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
- *[InputEventVRDevice.ACTION](../../../api/library/controls/class.inputeventvrdevice_cs.md#ACTION)* **action** - Type of the VR device input event, one of the [ACTION](#ACTION) values.
- *int* **connection_id** - Connection identifier.
- *[InputVRDevice.TYPE](../../../api/library/controls/class.inputvrdevice_cs.md#TYPE)* **type** - VR device type.
