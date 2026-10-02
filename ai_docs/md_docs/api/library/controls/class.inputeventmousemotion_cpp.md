# Unigine::InputEventMouseMotion Class (CPP)

**Header:** #include <UnigineInput.h>

**Inherits from:** InputEvent


This class controls mouse motion event information.


Events of this type are created by the engine and passed to your handlers. You can also construct one yourself and dispatch it via *[Input::sendEvent()](../../../api/library/controls/class.input_cpp.md#sendEvent_InputEvent_void)*, which is what a custom SystemProxy implementation or a device emulator does.


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

Returns the raw movement reported by the mouse for this event. The value comes from the raw input of the OS, so it is not affected by pointer acceleration or desktop sensitivity settings and is not limited by the screen borders. [Input::MouseDeltaRaw](../../../api/library/controls/class.input_cpp.md#MouseDeltaRaw) is the sum of these values over the frame.
### Return value

Delta of the mouse position from the previous event.
