# Unigine::Plugins::FMOD::FMODCore Class (CPP)

**Header:** #include <plugins/Unigine/FMOD/UnigineFMOD.h>


> **Notice:** This set of functions is available when the [FMOD](../../../../code/plugins/fmod/index.md) plugin is loaded.


This class is intended to cover the basics / primitives of sound.


## FMODCore Class

---

## void close ( )

Closes the connection to the output and returns to an uninitialized state without releasing the object.
## void release ( )

Closes and frees this object and its resources.
## void update ( )

Updates the FMOD system.
## void initCore ( int max_channels , FMODEnums::INIT_FLAGS flags )

Initializes the system object and prepares FMOD for playback.
### Arguments

- *int* **max_channels** - Maximum number of Channel objects available for playback, also known as virtual channels. Virtual channels will play with minimal overhead, with a subset of 'real' voices that are mixed, and selected based on priority and audibility. Range: [0; 4095]
- *[FMODEnums::INIT_FLAGS](../../../../api/library/plugins/fmod/class.fmodenums_cpp.md#INIT_FLAGS)* **flags** - Initialization flags. More than one mode can be set at once by combining them with the OR operator.

## Sound * createSound ( const char * file_name , FMODEnums::FMOD_MODE mode )

Loads a sound into memory, opens it for streaming or sets it up for callback based sounds.
### Arguments

- *const char ** **file_name** - Name of the file or URL to open (UTF-8 string) or a pointer to a preloaded sound memory block.
- *[FMODEnums::FMOD_MODE](../../../../api/library/plugins/fmod/class.fmodenums_cpp.md#FMOD_MODE)* **mode** - Behavior modifier for opening the sound.

### Return value

Newly created Sound object.
## Sound * createStream ( const char * url )

Creates a stream, for example, an internet stream to be used as a radio.
### Arguments

- *const char ** **url** - URL of the resource.

### Return value

Newly created Sound object.
## Channel * playSound ( Sound * OUT_sound , ChannelGroup * OUT_channel_group , bool paused )

Plays a sound on a channel.
### Arguments

- *[Sound](../../../../api/library/engine/class.sound_cpp.md) ** **OUT_sound** - Sound to play. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *[ChannelGroup](../../../../api/library/plugins/fmod/class.channelgroup_cpp.md) ** **OUT_channel_group** - Group to output to instead of the master. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *bool* **paused** - Determines whether to start in the paused state. Start a Channel paused to allow altering attributes without it being audible, then follow it up with a call to *ChannelControl::setPaused* with *paused* = False.

### Return value

Newly playing channel.
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

## Channel * getChannel ( int index )

Returns the channel object at the specified index.
### Arguments

- *int* **index** - Channel index.

### Return value

Channel object.
## ChannelGroup * createChannelGroup ( const char * name )

Create a ChannelGroup object.
### Arguments

- *const char ** **name** - Label for identification purposes, in the UTF-8 format.

### Return value

Newly created group.
## Sound * createSound ( const Ptr < Blob > & data , FMODEnums::FMOD_MODE mode )

Creates a sound from the in-memory contents of a blob instead of a file.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Blob](../../../../api/library/common/class.blob_cpp.md)> &* **data** - Blob whose raw contents hold the audio file data.
- *[FMODEnums::FMOD_MODE](../../../../api/library/plugins/fmod/class.fmodenums_cpp.md#FMOD_MODE)* **mode** - Behavior modifier for opening the sound, a combination of the *FMODEnums::FMOD_MODE* flags. For an in-memory buffer the OPENMEMORY flag is required; it is not added automatically.

### Return value

Newly created sound.
