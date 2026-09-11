# Unigine::InputEventPadGyroscopeMotion Class (CS)

**Inherits from:** InputEvent


This class contains the game pad gyroscope motion event information: the connection ID of the game pad and the angular velocity it reports. The engine dispatches this event each time the gyroscope of a connected controller reports a new state.


The last reported value for each game pad is also available via the *[InputGamePad](../../../api/library/controls/class.inputgamepad_cs.md)* class (the **[AngularVelocity](../../../api/library/controls/class.inputgamepad_cs.md#getAngularVelocity_vec3)** property; gyroscope support can be checked via the **[IsAngularVelocitySupported](../../../api/library/controls/class.inputgamepad_cs.md#isAngularVelocitySupported_int)** property).


## InputEventPadGyroscopeMotion Class

### Properties

## int ConnectionID

The connection identifier of the game pad that produced the sensor update. -1 means no device.
## vec3 AngularVelocity

The angular velocity measured by the game pad gyroscope, in degrees per second.
### Members

---

## InputEventPadGyroscopeMotion ( )

Default constructor. Creates an event of the *INPUT_EVENT_PAD_GYROSCOPE_MOTION* type with the connection ID equal to -1 and zero angular velocity.
## InputEventPadGyroscopeMotion ( ulong timestamp , ivec2 mouse_pos )

Constructor. Creates an event of the *INPUT_EVENT_PAD_GYROSCOPE_MOTION* type with the given timestamp and mouse cursor position.
### Arguments

- *ulong* **timestamp** - Event timestamp.
- *ivec2* **mouse_pos** - Mouse cursor position at the moment of the event.

## InputEventPadGyroscopeMotion ( ulong timestamp , ivec2 mouse_pos , int connection_id , vec3 angular_velocity )

Constructor. Creates an event of the *INPUT_EVENT_PAD_GYROSCOPE_MOTION* type with the given parameters.
### Arguments

- *ulong* **timestamp** - Event timestamp.
- *ivec2* **mouse_pos** - Mouse cursor position at the moment of the event.
- *int* **connection_id** - Connection identifier of the game pad.
- *vec3* **angular_velocity** - Angular velocity vector, in degrees per second.
