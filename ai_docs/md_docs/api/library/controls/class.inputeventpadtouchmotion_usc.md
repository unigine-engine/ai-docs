# Unigine::InputEventPadTouchMotion Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** InputEvent


This class controls the gamepad physical touch panel event information.


## InputEventPadTouchMotion Class

### Members

---

## InputEventPadTouchMotion ( )

Default constructor.
## InputEventPadTouchMotion ( long timestamp , ivec2 mouse_pos )

Touch panel input event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.

## InputEventPadTouchMotion ( long timestamp , ivec2 mouse_pos , int connection_id , int action , int touch , int finger , float pressure , vec2 position )

Touch panel input event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
- *int* **connection_id** - The connection identifier.
- *int* **action** - The type of the touch input event, one of the [INPUT_EVENT_PAD_TOUCH_MOTION_ACTION_*](#ACTION_DOWN) values.
- *int* **touch** - The index of the gamepad touch panel, the number from 0 to the [total number](../../../api/library/controls/class.inputgamepad_usc.md#getNumTouches_int) of touch panels.
- *int* **finger** - The index of the finger, the number from 0 to the [total number](../../../api/library/controls/class.inputgamepad_usc.md#getNumTouchFingers_int_int) of supported fingers.
- *float* **pressure** - Pressure with which the finger is currently pressed.
- *vec2* **position** - The normalized position of the touch along the axes from (0,0) to (1,1).

## void setConnectionID ( int connectionid )

Sets the connection identifier.
### Arguments

- *int* **connectionid** - The connection identifier.

## int getConnectionID ( )

Returns the connection identifier.
### Return value

The connection identifier.
## void setAction ( int action )

Sets the type of the touch panel input event.
### Arguments

- *int* **action** - The type of the touch input event, one of the [INPUT_EVENT_PAD_TOUCH_MOTION_ACTION_*](#ACTION_DOWN) values.

## int getAction ( )

Returns the type of the touch panel input event.
### Return value

The type of the touch input event, one of the [INPUT_EVENT_PAD_TOUCH_MOTION_ACTION_*](#ACTION_DOWN) values.
## void setTouch ( int touch )

Sets the index of the gamepad touch panel.
### Arguments

- *int* **touch** - The index of the gamepad touch panel, the number from 0 to the [total number](../../../api/library/controls/class.inputgamepad_usc.md#getNumTouches_int) of touch panels.

## int getTouch ( )

Returns the index of the gamepad touch panel.
### Return value

The index of the gamepad touch panel, the number from 0 to the [total number](../../../api/library/controls/class.inputgamepad_usc.md#getNumTouches_int) of touch panels.
## void setTouchFinger ( int finger )

Sets the index of the finger.
### Arguments

- *int* **finger** - The index of the finger, the number from 0 to the [total number](../../../api/library/controls/class.inputgamepad_usc.md#getNumTouchFingers_int_int) of supported fingers.

## int getTouchFinger ( )

Returns the index of the finger.
### Return value

The index of the finger, the number from 0 to the [total number](../../../api/library/controls/class.inputgamepad_usc.md#getNumTouchFingers_int_int) of supported fingers.
## void setPosition ( vec2 position )

Sets the touch position.
### Arguments

- *vec2* **position** - The normalized position of the touch along the axes from (0,0) to (1,1).

## vec2 getPosition ( )

Returns the current touch position.
### Return value

The normalized position of the touch along the axes from (0,0) to (1,1).
## void setPressure ( float pressure )

Sets the pressure with which the finger is pressed.
### Arguments

- *float* **pressure** - The pressure with which the finger is pressed, a value from 0 (not pressed) to 1 (fully pressed).

## float getPressure ( )

Returns the pressure with which the finger is pressed.
### Return value

The pressure with which the finger is currently pressed, a value from 0 (not pressed) to 1 (fully pressed).
