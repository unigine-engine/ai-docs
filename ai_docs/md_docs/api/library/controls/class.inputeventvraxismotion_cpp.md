# Unigine::InputEventVRAxisMotion Class (CPP)

**Header:** #include <UnigineInput.h>

**Inherits from:** InputEvent


This class controls the VR controller axis motion event information.


## InputEventVRAxisMotion Class

### Members

---

## InputEventVRAxisMotion ( )

Default constructor.
## InputEventVRAxisMotion ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos )

VR controller axis motion event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.

## InputEventVRAxisMotion ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos , int connection_id , int axis , float value )

VR controller axis motion event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.
- *int* **connection_id** - Connection identifier.
- *int* **axis** - VR controller axis index.
- *float* **value** - Axis position value.

## void setConnectionID ( int connectionid )

Sets the connection identifier.
### Arguments

- *int* **connectionid** - Connection identifier to be set.

## int getConnectionID ( ) const

Returns the current connection identifier.
### Return value

Connection identifier.
## void setAxis ( int axis )

Sets the VR controller axis.
### Arguments

- *int* **axis** - The VR controller axis.

## int getAxis ( ) const

Returns the VR controller axis.
### Return value

The VR controller axis.
## void setValue ( float value )

Sets the axis position value.
### Arguments

- *float* **value** - The axis position value.

## float getValue ( ) const

Returns the axis position value.
### Return value

The axis position value.
