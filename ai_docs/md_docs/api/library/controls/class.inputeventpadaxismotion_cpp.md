# Unigine::InputEventPadAxisMotion Class (CPP)

**Header:** #include <UnigineInput.h>

**Inherits from:** InputEvent


This class controls the game pad axis motion event information.


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

Sets the connection identifier.
### Arguments

- *int* **id** - Connection identifier to be set.

## int getConnectionID ( ) const

Returns the current connection identifier.
### Return value

Connection identifier.
## void setAxis ( Input::GAMEPAD_AXIS axis )

Sets the game pad axis.
### Arguments

- *[Input::GAMEPAD_AXIS](../../../api/library/controls/class.input_cpp.md#GAMEPAD_AXIS)* **axis** - The game pad axis, one of the *[Input::GAMEPAD_AXIS_*](../../../api/library/controls/class.input_cpp.md#GAMEPAD_AXIS_LEFT_X)* values.

## Input::GAMEPAD_AXIS getAxis ( ) const

Returns the game pad axis.
### Return value

The game pad axis, one of the *[Input::GAMEPAD_AXIS_*](../../../api/library/controls/class.input_cpp.md#GAMEPAD_AXIS_LEFT_X)* values.
## void setValue ( float value )

Sets the axis position value.
### Arguments

- *float* **value** - The axis position value.

## float getValue ( ) const

Returns the axis position value.
### Return value

The axis position value.
