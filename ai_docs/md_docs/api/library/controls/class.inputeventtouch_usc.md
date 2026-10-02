# Unigine::InputEventTouch Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** InputEvent


This class controls touch event information.


Events of this type are created by the engine and passed to your handlers. You can also construct one yourself and dispatch it via *[engine.input.sendEvent()()](../../../api/library/controls/class.input_usc.md#sendEvent_InputEvent_void)*, which is what a custom SystemProxy implementation or a device emulator does.


## InputEventTouch Class

### Members

---

## InputEventTouch ( )

Default constructor.
## InputEventTouch ( long timestamp , ivec2 mouse_pos )

Touch input event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.

## InputEventTouch ( long timestamp , ivec2 mouse_pos , int action , long device_id , long touch_id )

Touch input event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
- *int* **action** - The type of the touch input event, one of the [INPUT_EVENT_TOUCH_ACTION_*](#ACTION_DOWN) values.
- *long* **device_id** - Device identifier.
- *long* **touch_id** - Touch identifier.

## InputEventTouch ( long timestamp , ivec2 mouse_pos , int action , long device_id , long touch_id , ivec2 pos , ivec2 delta , float pressure )

Touch input event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
- *int* **action** - The type of the touch input event, one of the [INPUT_EVENT_TOUCH_ACTION_*](#ACTION_DOWN) values.
- *long* **device_id** - Device identifier.
- *long* **touch_id** - Touch identifier.
- *ivec2* **pos** - Touch position.
- *ivec2* **delta** - Delta of the touch position from the previous event.
- *float* **pressure** - Pressure with which the finger is currently pressed.

## void setAction ( int action )

Sets the action the event represents. See *[getAction()()](../../...md#getAction_int)*.
### Arguments

- *int* **action** - The type of the touch input event, one of the [INPUT_EVENT_TOUCH_ACTION_*](#ACTION_DOWN) values.

## int getAction ( )

Returns the action the event represents: one of the [ACTION](#ACTION) values � the touch began, moved, or ended.
### Return value

The type of the touch input event, one of the [INPUT_EVENT_TOUCH_ACTION_*](#ACTION_DOWN) values.
## void setDeviceID ( long id )

Sets the touch device identifier.
### Arguments

- *long* **id** - The device identifier.

## long getDeviceID ( )

Returns the identifier of the touch device that produced the event. A system can have several touch devices, and every touch belongs to one of them.
### Return value

The device identifier.
## void setTouchID ( long id )

Sets the touch identifier.
### Arguments

- *long* **id** - The touch identifier.

## long getTouchID ( )

Returns the identifier of the individual touch. It stays the same from the moment the finger touches the screen until it is lifted, which makes it possible to follow a single finger across events.
### Return value

The touch identifier.
## void setPosition ( ivec2 pos )

Sets the touch position.
### Arguments

- *ivec2* **pos** - The touch position.

## ivec2 getPosition ( )

Returns the position of the touch in global (desktop) coordinates: the normalized position reported by the OS scaled by the window size and offset by the window position.
### Return value

The touch position.
## void setDelta ( ivec2 delta )

Sets the touch movement since the previous event of this touch.
### Arguments

- *ivec2* **delta** - The touch movement since the previous event of this touch, in screen pixels.

## ivec2 getDelta ( )

Returns the touch movement since the previous event of this touch, in screen pixels. The value comes from the normalized finger delta reported by the OS, scaled by the window size.
### Return value

The touch movement since the previous event of this touch, in screen pixels.
## void setPressure ( float pressure )

Sets the pressure with which the finger is pressed.
### Arguments

- *float* **pressure** - The pressure with which the finger is pressed.

## float getPressure ( )

Returns how hard the finger presses the screen, normalized to the [0; 1] range.
### Return value

The pressure with which the finger is currently pressed.
