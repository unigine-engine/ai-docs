# Unigine::InputEventPadDevice Class (CS)

**Inherits from:** InputEvent


This class controls the game pad event information.


## InputEventPadDevice Class

### Enums

## ACTION

| Name | Description |
|---|---|
| **CONNECTED** = 0 | Game pad state is "connected". |
| **DISCONNECTED** = 1 | Game pad state is "disconnected". |

### Properties

## InputEventPadDevice.ACTION Action

The Type of the game pad input event, one of the [ACTION](#ACTION) values.
## int ConnectionID

The Connection identifier.
## int PlayerIndex

The Player index.
## string ModelGUID

The GUID of the game pad model.
### Members

---

## InputEventPadDevice ( )

Default constructor.
## InputEventPadDevice ( ulong timestamp , ivec2 mouse_pos )

Game pad input event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.

## InputEventPadDevice ( ulong timestamp , ivec2 mouse_pos , InputEventPadDevice.ACTION action , int connection_id , int player_index , string model_guid )

Game pad input event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
- *[InputEventPadDevice.ACTION](../../../api/library/controls/class.inputeventpaddevice_cs.md#ACTION)* **action** - Type of the game pad input event, one of the [ACTION](#ACTION) values.
- *int* **connection_id** - Connection identifier.
- *int* **player_index** - Index of the player.
- *string* **model_guid** - GUID of the game pad model.
