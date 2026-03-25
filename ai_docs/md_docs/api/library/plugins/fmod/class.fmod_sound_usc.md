# Unigine::Plugins::FMOD::Sound Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


> **Notice:** This set of functions is available when the [FMOD](../../../../code/plugins/fmod/index.md) plugin is loaded.


Container for sample data that can be played on a Channel.


## Sound Class

---

## Channel play ( )

Starts playback of the sound.
### Return value

Newly playing channel.
## void release ( )

Releases the Sound object and frees its resources.
## unsigned int getLength ( int time_unit )

Returns the length using the specified time unit. A length of 0xFFFFFFFF means it is of unlimited length, such as an internet radio stream or MOD/S3M/XM/IT file which may loop forever.


Using a VBR (Variable Bit Rate) source that does not have metadata containing its accurate length (such as un-tagged MP3 or MOD/S3M/XM/IT) may return inaccurate length values. For these formats, use [ACCURATETIME](../../../../api/library/plugins/fmod/class.fmodenums_usc.md#ACCURATETIME) when creating the sound. This will cause a slight delay and memory increase, as FMOD will scan the whole during creation to find the correct length. This flag also creates a seek table to enable sample accurate seeking.

### Arguments

- *int* **time_unit** - Time unit type.

### Return value

Sound's length.
