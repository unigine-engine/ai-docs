# Unigine::InputEventPadDevice Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** InputEvent


This class controls the game pad event information.


Events of this type are created by the engine and passed to your handlers. You can also construct one yourself and dispatch it via *[engine.input.sendEvent()()](../../../api/library/controls/class.input_usc.md#sendEvent_InputEvent_void)*, which is what a custom SystemProxy implementation or a device emulator does.


## InputEventPadDevice Class

### Members

---

## InputEventPadDevice ( )

Default constructor.
## InputEventPadDevice ( long timestamp , ivec2 mouse_pos )

Game pad input event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.

## InputEventPadDevice ( long timestamp , ivec2 mouse_pos , int action , int connection_id , int player_index , string model_guid )

Game pad input event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
- *int* **action** - Type of the game pad input event, one of the [INPUT_EVENT_PAD_DEVICE_ACTION_*](#ACTION_CONNECTED) values.
- *int* **connection_id** - Connection identifier.
- *int* **player_index** - Index of the player.
- *string* **model_guid** - GUID of the game pad model.

## void setAction ( int action )

Sets the action the event represents. See *[getAction()()](../../...md#getAction_int)*.
### Arguments

- *int* **action** - Type of the game pad input event, one of the [INPUT_EVENT_PAD_DEVICE_ACTION_*](#ACTION_CONNECTED) values.

## int getAction ( )

Returns the action the event represents: one of the [ACTION](#ACTION) values � the gamepad was connected or disconnected.
### Return value

Type of the game pad input event, one of the [INPUT_EVENT_PAD_DEVICE_ACTION_*](#ACTION_CONNECTED) values.
## void setConnectionID ( int id )

Sets the identifier of the device connection the event comes from. See *[getConnectionID()()](../../...md#getConnectionID_int)*.
### Arguments

- *int* **id** - Connection identifier.

## int getConnectionID ( )

Returns the identifier of the device connection the event comes from � the value assigned by the OS when the device was connected. The engine uses it to match the event against a device slot; it is not the slot index itself.
### Return value

Connection identifier.
## void setPlayerIndex ( int index )

Sets the player index.
### Arguments

- *int* **index** - Player index.

## int getPlayerIndex ( )

Returns the index of the player the device is assigned to. Some platforms let several players connect at once (for example, up to four gamepads on an Xbox 360), and the index identifies which of them this device belongs to.
### Return value

Player index.
## void setModelGUID ( string modelguid )

Sets the GUID of the device model. See *[getModelGUID()()](../../...md#getModelGUID_cstr)*.
### Arguments

- *string* **modelguid** - GUID of the game pad model.

## string getModelGUID ( )

Returns the GUID of the device model as reported by the input backend � a 32-character hexadecimal string built from the vendor, product and version identifiers. Devices of the same model share the same GUID, so it identifies the model and not a particular unit. An empty string is returned if the backend no longer knows the device.
### Return value

GUID of the game pad model.
