# Unigine::InputEventPadTouchMotion Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** InputEvent


This class controls the gamepad physical touch panel event information.


Events of this type are created by the engine and passed to your handlers. You can also construct one yourself and dispatch it via *[engine.input.sendEvent()()](../../../api/library/controls/class.input_usc.md#sendEvent_InputEvent_void)*, which is what a custom SystemProxy implementation or a device emulator does.


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

Sets the identifier of the device connection the event comes from. See *[getConnectionID()()](../../...md#getConnectionID_int)*.
### Arguments

- *int* **connectionid** - The connection identifier.

## int getConnectionID ( )

Returns the identifier of the device connection the event comes from � the value assigned by the OS when the device was connected. The engine uses it to match the event against a device slot; it is not the slot index itself.
### Return value

The connection identifier.
## void setAction ( int action )

Sets the action the event represents. See *[getAction()()](../../...md#getAction_int)*.
### Arguments

- *int* **action** - The type of the touch input event, one of the [INPUT_EVENT_PAD_TOUCH_MOTION_ACTION_*](#ACTION_DOWN) values.

## int getAction ( )

Returns the action the event represents: one of the [ACTION](#ACTION) values � the finger touched the panel, moved across it, or was lifted.
### Return value

The type of the touch input event, one of the [INPUT_EVENT_PAD_TOUCH_MOTION_ACTION_*](#ACTION_DOWN) values.
## void setTouch ( int touch )

Sets the index of the gamepad touch panel.
### Arguments

- *int* **touch** - The index of the gamepad touch panel, the number from 0 to the [total number](../../../api/library/controls/class.inputgamepad_usc.md#getNumTouches_int) of touch panels.

## int getTouch ( )

Returns the index of the gamepad touch panel that generated the event. The index is within the number of panels reported by *[engine.inputgamepad.getNumTouches()()](../../../api/library/controls/class.inputgamepad_usc.md#getNumTouches_int)*.
### Return value

The index of the gamepad touch panel, the number from 0 to the [total number](../../../api/library/controls/class.inputgamepad_usc.md#getNumTouches_int) of touch panels.
## void setTouchFinger ( int finger )

Sets the index of the finger.
### Arguments

- *int* **finger** - The index of the finger, the number from 0 to the [total number](../../../api/library/controls/class.inputgamepad_usc.md#getNumTouchFingers_int_int) of supported fingers.

## int getTouchFinger ( )

Returns the index of the finger that generated the event. A panel tracks several fingers at once; the index is within the number reported by *[engine.inputgamepad.getNumTouchFingers()()](../../../api/library/controls/class.inputgamepad_usc.md#getNumTouchFingers_int_int)*.
### Return value

The index of the finger, the number from 0 to the [total number](../../../api/library/controls/class.inputgamepad_usc.md#getNumTouchFingers_int_int) of supported fingers.
## void setPosition ( vec2 position )

Sets the touch position.
### Arguments

- *vec2* **position** - The normalized position of the touch along the axes from (0,0) to (1,1).

## vec2 getPosition ( )

Returns the position of the finger on the touch panel, normalized to the [0; 1] range along both axes, with (0,0) at the upper-left corner of the panel.
### Return value

The normalized position of the touch along the axes from (0,0) to (1,1).
## void setPressure ( float pressure )

Sets the pressure with which the finger is pressed.
### Arguments

- *float* **pressure** - The pressure with which the finger is pressed, a value from 0 (not pressed) to 1 (fully pressed).

## float getPressure ( )

Returns how hard the finger presses the panel, normalized to the [0; 1] range.
### Return value

The pressure with which the finger is currently pressed, a value from 0 (not pressed) to 1 (fully pressed).
