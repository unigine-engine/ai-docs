# Unigine::Plugins::FMOD::EventInstance Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


> **Notice:** This set of functions is available when the [FMOD](../../../../code/plugins/fmod/index.md) plugin is loaded.


An instance of an FMOD Studio Event.


## EventInstance Class

### Members

## void setPaused ( int paused )

Sets a new value indicating the pause state of the event.
### Arguments

- *int* **paused** - The pause state of the event

## int isPaused () const

Returns the current value indicating the pause state of the event.
### Return value

Current pause state of the event
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
## int isVirtual () const

Returns the current value indicating if the event instance has been virtualized due to the polyphony limit being exceeded.
### Return value

Current event instance has been virtualized
## int isStarting () const

Returns the current value indicating if the event instance is preparing to start.
### Return value

Current event instance is preparing to start
## int isStopping () const

Returns the current value indicating if the event instance is preparing to stop.
### Return value

Current event instance is preparing to stop
## int isStopped () const

Returns the current value indicating if the event instance is stopped.
### Return value

Current event instance is stopped
## int isSustaining () const

Returns the current value indicating if the timeline cursor is paused on a sustain point.
### Return value

Current timeline cursor is paused on a sustain point
## int isPlaying () const

Returns the current value indicating if the event instance is playing.
### Return value

Current event instance is playing
## int isValid () const

Returns the current value indicating if the EventInstance reference is valid.
### Return value

Current EventInstance reference is valid
## void setPriority ( float priority )

Sets a new priority of the Channels created by the current EventInstance.
### Arguments

- *float* **priority** - The priority in range [-1;256]: 0 means *the most important*, 256 means *the least important*. The default is -1.

## float getPriority () const

Returns the current priority of the Channels created by the current EventInstance.
### Return value

Current priority in range [-1;256]: 0 means *the most important*, 256 means *the least important*. The default is -1.
---

## void set3DAttributes ( const Vec3 & position , const Vec3 & up , const Vec3 & forward , const Vec3 & velocity )

Sets event's position, velocity and orientation used to calculate 3D panning, doppler and the values of automatic distance and angle parameters.
### Arguments

- *const Vec3 &* **position** - Position in world space used for panning and attenuation.
- *const Vec3 &* **up** - Upwards orientation, must be of unit length (1.0) and perpendicular to forward.
- *const Vec3 &* **forward** - Forwards orientation, must be of unit length (1.0) and perpendicular to up.
- *const Vec3 &* **velocity** - Velocity in world space used for doppler, in distance units per second.

## void get3DAttributes ( Vec3 & position , Vec3 & up , Vec3 & forward , Vec3 & velocity )

Returns event's position, velocity and orientation.
### Arguments

- *Vec3 &* **position** - Position in world space.
- *Vec3 &* **up** - Upwards orientation.
- *Vec3 &* **forward** - Forwards orientation.
- *Vec3 &* **velocity** - Velocity in world space.

## void setVelocity ( const Vec3 & velocity )

Sets event's velocity.
### Arguments

- *const Vec3 &* **velocity** - Velocity in world space, in distance units per second.

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
## void setParameter ( string name , float value )

Sets a parameter value by name.
### Arguments

- *string* **name** - Parameter name (case-insensitive) of an FMOD Studio event. (UTF-8 string)
- *float* **value** - Value for a given name.

## float getParameter ( string name )

Returns a parameter value by name.
### Arguments

- *string* **name** - Parameter name (case-insensitive). (UTF-8 string)

### Return value

Value for a given name.
## void setTransform ( Mat4 transform )

Sets the transformation matrix for the node in world coordinates.
### Arguments

- *Mat4* **transform** - New transformation matrix to be set for the node (world coordinates).

## void setParent ( Node parent )

Sets a new parent for the node. Transformations of the current node will be done in the coordinates of the parent.
### Arguments

- *[Node](../../../../api/library/nodes/class.node_usc.md)* **parent** - New parent node.

## void releaseFromDefinition ( )

Auxiliary function, not to be used.
## String getDescriptionPath ( )

Returns the path for the EventDescription of the current EventInstance.
### Return value

EventDescription path.
## void setParameterWithLabel ( string name , string label , bool ignore_seek = false )

Sets a labeled event parameter to the value associated with the given text label, instead of passing a raw numeric value as **[setParameter()()](../../../...md#setParameter_cstr_float_void)** does.
### Arguments

- *string* **name** - Name of the event parameter.
- *string* **label** - Text label of the desired parameter value, as authored in *FMOD Studio*.
- *bool* **ignore_seek** - Flag defining whether the value is set instantly, bypassing the parameter's authored seek speed.
