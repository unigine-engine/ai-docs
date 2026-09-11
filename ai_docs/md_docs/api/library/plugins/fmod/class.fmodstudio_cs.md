# Unigine::Plugins::FMOD::FMODStudio Class (CS)


> **Notice:** This set of functions is available when the [FMOD](../../../../code/plugins/fmod/index.md) plugin is loaded.


This class is intended to interact with the data driven projects created via FMOD Studio at run time.


## FMODStudio Class

### Members

---

## Bank LoadBank ( string path )

Loads a bank at a given path.
### Arguments

- *string* **path** - Path to the bank file.

### Return value

Bank object.
## Bank LoadBankFromMemory ( string buffer , int size )

Loads a bank from the specified buffer in memory.
### Arguments

- *string* **buffer** - Buffer containing a bank to be loaded.
- *int* **size** - Size of the bank to be loaded, in bytes.

### Return value

Bank object.
## VCA GetVCA ( string path )

Auxiliary function, not to be used.
### Arguments

- *string* **path**

## Bus GetBus ( string path )

Auxiliary function, not to be used.
### Arguments

- *string* **path**

## EventInstance GetEvent ( string path )

Returns the EventInstance object at a given path.
### Arguments

- *string* **path** - Path of the EventInstance.

### Return value

EventInstance object.
## EventDescription GetEventDescription ( string path )

Auxiliary function, not to be used.
### Arguments

- *string* **path**

## void SetListener3DAttributes ( int listener , vec3 position , vec3 up , vec3 forward , vec3 velocity )

Sets the 3D attributes of the listener. Vectors must be provided in the correct handedness.
### Arguments

- *int* **listener** - Listener index.
- *vec3* **position** - Position in world space used for panning and attenuation.
- *vec3* **up** - Upwards orientation, must be of unit length (1.0) and perpendicular to forward.
- *vec3* **forward** - Forwards orientation, must be of unit length (1.0) and perpendicular to up.
- *vec3* **velocity** - Velocity in world space used for doppler.

## void GetListener3DAttributes ( int listener , out Vec3 position , out Vec3 up , out Vec3 forward , out Vec3 velocity )

Returns the 3D attributes of the listener.
### Arguments

- *int* **listener** - Listener index.
- *out Vec3* **position** - Position in world space.
- *out Vec3* **up** - Upwards orientation.
- *out Vec3* **forward** - Forwards orientation.
- *out Vec3* **velocity** - Velocity in world space.

## void SetListenerVelocity ( vec3 velocity )

Sets the velocity of the listener.
### Arguments

- *vec3* **velocity** - Velocity in world space.

## void SetListenerTransform ( mat4 transform )

Sets the transformation matrix of the listener. Currently the listener only works with the standard camera.
### Arguments

- *mat4* **transform** - Transformation matrix.

## void SetParentForListener ( Node parent )

Sets a parent node for the listener.
### Arguments

- *[Node](../../../../api/library/nodes/class.node_cs.md)* **parent** - Node to be set as a parent.

## void UseStudioLiveUpdateFlag ( )

Enables live update.
## void UseStudioSyncUpdateFlag ( )

Disables asynchronous processing and perform all processing on the calling thread instead.
## void UseStudioLoadFromUpdateFlag ( )

No additional threads are created for bank and resource loading.
## void UseCoreStreamFromUpdateFlag ( )

No stream thread is created internally. Mainly used with non-realtime outputs.
## void Update ( )

Updates the FMOD system.
## void InitStudio ( )

Studio initialization.
## Bank GetBank ( int id )

Auxiliary function, not to be used.
### Arguments

- *int* **id**

## EventDescription GetEventDescription ( int id )

Auxiliary function, not to be used.
### Arguments

- *int* **id**

## Bus GetBus ( int id )

Auxiliary function, not to be used.
### Arguments

- *int* **id**

## VCA GetVCA ( int id )

Auxiliary function, not to be used.
### Arguments

- *int* **id**

## int GetBankCount ( )

Returns the number of loaded banks.
### Return value

Number of banks.
## int GetEventDescriptionCount ( )

Returns the number of event descriptions.
### Return value

Event description count.
## int GetBusCount ( )

Returns the number of buses.
### Return value

Number of buses.
## int GetVCACount ( )

Returns the number of VCAs.
### Return value

VCA count.
## BufferUsage GetBufferUsage ( )

Returns buffer usage information.
### Return value

Buffer usage information.
## void ResetBufferUsage ( )

Resets memory buffer usage statistics.
## CPUUsageTotal GetCPUUsageTotal ( )

Returns the total amount of CPU used.
### Return value

Total CPU usage.
## void GetMemoryUsage ( out int exclusive , out int inclusive , out int sample_data )

Returns memory usage statistics.
### Arguments

- *out int* **exclusive** - Size of memory belonging to the bus or event instance.
- *out int* **inclusive** - Size of memory belonging exclusively to the bus or event plus the inclusive memory sizes of all buses and event instances which route into it.
- *out int* **sample_data** - Size of shared sample memory referenced by the bus or event instance, inclusive of all sample memory referenced by all buses and event instances which route into it.

## void Release ( )

Shuts down and frees the Studio System object.
## void ReleaseBuses ( )

Releases bus objects.
## void ReleaseVCAs ( )

Releases VCA objects.
## void ReleaseEventDescriptions ( )

Releases event description objects.
## void ReleaseBanks ( )

Releases bank objects.
## void UseChannelsCount ( int count )

Updates the maximum number of Channels (both virtual and real) to be used in FMOD system.
### Arguments

- *int* **count** - Number of Channels.

## bool UnloadBank ( string path )

Destroys all objects created from the bank, unloads all sample data inside the bank, and invalidates all API handles referring to the bank.
### Arguments

- *string* **path** - The path to the bank that should be unloaded.

### Return value

true if bank is unloaded successfully; otherwise, false.
## float GetGlobalParameter ( string name )

Returns the current value of a global parameter of the *FMOD Studio* system. An unknown name is reported to the log.
### Arguments

- *string* **name** - Name of the global parameter, as authored in *FMOD Studio*.

### Return value

Current value of the parameter.
## void SetGlobalParameterWithLabel ( string name , string label , bool ignore_seek = false )

Sets a global parameter of the *FMOD Studio* system to the value associated with the given text label.
### Arguments

- *string* **name** - Name of the global parameter.
- *string* **label** - Text label of the desired parameter value, as authored in *FMOD Studio*.
- *bool* **ignore_seek** - Flag defining whether the value is set instantly, bypassing the parameter's authored seek speed.

## void SetGlobalParameter ( string name , float value )

Sets a global (system-wide) parameter of the *FMOD Studio* system by name. Global parameters affect the whole system rather than a single event instance.
### Arguments

- *string* **name** - Name of the global parameter, as authored in *FMOD Studio*.
- *float* **value** - New value of the parameter.
