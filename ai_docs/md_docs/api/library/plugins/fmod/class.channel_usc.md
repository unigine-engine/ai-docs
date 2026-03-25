# Unigine::Plugins::FMOD::Channel Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


> **Notice:** This set of functions is available when the [FMOD](../../../../code/plugins/fmod/index.md) plugin is loaded.


A source of audio signal that connects to the ChannelGroup mixing hierarchy.


## Channel Class

### Members

## void setPitch ( float pitch )

Sets a new relative pitch or playback rate. Scales the playback frequency of a Channel object. The pitch value of 0.5f represents half pitch (one octave down), 1.0f represents unmodified pitch and 2.0f represents double pitch (one octave up).
### Arguments

- *float* **pitch** - The pitch value: 0.5f represents half pitch (one octave down), 1.0f represents unmodified pitch and 2.0f represents double pitch (one octave up).

## float getPitch () const

Returns the current relative pitch or playback rate. Scales the playback frequency of a Channel object. The pitch value of 0.5f represents half pitch (one octave down), 1.0f represents unmodified pitch and 2.0f represents double pitch (one octave up).
### Return value

Current pitch value: 0.5f represents half pitch (one octave down), 1.0f represents unmodified pitch and 2.0f represents double pitch (one octave up).
## void setFrequency ( float frequency )

Sets a new playback frequency or playback rate. The default frequency is determined by the audio format of the [Sound](../../../../api/library/plugins/fmod/class.fmod_sound_usc.md) or [DSP](../../../../api/library/plugins/fmod/class.dsp_usc.md).
### Arguments

- *float* **frequency** - The playback frequency.

## float getFrequency () const

Returns the current playback frequency or playback rate. The default frequency is determined by the audio format of the [Sound](../../../../api/library/plugins/fmod/class.fmod_sound_usc.md) or [DSP](../../../../api/library/plugins/fmod/class.dsp_usc.md).
### Return value

Current playback frequency.
## void setPaused ( int paused )

Sets a new pause state for the channel.
### Arguments

- *int* **paused** - The pause state of the channel

## int isPaused () const

Returns the current pause state for the channel.
### Return value

Current pause state of the channel
## void setPriority ( int priority )

Sets a new priority used for virtual voice ordering. 0 means *the most important*, 256 means *the least important*. The priority is used as a coarse grain control for the virtual voice system. Channels with the lower priority will always be stolen before Channels with the higher ones. For Channels of the equal priority, those with the quietest audibility value will be stolen first.
### Arguments

- *int* **priority** - The priority used for virtual voice ordering: 0 means *the most important*, 256 means *the least important*.

## int getPriority () const

Returns the current priority used for virtual voice ordering. 0 means *the most important*, 256 means *the least important*. The priority is used as a coarse grain control for the virtual voice system. Channels with the lower priority will always be stolen before Channels with the higher ones. For Channels of the equal priority, those with the quietest audibility value will be stolen first.
### Return value

Current priority used for virtual voice ordering: 0 means *the most important*, 256 means *the least important*.
## void setMute ( int mute )

Sets a new mute state. Mute is an additional control for volume, the effect of which is equivalent to setting the volume to zero.
### Arguments

- *int* **mute** - The mute (silent) state

## int isMute () const

Returns the current mute state. Mute is an additional control for volume, the effect of which is equivalent to setting the volume to zero.
### Return value

Current mute (silent) state
## void setLoopCount ( int count )

Sets a new number of times to loop before stopping.
### Arguments

- *int* **count** - The number of times to loop before stopping: 0 means *oneshot*, 1 means *loop once then stop* and -1 represents *loop forever*.

## int getLoopCount () const

Returns the current number of times to loop before stopping.
### Return value

Current number of times to loop before stopping: 0 means *oneshot*, 1 means *loop once then stop* and -1 represents *loop forever*.
## void setVolume ( float volume )

Sets a new volume level. Range [-inf; inf]. 0 = silent, 1 = full. Negative level inverts the signal. Values larger than 1 amplify the signal.
### Arguments

- *float* **volume** - The volume level in range [-inf; inf]. 0 = silent, 1 = full. Negative level inverts the signal. Values larger than 1 amplify the signal..

## float getVolume () const

Returns the current volume level. Range [-inf; inf]. 0 = silent, 1 = full. Negative level inverts the signal. Values larger than 1 amplify the signal.
### Return value

Current volume level in range [-inf; inf]. 0 = silent, 1 = full. Negative level inverts the signal. Values larger than 1 amplify the signal..
## void setVolumeRamp ( int ramp )

Sets a new value indicating if the volume changes are ramped or instantaneous. If not paused, volume changes are ramped to the target value to avoid a pop sound. This function allows you to override that setting and apply volume changes immediately.
### Arguments

- *int* **ramp** - The ramped volume change

## int isVolumeRamp () const

Returns the current value indicating if the volume changes are ramped or instantaneous. If not paused, volume changes are ramped to the target value to avoid a pop sound. This function allows you to override that setting and apply volume changes immediately.
### Return value

Current ramped volume change
## int isPlaying () const

Returns the current playing state.
### Return value

Current channel is playing
## float getAudibility () const

Returns the current estimation of the output volume. The estimated volume is calculated based on 3D spatialization, occlusion, API volume levels and DSPs used. This value is used to determine which Channels should be audible and which Channels should be virtualized when resources are limited.
### Return value

Current estimated audibility.
## int isVirtual () const

Returns the current value indicating whether the Channel is being emulated by the virtual voice system. True means *silent* / *emulated*, false means *audible* / *real*.
### Return value

Current virtual state is silent/emulated
## int getIndex () const

Returns the current index of this object in the System Channel pool.
### Return value

Current index within the System Channel pool - a value from 0 to the [total number of System Channels](../../../../api/library/plugins/fmod/class.fmodcore_usc.md#initCore_int_int_void) - 1.
---

## void stop ( )

Stops the Channel (or all Channels in nested ChannelGroups) from playing.
## void setMinMaxDistance ( float min , float max )

Sets the minimum and maximum distances used to calculate the 3D rolloff attenuation.
### Arguments

- *float* **min** - Distance from the source where attenuation begins. Range: [0; max]. Default: 1
- *float* **max** - Distance from the source where attenuation ends. Range: [min; inf]. Default: 10000.

## void setPosition ( Vec3 position )

Sets the 3D position used to apply panning and attenuation.
### Arguments

- *Vec3* **position** - Position in 3D space used for panning and attenuation.

## void setPositionTimeLine ( unsigned int position , int time_unit )

Sets the current playback position.
### Arguments

- *unsigned int* **position** - Playback position.
- *int* **time_unit** - Time units for position.

## void getPositionTimeLine ( uint & position , int time_unit )

Returns the current playback position.
### Arguments

- *uint &* **position** - Playback position.
- *int* **time_unit** - Time units for position.

## void release ( )

Releases the channel object.
## void setVelocity ( Vec3 velocity )

Sets the velocity used to apply doppler.
### Arguments

- *Vec3* **velocity** - Velocity in 3D space used for doppler.

## DSP addDSP ( int index , int dsp_type )

Adds a DSP unit to the specified index in the DSP chain.
### Arguments

- *int* **index** - Offset into the DSP chain.
- *int* **dsp_type** - Type of the DSP.

### Return value

Added DSP.
## void removeDSP ( int index )

Removes the specified DSP unit from the DSP chain.
### Arguments

- *int* **index** - Index of the DSP unit.

## DSP getDSP ( int index )

Returns the DSP unit at the specified index in the DSP chain.
### Arguments

- *int* **index** - Index of the DSP unit.

### Return value

DSP unit at the specified index.
## void setPan ( float pan )

Sets the left/right pan level.
### Arguments

- *float* **pan** - Pan level: -1 represents *the full left*, 0 represents *the center*, 1 represents *the full right*.

## int getNumDSPs ( )

Returns the number of DSP units in the DSP chain.
### Return value

The number of DSP units in the DSP chain.
