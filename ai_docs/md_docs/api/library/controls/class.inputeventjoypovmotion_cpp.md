# Unigine::InputEventJoyPovMotion Class (CPP)

**Header:** #include <UnigineInput.h>

**Inherits from:** InputEvent


This class controls joystick POV hat motion event information.


Events of this type are created by the engine and passed to your handlers. You can also construct one yourself and dispatch it via *[Input::sendEvent()](../../../api/library/controls/class.input_cpp.md#sendEvent_InputEvent_void)*, which is what a custom SystemProxy implementation or a device emulator does.


### See Also


- C++ sample
- C# Component sample


## InputEventJoyPovMotion Class

### Members

---

## InputEventJoyPovMotion ( )

Default constructor.
## InputEventJoyPovMotion ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos )

Joystick POV hat motion event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.

## InputEventJoyPovMotion ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos , int connection_id , int pov , int value )

Joystick POV hat motion event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.
- *int* **connection_id** - Connection identifier.
- *int* **pov** - Index of the POV hat.
- *int* **value** - Position of the POV hat.

## void setConnectionID ( int id )

Sets the identifier of the device connection the event comes from. See *[getConnectionID()](../../...md#getConnectionID_int)*.
### Arguments

- *int* **id** - Connection identifier to be set.

## int getConnectionID ( ) const

Returns the identifier of the device connection the event comes from � the value assigned by the OS when the device was connected. The engine uses it to match the event against a device slot; it is not the slot index itself.
### Return value

Connection identifier.
## void setPov ( int pov )

Sets the POV hat the event refers to. See *[getPov()](../../...md#getPov_int)*.
### Arguments

- *int* **pov** - Index of the POV hat.

## int getPov ( ) const

Returns the index of the POV hat that generated the event. The index is within the number of hats reported by *[InputJoystick::getNumPovs()](../../../api/library/controls/class.inputjoystick_cpp.md#getNumPovs_int)*.
### Return value

Index of the POV hat.
## void setValue ( int value )

Sets the POV hat direction carried by the event. See *[getValue()](../../...md#getValue_int)*.
### Arguments

- *int* **value** - Position of the POV hat.

## int getValue ( ) const

Returns the direction the POV hat points at the moment of the event � one of the [Input::JOYSTICK_POV](../../../api/library/controls/class.input_cpp.md#JOYSTICK_POV) values, or [JOYSTICK_POV_NOT_PRESSED](../../../api/library/controls/class.input_cpp.md#JOYSTICK_POV_NOT_PRESSED) when the hat is centered.
### Return value

Position of the POV hat.
