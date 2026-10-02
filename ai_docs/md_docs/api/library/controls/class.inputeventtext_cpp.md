# Unigine::InputEventText Class (CPP)

**Header:** #include <UnigineInput.h>

**Inherits from:** InputEvent


This class controls text event information.


Events of this type are created by the engine and passed to your handlers. You can also construct one yourself and dispatch it via *[Input::sendEvent()](../../../api/library/controls/class.input_cpp.md#sendEvent_InputEvent_void)*, which is what a custom SystemProxy implementation or a device emulator does.


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

Returns the Unicode character code the event carries. A text event is produced by the OS after the keyboard input has been processed, so the character already accounts for the current layout and the modifiers held.
### Return value

Unicode symbol.
