# Unigine::InputEventSystem Class (CS)

**Inherits from:** InputEvent


This class controls system events such as changing the input language of the keyboard layout.


Events of this type are created by the engine and passed to your handlers. You can also construct one yourself and dispatch it via *[Input.SendEvent()](../../../api/library/controls/class.input_cs.md#sendEvent_InputEvent_void)*, which is what a custom SystemProxy implementation or a device emulator does.


## InputEventSystem Class

### Enums

## ACTION

System event actions.
| Name | Description |
|---|---|
| **KEYBOARD_LAYOUT_CHANGED** = 0 | Keyboard layout has changed. |

### Properties

## InputEventSystem.ACTION Action

The action of the system event.
### Members

---

## InputEventSystem ( )

Default constructor.
## InputEventSystem ( uint timestamp , ivec2 mouse_pos )

Default constructor.
### Arguments

- *uint* **timestamp** - Timestamp of the event (time when the event occurred).
- *ivec2* **mouse_pos** - Coordinates of the mouse cursor position along X and Y axes.

## InputEventSystem ( uint timestamp , ivec2 mouse_pos , InputEventSystem.ACTION action )

Default constructor.
### Arguments

- *uint* **timestamp** - Timestamp of the event (time when the event occurred).
- *ivec2* **mouse_pos** - Coordinates of the mouse cursor position along X and Y axes.
- *[InputEventSystem.ACTION](../../../api/library/controls/class.inputeventsystem_cs.md#ACTION)* **action** - action of the system event.
