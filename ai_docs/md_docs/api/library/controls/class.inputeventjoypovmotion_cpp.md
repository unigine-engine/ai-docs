# Unigine::InputEventJoyPovMotion Class (CPP)

**Header:** #include <UnigineInput.h>

**Inherits from:** InputEvent


This class controls joystick POV hat motion event information.


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

Sets the connection identifier.
### Arguments

- *int* **id** - Connection identifier to be set.

## int getConnectionID ( ) const

Returns the connection identifier.
### Return value

Connection identifier.
## void setPov ( int pov )

Sets the index of the POV hat.
### Arguments

- *int* **pov** - Index of the POV hat.

## int getPov ( ) const

Returns the index of the POV hat.
### Return value

Index of the POV hat.
## void setValue ( int value )

Sets the position of the POV hat.
### Arguments

- *int* **value** - Position of the POV hat.

## int getValue ( ) const

Returns the position of the POV hat.
### Return value

Position of the POV hat.
