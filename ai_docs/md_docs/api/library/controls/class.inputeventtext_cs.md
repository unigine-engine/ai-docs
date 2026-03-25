# Unigine::InputEventText Class (CS)

**Inherits from:** InputEvent


This class controls text event information.


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
