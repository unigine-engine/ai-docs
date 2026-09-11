# Unigine::SoundSource Class (CPP)

**Header:** #include <UnigineSounds.h>

**Inherits from:** Node


This class is used to create directional [sound sources](../../../objects/sounds/sound_source.md). The source's sound fades out linearly in a specified range (see [*getMinDistance()*](#getMinDistance_float) and [*getMaxDistance()*](#getMaxDistance_float)). If inner and outer sound cones are defined, they will also have their share in the attenuation factor (see the [*getConeInnerAngle()*](#getConeInnerAngle_float) and [*getConeOuterAngle()*](#getConeOuterAngle_float) functions).

> **Notice:** Attenuation is available only for mono sound sources. If a source is the stereo one, it won't attenuate with the distance.


Sound sources are automatically handled by the sound manager. When the sound source is within the [audible range](#getMaxDistance_float), it is loaded into the memory (a full sample or its chunk, depending on whether the source is [static or streamed](#static_vs_stream)). When it gets outside the audible range, the sound file is automatically deleted from the memory. Static sound sources are instanced; streamed ones are not.
 If you still want to manage a sound source manually, you can check if it has stopped [playing](#isPlaying_int) and after that delete it.


There is also no limitation on the number of sound sources in the world, as only currently audible ones are rendered. In the worst case scenario, when the number of simultaneously heard sound sources exceeds the hardware capabilities, some of them will not be played.


### Creating a Sound Source


To create a sound source, create an instance of the SoundSource class and specify all required settings:


```cpp
// create a new sound source using the given sound sample file
SoundSourcePtr sound = SoundSource::create("sound.mp3");

// disable sound muffling when being occluded
sound->setOcclusion(0);
// set the distance at which the sound gets clear
sound->setMinDistance(10.0f);
// set the distance at which the sound becomes out of audible range
sound->setMaxDistance(100.0f);
// set the gain that result in attenuation of 6 dB
sound->setGain(0.5f);
// loop the sound
sound->setLoop(1);
// start playing the sound sample
sound->play();


```


### Updating an Existing Sound Source


To update the sound source settings, you can call the corresponding methods:


```cpp
// change the sample file of the playing sound source
if ((sound->isPlaying()) && (Input::isKeyDown(Input::KEY::KEY_C)))
{
	// specify a new sample file
	sound->setSampleName("sound_1.mp3");
	// reduce the gain
	sound->setGain(0.2f);
}


```


As sound has its own thread that updates at 30 FPS, changes won't be applied immediately. However, you can force updating by using the *[renderWorld()](../../../api/library/engine/class.sound_cpp.md#renderWorld_int_void)* method.


Sound events like *[play()](#play_void)* or *[stop()](#stop_void)* aren't updated immediately as well. So, when you need to perform operations that require stopping of the playback (for example, updating the time from which the sample should be played), you need to force update the sound thread after stopping the playback:


```cpp
// check if the sound sample is playing
if (sound->isPlaying())
{
	// stop playing the sample
	sound->stop();
	// force updating of the sound thread
	Sound::renderWorld(1);
	// update time
	sound->setTime(0.0f);
	// play the sample
	sound->play();
}


```


### See Also


- *[Playing Sounds on Collisions](../../../code/usage/sound_source/index_cpp.md)* article to learn how to play sound sources on collisions with physical bodies
- *[Controlling Sound Sources Globally](../../../code/usage/controlling_sound_sources_globally/index_cpp.md)* article to learn how to toggle all sounds at the same time
- C# Component sample
- UnigineScript samples:

  -
  -
  -
  -
  -
  -


## SoundSource Class

### Members

## bool isStopped () const

Returns the current value indicating if playback is stopped.
### Return value

**true** if the sample is stopped; otherwise **false**.
## bool isPlaying () const

Returns the current value indicating if the sample is being played.
### Return value

**true** if the sample is being played; otherwise **false**.
## void setRoomRolloff ( float rolloff )

Sets a new scaling room rolloff factor for the sound source that determines attenuation of the reverberation sound over distance.
### Arguments

- *float* **rolloff** - The room rolloff factor in range **[0.0; 10.0]**.

## float getRoomRolloff () const

Returns the current scaling room rolloff factor for the sound source that determines attenuation of the reverberation sound over distance.
### Return value

Current room rolloff factor in range **[0.0; 10.0]**.
## void setAdaptation ( float adaptation )

Sets a new adaptation time period for the sound source during which the volume of the occluded sound gradually changes (fading in and out). this parameter is used to make sounds fade in and out smoothly.
### Arguments

- *float* **adaptation** - The adaptation time, in seconds. 0.0f means instant adaptation.

## float getAdaptation () const

Returns the current adaptation time period for the sound source during which the volume of the occluded sound gradually changes (fading in and out). this parameter is used to make sounds fade in and out smoothly.
### Return value

Current adaptation time, in seconds. 0.0f means instant adaptation.
## void setOcclusion ( int occlusion )

Sets a new value indicating if sound source should be muffled when being occluded.
### Arguments

- *int* **occlusion** - The positive number for the sound to be muffled by occlusion; otherwise, **0**.

## int getOcclusion () const

Returns the current value indicating if sound source should be muffled when being occluded.
### Return value

Current positive number for the sound to be muffled by occlusion; otherwise, **0**.
## void setOcclusionMask ( int mask )

Sets a new bit mask that determines which objects occlude the sound source. For a sound to be occluded by an object's surface, at least one bit of this mask should match the [occlusion mask of object's surface](../../../api/library/objects/class.object_cpp.md#setSoundOcclusionMask_int_int_void). Each surface has its own [occlusion value](../../../api/library/objects/class.object_cpp.md#setSoundOcclusion_float_int_void), that determines how much it affects sounds in case of occlusion.
> **Notice:** [Sound occlusion](../../../api/library/engine/class.sound_cpp.md#setSourceOcclusion_int_void) must be enabled.


### Arguments

- *int* **mask** - The integer each bit of which is a mask for sound source occlusion.

## int getOcclusionMask () const

Returns the current bit mask that determines which objects occlude the sound source. For a sound to be occluded by an object's surface, at least one bit of this mask should match the [occlusion mask of object's surface](../../../api/library/objects/class.object_cpp.md#setSoundOcclusionMask_int_int_void). Each surface has its own [occlusion value](../../../api/library/objects/class.object_cpp.md#setSoundOcclusion_float_int_void), that determines how much it affects sounds in case of occlusion.
> **Notice:** [Sound occlusion](../../../api/library/engine/class.sound_cpp.md#setSourceOcclusion_int_void) must be enabled.


### Return value

Current integer each bit of which is a mask for sound source occlusion.
## void setMinDistance ( float distance )

Sets a new distance at which the sound starts to fade.
### Arguments

- *float* **distance** - The distance at which the sound starts to fade, in units.

## float getMinDistance () const

Returns the current distance at which the sound starts to fade.
### Return value

Current distance at which the sound starts to fade, in units.
## void setMaxDistance ( float distance )

Sets a new distance at which the sound completely fades out.
### Arguments

- *float* **distance** - The distance at which the sound completely fades out, in units.

## float getMaxDistance () const

Returns the current distance at which the sound completely fades out.
### Return value

Current distance at which the sound completely fades out, in units.
## void setConeOuterGain ( float gain )

Sets a new gain controlling the sound intensity outside the oriented cone defined by the [outer angle](#getConeOuterAngle_float).
### Arguments

- *float* **gain** - The cone outer gain.

## float getConeOuterGain () const

Returns the current gain controlling the sound intensity outside the oriented cone defined by the [outer angle](#getConeOuterAngle_float).
### Return value

Current cone outer gain.
## void setConeOuterGainHF ( float hf )

Sets a new gain filter value for the sound source that attenuates the reverberation sound at high frequencies outside the oriented cone.
### Arguments

- *float* **hf** - The high-frequency reverberation gain value.

## float getConeOuterGainHF () const

Returns the current gain filter value for the sound source that attenuates the reverberation sound at high frequencies outside the oriented cone.
### Return value

Current high-frequency reverberation gain value.
## void setConeOuterAngle ( float angle )

Sets a new angle of the outer sound cone. When moving to the edge of the outer cone, sound volume is fading up to the [outside the cone gain value](#getConeOuterGain_float).
### Arguments

- *float* **angle** - The cone outer angle in degrees.

## float getConeOuterAngle () const

Returns the current angle of the outer sound cone. When moving to the edge of the outer cone, sound volume is fading up to the [outside the cone gain value](#getConeOuterGain_float).
### Return value

Current cone outer angle in degrees.
## void setConeInnerAngle ( float angle )

Sets a new angle of the inner sound cone. Sound volume in the inner cone does not change.
### Arguments

- *float* **angle** - The cone inner angle in degrees. **360** degrees represents an omnidirectional sound source.

## float getConeInnerAngle () const

Returns the current angle of the inner sound cone. Sound volume in the inner cone does not change.
### Return value

Current cone inner angle in degrees. **360** degrees represents an omnidirectional sound source.
## void setAirAbsorption ( float absorption )

Sets a new air absorption value for the sound source that determines the distance-dependent attenuation of the reverberation sound at high frequencies caused by the propagation medium.
### Arguments

- *float* **absorption** - The air absorption value in range **[0.0;10.0]**.

## float getAirAbsorption () const

Returns the current air absorption value for the sound source that determines the distance-dependent attenuation of the reverberation sound at high frequencies caused by the propagation medium.
### Return value

Current air absorption value in range **[0.0;10.0]**.
## void setTime ( float time )

Sets a new time from the beginning of the sample. You can't set time if the sample is already playing: [stop](#stop_void) the playback, set the time, and [resume](#play_void) the playback.
### Arguments

- *float* **time** - The time from the beginning of the sample, in seconds.

## float getTime () const

Returns the current time from the beginning of the sample. You can't set time if the sample is already playing: [stop](#stop_void) the playback, set the time, and [resume](#play_void) the playback.
### Return value

Current time from the beginning of the sample, in seconds.
## void setReverbMask ( int mask )

Sets a new bit mask that determines what [reverberation zones](../../../api/library/sounds/class.soundreverb_cpp.md) can be heard. For sound to reverberate, at least one bit of this mask should match the [player's reverberation mask](../../../api/library/players/class.player_cpp.md#setReverbMask_int_void). At the same time, [reverb mask of the reverberation zone](../../../api/library/sounds/class.soundreverb_cpp.md#setReverbMask_int_void) should also match the player's one (but not necessarily in the same bit as this mask matches it).
### Arguments

- *int* **mask** - The integer each bit of which is a mask for reverberating sound sources.

## int getReverbMask () const

Returns the current bit mask that determines what [reverberation zones](../../../api/library/sounds/class.soundreverb_cpp.md) can be heard. For sound to reverberate, at least one bit of this mask should match the [player's reverberation mask](../../../api/library/players/class.player_cpp.md#setReverbMask_int_void). At the same time, [reverb mask of the reverberation zone](../../../api/library/sounds/class.soundreverb_cpp.md#setReverbMask_int_void) should also match the player's one (but not necessarily in the same bit as this mask matches it).
### Return value

Current integer each bit of which is a mask for reverberating sound sources.
## void setSourceMask ( int mask )

Sets a new bit mask that determines to what [sound channels](../../../api/library/engine/class.sound_cpp.md#setSourceVolume_int_float_void) the source belongs to. For a sound source to be heard, its mask should match the [player's sound mask](../../../api/library/players/class.player_cpp.md#setSourceMask_int_void) in one bit at least.
### Arguments

- *int* **mask** - The integer each bit of which specifies a sound channel.

## int getSourceMask () const

Returns the current bit mask that determines to what [sound channels](../../../api/library/engine/class.sound_cpp.md#setSourceVolume_int_float_void) the source belongs to. For a sound source to be heard, its mask should match the [player's sound mask](../../../api/library/players/class.player_cpp.md#setSourceMask_int_void) in one bit at least.
### Return value

Current integer each bit of which specifies a sound channel.
## void setSampleName ( const char * name )

Sets a new sound file for the ambient sound.
> **Notice:** To change the sound file of the currently played ambient sound, [stop](#stop_void) the playback, set the sample name, and then [resume](#play_void) the playback.


```cpp
if (sound->isPlaying())
{
	// stop the playing sound
	sound->stop();
	// force updating of the sound thread
	Sound::renderWorld(1);
	// set a new sample file to be played
	sound->setSampleName("stream_stereo_01.oga");
	// play the sound
	sound->play();
}


```


### Arguments

- *const char ** **name** - The path to the sound file.

## const char * getSampleName () const

Returns the current sound file for the ambient sound.
> **Notice:** To change the sound file of the currently played ambient sound, [stop](#stop_void) the playback, set the sample name, and then [resume](#play_void) the playback.


```cpp
if (sound->isPlaying())
{
	// stop the playing sound
	sound->stop();
	// force updating of the sound thread
	Sound::renderWorld(1);
	// set a new sample file to be played
	sound->setSampleName("stream_stereo_01.oga");
	// play the sound
	sound->play();
}


```


### Return value

Current path to the sound file.
## void setPitch ( float pitch )

Sets a new sound pitch.
### Arguments

- *float* **pitch** - The factor by which the current pitch will be multiplied in range **[0.1;10.0]**.

## float getPitch () const

Returns the current sound pitch.
### Return value

Current factor by which the current pitch will be multiplied in range **[0.1;10.0]**.
## void setStream ( bool stream )

Sets a new value indicating whether the sound is streamed or not.
### Arguments

- *bool* **stream** - Set **true** to enable the sound streaming; **false** - to disable it.

## bool isStream () const

Returns the current value indicating whether the sound is streamed or not.
### Return value

**true** if the sound streaming is enabled ; otherwise **false**.
## void setRestartOnEnable ( bool enable )

Sets a new value indicating if playback is to be restarted from the beginning each time the sound source is enabled.
### Arguments

- *bool* **enable** - Set **true** to enable playback restart on enabling the sound source; **false** - to disable it.

## bool isRestartOnEnable () const

Returns the current value indicating if playback is to be restarted from the beginning each time the sound source is enabled.
### Return value

**true** if playback restart on enabling the sound source is enabled ; otherwise **false**.
## void setPlayOnEnable ( bool enable )

Sets a new value indicating if playback is to be started each time the sound source is enabled.
> **Notice:** Playback will begin from the moment it was previously stopped. To enable playback from the beginning, use [*setRestartOnEnable()*](#setRestartOnEnable_int_void).


### Arguments

- *bool* **enable** - Set **true** to enable playback start on enabling the sound source; **false** - to disable it.

## bool isPlayOnEnable () const

Returns the current value indicating if playback is to be started each time the sound source is enabled.
> **Notice:** Playback will begin from the moment it was previously stopped. To enable playback from the beginning, use [*setRestartOnEnable()*](#setRestartOnEnable_int_void).


### Return value

**true** if playback start on enabling the sound source is enabled ; otherwise **false**.
## void setLoop ( int loop )

Sets a new value indicating if the sample is looped.
### Arguments

- *int* **loop** - The positive number if the sample is looped; otherwise, **0**.

## int getLoop () const

Returns the current value indicating if the sample is looped.
### Return value

Current positive number if the sample is looped; otherwise, **0**.
## float getLength () const

Returns the current total length of the sound sample.
### Return value

Current length of the sample in seconds.
## void setGain ( float gain )

Sets a new gain controlling the sound intensity.
### Arguments

- *float* **gain** - The volume in range [0, 1] where **0** means muted, **1** means maximum volume.

## float getGain () const

Returns the current gain controlling the sound intensity.
### Return value

Current volume in range [0, 1] where **0** means muted, **1** means maximum volume.
## void setPitchShift ( float shift )

Sets a new pitch shift of the played sample in semitones, clamped to the [-12; 12] range (one octave down to one octave up), with the default of 0 (no shift). Unlike the **[getPitch()](../../...md#getPitch_float)** property, it changes the tone without changing the playback speed. The effect requires pitch-shifter support in the sound device; otherwise the value has no audible effect.
### Arguments

- *float* **shift** - The pitch shift of the played sample, in semitones

## float getPitchShift () const

Returns the current pitch shift of the played sample in semitones, clamped to the [-12; 12] range (one octave down to one octave up), with the default of 0 (no shift). Unlike the **[getPitch()](../../...md#getPitch_float)** property, it changes the tone without changing the playback speed. The effect requires pitch-shifter support in the sound device; otherwise the value has no audible effect.
### Return value

Current pitch shift of the played sample, in semitones
---

## static SoundSourcePtr create ( const char * name , int stream = 0 )

Constructor. Creates a new world sound source using a given sound sample file.
### Arguments

- *const char ** **name** - Path to the sound sample file.
- *int* **stream** -  Positive value to create a streaming source, **0** to create a static source. If the flag is set, the sample will not be fully loaded into memory. Instead, its successive parts will be read one by one into a memory buffer.

## void play ( )

Starts playing the sample.
## void stop ( )

Stops playback. This function doesn't reset the playback position so that playing of the file can be [resumed](#play_void) from the same point.
> **Notice:** The playback won't stop immediately, as the sound thread is updated at 30 FPS. So, when you need to perform operations that require stopping of the playback (for example, updating the time, from which the sample should be played), you need to [force update](../../../api/library/engine/class.sound_cpp.md#renderWorld_int_void) the sound thread after stopping the playback.


## static int type ( )

Returns the type of the node.
### Return value

[Sound](../../../api/library/engine/class.sound_cpp.md) type identifier.
