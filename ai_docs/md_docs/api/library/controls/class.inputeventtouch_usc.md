# Unigine::InputEventTouch Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** InputEvent


This class controls touch event information.


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

Sets the type of the touch input event.
### Arguments

- *int* **action** - The type of the touch input event, one of the [INPUT_EVENT_TOUCH_ACTION_*](#ACTION_DOWN) values.

## int getAction ( )

Returns the type of the touch input event.
### Return value

The type of the touch input event, one of the [INPUT_EVENT_TOUCH_ACTION_*](#ACTION_DOWN) values.
## void setDeviceID ( long id )

Sets the touch device identifier.
### Arguments

- *long* **id** - The device identifier.

## long getDeviceID ( )

Returns the current touch device identifier.
### Return value

The device identifier.
## void setTouchID ( long id )

Sets the touch identifier.
### Arguments

- *long* **id** - The touch identifier.

## long getTouchID ( )

Returns the current touch identifier.
### Return value

The touch identifier.
## void setPosition ( ivec2 pos )

Sets the touch position.
### Arguments

- *ivec2* **pos** - The touch position.

## ivec2 getPosition ( )

Returns the current touch position.
### Return value

The touch position.
## void setDelta ( ivec2 delta )

Sets the delta of the mouse position from the previous event.
### Arguments

- *ivec2* **delta** - The delta of the mouse position from the previous event.

## ivec2 getDelta ( )

Returns the delta of the mouse position from the previous event.
### Return value

The delta of the mouse position from the previous event.
## void setPressure ( float pressure )

Sets the pressure with which the finger is pressed.
### Arguments

- *float* **pressure** - The pressure with which the finger is pressed.

## float getPressure ( )

Returns the pressure with which the finger is pressed.
### Return value

The pressure with which the finger is currently pressed.
