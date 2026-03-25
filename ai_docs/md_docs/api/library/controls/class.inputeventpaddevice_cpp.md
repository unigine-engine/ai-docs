# Unigine::InputEventPadDevice Class (CPP)

**Header:** #include <UnigineInput.h>

**Inherits from:** InputEvent


This class controls the game pad event information.


### See Also


- C++ sample
- C# Component sample


## InputEventPadDevice Class

### Enums

## ACTION

| Name | Description |
|---|---|
| **ACTION_CONNECTED** = 0 | Game pad state is "connected". |
| **ACTION_DISCONNECTED** = 1 | Game pad state is "disconnected". |

### Members

---

## InputEventPadDevice ( )

Default constructor.
## InputEventPadDevice ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos )

Game pad input event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.

## InputEventPadDevice ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos , InputEventPadDevice::ACTION action , int connection_id , int player_index , const char * model_guid )

Game pad input event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.
- *[InputEventPadDevice::ACTION](../../../api/library/controls/class.inputeventpaddevice_cpp.md#ACTION)* **action** - Type of the game pad input event, one of the [ACTION_*](#ACTION_CONNECTED) values.
- *int* **connection_id** - Connection identifier.
- *int* **player_index** - Index of the player.
- *const char ** **model_guid** - GUID of the game pad model.

## void setAction ( InputEventPadDevice::ACTION action )

Sets the type of the game pad input event.
### Arguments

- *[InputEventPadDevice::ACTION](../../../api/library/controls/class.inputeventpaddevice_cpp.md#ACTION)* **action** - Type of the game pad input event, one of the [ACTION_*](#ACTION_CONNECTED) values.

## InputEventPadDevice::ACTION getAction ( ) const

Returns the type of the game pad input event.
### Return value

Type of the game pad input event, one of the [ACTION_*](#ACTION_CONNECTED) values.
## void setConnectionID ( int id )

Sets the connection identifier.
### Arguments

- *int* **id** - Connection identifier.

## int getConnectionID ( ) const

Returns the connection identifier.
### Return value

Connection identifier.
## void setPlayerIndex ( int index )

Sets the player index.
### Arguments

- *int* **index** - Player index.

## int getPlayerIndex ( ) const

Returns the player index.
### Return value

Player index.
## void setModelGUID ( const char * modelguid )

Sets the GUID of the game pad model.
### Arguments

- *const char ** **modelguid** - GUID of the game pad model.

## const char * getModelGUID ( ) const

Returns the GUID of the game pad model.
### Return value

GUID of the game pad model.
