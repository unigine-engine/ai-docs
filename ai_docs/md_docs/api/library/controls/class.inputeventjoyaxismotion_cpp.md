# Unigine::InputEventJoyAxisMotion Class (CPP)

**Header:** #include <UnigineInput.h>

**Inherits from:** InputEvent


This class controls joystick axis motion event information.


Events of this type are created by the engine and passed to your handlers. You can also construct one yourself and dispatch it via *[Input::sendEvent()](../../../api/library/controls/class.input_cpp.md#sendEvent_InputEvent_void)*, which is what a custom SystemProxy implementation or a device emulator does.


### See Also


- C++ sample
- C# Component sample


## InputEventJoyAxisMotion Class

### Members

---

## InputEventJoyAxisMotion ( )

Default constructor.
## InputEventJoyAxisMotion ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos )

Joystick axis motion event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.

## InputEventJoyAxisMotion ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos , int connection_id , int axis , float value )

Joystick axis motion event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.
- *int* **connection_id** - Connection identifier.
- *int* **axis** - Joystick axis index.
- *float* **value** - Axis position value.

## void setConnectionID ( int id )

Sets the identifier of the device connection the event comes from. See *[getConnectionID()](../../...md#getConnectionID_int)*.
### Arguments

- *int* **id** - Connection identifier.

## int getConnectionID ( ) const

Returns the identifier of the device connection the event comes from � the value assigned by the OS when the device was connected. The engine uses it to match the event against a device slot; it is not the slot index itself.
### Return value

Connection identifier.
## void setAxis ( int axis )

Sets the joystick axis the event refers to. See *[getAxis()](../../...md#getAxis_int)*.
### Arguments

- *int* **axis** - Joystick axis index.

## int getAxis ( ) const

Returns the index of the joystick axis that generated the event. The index is within the number of axes reported by *[InputJoystick::getNumAxes()](../../../api/library/controls/class.inputjoystick_cpp.md#getNumAxes_int)*.
### Return value

Joystick axis index.
## void setValue ( float value )

Sets the axis position carried by the event. See *[getValue()](../../...md#getValue_float)*.
### Arguments

- *float* **value** - Axis position value.

## float getValue ( ) const

Returns the position of the axis at the moment of the event, in the [-1; 1] range. Zero means the axis is in its center position.
### Return value

Axis position value.
