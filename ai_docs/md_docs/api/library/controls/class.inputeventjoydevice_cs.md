# Unigine::InputEventJoyDevice Class (CS)

**Inherits from:** InputEvent


This class controls joystick device event information.


Events of this type are created by the engine and passed to your handlers. You can also construct one yourself and dispatch it via *[Input.SendEvent()](../../../api/library/controls/class.input_cs.md#sendEvent_InputEvent_void)*, which is what a custom SystemProxy implementation or a device emulator does.


## InputEventJoyDevice Class

### Enums

## ACTION

| Name | Description |
|---|---|
| **CONNECTED** = 0 | Joystick state is "connected". |
| **DISCONNECTED** = 1 | Joystick state is "disconnected". |

### Properties

## InputEventJoyDevice.ACTION Action

The Type of the joystick input event, one of the [ACTION](#ACTION) values.
## int ConnectionID

The Connection identifier.
## int PlayerIndex

The Player index.
## string ModelGUID

The GUID of the joystick model.
### Members

---

## InputEventJoyDevice ( )

Default constructor.
## InputEventJoyDevice ( ulong timestamp , ivec2 mouse_pos )

Joystick input event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.

## InputEventJoyDevice ( ulong timestamp , ivec2 mouse_pos , InputEventJoyDevice.ACTION action , int connection_id , int player_index , string model_guid )

Joystick input event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
- *[InputEventJoyDevice.ACTION](../../../api/library/controls/class.inputeventjoydevice_cs.md#ACTION)* **action** - Type of the joystick input event, one of the [ACTION](#ACTION) values.
- *int* **connection_id** - Connection identifier.
- *int* **player_index** - Index of the player.
- *string* **model_guid** - GUID of the joystick model.
