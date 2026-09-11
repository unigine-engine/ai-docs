# Unigine::AmbientSource Class (CS)


This class is used to create a non-directional ambient background sound.


### Creating an Ambient Sound Source


To create an ambient sound source, create an instance of the AmbientSource class and specify all required settings:


> **Notice:** For an ambient source to be played, a [player](../../../api/library/players/index.md) is always required. In case an ambient source needs to be played when neither a world, nor the editor are loaded, a player, as well as the sound source (see code below), should be created in the [*SystemLogic.Init()*](../../../api/library/common/logic/class.systemlogic_cs.md#init_int) method; otherwise, no sound will be heard.


```csharp
// create a player so that an ambient sound source is played
PlayerSpectator player = new PlayerSpectator();
player.Position = new Vec3(0.0f, -3.401f, 1.5f);
player.ViewDirection = new vec3(0.0f, 1.0f, -0.4f);
Game.Player = player;

// create the ambient sound source
AmbientSource sound = new AmbientSource("sound.mp3");
// set necessary sound settings
sound.Gain = 0.5f;
sound.Pitch = 1.0f;
sound.Loop = 1;
sound.Play();


```


### Updating an Existing Ambient Sound Source


To update the settings of the ambient sound source, you can simply call the corresponding methods:


```csharp
// change the sample file of the playing sound source
if ((sound.IsPlaying) && (Input.IsKeyDown(Input.KEY.C)))
{
	// increase the pitch
    sound.Pitch = 2.0f;

    // reduce the gain
    sound.Gain = 0.2f;
}


```


As sound has its own thread that updates at 30 FPS, changes won't be applied immediately. However, you can force updating by using the *[RenderWorld()](../../../api/library/engine/class.sound_cs.md#renderWorld_int_void)* method.


Sound events like *[Play()](#play_void)* or *[Stop()](#stop_void)* aren't updated immediately as well. So, when you need to perform operations that require stopping of the playback (for example, updating the time from which the sample should be played, or the sample name), you need to force update the sound thread after stopping the playback:


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


- *[Controlling Sound Sources Globally](../../../code/usage/controlling_sound_sources_globally/index_cs.md)* article to learn how to toggle all sounds at the same time
- C# Component sample
- [Sound](../../../sdk/api_samples/cs/sounds.md) samples in *C# Component Samples* suite
- UnigineScript samples:

  -
  -
  -
  -


## AmbientSource Class

### Properties

## 🔒︎ bool IsStopped

The value indicating if playback is stopped.
## 🔒︎ bool IsPlaying

The value indicating if the sample is being played.
## float Time

The time from the beginning of the sample. You can't set time if the sample is already playing: [stop](#stop_void) the playback, set the time, and [resume](#play_void) the playback.
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
## int Loop

The value indicating if the sample is looped.
## 🔒︎ float Length

The total length of the sound sample.
## float Gain

The volume of the sound.
## float PitchShift

The pitch shift of the played sample in semitones, clamped to the [-12; 12] range (one octave down to one octave up), with the default of 0 (no shift). Unlike the **[Pitch](../../...md#getPitch_float)** property, it changes the tone without changing the playback speed. The effect requires pitch-shifter support in the sound device; otherwise the value has no audible effect.
### Members

---

## AmbientSource ( string name , int stream = 0 )

Constructor. Creates a new ambient sound source using a given sound file.
### Arguments

- *string* **name** - Path to the sound file.
- *int* **stream** - Positive value to create a streaming source, **0** to create a static source. If the flag is set, the sample will not be fully loaded into memory. Instead, its successive parts will be read one by one into a memory buffer.

## void Play ( )

Starts playing the sample.
## void Stop ( )

Stops playback. This function saves the playback position so that playing of the file can be resumed from the same point.
> **Notice:** The playback won't stop immediately, as the sound thread is updated at 30 FPS. So, when you need to perform operations that require stopping of the playback (for example, updating the time, from which the sample should be played), you need to [force update](../../../api/library/engine/class.sound_cs.md#renderWorld_int_void) the sound thread after stopping the playback.
