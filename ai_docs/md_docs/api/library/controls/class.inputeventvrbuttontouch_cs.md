# Unigine::InputEventVRButtonTouch Class (CS)

**Inherits from:** InputEvent


This class controls VR controller button touch event information.


## InputEventVRButtonTouch Class

### Enums

## ACTION

| Name | Description |
|---|---|
| **DOWN** = 0 | Button state is "pressed". |
| **UP** = 1 | Button state is "released". |

### Properties

## InputEventVRButtonTouch.ACTION Action

The Type of the VR controller button touch input event, one of the [ACTION](#ACTION) values.
## int ConnectionID

The Connection identifier.
## Input.VR_BUTTON Button

The VR controller button index.
### Members

---

## InputEventVRButtonTouch ( )

Default constructor.
## InputEventVRButtonTouch ( ulong timestamp , ivec2 mouse_pos )

VR controller button touch input event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.

## InputEventVRButtonTouch ( ulong timestamp , ivec2 mouse_pos , InputEventVRButtonTouch.ACTION action , int connection_id , Input.VR_BUTTON button )

VR controller button touch input event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
- *[InputEventVRButtonTouch.ACTION](../../../api/library/controls/class.inputeventvrbuttontouch_cs.md#ACTION)* **action** - Type of the VR controller button touch input event, one of the [ACTION](#ACTION) values.
- *int* **connection_id** - Connection identifier.
- *[Input.VR_BUTTON](../../../api/library/controls/class.input_cs.md#VR_BUTTON)* **button** - VR controller button touch index.
