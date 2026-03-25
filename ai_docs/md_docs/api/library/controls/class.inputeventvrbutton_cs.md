# Unigine::InputEventVRButton Class (CS)

**Inherits from:** InputEvent


This class controls VR controller button event information.


## InputEventVRButton Class

### Enums

## ACTION

| Name | Description |
|---|---|
| **DOWN** = 0 | Button state is "pressed". |
| **UP** = 1 | Button state is "released". |

### Properties

## InputEventVRButton.ACTION Action

The Type of the VR controller button input event, one of the [ACTION](#ACTION) values.
## int ConnectionID

The Connection identifier.
## Input.VR_BUTTON Button

The VR controller button index.
### Members

---

## InputEventVRButton ( )

Default constructor.
## InputEventVRButton ( ulong timestamp , ivec2 mouse_pos )

VR controller button input event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.

## InputEventVRButton ( ulong timestamp , ivec2 mouse_pos , InputEventVRButton.ACTION action , int connection_id , Input.VR_BUTTON button )

VR controller button input event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
- *[InputEventVRButton.ACTION](../../../api/library/controls/class.inputeventvrbutton_cs.md#ACTION)* **action** - Type of the VR controller button input event, one of the [ACTION](#ACTION) values.
- *int* **connection_id** - Connection identifier.
- *[Input.VR_BUTTON](../../../api/library/controls/class.input_cs.md#VR_BUTTON)* **button** - VR controller button index.
