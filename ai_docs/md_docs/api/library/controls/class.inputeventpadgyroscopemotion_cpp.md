# Unigine::InputEventPadGyroscopeMotion Class (CPP)

**Header:** #include <UnigineInput.h>

**Inherits from:** InputEvent


This class contains the game pad gyroscope motion event information: the connection ID of the game pad and the angular velocity it reports. The engine dispatches this event each time the gyroscope of a connected controller reports a new state.


The last reported value for each game pad is also available via the *[InputGamePad](../../../api/library/controls/class.inputgamepad_cpp.md)* class (the **[getAngularVelocity()](../../../api/library/controls/class.inputgamepad_cpp.md#getAngularVelocity_vec3)** property; gyroscope support can be checked via the **[isAngularVelocitySupported()](../../../api/library/controls/class.inputgamepad_cpp.md#isAngularVelocitySupported_int)** property).


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
## void setAngularVelocity ( const Math:: vec3 & velocity )

Sets a new angular velocity measured by the game pad gyroscope, in degrees per second.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **velocity** - The angular velocity vector, in degrees per second

## Math:: vec3 getAngularVelocity () const

Returns the current angular velocity measured by the game pad gyroscope, in degrees per second.
### Return value

Current angular velocity vector, in degrees per second
---

## InputEventPadGyroscopeMotion ( )

Default constructor. Creates an event of the *INPUT_EVENT_PAD_GYROSCOPE_MOTION* type with the connection ID equal to -1 and zero angular velocity.
## InputEventPadGyroscopeMotion ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos )

Constructor. Creates an event of the *INPUT_EVENT_PAD_GYROSCOPE_MOTION* type with the given timestamp and mouse cursor position.
### Arguments

- *unsigned long long* **timestamp** - Event timestamp.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Mouse cursor position at the moment of the event.

## InputEventPadGyroscopeMotion ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos , int connection_id , const Math:: vec3 & angular_velocity )

Constructor. Creates an event of the *INPUT_EVENT_PAD_GYROSCOPE_MOTION* type with the given parameters.
### Arguments

- *unsigned long long* **timestamp** - Event timestamp.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Mouse cursor position at the moment of the event.
- *int* **connection_id** - Connection identifier of the game pad.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **angular_velocity** - Angular velocity vector, in degrees per second.
