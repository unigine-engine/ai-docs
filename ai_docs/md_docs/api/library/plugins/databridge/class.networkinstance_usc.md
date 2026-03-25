# Unigine::Plugins::DataBridge::NetworkInstance Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class provides access to the network instance, which may be either [Server](../../../../api/library/plugins/databridge/class.server_usc.md) or [Client](../../../../api/library/plugins/databridge/class.client_usc.md).


## NetworkInstance Class

### Members

## double getTime () const

Returns the current server frame time, in seconds (even if called from a Client computer). It is the time of the last buffer swap operation (i.e., beginning of the next frame). This value is more accurate than that of the [Game](../../../../api/library/engine/class.game_usc.md#Time) class.
### Return value

Current server frame time, in seconds
## double getIFps () const

Returns the current duration of the last frame. This method is more accurate than the same method of the [Game](../../../../api/library/engine/class.game_usc.md#getIFps_float) class and returns a double-precision value.
### Return value

Current duration of the previous frame, in seconds.
---

## void update ( )

Updates the network instance.
## void shutdown ( )

Shuts down the network instance.
## void setDisconnectTimeout ( float seconds )

Sets a timeout period after which a Client is considered as disconnected.
### Arguments

- *float* **seconds** - Duration of the timeout period, in seconds.

## float getDisconnectTimeout ( )

Returns the current timeout period after which a Client is considered as disconnected.
### Return value

Duration of the timeout period, in seconds.
