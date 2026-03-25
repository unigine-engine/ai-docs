# Unigine::InputEventPadTouchMotion Class (CPP)

**Header:** #include <UnigineInput.h>

**Inherits from:** InputEvent


This class controls the gamepad physical touch panel event information.


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

Sets the connection identifier.
### Arguments

- *int* **connectionid** - The connection identifier.

## int getConnectionID ( ) const

Returns the connection identifier.
### Return value

The connection identifier.
## void setAction ( InputEventPadTouchMotion::ACTION action )

Sets the type of the touch panel input event.
### Arguments

- *[InputEventPadTouchMotion::ACTION](../../../api/library/controls/class.inputeventpadtouchmotion_cpp.md#ACTION)* **action** - The type of the touch input event, one of the [ACTION_*](#ACTION_DOWN) values.

## InputEventPadTouchMotion::ACTION getAction ( ) const

Returns the type of the touch panel input event.
### Return value

The type of the touch input event, one of the [ACTION_*](#ACTION_DOWN) values.
## void setTouch ( int touch )

Sets the index of the gamepad touch panel.
### Arguments

- *int* **touch** - The index of the gamepad touch panel, the number from 0 to the [total number](../../../api/library/controls/class.inputgamepad_cpp.md#getNumTouches_int) of touch panels.

## int getTouch ( ) const

Returns the index of the gamepad touch panel.
### Return value

The index of the gamepad touch panel, the number from 0 to the [total number](../../../api/library/controls/class.inputgamepad_cpp.md#getNumTouches_int) of touch panels.
## void setTouchFinger ( int finger )

Sets the index of the finger.
### Arguments

- *int* **finger** - The index of the finger, the number from 0 to the [total number](../../../api/library/controls/class.inputgamepad_cpp.md#getNumTouchFingers_int_int) of supported fingers.

## int getTouchFinger ( ) const

Returns the index of the finger.
### Return value

The index of the finger, the number from 0 to the [total number](../../../api/library/controls/class.inputgamepad_cpp.md#getNumTouchFingers_int_int) of supported fingers.
## void setPosition ( const Math:: vec2 & position )

Sets the touch position.
### Arguments

- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **position** - The normalized position of the touch along the axes from (0,0) to (1,1).

## Math:: vec2 getPosition ( ) const

Returns the current touch position.
### Return value

The normalized position of the touch along the axes from (0,0) to (1,1).
## void setPressure ( float pressure )

Sets the pressure with which the finger is pressed.
### Arguments

- *float* **pressure** - The pressure with which the finger is pressed, a value from 0 (not pressed) to 1 (fully pressed).

## float getPressure ( ) const

Returns the pressure with which the finger is pressed.
### Return value

The pressure with which the finger is currently pressed, a value from 0 (not pressed) to 1 (fully pressed).
