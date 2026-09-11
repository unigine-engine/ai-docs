# Unigine::Plugins::FMOD::FMODCore Class (CS)


> **Notice:** This set of functions is available when the [FMOD](../../../../code/plugins/fmod/index.md) plugin is loaded.


This class is intended to cover the basics / primitives of sound.


## FMODCore Class

### Members

---

## void Close ( )

Closes the connection to the output and returns to an uninitialized state without releasing the object.
## void Release ( )

Closes and frees this object and its resources.
## void Update ( )

Updates the FMOD system.
## void InitCore ( int max_channels , FMODEnums.INIT_FLAGS flags )

Initializes the system object and prepares FMOD for playback.
### Arguments

- *int* **max_channels** - Maximum number of Channel objects available for playback, also known as virtual channels. Virtual channels will play with minimal overhead, with a subset of 'real' voices that are mixed, and selected based on priority and audibility. Range: [0; 4095]
- *[FMODEnums.INIT_FLAGS](../../../../api/library/plugins/fmod/class.fmodenums_cs.md#INIT_FLAGS)* **flags** - Initialization flags. More than one mode can be set at once by combining them with the OR operator.

## Sound CreateSound ( string file_name , FMODEnums.FMOD_MODE mode )

Loads a sound into memory, opens it for streaming or sets it up for callback based sounds.
### Arguments

- *string* **file_name** - Name of the file or URL to open (UTF-8 string) or a pointer to a preloaded sound memory block.
- *[FMODEnums.FMOD_MODE](../../../../api/library/plugins/fmod/class.fmodenums_cs.md#FMOD_MODE)* **mode** - Behavior modifier for opening the sound.

### Return value

Newly created Sound object.
## Sound CreateStream ( string url )

Creates a stream, for example, an internet stream to be used as a radio.
### Arguments

- *string* **url** - URL of the resource.

### Return value

Newly created Sound object.
## Channel PlaySound ( Sound [] OUT_sound , ChannelGroup [] OUT_channel_group , bool paused )

Plays a sound on a channel.
### Arguments

- *[Sound](../../../../api/library/engine/class.sound_cs.md)[]* **OUT_sound** - Sound to play. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *[ChannelGroup](../../../../api/library/plugins/fmod/class.channelgroup_cs.md)[]* **OUT_channel_group** - Group to output to instead of the master. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *bool* **paused** - Determines whether to start in the paused state. Start a Channel paused to allow altering attributes without it being audible, then follow it up with a call to *ChannelControl::setPaused* with *paused* = False.

### Return value

Newly playing channel.
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

## Channel GetChannel ( int index )

Returns the channel object at the specified index.
### Arguments

- *int* **index** - Channel index.

### Return value

Channel object.
## ChannelGroup CreateChannelGroup ( string name )

Create a ChannelGroup object.
### Arguments

- *string* **name** - Label for identification purposes, in the UTF-8 format.

### Return value

Newly created group.
## Sound CreateSound ( Blob data , FMODEnums.FMOD_MODE mode )

Creates a sound from the in-memory contents of a blob instead of a file.
### Arguments

- *[Blob](../../../../api/library/common/class.blob_cs.md)* **data** - Blob whose raw contents hold the audio file data.
- *[FMODEnums.FMOD_MODE](../../../../api/library/plugins/fmod/class.fmodenums_cs.md#FMOD_MODE)* **mode** - Behavior modifier for opening the sound, a combination of the *FMODEnums::FMOD_MODE* flags. For an in-memory buffer the OPENMEMORY flag is required; it is not added automatically.

### Return value

Newly created sound.
