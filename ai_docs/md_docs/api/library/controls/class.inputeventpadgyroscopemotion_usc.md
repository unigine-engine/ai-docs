# Unigine::InputEventPadGyroscopeMotion Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** InputEvent


This class contains the game pad gyroscope motion event information: the connection ID of the game pad and the angular velocity it reports. The engine dispatches this event each time the gyroscope of a connected controller reports a new state.


The last reported value for each game pad is also available via the *[InputGamePad](../../../api/library/controls/class.inputgamepad_usc.md)* class (the **[getAngularVelocity()()](../../../api/library/controls/class.inputgamepad_usc.md#getAngularVelocity_vec3)** property; gyroscope support can be checked via the **[isAngularVelocitySupported()()](../../../api/library/controls/class.inputgamepad_usc.md#isAngularVelocitySupported_int)** property).


## InputEventPadGyroscopeMotion Class

### Members

## void setConnectionID ( int id )

Sets a new connection identifier of the game pad that produced the sensor update. -1 means no device.
### Arguments

- *int* **id** - The connection identifier of the game pad

## int getConnectionID () const

Returns the current connection identifier of the game pad that produced the sensor update. -1 means no device.
### Return value

Current connection identifier of the game pad
## void setAngularVelocity ( vec3 velocity )

Sets a new angular velocity measured by the game pad gyroscope, in degrees per second.
### Arguments

- *vec3* **velocity** - The angular velocity vector, in degrees per second

## vec3 getAngularVelocity () const

Returns the current angular velocity measured by the game pad gyroscope, in degrees per second.
### Return value

Current angular velocity vector, in degrees per second
---

## InputEventPadGyroscopeMotion ( )

Default constructor. Creates an event of the *INPUT_EVENT_PAD_GYROSCOPE_MOTION* type with the connection ID equal to -1 and zero angular velocity.
## InputEventPadGyroscopeMotion ( long timestamp , ivec2 mouse_pos )

Constructor. Creates an event of the *INPUT_EVENT_PAD_GYROSCOPE_MOTION* type with the given timestamp and mouse cursor position.
### Arguments

- *long* **timestamp** - Event timestamp.
- *ivec2* **mouse_pos** - Mouse cursor position at the moment of the event.

## InputEventPadGyroscopeMotion ( long timestamp , ivec2 mouse_pos , int connection_id , vec3 angular_velocity )

Constructor. Creates an event of the *INPUT_EVENT_PAD_GYROSCOPE_MOTION* type with the given parameters.
### Arguments

- *long* **timestamp** - Event timestamp.
- *ivec2* **mouse_pos** - Mouse cursor position at the moment of the event.
- *int* **connection_id** - Connection identifier of the game pad.
- *vec3* **angular_velocity** - Angular velocity vector, in degrees per second.
