# Unigine::InputEventTouch Class (CPP)

**Header:** #include <UnigineInput.h>

**Inherits from:** InputEvent


This class controls touch event information.


Events of this type are created by the engine and passed to your handlers. You can also construct one yourself and dispatch it via *[Input::sendEvent()](../../../api/library/controls/class.input_cpp.md#sendEvent_InputEvent_void)*, which is what a custom SystemProxy implementation or a device emulator does.


### See Also


- C++ sample
- C# Component sample


## InputEventTouch Class

### Enums

## ACTION

| Name | Description |
|---|---|
| **ACTION_DOWN** = 0 | Touch state is "pressed". |
| **ACTION_MOTION** = 1 | Touch state is "pressed and moving". |
| **ACTION_UP** = 2 | Touch state is "released". |

### Members

---

## InputEventTouch ( )

Default constructor.
## InputEventTouch ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos )

Touch input event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.

## InputEventTouch ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos , InputEventTouch::ACTION action , long long device_id , long long touch_id )

Touch input event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.
- *[InputEventTouch::ACTION](../../../api/library/controls/class.inputeventtouch_cpp.md#ACTION)* **action** - The type of the touch input event, one of the [ACTION_*](#ACTION_DOWN) values.
- *long long* **device_id** - Device identifier.
- *long long* **touch_id** - Touch identifier.

## InputEventTouch ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos , InputEventTouch::ACTION action , long long device_id , long long touch_id , const Math:: ivec2 & pos , const Math:: ivec2 & delta , float pressure )

Touch input event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.
- *[InputEventTouch::ACTION](../../../api/library/controls/class.inputeventtouch_cpp.md#ACTION)* **action** - The type of the touch input event, one of the [ACTION_*](#ACTION_DOWN) values.
- *long long* **device_id** - Device identifier.
- *long long* **touch_id** - Touch identifier.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **pos** - Touch position.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **delta** - Delta of the touch position from the previous event.
- *float* **pressure** - Pressure with which the finger is currently pressed.

## void setAction ( InputEventTouch::ACTION action )

Sets the action the event represents. See *[getAction()](../../...md#getAction_int)*.
### Arguments

- *[InputEventTouch::ACTION](../../../api/library/controls/class.inputeventtouch_cpp.md#ACTION)* **action** - The type of the touch input event, one of the [ACTION_*](#ACTION_DOWN) values.

## InputEventTouch::ACTION getAction ( ) const

Returns the action the event represents: one of the [ACTION](#ACTION) values � the touch began, moved, or ended.
### Return value

The type of the touch input event, one of the [ACTION_*](#ACTION_DOWN) values.
## void setDeviceID ( long long id )

Sets the touch device identifier.
### Arguments

- *long long* **id** - The device identifier.

## long long getDeviceID ( ) const

Returns the identifier of the touch device that produced the event. A system can have several touch devices, and every touch belongs to one of them.
### Return value

The device identifier.
## void setTouchID ( long long id )

Sets the touch identifier.
### Arguments

- *long long* **id** - The touch identifier.

## long long getTouchID ( ) const

Returns the identifier of the individual touch. It stays the same from the moment the finger touches the screen until it is lifted, which makes it possible to follow a single finger across events.
### Return value

The touch identifier.
## void setPosition ( const Math:: ivec2 & pos )

Sets the touch position.
### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **pos** - The touch position.

## Math:: ivec2 getPosition ( ) const

Returns the position of the touch in global (desktop) coordinates: the normalized position reported by the OS scaled by the window size and offset by the window position.
### Return value

The touch position.
## void setDelta ( const Math:: ivec2 & delta )

Sets the touch movement since the previous event of this touch.
### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **delta** - The touch movement since the previous event of this touch, in screen pixels.

## Math:: ivec2 getDelta ( ) const

Returns the touch movement since the previous event of this touch, in screen pixels. The value comes from the normalized finger delta reported by the OS, scaled by the window size.
### Return value

The touch movement since the previous event of this touch, in screen pixels.
## void setPressure ( float pressure )

Sets the pressure with which the finger is pressed.
### Arguments

- *float* **pressure** - The pressure with which the finger is pressed.

## float getPressure ( ) const

Returns how hard the finger presses the screen, normalized to the [0; 1] range.
### Return value

The pressure with which the finger is currently pressed.
