# Unigine::Plugins::FMOD::FMODCore Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


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
## void initCore ( int max_channels , int flags )

Initializes the system object and prepares FMOD for playback.
### Arguments

- *int* **max_channels** - Maximum number of Channel objects available for playback, also known as virtual channels. Virtual channels will play with minimal overhead, with a subset of 'real' voices that are mixed, and selected based on priority and audibility. Range: [0; 4095]
- *int* **flags** - Initialization flags. More than one mode can be set at once by combining them with the OR operator.

## Sound createSound ( string file_name , int mode )

Loads a sound into memory, opens it for streaming or sets it up for callback based sounds.
### Arguments

- *string* **file_name** - Name of the file or URL to open (UTF-8 string) or a pointer to a preloaded sound memory block.
- *int* **mode** - Behavior modifier for opening the sound.

### Return value

Newly created Sound object.
## Sound createStream ( string url )

Creates a stream, for example, an internet stream to be used as a radio.
### Arguments

- *string* **url** - URL of the resource.

### Return value

Newly created Sound object.
## Channel playSound ( Sound * OUT_sound , ChannelGroup * OUT_channel_group , bool paused )

Plays a sound on a channel.
### Arguments

- *[Sound](../../../../api/library/engine/class.sound_usc.md) ** **OUT_sound** - Sound to play. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *[ChannelGroup](../../../../api/library/plugins/fmod/class.channelgroup_usc.md) ** **OUT_channel_group** - Group to output to instead of the master. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *bool* **paused** - Determines whether to start in the paused state. Start a Channel paused to allow altering attributes without it being audible, then follow it up with a call to *ChannelControl::setPaused* with *paused* = False.

### Return value

Newly playing channel.
## void setListener3DAttributes ( int listener , const Vec3 & position , const Vec3 & up , const Vec3 & forward , const Vec3 & velocity )

Sets the 3D attributes of the listener. Vectors must be provided in the correct handedness.
### Arguments

- *int* **listener** - Listener index.
- *const Vec3 &* **position** - Position in world space used for panning and attenuation.
- *const Vec3 &* **up** - Upwards orientation, must be of unit length (1.0) and perpendicular to forward.
- *const Vec3 &* **forward** - Forwards orientation, must be of unit length (1.0) and perpendicular to up.
- *const Vec3 &* **velocity** - Velocity in world space used for doppler.

## void getListener3DAttributes ( int listener , Vec3 & position , Vec3 & up , Vec3 & forward , Vec3 & velocity )

Returns the 3D attributes of the listener.
### Arguments

- *int* **listener** - Listener index.
- *Vec3 &* **position** - Position in world space.
- *Vec3 &* **up** - Upwards orientation.
- *Vec3 &* **forward** - Forwards orientation.
- *Vec3 &* **velocity** - Velocity in world space.

## Channel getChannel ( int index )

Returns the channel object at the specified index.
### Arguments

- *int* **index** - Channel index.

### Return value

Channel object.
## ChannelGroup createChannelGroup ( string name )

Create a ChannelGroup object.
### Arguments

- *string* **name** - Label for identification purposes, in the UTF-8 format.

### Return value

Newly created group.
## Sound createSound ( Blob data , int mode )

Creates a sound from the in-memory contents of a blob instead of a file.
### Arguments

- *[Blob](../../../../api/library/common/class.blob_usc.md)* **data** - Blob whose raw contents hold the audio file data.
- *int* **mode** - Behavior modifier for opening the sound, a combination of the *FMODEnums::FMOD_MODE* flags. For an in-memory buffer the OPENMEMORY flag is required; it is not added automatically.

### Return value

Newly created sound.
