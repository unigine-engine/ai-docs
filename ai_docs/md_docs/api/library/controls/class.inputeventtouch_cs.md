# Unigine::InputEventTouch Class (CS)

**Inherits from:** InputEvent


This class controls touch event information.


Events of this type are created by the engine and passed to your handlers. You can also construct one yourself and dispatch it via *[Input.SendEvent()](../../../api/library/controls/class.input_cs.md#sendEvent_InputEvent_void)*, which is what a custom SystemProxy implementation or a device emulator does.


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

The touch movement since the previous event of this touch, in screen pixels.
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
