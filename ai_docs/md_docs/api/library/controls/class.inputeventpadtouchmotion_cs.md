# Unigine::InputEventPadTouchMotion Class (CS)

**Inherits from:** InputEvent


This class controls the gamepad physical touch panel event information.


## InputEventPadTouchMotion Class

### Enums

## ACTION

| Name | Description |
|---|---|
| **DOWN** = 0 | Touch state is "pressed". |
| **MOTION** = 1 | Touch state is "pressed and moving". |
| **UP** = 2 | Touch state is "released". |

### Properties

## int ConnectionID

The connection identifier.
## InputEventPadTouchMotion.ACTION Action

The type of the touch input event, one of the [ACTION](#ACTION) values.
## int Touch

The index of the gamepad touch panel, the number from 0 to the [total number](../../../api/library/controls/class.inputgamepad_cs.md#getNumTouches_int) of touch panels.
## int TouchFinger

The index of the finger, the number from 0 to the [total number](../../../api/library/controls/class.inputgamepad_cs.md#getNumTouchFingers_int_int) of supported fingers.
## vec2 Position

The normalized position of the touch along the axes from (0,0) to (1,1).
## float Pressure

The pressure with which the finger is currently pressed, a value from 0 (not pressed) to 1 (fully pressed).
### Members

---

## InputEventPadTouchMotion ( )

Default constructor.
## InputEventPadTouchMotion ( ulong timestamp , ivec2 mouse_pos )

Touch panel input event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.

## InputEventPadTouchMotion ( ulong timestamp , ivec2 mouse_pos , int connection_id , int action , int touch , int finger , float pressure , vec2 position )

Touch panel input event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
- *int* **connection_id** - The connection identifier.
- *int* **action** - The type of the touch input event, one of the [ACTION](#ACTION) values.
- *int* **touch** - The index of the gamepad touch panel, the number from 0 to the [total number](../../../api/library/controls/class.inputgamepad_cs.md#getNumTouches_int) of touch panels.
- *int* **finger** - The index of the finger, the number from 0 to the [total number](../../../api/library/controls/class.inputgamepad_cs.md#getNumTouchFingers_int_int) of supported fingers.
- *float* **pressure** - Pressure with which the finger is currently pressed.
- *vec2* **position** - The normalized position of the touch along the axes from (0,0) to (1,1).
