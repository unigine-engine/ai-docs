# Unigine::InputEventPadTouchMotion Class (CPP)

**Header:** #include <UnigineInput.h>

**Inherits from:** InputEvent


This class controls the gamepad physical touch panel event information.


Events of this type are created by the engine and passed to your handlers. You can also construct one yourself and dispatch it via *[Input::sendEvent()](../../../api/library/controls/class.input_cpp.md#sendEvent_InputEvent_void)*, which is what a custom SystemProxy implementation or a device emulator does.


### See Also


- C++ sample
- C# Component sample


## InputEventPadTouchMotion Class

### Enums

## ACTION

| Name | Description |
|---|---|
| **ACTION_DOWN** = 0 | Touch state is "pressed". |
| **ACTION_MOTION** = 1 | Touch state is "pressed and moving". |
| **ACTION_UP** = 2 | Touch state is "released". |

### Members

---

## InputEventPadTouchMotion ( )

Default constructor.
## InputEventPadTouchMotion ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos )

Touch panel input event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.

## InputEventPadTouchMotion ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos , int connection_id , int action , int touch , int finger , float pressure , const Math:: vec2 & position )

Touch panel input event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.
- *int* **connection_id** - The connection identifier.
- *int* **action** - The type of the touch input event, one of the [ACTION_*](#ACTION_DOWN) values.
- *int* **touch** - The index of the gamepad touch panel, the number from 0 to the [total number](../../../api/library/controls/class.inputgamepad_cpp.md#getNumTouches_int) of touch panels.
- *int* **finger** - The index of the finger, the number from 0 to the [total number](../../../api/library/controls/class.inputgamepad_cpp.md#getNumTouchFingers_int_int) of supported fingers.
- *float* **pressure** - Pressure with which the finger is currently pressed.
- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **position** - The normalized position of the touch along the axes from (0,0) to (1,1).

## void setConnectionID ( int connectionid )

Sets the identifier of the device connection the event comes from. See *[getConnectionID()](../../...md#getConnectionID_int)*.
### Arguments

- *int* **connectionid** - The connection identifier.

## int getConnectionID ( ) const

Returns the identifier of the device connection the event comes from � the value assigned by the OS when the device was connected. The engine uses it to match the event against a device slot; it is not the slot index itself.
### Return value

The connection identifier.
## void setAction ( InputEventPadTouchMotion::ACTION action )

Sets the action the event represents. See *[getAction()](../../...md#getAction_int)*.
### Arguments

- *[InputEventPadTouchMotion::ACTION](../../../api/library/controls/class.inputeventpadtouchmotion_cpp.md#ACTION)* **action** - The type of the touch input event, one of the [ACTION_*](#ACTION_DOWN) values.

## InputEventPadTouchMotion::ACTION getAction ( ) const

Returns the action the event represents: one of the [ACTION](#ACTION) values � the finger touched the panel, moved across it, or was lifted.
### Return value

The type of the touch input event, one of the [ACTION_*](#ACTION_DOWN) values.
## void setTouch ( int touch )

Sets the index of the gamepad touch panel.
### Arguments

- *int* **touch** - The index of the gamepad touch panel, the number from 0 to the [total number](../../../api/library/controls/class.inputgamepad_cpp.md#getNumTouches_int) of touch panels.

## int getTouch ( ) const

Returns the index of the gamepad touch panel that generated the event. The index is within the number of panels reported by *[InputGamePad::getNumTouches()](../../../api/library/controls/class.inputgamepad_cpp.md#getNumTouches_int)*.
### Return value

The index of the gamepad touch panel, the number from 0 to the [total number](../../../api/library/controls/class.inputgamepad_cpp.md#getNumTouches_int) of touch panels.
## void setTouchFinger ( int finger )

Sets the index of the finger.
### Arguments

- *int* **finger** - The index of the finger, the number from 0 to the [total number](../../../api/library/controls/class.inputgamepad_cpp.md#getNumTouchFingers_int_int) of supported fingers.

## int getTouchFinger ( ) const

Returns the index of the finger that generated the event. A panel tracks several fingers at once; the index is within the number reported by *[InputGamePad::getNumTouchFingers()](../../../api/library/controls/class.inputgamepad_cpp.md#getNumTouchFingers_int_int)*.
### Return value

The index of the finger, the number from 0 to the [total number](../../../api/library/controls/class.inputgamepad_cpp.md#getNumTouchFingers_int_int) of supported fingers.
## void setPosition ( const Math:: vec2 & position )

Sets the touch position.
### Arguments

- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **position** - The normalized position of the touch along the axes from (0,0) to (1,1).

## Math:: vec2 getPosition ( ) const

Returns the position of the finger on the touch panel, normalized to the [0; 1] range along both axes, with (0,0) at the upper-left corner of the panel.
### Return value

The normalized position of the touch along the axes from (0,0) to (1,1).
## void setPressure ( float pressure )

Sets the pressure with which the finger is pressed.
### Arguments

- *float* **pressure** - The pressure with which the finger is pressed, a value from 0 (not pressed) to 1 (fully pressed).

## float getPressure ( ) const

Returns how hard the finger presses the panel, normalized to the [0; 1] range.
### Return value

The pressure with which the finger is currently pressed, a value from 0 (not pressed) to 1 (fully pressed).
