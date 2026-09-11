# Unigine::InputEventPadAccelerometerMotion Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** InputEvent


This class contains the game pad accelerometer motion event information: the connection ID of the game pad and the acceleration vector it reports. The engine dispatches this event each time the accelerometer of a connected controller reports a new state.


The last reported value for each game pad is also available via the *[InputGamePad](../../../api/library/controls/class.inputgamepad_usc.md)* class (the **[getAcceleration()()](../../../api/library/controls/class.inputgamepad_usc.md#getAcceleration_vec3)** property; accelerometer support can be checked via the **[isAccelerationSupported()()](../../../api/library/controls/class.inputgamepad_usc.md#isAccelerationSupported_int)** property).


## InputEventPadAccelerometerMotion Class

### Members

## void setConnectionID ( int id )

Sets a new connection identifier of the game pad that produced the sensor update. -1 means no device.
### Arguments

- *int* **id** - The connection identifier of the game pad

## int getConnectionID () const

Returns the current connection identifier of the game pad that produced the sensor update. -1 means no device.
### Return value

Current connection identifier of the game pad
## void setAcceleration ( vec3 acceleration )

Sets a new acceleration measured by the game pad accelerometer, in meters per second squared. The value includes the gravity vector while the controller is at rest.
### Arguments

- *vec3* **acceleration** - The acceleration vector, in meters per second squared

## vec3 getAcceleration () const

Returns the current acceleration measured by the game pad accelerometer, in meters per second squared. The value includes the gravity vector while the controller is at rest.
### Return value

Current acceleration vector, in meters per second squared
---

## InputEventPadAccelerometerMotion ( )

Default constructor. Creates an event of the *INPUT_EVENT_PAD_ACCELEROMETER_MOTION* type with the connection ID equal to -1 and zero acceleration.
## InputEventPadAccelerometerMotion ( long timestamp , ivec2 mouse_pos )

Constructor. Creates an event of the *INPUT_EVENT_PAD_ACCELEROMETER_MOTION* type with the given timestamp and mouse cursor position.
### Arguments

- *long* **timestamp** - Event timestamp.
- *ivec2* **mouse_pos** - Mouse cursor position at the moment of the event.

## InputEventPadAccelerometerMotion ( long timestamp , ivec2 mouse_pos , int connection_id , vec3 acceleration )

Constructor. Creates an event of the *INPUT_EVENT_PAD_ACCELEROMETER_MOTION* type with the given parameters.
### Arguments

- *long* **timestamp** - Event timestamp.
- *ivec2* **mouse_pos** - Mouse cursor position at the moment of the event.
- *int* **connection_id** - Connection identifier of the game pad.
- *vec3* **acceleration** - Acceleration vector, in meters per second squared.
