# Unigine::Plugins::FMOD::Channel Class (CS)


> **Notice:** This set of functions is available when the [FMOD](../../../../code/plugins/fmod/index.md) plugin is loaded.


A source of audio signal that connects to the ChannelGroup mixing hierarchy.


## Channel Class

### Properties

## float Pitch

The relative pitch or playback rate. Scales the playback frequency of a Channel object. The pitch value of 0.5f represents half pitch (one octave down), 1.0f represents unmodified pitch and 2.0f represents double pitch (one octave up).
## float Frequency

The playback frequency or playback rate. The default frequency is determined by the audio format of the [Sound](../../../../api/library/plugins/fmod/class.fmod_sound_cs.md) or [DSP](../../../../api/library/plugins/fmod/class.dsp_cs.md).
## bool Paused

The pause state for the channel.
## int Priority

The priority used for virtual voice ordering. 0 means *the most important*, 256 means *the least important*. The priority is used as a coarse grain control for the virtual voice system. Channels with the lower priority will always be stolen before Channels with the higher ones. For Channels of the equal priority, those with the quietest audibility value will be stolen first.
## bool Mute

The mute state. Mute is an additional control for volume, the effect of which is equivalent to setting the volume to zero.
## int LoopCount

The number of times to loop before stopping.
## float Volume

The volume level. Range [-inf; inf]. 0 = silent, 1 = full. Negative level inverts the signal. Values larger than 1 amplify the signal.
## bool VolumeRamp

The value indicating if the volume changes are ramped or instantaneous. If not paused, volume changes are ramped to the target value to avoid a pop sound. This function allows you to override that setting and apply volume changes immediately.
## 🔒︎ bool IsPlaying

The playing state.
## 🔒︎ float Audibility

The estimation of the output volume. The estimated volume is calculated based on 3D spatialization, occlusion, API volume levels and DSPs used. This value is used to determine which Channels should be audible and which Channels should be virtualized when resources are limited.
## 🔒︎ bool IsVirtual

The value indicating whether the Channel is being emulated by the virtual voice system. True means *silent* / *emulated*, false means *audible* / *real*.
## 🔒︎ int Index

The index of this object in the System Channel pool.
### Members

---

## void Stop ( )

Stops the Channel (or all Channels in nested ChannelGroups) from playing.
## void SetMinMaxDistance ( float min , float max )

Sets the minimum and maximum distances used to calculate the 3D rolloff attenuation.
### Arguments

- *float* **min** - Distance from the source where attenuation begins. Range: [0; max]. Default: 1
- *float* **max** - Distance from the source where attenuation ends. Range: [min; inf]. Default: 10000.

## void SetPosition ( vec3 position )

Sets the 3D position used to apply panning and attenuation.
### Arguments

- *vec3* **position** - Position in 3D space used for panning and attenuation.

## void SetPositionTimeLine ( uint position , FMODEnums.TIME_UNIT time_unit )

Sets the current playback position.
### Arguments

- *uint* **position** - Playback position.
- *[FMODEnums.TIME_UNIT](../../../../api/library/plugins/fmod/class.fmodenums_cs.md#TIME_UNIT)* **time_unit** - Time units for position.

## void GetPositionTimeLine ( out uint position , FMODEnums.TIME_UNIT time_unit )

Returns the current playback position.
### Arguments

- *out uint* **position** - Playback position.
- *[FMODEnums.TIME_UNIT](../../../../api/library/plugins/fmod/class.fmodenums_cs.md#TIME_UNIT)* **time_unit** - Time units for position.

## void Release ( )

Releases the channel object.
## void SetVelocity ( vec3 velocity )

Sets the velocity used to apply doppler.
### Arguments

- *vec3* **velocity** - Velocity in 3D space used for doppler.

## DSP AddDSP ( int index , DSPType.TYPE dsp_type )

Adds a DSP unit to the specified index in the DSP chain.
### Arguments

- *int* **index** - Offset into the DSP chain.
- *[DSPType.TYPE](../../../../api/library/plugins/fmod/class.dsptype_cs.md#TYPE)* **dsp_type** - Type of the DSP.

### Return value

Added DSP.
## void RemoveDSP ( int index )

Removes the specified DSP unit from the DSP chain.
### Arguments

- *int* **index** - Index of the DSP unit.

## DSP GetDSP ( int index )

Returns the DSP unit at the specified index in the DSP chain.
### Arguments

- *int* **index** - Index of the DSP unit.

### Return value

DSP unit at the specified index.
## void SetPan ( float pan )

Sets the left/right pan level.
### Arguments

- *float* **pan** - Pan level: -1 represents *the full left*, 0 represents *the center*, 1 represents *the full right*.

## int GetNumDSPs ( )

Returns the number of DSP units in the DSP chain.
### Return value

The number of DSP units in the DSP chain.
