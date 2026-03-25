# Unigine::InputEventTouch Class (CS)

**Inherits from:** InputEvent


This class controls touch event information.


## InputEventTouch Class

### Enums

## ACTION

| Name | Description |
|---|---|
| **DOWN** = 0 | Touch state is "pressed". |
| **MOTION** = 1 | Touch state is "pressed and moving". |
| **UP** = 2 | Touch state is "released". |

### Properties

## InputEventTouch.ACTION Action

The type of the touch input event, one of the [ACTION](#ACTION) values.
## long DeviceID

The device identifier.
## long TouchID

The touch identifier.
## ivec2 Position

The touch position.
## ivec2 Delta

The delta of the mouse position from the previous event.
## float Pressure

The pressure with which the finger is currently pressed.
### Members

---

## InputEventTouch ( )

Default constructor.
## InputEventTouch ( ulong timestamp , ivec2 mouse_pos )

Touch input event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.

## InputEventTouch ( ulong timestamp , ivec2 mouse_pos , InputEventTouch.ACTION action , long device_id , long touch_id )

Touch input event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
- *[InputEventTouch.ACTION](../../../api/library/controls/class.inputeventtouch_cs.md#ACTION)* **action** - The type of the touch input event, one of the [ACTION](#ACTION) values.
- *long* **device_id** - Device identifier.
- *long* **touch_id** - Touch identifier.

## InputEventTouch ( ulong timestamp , ivec2 mouse_pos , InputEventTouch.ACTION action , long device_id , long touch_id , ivec2 pos , ivec2 delta , float pressure )

Touch input event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
- *[InputEventTouch.ACTION](../../../api/library/controls/class.inputeventtouch_cs.md#ACTION)* **action** - The type of the touch input event, one of the [ACTION](#ACTION) values.
- *long* **device_id** - Device identifier.
- *long* **touch_id** - Touch identifier.
- *ivec2* **pos** - Touch position.
- *ivec2* **delta** - Delta of the touch position from the previous event.
- *float* **pressure** - Pressure with which the finger is currently pressed.
