# Unigine::InputEventPadAxisMotion Class (CPP)

**Header:** #include <UnigineInput.h>

**Inherits from:** InputEvent


This class controls the game pad axis motion event information.


Events of this type are created by the engine and passed to your handlers. You can also construct one yourself and dispatch it via *[Input::sendEvent()](../../../api/library/controls/class.input_cpp.md#sendEvent_InputEvent_void)*, which is what a custom SystemProxy implementation or a device emulator does.


### See Also


- C++ sample
- C# Component sample


## InputEventPadAxisMotion Class

### Members

---

## InputEventPadAxisMotion ( )

Default constructor.
## InputEventPadAxisMotion ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos )

Game pad axis motion event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.

## InputEventPadAxisMotion ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos , int connection_id , int axis , float value )

Game pad axis motion event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.
- *int* **connection_id** - Connection identifier.
- *int* **axis** - Game pad axis index.
- *float* **value** - Axis position value.

## void setConnectionID ( int id )

Sets the identifier of the device connection the event comes from. See *[getConnectionID()](../../...md#getConnectionID_int)*.
### Arguments

- *int* **id** - Connection identifier to be set.

## int getConnectionID ( ) const

Returns the identifier of the device connection the event comes from � the value assigned by the OS when the device was connected. The engine uses it to match the event against a device slot; it is not the slot index itself.
### Return value

Connection identifier.
## void setAxis ( Input::GAMEPAD_AXIS axis )

Sets the gamepad axis the event refers to. See *[getAxis()](../../...md#getAxis_int)*.
### Arguments

- *[Input::GAMEPAD_AXIS](../../../api/library/controls/class.input_cpp.md#GAMEPAD_AXIS)* **axis** - The game pad axis, one of the *[Input::GAMEPAD_AXIS_*](../../../api/library/controls/class.input_cpp.md#GAMEPAD_AXIS_LEFT_X)* values.

## Input::GAMEPAD_AXIS getAxis ( ) const

Returns the gamepad axis the event refers to � one of the [Input::GAMEPAD_AXIS](../../../api/library/controls/class.input_cpp.md#GAMEPAD_AXIS) values.
### Return value

The game pad axis, one of the *[Input::GAMEPAD_AXIS_*](../../../api/library/controls/class.input_cpp.md#GAMEPAD_AXIS_LEFT_X)* values.
## void setValue ( float value )

Sets the axis position carried by the event. See *[getValue()](../../...md#getValue_float)*.
### Arguments

- *float* **value** - The axis position value.

## float getValue ( ) const

Returns the position of the axis at the moment of the event, in the [-1; 1] range. The sticks use the whole range with zero at the center, while the triggers are reported by the hardware as unsigned values and therefore stay within [0; 1]. The Y axes are inverted, so positive values mean up.
### Return value

The axis position value.
