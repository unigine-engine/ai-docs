# Unigine::InputEventVRButton Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** InputEvent


This class controls VR controller button event information.


Events of this type are created by the engine and passed to your handlers. You can also construct one yourself and dispatch it via *[engine.input.sendEvent()()](../../../api/library/controls/class.input_usc.md#sendEvent_InputEvent_void)*, which is what a custom SystemProxy implementation or a device emulator does.


## InputEventVRButton Class

### Members

---

## InputEventVRButton ( )

Default constructor.
## InputEventVRButton ( long timestamp , ivec2 mouse_pos )

VR controller button input event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.

## InputEventVRButton ( long timestamp , ivec2 mouse_pos , int action , int connection_id , int button )

VR controller button input event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
- *int* **action** - Type of the VR controller button input event, one of the [INPUT_EVENT_VR_BUTTON_ACTION_*](#ACTION_DOWN) values.
- *int* **connection_id** - Connection identifier.
- *int* **button** - VR controller button index.

## void setAction ( int action )

Sets the action the event represents. See *[getAction()()](../../...md#getAction_int)*.
### Arguments

- *int* **action** - Type of the VR controller button input event, one of the [INPUT_EVENT_VR_BUTTON_ACTION_*](#ACTION_DOWN) values.

## int getAction ( )

Returns the action the event represents: one of the [ACTION](#ACTION) values � the button was pressed or released.
### Return value

Type of the VR controller button input event, one of the [INPUT_EVENT_VR_BUTTON_ACTION_*](#ACTION_DOWN) values.
## void setConnectionID ( int connectionid )

Sets the identifier of the device connection the event comes from. See *[getConnectionID()()](../../...md#getConnectionID_int)*.
### Arguments

- *int* **connectionid** - Connection identifier.

## int getConnectionID ( )

Returns the identifier of the device connection the event comes from � the value assigned by the OS when the device was connected. The engine uses it to match the event against a device slot; it is not the slot index itself.
### Return value

Connection identifier.
## void setButton ( int button )

Sets the VR controller button the event refers to. See *[getButton()()](../../...md#getButton_int)*.
### Arguments

- *int* **button** - VR controller button index.

## int getButton ( )

Returns the VR controller button the event refers to � one of the [Input::VR_BUTTON](../../../api/library/controls/class.input_usc.md#VR_BUTTON) values.
### Return value

VR controller button index.
