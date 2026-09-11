# Unigine::SoundSource Class (CS)

**Inherits from:** Node


This class is used to create directional [sound sources](../../../objects/sounds/sound_source.md). The source's sound fades out linearly in a specified range (see [*MinDistance*](#getMinDistance_float) and [*MaxDistance*](#getMaxDistance_float)). If inner and outer sound cones are defined, they will also have their share in the attenuation factor (see the [*ConeInnerAngle*](#getConeInnerAngle_float) and [*ConeOuterAngle*](#getConeOuterAngle_float) functions).

> **Notice:** Attenuation is available only for mono sound sources. If a source is the stereo one, it won't attenuate with the distance.


Sound sources are automatically handled by the sound manager. When the sound source is within the [audible range](#getMaxDistance_float), it is loaded into the memory (a full sample or its chunk, depending on whether the source is [static or streamed](#static_vs_stream)). When it gets outside the audible range, the sound file is automatically deleted from the memory. Static sound sources are instanced; streamed ones are not.
 If you still want to manage a sound source manually, you can check if it has stopped [playing](#isPlaying_int) and after that delete it.


There is also no limitation on the number of sound sources in the world, as only currently audible ones are rendered. In the worst case scenario, when the number of simultaneously heard sound sources exceeds the hardware capabilities, some of them will not be played.


### Creating a Sound Source


To create a sound source, create an instance of the SoundSource class and specify all required settings:


```csharp
// create a new sound source using the given sound sample file
SoundSource sound = new SoundSource("sound.mp3");

// disable sound muffling when being occluded
sound.Occlusion = 0;
// set the distance at which the sound gets clear
sound.MinDistance = 10.0f;
// set the distance at which the sound becomes out of audible range
sound.MaxDistance = 100.0f;
// set the gain that result in attenuation of 6 dB
sound.Gain = 0.5f;
// loop the sound
sound.Loop = 1;
// start playing the sound sample
sound.Play();


```


### Updating an Existing Sound Source


To update the sound source settings, you can call the corresponding methods:


```csharp
// change the sample file of the playing sound source
if ((sound.IsPlaying) && (Input.IsKeyDown(Input.KEY.C)))
{
	// specify a new sample file
	sound.SampleName = "sound_1.mp3";
	// reduce the gain
	sound.Gain = 0.2f;
}


```


As sound has its own thread that updates at 30 FPS, changes won't be applied immediately. However, you can force updating by using the *[RenderWorld()](../../../api/library/engine/class.sound_cs.md#renderWorld_int_void)* method.


Sound events like *[Play()](#play_void)* or *[Stop()](#stop_void)* aren't updated immediately as well. So, when you need to perform operations that require stopping of the playback (for example, updating the time from which the sample should be played), you need to force update the sound thread after stopping the playback:


```csharp
// check if the sound sample is playing
if (sound.IsPlaying)
{
	// stop playing the sample
	sound.Stop();
	// force updating of the sound thread
	Sound.RenderWorld(1);
	// update time
	sound.Time = 0.0f;
	// play the sample
	sound.Play();
}


```


### See Also


- *[Playing Sounds on Collisions](../../../code/usage/sound_source/index_cs.md)* article to learn how to play sound sources on collisions with physical bodies
- *[Controlling Sound Sources Globally](../../../code/usage/controlling_sound_sources_globally/index_cs.md)* article to learn how to toggle all sounds at the same time
- C# Component sample
- UnigineScript samples:

  -
  -
  -
  -
  -
  -


## SoundSource Class

### Properties

## 🔒︎ bool IsStopped

The value indicating if playback is stopped.
## 🔒︎ bool IsPlaying

The value indicating if the sample is being played.
## float RoomRolloff

The scaling room rolloff factor for the sound source that determines attenuation of the reverberation sound over distance.
## float Adaptation

The adaptation time period for the sound source during which the volume of the occluded sound gradually changes (fading in and out). this parameter is used to make sounds fade in and out smoothly.
## int Occlusion

The value indicating if sound source should be muffled when being occluded.
## int OcclusionMask

The bit mask that determines which objects occlude the sound source. For a sound to be occluded by an object's surface, at least one bit of this mask should match the [occlusion mask of object's surface](../../../api/library/objects/class.object_cs.md#setSoundOcclusionMask_int_int_void). Each surface has its own [occlusion value](../../../api/library/objects/class.object_cs.md#setSoundOcclusion_float_int_void), that determines how much it affects sounds in case of occlusion.
> **Notice:** [Sound occlusion](../../../api/library/engine/class.sound_cs.md#setSourceOcclusion_int_void) must be enabled.


## float MinDistance

The distance at which the sound starts to fade.
## float MaxDistance

The distance at which the sound completely fades out.
## float ConeOuterGain

The gain controlling the sound intensity outside the oriented cone defined by the [outer angle](#getConeOuterAngle_float).
## float ConeOuterGainHF

The gain filter value for the sound source that attenuates the reverberation sound at high frequencies outside the oriented cone.
## float ConeOuterAngle

The angle of the outer sound cone. When moving to the edge of the outer cone, sound volume is fading up to the [outside the cone gain value](#getConeOuterGain_float).
## float ConeInnerAngle

The angle of the inner sound cone. Sound volume in the inner cone does not change.
## float AirAbsorption

The air absorption value for the sound source that determines the distance-dependent attenuation of the reverberation sound at high frequencies caused by the propagation medium.
## float Time

The time from the beginning of the sample. You can't set time if the sample is already playing: [stop](#stop_void) the playback, set the time, and [resume](#play_void) the playback.
## int ReverbMask

The bit mask that determines what [reverberation zones](../../../api/library/sounds/class.soundreverb_cs.md) can be heard. For sound to reverberate, at least one bit of this mask should match the [player's reverberation mask](../../../api/library/players/class.player_cs.md#setReverbMask_int_void). At the same time, [reverb mask of the reverberation zone](../../../api/library/sounds/class.soundreverb_cs.md#setReverbMask_int_void) should also match the player's one (but not necessarily in the same bit as this mask matches it).
## int SourceMask

The bit mask that determines to what [sound channels](../../../api/library/engine/class.sound_cs.md#setSourceVolume_int_float_void) the source belongs to. For a sound source to be heard, its mask should match the [player's sound mask](../../../api/library/players/class.player_cs.md#setSourceMask_int_void) in one bit at least.
## string SampleName

The sound file for the ambient sound.
> **Notice:** To change the sound file of the currently played ambient sound, [stop](#stop_void) the playback, set the sample name, and then [resume](#play_void) the playback.


```csharp
if (sound.IsPlaying)
{
	// stop the playing sound
	sound.Stop();
	// force updating of the sound thread
	Sound.RenderWorld(1);
	// set a new sample file to be played
	sound.SampleName = "stream_stereo_01.oga";
	// play the sound
	sound.Play();
}


```


## float Pitch

The sound pitch.
## bool Stream

The value indicating whether the sound is streamed or not.
## bool RestartOnEnable

The value indicating if playback is to be restarted from the beginning each time the sound source is enabled.
## bool PlayOnEnable

The value indicating if playback is to be started each time the sound source is enabled.
> **Notice:** Playback will begin from the moment it was previously stopped. To enable playback from the beginning, use [*RestartOnEnable*](#setRestartOnEnable_int_void).


## int Loop

The value indicating if the sample is looped.
## 🔒︎ float Length

The total length of the sound sample.
## float Gain

The gain controlling the sound intensity.
## float PitchShift

The pitch shift of the played sample in semitones, clamped to the [-12; 12] range (one octave down to one octave up), with the default of 0 (no shift). Unlike the **[Pitch](../../...md#getPitch_float)** property, it changes the tone without changing the playback speed. The effect requires pitch-shifter support in the sound device; otherwise the value has no audible effect.
### Members

---

## SoundSource ( string name , int stream = 0 )

Constructor. Creates a new world sound source using a given sound sample file.
### Arguments

- *string* **name** - Path to the sound sample file.
- *int* **stream** -  Positive value to create a streaming source, **0** to create a static source. If the flag is set, the sample will not be fully loaded into memory. Instead, its successive parts will be read one by one into a memory buffer.

## void Play ( )

Starts playing the sample.
## void Stop ( )

Stops playback. This function doesn't reset the playback position so that playing of the file can be [resumed](#play_void) from the same point.
> **Notice:** The playback won't stop immediately, as the sound thread is updated at 30 FPS. So, when you need to perform operations that require stopping of the playback (for example, updating the time, from which the sample should be played), you need to [force update](../../../api/library/engine/class.sound_cs.md#renderWorld_int_void) the sound thread after stopping the playback.


## static int type ( )

Returns the type of the node.
### Return value

[Sound](../../../api/library/engine/class.sound_cs.md) type identifier.
