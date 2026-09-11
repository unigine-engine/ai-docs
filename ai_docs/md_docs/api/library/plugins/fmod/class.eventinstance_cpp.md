# Unigine::Plugins::FMOD::EventInstance Class (CPP)

**Header:** #include <plugins/Unigine/FMOD/UnigineFMOD.h>


> **Notice:** This set of functions is available when the [FMOD](../../../../code/plugins/fmod/index.md) plugin is loaded.


An instance of an FMOD Studio Event.


## EventInstance Class

### Members

## void setPaused ( bool paused )

Sets a new value indicating the pause state of the event.
### Arguments

- *bool* **paused** - Set **true** to enable pause state of the event; **false** - to disable it.

## bool isPaused () const

Returns the current value indicating the pause state of the event.
### Return value

**true** if pause state of the event is enabled ; otherwise **false**.
## void setPitch ( float pitch )

Sets a new pitch value. Range: [0; inf]. Default: 1. The pitch multiplier can be set to any value greater than or equal to zero but the final combined pitch is clamped to the range [0; 100] before being applied.
### Arguments

- *float* **pitch** - The pitch multiplier. Range: [0; inf]. Default: 1. The pitch multiplier can be set to any value greater than or equal to zero but the final combined pitch is clamped to the range [0; 100] before being applied.

## float getPitch () const

Returns the current pitch value. Range: [0; inf]. Default: 1. The pitch multiplier can be set to any value greater than or equal to zero but the final combined pitch is clamped to the range [0; 100] before being applied.
### Return value

Current pitch multiplier. Range: [0; inf]. Default: 1. The pitch multiplier can be set to any value greater than or equal to zero but the final combined pitch is clamped to the range [0; 100] before being applied.
## void setGain ( float gain )

Sets a new gain value.
### Arguments

- *float* **gain** - The gain value.

## float getGain () const

Returns the current gain value.
### Return value

Current gain value.
## void setMaxDistance ( float distance )

Sets a new maximum distance used for 3D attenuation, in distance units.
### Arguments

- *float* **distance** - The maximum distance, in distance units.

## float getMaxDistance () const

Returns the current maximum distance used for 3D attenuation, in distance units.
### Return value

Current maximum distance, in distance units.
## void setMinDistance ( float distance )

Sets a new minimum distance used for 3D attenuation, in distance units.
### Arguments

- *float* **distance** - The minimum distance, in distance units.

## float getMinDistance () const

Returns the current minimum distance used for 3D attenuation, in distance units.
### Return value

Current minimum distance, in distance units.
## void setTimeLinePosition ( int position )

Sets a new timeline cursor position, in milliseconds. Range: [0; inf].
### Arguments

- *int* **position** - The timeline cursor position, in milliseconds. Range: [0; inf].

## int getTimeLinePosition () const

Returns the current timeline cursor position, in milliseconds. Range: [0; inf].
### Return value

Current timeline cursor position, in milliseconds. Range: [0; inf].
## bool isVirtual () const

Returns the current value indicating if the event instance has been virtualized due to the polyphony limit being exceeded.
### Return value

**true** if event instance has been virtualized; otherwise **false**.
## bool isStarting () const

Returns the current value indicating if the event instance is preparing to start.
### Return value

**true** if event instance is preparing to start; otherwise **false**.
## bool isStopping () const

Returns the current value indicating if the event instance is preparing to stop.
### Return value

**true** if event instance is preparing to stop; otherwise **false**.
## bool isStopped () const

Returns the current value indicating if the event instance is stopped.
### Return value

**true** if event instance is stopped; otherwise **false**.
## bool isSustaining () const

Returns the current value indicating if the timeline cursor is paused on a sustain point.
### Return value

**true** if timeline cursor is paused on a sustain point; otherwise **false**.
## bool isPlaying () const

Returns the current value indicating if the event instance is playing.
### Return value

**true** if event instance is playing; otherwise **false**.
## bool isValid () const

Returns the current value indicating if the EventInstance reference is valid.
### Return value

**true** if EventInstance reference is valid; otherwise **false**.
## void setPriority ( float priority )

Sets a new priority of the Channels created by the current EventInstance.
### Arguments

- *float* **priority** - The priority in range [-1;256]: 0 means *the most important*, 256 means *the least important*. The default is -1.

## float getPriority () const

Returns the current priority of the Channels created by the current EventInstance.
### Return value

Current priority in range [-1;256]: 0 means *the most important*, 256 means *the least important*. The default is -1.
---

## void set3DAttributes ( const Math:: Vec3 & position , const Math:: Vec3 & up , const Math:: Vec3 & forward , const Math:: Vec3 & velocity )

Sets event's position, velocity and orientation used to calculate 3D panning, doppler and the values of automatic distance and angle parameters.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **position** - Position in world space used for panning and attenuation.
- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **up** - Upwards orientation, must be of unit length (1.0) and perpendicular to forward.
- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **forward** - Forwards orientation, must be of unit length (1.0) and perpendicular to up.
- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **velocity** - Velocity in world space used for doppler, in distance units per second.

## void get3DAttributes ( Math:: Vec3 & position , Math:: Vec3 & up , Math:: Vec3 & forward , Math:: Vec3 & velocity )

Returns event's position, velocity and orientation.
### Arguments

- *Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **position** - Position in world space.
- *Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **up** - Upwards orientation.
- *Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **forward** - Forwards orientation.
- *Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **velocity** - Velocity in world space.

## void setVelocity ( const Math:: Vec3 & velocity )

Sets event's velocity.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **velocity** - Velocity in world space, in distance units per second.

## void play ( )

Starts playback. If the instance was already playing then calling this function will restart the event.
## void stop ( )

Stops playback.
## void stopWithFadeout ( )

Stops playback with the fadeout effect.
## void release ( )

Marks the event instance for release. Event instances marked for release are destroyed by the asynchronous update when they are in the stopped state.
## void update ( )

Updates the position of the event instance in world space.
## void setParameter ( const char * name , float value )

Sets a parameter value by name.
### Arguments

- *const char ** **name** - Parameter name (case-insensitive) of an FMOD Studio event. (UTF-8 string)
- *float* **value** - Value for a given name.

## float getParameter ( const char * name )

Returns a parameter value by name.
### Arguments

- *const char ** **name** - Parameter name (case-insensitive). (UTF-8 string)

### Return value

Value for a given name.
## void setTransform ( const Math:: Mat4 & transform )

Sets the transformation matrix for the node in world coordinates.
### Arguments

- *const  Math::[Mat4](../../../../api/library/math/class.mat4_cpp.md) &* **transform** - New transformation matrix to be set for the node (world coordinates).

## void setParent ( const Ptr < Node > & parent )

Sets a new parent for the node. Transformations of the current node will be done in the coordinates of the parent.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Node](../../../../api/library/nodes/class.node_cpp.md)> &* **parent** - New parent node.

## void releaseFromDefinition ( )

Auxiliary function, not to be used.
## String getDescriptionPath ( ) const

Returns the path for the EventDescription of the current EventInstance.
### Return value

EventDescription path.
## void setParameterWithLabel ( const char * name , const char * label , bool ignore_seek = false )

Sets a labeled event parameter to the value associated with the given text label, instead of passing a raw numeric value as **[setParameter()](../../../...md#setParameter_cstr_float_void)** does.
### Arguments

- *const char ** **name** - Name of the event parameter.
- *const char ** **label** - Text label of the desired parameter value, as authored in *FMOD Studio*.
- *bool* **ignore_seek** - Flag defining whether the value is set instantly, bypassing the parameter's authored seek speed.
