# Unigine::InputEventMouseMotion Class (CPP)

**Header:** #include <UnigineInput.h>

**Inherits from:** InputEvent


This class controls mouse motion event information.


### See Also


- C++ sample
- C# Component sample


## InputEventMouseMotion Class

### Members

---

## InputEventMouseMotion ( )

Default constructor.
## InputEventMouseMotion ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos , const Math:: ivec2 & delta )

Mouse motion input event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **delta** - Delta of the mouse position from the previous event.

## InputEventMouseMotion ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos )

Mouse motion input event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.

## void setDelta ( const Math:: ivec2 & delta )

Sets the delta of the mouse position from the previous event.
### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **delta** - Delta of the mouse position from the previous event.

## Math:: ivec2 getDelta ( ) const

Returns the delta of the mouse position from the previous event.
### Return value

Delta of the mouse position from the previous event.
