# Unigine::InputEventVRButton Class (CPP)

**Header:** #include <UnigineInput.h>

**Inherits from:** InputEvent


This class controls VR controller button event information.


## InputEventVRButton Class

### Enums

## ACTION

| Name | Description |
|---|---|
| **ACTION_DOWN** = 0 | Button state is "pressed". |
| **ACTION_UP** = 1 | Button state is "released". |

### Members

---

## InputEventVRButton ( )

Default constructor.
## InputEventVRButton ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos )

VR controller button input event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.

## InputEventVRButton ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos , InputEventVRButton::ACTION action , int connection_id , Input::VR_BUTTON button )

VR controller button input event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.
- *[InputEventVRButton::ACTION](../../../api/library/controls/class.inputeventvrbutton_cpp.md#ACTION)* **action** - Type of the VR controller button input event, one of the [ACTION_*](#ACTION_DOWN) values.
- *int* **connection_id** - Connection identifier.
- *[Input::VR_BUTTON](../../../api/library/controls/class.input_cpp.md#VR_BUTTON)* **button** - VR controller button index.

## void setAction ( InputEventVRButton::ACTION action )

Sets the type of the VR controller button input event.
### Arguments

- *[InputEventVRButton::ACTION](../../../api/library/controls/class.inputeventvrbutton_cpp.md#ACTION)* **action** - Type of the VR controller button input event, one of the [ACTION_*](#ACTION_DOWN) values.

## InputEventVRButton::ACTION getAction ( ) const

Returns the type of the VR controller button input event.
### Return value

Type of the VR controller button input event, one of the [ACTION_*](#ACTION_DOWN) values.
## void setConnectionID ( int connectionid )

Sets the connection identifier.
### Arguments

- *int* **connectionid** - Connection identifier.

## int getConnectionID ( ) const

Returns the current connection identifier.
### Return value

Connection identifier.
## void setButton ( Input::VR_BUTTON button )

Sets the VR controller button index.
### Arguments

- *[Input::VR_BUTTON](../../../api/library/controls/class.input_cpp.md#VR_BUTTON)* **button** - VR controller button index.

## Input::VR_BUTTON getButton ( ) const

Returns the VR controller button index.
### Return value

VR controller button index.
