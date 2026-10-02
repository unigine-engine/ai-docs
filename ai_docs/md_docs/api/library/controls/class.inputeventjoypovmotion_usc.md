# Unigine::InputEventJoyPovMotion Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** InputEvent


This class controls joystick POV hat motion event information.


Events of this type are created by the engine and passed to your handlers. You can also construct one yourself and dispatch it via *[engine.input.sendEvent()()](../../../api/library/controls/class.input_usc.md#sendEvent_InputEvent_void)*, which is what a custom SystemProxy implementation or a device emulator does.


## InputEventJoyPovMotion Class

### Members

---

## InputEventJoyPovMotion ( )

Default constructor.
## InputEventJoyPovMotion ( long timestamp , ivec2 mouse_pos )

Joystick POV hat motion event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.

## InputEventJoyPovMotion ( long timestamp , ivec2 mouse_pos , int connection_id , int pov , int value )

Joystick POV hat motion event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
- *int* **connection_id** - Connection identifier.
- *int* **pov** - Index of the POV hat.
- *int* **value** - Position of the POV hat.

## void setConnectionID ( int id )

Sets the identifier of the device connection the event comes from. See *[getConnectionID()()](../../...md#getConnectionID_int)*.
### Arguments

- *int* **id** - Connection identifier to be set.

## int getConnectionID ( )

Returns the identifier of the device connection the event comes from � the value assigned by the OS when the device was connected. The engine uses it to match the event against a device slot; it is not the slot index itself.
### Return value

Connection identifier.
## void setPov ( int pov )

Sets the POV hat the event refers to. See *[getPov()()](../../...md#getPov_int)*.
### Arguments

- *int* **pov** - Index of the POV hat.

## int getPov ( )

Returns the index of the POV hat that generated the event. The index is within the number of hats reported by *[engine.inputjoystick.getNumPovs()()](../../../api/library/controls/class.inputjoystick_usc.md#getNumPovs_int)*.
### Return value

Index of the POV hat.
## void setValue ( int value )

Sets the POV hat direction carried by the event. See *[getValue()()](../../...md#getValue_int)*.
### Arguments

- *int* **value** - Position of the POV hat.

## int getValue ( )

Returns the direction the POV hat points at the moment of the event � one of the [Input::JOYSTICK_POV](../../../api/library/controls/class.input_usc.md#JOYSTICK_POV) values, or [JOYSTICK_POV_NOT_PRESSED](../../../api/library/controls/class.input_usc.md#JOYSTICK_POV_NOT_PRESSED) when the hat is centered.
### Return value

Position of the POV hat.
