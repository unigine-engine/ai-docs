# Unigine::InputEventMouseWheel Class (CPP)

**Header:** #include <UnigineInput.h>

**Inherits from:** InputEvent


This class controls mouse wheel event information.


Events of this type are created by the engine and passed to your handlers. You can also construct one yourself and dispatch it via *[Input::sendEvent()](../../../api/library/controls/class.input_cpp.md#sendEvent_InputEvent_void)*, which is what a custom SystemProxy implementation or a device emulator does.


### See Also


- C++ sample
- C# Component sample


## InputEventMouseWheel Class

### Members

---

## static InputEventMouseWheelPtr create ( )

Default constructor.
## InputEventMouseWheel ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos )

Mouse wheel input event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.

## InputEventMouseWheel ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos , int wheel , int wheel_h )

Mouse wheel input event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.
- *int* **wheel** - Delta amount scrolled vertically (positive value - away from the user, negative - towards the user.
- *int* **wheel_h** - Delta amount scrolled horizontally (positive value - to the right, negative - to the left).

## void setWheel ( int wheel )

Sets the delta of the vertical mouse scroll movement.
### Arguments

- *int* **wheel** - The amount scrolled vertically, positive away from the user and negative towards the user.

## int getWheel ( ) const

Returns the vertical scroll amount carried by this event. Negative values correspond to scrolling downwards, positive ones � upwards. Unlike [Input::MouseWheel](../../../api/library/controls/class.input_cpp.md#MouseWheel), which sums up the whole frame, this is the amount of a single event.
### Return value

The amount scrolled vertically, positive away from the user and negative towards the user.
## void setWheelHorizontal ( int horizontal )

Sets the delta of the horizontal mouse scroll movement.
### Arguments

- *int* **horizontal** - The amount scrolled horizontally, positive to the right and negative to the left.

## int getWheelHorizontal ( ) const

Returns the horizontal scroll amount carried by this event. Negative values correspond to scrolling leftwards, positive ones � rightwards. Unlike [Input::MouseWheelHorizontal](../../../api/library/controls/class.input_cpp.md#MouseWheelHorizontal), which sums up the whole frame, this is the amount of a single event.
### Return value

The amount scrolled horizontally, positive to the right and negative to the left.
