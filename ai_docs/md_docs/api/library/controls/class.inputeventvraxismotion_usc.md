# Unigine::InputEventVRAxisMotion Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** InputEvent


This class controls the VR controller axis motion event information.


Events of this type are created by the engine and passed to your handlers. You can also construct one yourself and dispatch it via *[engine.input.sendEvent()()](../../../api/library/controls/class.input_usc.md#sendEvent_InputEvent_void)*, which is what a custom SystemProxy implementation or a device emulator does.


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

Sets the identifier of the device connection the event comes from. See *[getConnectionID()()](../../...md#getConnectionID_int)*.
### Arguments

- *int* **connectionid** - Connection identifier to be set.

## int getConnectionID ( )

Returns the identifier of the device connection the event comes from � the value assigned by the OS when the device was connected. The engine uses it to match the event against a device slot; it is not the slot index itself.
### Return value

Connection identifier.
## void setAxis ( int axis )

Sets the VR controller axis the event refers to. See *[getAxis()()](../../...md#getAxis_int)*.
### Arguments

- *int* **axis** - The VR controller axis.

## int getAxis ( )

Returns the index of the VR controller axis that generated the event.
### Return value

The VR controller axis.
## void setValue ( float value )

Sets the axis position carried by the event. See *[getValue()()](../../...md#getValue_float)*.
### Arguments

- *float* **value** - The axis position value.

## float getValue ( )

Returns the position of the axis at the moment of the event, in the [-1; 1] range. Zero means the axis is in its center position.
### Return value

The axis position value.
