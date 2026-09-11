# Unigine::InputEventPadAccelerometerMotion Class (CPP)

**Header:** #include <UnigineInput.h>

**Inherits from:** InputEvent


This class contains the game pad accelerometer motion event information: the connection ID of the game pad and the acceleration vector it reports. The engine dispatches this event each time the accelerometer of a connected controller reports a new state.


The last reported value for each game pad is also available via the *[InputGamePad](../../../api/library/controls/class.inputgamepad_cpp.md)* class (the **[getAcceleration()](../../../api/library/controls/class.inputgamepad_cpp.md#getAcceleration_vec3)** property; accelerometer support can be checked via the **[isAccelerationSupported()](../../../api/library/controls/class.inputgamepad_cpp.md#isAccelerationSupported_int)** property).


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
## void setAcceleration ( const Math:: vec3 & acceleration )

Sets a new acceleration measured by the game pad accelerometer, in meters per second squared. The value includes the gravity vector while the controller is at rest.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **acceleration** - The acceleration vector, in meters per second squared

## Math:: vec3 getAcceleration () const

Returns the current acceleration measured by the game pad accelerometer, in meters per second squared. The value includes the gravity vector while the controller is at rest.
### Return value

Current acceleration vector, in meters per second squared
---

## InputEventPadAccelerometerMotion ( )

Default constructor. Creates an event of the *INPUT_EVENT_PAD_ACCELEROMETER_MOTION* type with the connection ID equal to -1 and zero acceleration.
## InputEventPadAccelerometerMotion ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos )

Constructor. Creates an event of the *INPUT_EVENT_PAD_ACCELEROMETER_MOTION* type with the given timestamp and mouse cursor position.
### Arguments

- *unsigned long long* **timestamp** - Event timestamp.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Mouse cursor position at the moment of the event.

## InputEventPadAccelerometerMotion ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos , int connection_id , const Math:: vec3 & acceleration )

Constructor. Creates an event of the *INPUT_EVENT_PAD_ACCELEROMETER_MOTION* type with the given parameters.
### Arguments

- *unsigned long long* **timestamp** - Event timestamp.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Mouse cursor position at the moment of the event.
- *int* **connection_id** - Connection identifier of the game pad.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **acceleration** - Acceleration vector, in meters per second squared.
