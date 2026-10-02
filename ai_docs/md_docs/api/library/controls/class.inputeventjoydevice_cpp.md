# Unigine::InputEventJoyDevice Class (CPP)

**Header:** #include <UnigineInput.h>

**Inherits from:** InputEvent


This class controls joystick device event information.


Events of this type are created by the engine and passed to your handlers. You can also construct one yourself and dispatch it via *[Input::sendEvent()](../../../api/library/controls/class.input_cpp.md#sendEvent_InputEvent_void)*, which is what a custom SystemProxy implementation or a device emulator does.


### See Also


- C++ sample
- C# Component sample


## InputEventJoyDevice Class

### Enums

## ACTION

| Name | Description |
|---|---|
| **ACTION_CONNECTED** = 0 | Joystick state is "connected". |
| **ACTION_DISCONNECTED** = 1 | Joystick state is "disconnected". |

### Members

---

## InputEventJoyDevice ( )

Default constructor.
## InputEventJoyDevice ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos )

Joystick input event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.

## InputEventJoyDevice ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos , InputEventJoyDevice::ACTION action , int connection_id , int player_index , const char * model_guid )

Joystick input event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.
- *[InputEventJoyDevice::ACTION](../../../api/library/controls/class.inputeventjoydevice_cpp.md#ACTION)* **action** - Type of the joystick input event, one of the [ACTION_*](#ACTION_CONNECTED) values.
- *int* **connection_id** - Connection identifier.
- *int* **player_index** - Index of the player.
- *const char ** **model_guid** - GUID of the joystick model.

## void setAction ( InputEventJoyDevice::ACTION action )

Sets the action the event represents. See *[getAction()](../../...md#getAction_int)*.
### Arguments

- *[InputEventJoyDevice::ACTION](../../../api/library/controls/class.inputeventjoydevice_cpp.md#ACTION)* **action** - Type of the joystick input event, one of the [ACTION_*](#ACTION_CONNECTED) values.

## InputEventJoyDevice::ACTION getAction ( ) const

Returns the action the event represents: one of the [ACTION](#ACTION) values � the joystick was connected or disconnected.
### Return value

Type of the joystick input event, one of the [ACTION_*](#ACTION_CONNECTED) values.
## void setConnectionID ( int id )

Sets the identifier of the device connection the event comes from. See *[getConnectionID()](../../...md#getConnectionID_int)*.
### Arguments

- *int* **id** - Connection identifier to be set.

## int getConnectionID ( ) const

Returns the identifier of the device connection the event comes from � the value assigned by the OS when the device was connected. The engine uses it to match the event against a device slot; it is not the slot index itself.
### Return value

Connection identifier.
## void setPlayerIndex ( int index )

Sets the player index.
### Arguments

- *int* **index** - Player index.

## int getPlayerIndex ( ) const

Returns the index of the player the device is assigned to. Some platforms let several players connect at once (for example, up to four gamepads on an Xbox 360), and the index identifies which of them this device belongs to.
### Return value

Player index.
## void setModelGUID ( const char * modelguid )

Sets the GUID of the device model. See *[getModelGUID()](../../...md#getModelGUID_cstr)*.
### Arguments

- *const char ** **modelguid** - GUID of the joystick model.

## const char * getModelGUID ( ) const

Returns the GUID of the device model as reported by the input backend � a 32-character hexadecimal string built from the vendor, product and version identifiers. Devices of the same model share the same GUID, so it identifies the model and not a particular unit. An empty string is returned if the backend no longer knows the device.
### Return value

GUID of the joystick model.
