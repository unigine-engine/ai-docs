# Unigine::Plugins::FMOD::EventInstance Class (CS)


> **Notice:** This set of functions is available when the [FMOD](../../../../code/plugins/fmod/index.md) plugin is loaded.


An instance of an FMOD Studio Event.


## EventInstance Class

### Properties

## bool Paused

The value indicating the pause state of the event.
## float Pitch

The pitch value. Range: [0; inf]. Default: 1. The pitch multiplier can be set to any value greater than or equal to zero but the final combined pitch is clamped to the range [0; 100] before being applied.
## float Gain

The gain value.
## float MaxDistance

The maximum distance used for 3D attenuation, in distance units.
## float MinDistance

The minimum distance used for 3D attenuation, in distance units.
## int TimeLinePosition

The timeline cursor position, in milliseconds. Range: [0; inf].
## 🔒︎ bool IsVirtual

The value indicating if the event instance has been virtualized due to the polyphony limit being exceeded.
## 🔒︎ bool IsStarting

The value indicating if the event instance is preparing to start.
## 🔒︎ bool IsStopping

The value indicating if the event instance is preparing to stop.
## 🔒︎ bool IsStopped

The value indicating if the event instance is stopped.
## 🔒︎ bool IsSustaining

The value indicating if the timeline cursor is paused on a sustain point.
## 🔒︎ bool IsPlaying

The value indicating if the event instance is playing.
## 🔒︎ bool IsValid

The value indicating if the EventInstance reference is valid.
## float Priority

The priority of the Channels created by the current EventInstance.
### Members

---

## void Set3DAttributes ( vec3 position , vec3 up , vec3 forward , vec3 velocity )

Sets event's position, velocity and orientation used to calculate 3D panning, doppler and the values of automatic distance and angle parameters.
### Arguments

- *vec3* **position** - Position in world space used for panning and attenuation.
- *vec3* **up** - Upwards orientation, must be of unit length (1.0) and perpendicular to forward.
- *vec3* **forward** - Forwards orientation, must be of unit length (1.0) and perpendicular to up.
- *vec3* **velocity** - Velocity in world space used for doppler, in distance units per second.

## void Get3DAttributes ( out Vec3 position , out Vec3 up , out Vec3 forward , out Vec3 velocity )

Returns event's position, velocity and orientation.
### Arguments

- *out Vec3* **position** - Position in world space.
- *out Vec3* **up** - Upwards orientation.
- *out Vec3* **forward** - Forwards orientation.
- *out Vec3* **velocity** - Velocity in world space.

## void SetVelocity ( vec3 velocity )

Sets event's velocity.
### Arguments

- *vec3* **velocity** - Velocity in world space, in distance units per second.

## void Play ( )

Starts playback. If the instance was already playing then calling this function will restart the event.
## void Stop ( )

Stops playback.
## void StopWithFadeout ( )

Stops playback with the fadeout effect.
## void Release ( )

Marks the event instance for release. Event instances marked for release are destroyed by the asynchronous update when they are in the stopped state.
## void Update ( )

Updates the position of the event instance in world space.
## void SetParameter ( string name , float value )

Sets a parameter value by name.
### Arguments

- *string* **name** - Parameter name (case-insensitive) of an FMOD Studio event. (UTF-8 string)
- *float* **value** - Value for a given name.

## float GetParameter ( string name )

Returns a parameter value by name.
### Arguments

- *string* **name** - Parameter name (case-insensitive). (UTF-8 string)

### Return value

Value for a given name.
## void SetTransform ( mat4 transform )

Sets the transformation matrix for the node in world coordinates.
### Arguments

- *mat4* **transform** - New transformation matrix to be set for the node (world coordinates).

## void SetParent ( Node parent )

Sets a new parent for the node. Transformations of the current node will be done in the coordinates of the parent.
### Arguments

- *[Node](../../../../api/library/nodes/class.node_cs.md)* **parent** - New parent node.

## void ReleaseFromDefinition ( )

Auxiliary function, not to be used.
## string GetDescriptionPath ( )

Returns the path for the EventDescription of the current EventInstance.
### Return value

EventDescription path.
## void SetParameterWithLabel ( string name , string label , bool ignore_seek = false )

Sets a labeled event parameter to the value associated with the given text label, instead of passing a raw numeric value as **[SetParameter()](../../../...md#setParameter_cstr_float_void)** does.
### Arguments

- *string* **name** - Name of the event parameter.
- *string* **label** - Text label of the desired parameter value, as authored in *FMOD Studio*.
- *bool* **ignore_seek** - Flag defining whether the value is set instantly, bypassing the parameter's authored seek speed.
