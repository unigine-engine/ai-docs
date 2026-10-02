# Unigine::InputEventVRAxisMotion Class (CPP)

**Header:** #include <UnigineInput.h>

**Inherits from:** InputEvent


This class controls the VR controller axis motion event information.


Events of this type are created by the engine and passed to your handlers. You can also construct one yourself and dispatch it via *[Input::sendEvent()](../../../api/library/controls/class.input_cpp.md#sendEvent_InputEvent_void)*, which is what a custom SystemProxy implementation or a device emulator does.


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

Sets the identifier of the device connection the event comes from. See *[getConnectionID()](../../...md#getConnectionID_int)*.
### Arguments

- *int* **connectionid** - Connection identifier to be set.

## int getConnectionID ( ) const

Returns the identifier of the device connection the event comes from � the value assigned by the OS when the device was connected. The engine uses it to match the event against a device slot; it is not the slot index itself.
### Return value

Connection identifier.
## void setAxis ( int axis )

Sets the VR controller axis the event refers to. See *[getAxis()](../../...md#getAxis_int)*.
### Arguments

- *int* **axis** - The VR controller axis.

## int getAxis ( ) const

Returns the index of the VR controller axis that generated the event.
### Return value

The VR controller axis.
## void setValue ( float value )

Sets the axis position carried by the event. See *[getValue()](../../...md#getValue_float)*.
### Arguments

- *float* **value** - The axis position value.

## float getValue ( ) const

Returns the position of the axis at the moment of the event, in the [-1; 1] range. Zero means the axis is in its center position.
### Return value

The axis position value.
