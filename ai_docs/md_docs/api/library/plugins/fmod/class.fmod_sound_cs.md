# Unigine::Plugins::FMOD::Sound Class (CS)


> **Notice:** This set of functions is available when the [FMOD](../../../../code/plugins/fmod/index.md) plugin is loaded.


Container for sample data that can be played on a Channel.


## Sound Class

### Members

---

## Channel Play ( )

Starts playback of the sound.
### Return value

Newly playing channel.
## void Release ( )

Releases the Sound object and frees its resources.
## uint GetLength ( FMODEnums.TIME_UNIT time_unit )

Returns the length using the specified time unit. A length of 0xFFFFFFFF means it is of unlimited length, such as an internet radio stream or MOD/S3M/XM/IT file which may loop forever.


Using a VBR (Variable Bit Rate) source that does not have metadata containing its accurate length (such as un-tagged MP3 or MOD/S3M/XM/IT) may return inaccurate length values. For these formats, use [ACCURATETIME](../../../../api/library/plugins/fmod/class.fmodenums_cs.md#ACCURATETIME) when creating the sound. This will cause a slight delay and memory increase, as FMOD will scan the whole during creation to find the correct length. This flag also creates a seek table to enable sample accurate seeking.

### Arguments

- *[FMODEnums.TIME_UNIT](../../../../api/library/plugins/fmod/class.fmodenums_cs.md#TIME_UNIT)* **time_unit** - Time unit type.

### Return value

Sound's length.
