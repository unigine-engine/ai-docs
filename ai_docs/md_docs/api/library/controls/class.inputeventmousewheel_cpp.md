# Unigine::InputEventMouseWheel Class (CPP)

**Header:** #include <UnigineInput.h>

**Inherits from:** InputEvent


This class controls mouse wheel event information.


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

Returns the delta of the vertical mouse scroll movement.
### Return value

The amount scrolled vertically, positive away from the user and negative towards the user.
## void setWheelHorizontal ( int horizontal )

Sets the delta of the horizontal mouse scroll movement.
### Arguments

- *int* **horizontal** - The amount scrolled horizontally, positive to the right and negative to the left.

## int getWheelHorizontal ( ) const

Returns the delta of the horizontal mouse scroll movement.
### Return value

The amount scrolled horizontally, positive to the right and negative to the left.
