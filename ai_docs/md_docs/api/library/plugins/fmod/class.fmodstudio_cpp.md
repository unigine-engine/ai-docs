# Unigine::Plugins::FMOD::FMODStudio Class (CPP)

**Header:** #include <plugins/Unigine/FMOD/UnigineFMOD.h>


> **Notice:** This set of functions is available when the [FMOD](../../../../code/plugins/fmod/index.md) plugin is loaded.


This class is intended to interact with the data driven projects created via FMOD Studio at run time.


## FMODStudio Class

---

## Bank * loadBank ( const char * path )

Loads a bank at a given path.
### Arguments

- *const char ** **path** - Path to the bank file.

### Return value

Bank object.
## Bank * loadBankFromMemory ( const char * buffer , int size )

Loads a bank from the specified buffer in memory.
### Arguments

- *const char ** **buffer** - Buffer containing a bank to be loaded.
- *int* **size** - Size of the bank to be loaded, in bytes.

### Return value

Bank object.
## VCA * getVCA ( const char * path )

Auxiliary function, not to be used.
### Arguments

- *const char ** **path**

## Bus * getBus ( const char * path )

Auxiliary function, not to be used.
### Arguments

- *const char ** **path**

## EventInstance * getEvent ( const char * path )

Returns the EventInstance object at a given path.
### Arguments

- *const char ** **path** - Path of the EventInstance.

### Return value

EventInstance object.
## EventDescription * getEventDescription ( const char * path )

Auxiliary function, not to be used.
### Arguments

- *const char ** **path**

## void setListener3DAttributes ( int listener , const Math:: Vec3 & position , const Math:: Vec3 & up , const Math:: Vec3 & forward , const Math:: Vec3 & velocity )

Sets the 3D attributes of the listener. Vectors must be provided in the correct handedness.
### Arguments

- *int* **listener** - Listener index.
- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **position** - Position in world space used for panning and attenuation.
- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **up** - Upwards orientation, must be of unit length (1.0) and perpendicular to forward.
- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **forward** - Forwards orientation, must be of unit length (1.0) and perpendicular to up.
- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **velocity** - Velocity in world space used for doppler.

## void getListener3DAttributes ( int listener , Math:: Vec3 & position , Math:: Vec3 & up , Math:: Vec3 & forward , Math:: Vec3 & velocity )

Returns the 3D attributes of the listener.
### Arguments

- *int* **listener** - Listener index.
- *Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **position** - Position in world space.
- *Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **up** - Upwards orientation.
- *Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **forward** - Forwards orientation.
- *Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **velocity** - Velocity in world space.

## void setListenerVelocity ( const Math:: Vec3 & velocity )

Sets the velocity of the listener.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **velocity** - Velocity in world space.

## void setListenerTransform ( const Math:: Mat4 & transform )

Sets the transformation matrix of the listener. Currently the listener only works with the standard camera.
### Arguments

- *const  Math::[Mat4](../../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix.

## void setParentForListener ( const Ptr < Node > & parent )

Sets a parent node for the listener.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Node](../../../../api/library/nodes/class.node_cpp.md)> &* **parent** - Node to be set as a parent.

## void useStudioLiveUpdateFlag ( )

Enables live update.
## void useStudioSyncUpdateFlag ( )

Disables asynchronous processing and perform all processing on the calling thread instead.
## void useStudioLoadFromUpdateFlag ( )

No additional threads are created for bank and resource loading.
## void useCoreStreamFromUpdateFlag ( )

No stream thread is created internally. Mainly used with non-realtime outputs.
## void update ( )

Updates the FMOD system.
## void initStudio ( )

Studio initialization.
## Bank * getBank ( int id )

Auxiliary function, not to be used.
### Arguments

- *int* **id**

## EventDescription * getEventDescription ( int id )

Auxiliary function, not to be used.
### Arguments

- *int* **id**

## Bus * getBus ( int id )

Auxiliary function, not to be used.
### Arguments

- *int* **id**

## VCA * getVCA ( int id )

Auxiliary function, not to be used.
### Arguments

- *int* **id**

## int getBankCount ( )

Returns the number of loaded banks.
### Return value

Number of banks.
## int getEventDescriptionCount ( )

Returns the number of event descriptions.
### Return value

Event description count.
## int getBusCount ( )

Returns the number of buses.
### Return value

Number of buses.
## int getVCACount ( )

Returns the number of VCAs.
### Return value

VCA count.
## FMODStudio::BufferUsage getBufferUsage ( )

Returns buffer usage information.
### Return value

Buffer usage information.
## void resetBufferUsage ( )

Resets memory buffer usage statistics.
## FMODStudio::CPUUsageTotal getCPUUsageTotal ( )

Returns the total amount of CPU used.
### Return value

Total CPU usage.
## void getMemoryUsage ( int & exclusive , int & inclusive , int & sample_data )

Returns memory usage statistics.
### Arguments

- *int &* **exclusive** - Size of memory belonging to the bus or event instance.
- *int &* **inclusive** - Size of memory belonging exclusively to the bus or event plus the inclusive memory sizes of all buses and event instances which route into it.
- *int &* **sample_data** - Size of shared sample memory referenced by the bus or event instance, inclusive of all sample memory referenced by all buses and event instances which route into it.

## void release ( )

Shuts down and frees the Studio System object.
## void releaseBuses ( )

Releases bus objects.
## void releaseVCAs ( )

Releases VCA objects.
## void releaseEventDescriptions ( )

Releases event description objects.
## void releaseBanks ( )

Releases bank objects.
## void useChannelsCount ( int count )

Updates the maximum number of Channels (both virtual and real) to be used in FMOD system.
### Arguments

- *int* **count** - Number of Channels.

## bool unloadBank ( const char * path )

Destroys all objects created from the bank, unloads all sample data inside the bank, and invalidates all API handles referring to the bank.
### Arguments

- *const char ** **path** - The path to the bank that should be unloaded.

### Return value

true if bank is unloaded successfully; otherwise, false.
## float getGlobalParameter ( const char * name )

Returns the current value of a global parameter of the *FMOD Studio* system. An unknown name is reported to the log.
### Arguments

- *const char ** **name** - Name of the global parameter, as authored in *FMOD Studio*.

### Return value

Current value of the parameter.
## void setGlobalParameterWithLabel ( const char * name , const char * label , bool ignore_seek = false )

Sets a global parameter of the *FMOD Studio* system to the value associated with the given text label.
### Arguments

- *const char ** **name** - Name of the global parameter.
- *const char ** **label** - Text label of the desired parameter value, as authored in *FMOD Studio*.
- *bool* **ignore_seek** - Flag defining whether the value is set instantly, bypassing the parameter's authored seek speed.

## void setGlobalParameter ( const char * name , float value )

Sets a global (system-wide) parameter of the *FMOD Studio* system by name. Global parameters affect the whole system rather than a single event instance.
### Arguments

- *const char ** **name** - Name of the global parameter, as authored in *FMOD Studio*.
- *float* **value** - New value of the parameter.
