# Unigine::InputEventPadAccelerometerMotion Class (CS)

**Inherits from:** InputEvent


This class contains the game pad accelerometer motion event information: the connection ID of the game pad and the acceleration vector it reports. The engine dispatches this event each time the accelerometer of a connected controller reports a new state.


The last reported value for each game pad is also available via the *[InputGamePad](../../../api/library/controls/class.inputgamepad_cs.md)* class (the **[Acceleration](../../../api/library/controls/class.inputgamepad_cs.md#getAcceleration_vec3)** property; accelerometer support can be checked via the **[IsAccelerationSupported](../../../api/library/controls/class.inputgamepad_cs.md#isAccelerationSupported_int)** property).


## InputEventPadAccelerometerMotion Class

### Properties

## int ConnectionID

The connection identifier of the game pad that produced the sensor update. -1 means no device.
## vec3 Acceleration

The acceleration measured by the game pad accelerometer, in meters per second squared. The value includes the gravity vector while the controller is at rest.
### Members

---

## InputEventPadAccelerometerMotion ( )

Default constructor. Creates an event of the *INPUT_EVENT_PAD_ACCELEROMETER_MOTION* type with the connection ID equal to -1 and zero acceleration.
## InputEventPadAccelerometerMotion ( ulong timestamp , ivec2 mouse_pos )

Constructor. Creates an event of the *INPUT_EVENT_PAD_ACCELEROMETER_MOTION* type with the given timestamp and mouse cursor position.
### Arguments

- *ulong* **timestamp** - Event timestamp.
- *ivec2* **mouse_pos** - Mouse cursor position at the moment of the event.

## InputEventPadAccelerometerMotion ( ulong timestamp , ivec2 mouse_pos , int connection_id , vec3 acceleration )

Constructor. Creates an event of the *INPUT_EVENT_PAD_ACCELEROMETER_MOTION* type with the given parameters.
### Arguments

- *ulong* **timestamp** - Event timestamp.
- *ivec2* **mouse_pos** - Mouse cursor position at the moment of the event.
- *int* **connection_id** - Connection identifier of the game pad.
- *vec3* **acceleration** - Acceleration vector, in meters per second squared.
