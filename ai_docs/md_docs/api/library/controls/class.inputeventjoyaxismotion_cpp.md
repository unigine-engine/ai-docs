# Unigine::InputEventJoyAxisMotion Class (CPP)

**Header:** #include <UnigineInput.h>

**Inherits from:** InputEvent


This class controls joystick axis motion event information.


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

Sets the connection identifier.
### Arguments

- *int* **id** - Connection identifier.

## int getConnectionID ( ) const

Returns the current connection identifier.
### Return value

Connection identifier.
## void setAxis ( int axis )

Sets the joystick axis index.
### Arguments

- *int* **axis** - Joystick axis index.

## int getAxis ( ) const

Sets the joystick axis index.
### Return value

Joystick axis index.
## void setValue ( float value )

Sets the axis position value.
### Arguments

- *float* **value** - Axis position value.

## float getValue ( ) const

Returns the axis position value.
### Return value

Axis position value.
