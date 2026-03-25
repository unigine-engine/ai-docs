# Unigine::InputEventText Class (CPP)

**Header:** #include <UnigineInput.h>

**Inherits from:** InputEvent


This class controls text event information.


## InputEventText Class

### Members

---

## InputEventText ( )

Default constructor.
## InputEventText ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos )

Text input event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.

## InputEventText ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos , unsigned int unicode )

Text input event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.
- *unsigned int* **unicode** - Unicode symbol.

## void setUnicode ( unsigned int unicode )

Sets the input symbol.
### Arguments

- *unsigned int* **unicode** - Unicode symbol.

## unsigned int getUnicode ( ) const

Returns the input symbol.
### Return value

Unicode symbol.
