# Unigine::InputEventText Class (CS)

**Inherits from:** InputEvent


This class controls text event information.


Events of this type are created by the engine and passed to your handlers. You can also construct one yourself and dispatch it via *[Input.SendEvent()](../../../api/library/controls/class.input_cs.md#sendEvent_InputEvent_void)*, which is what a custom SystemProxy implementation or a device emulator does.


## InputEventText Class

### Properties

## uint Unicode

The Unicode symbol.
### Members

---

## InputEventText ( )

Default constructor.
## InputEventText ( ulong timestamp , ivec2 mouse_pos )

Text input event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.

## InputEventText ( ulong timestamp , ivec2 mouse_pos , uint unicode )

Text input event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
- *uint* **unicode** - Unicode symbol.
