# Unigine::AmbientSource Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is used to create a non-directional ambient background sound.


### Creating an Ambient Sound Source


To create an ambient sound source, create an instance of the AmbientSource class and specify all required settings:


> **Notice:** For an ambient source to be played, a [player](../../../api/library/players/index.md) is always required. In case an ambient source needs to be played when neither a world, nor the editor are loaded, a player, as well as the sound source (see code below), should be created in the system script `unigine.usc`; otherwise, no sound will be heard.


```cpp
// create a player so that an ambient sound source is played
PlayerSpectator player = new PlayerSpectator();
player.setPosition(Vec3(0.0f, -3.401f, 1.5f));
player.setViewDirection(vec3(0.0f, 1.0f, -0.4f));
engine.game.setPlayer(player);

// create the ambient sound source
AmbientSource sound = new AmbientSource("sound.mp3");
// set necessary sound settings
sound.setGain(0.5f);
sound.setPitch(1.0f);
sound.setLoop(1);
sound.play();

```


### Updating an Existing Ambient Sound Source


To update the settings of the ambient sound source, you can simply call the corresponding methods:


```cpp
// change the sample file of the playing sound source
if ((sound.isPlaying()) && (engine.app.clearKeyState('c')))
{
	// increase the pitch
	sound.setPitch(2.0f);
	// reduce the gain
	sound.setGain(0.2f);
}

```


As sound has its own thread that updates at 30 FPS, changes won't be applied immediately. However, you can force updating by using the *[renderWorld()](../../../api/library/engine/class.sound_usc.md#renderWorld_int_void)* method.


Sound events like *[play()](#play_void)* or *[stop()](#stop_void)* aren't updated immediately as well. So, when you need to perform operations that require stopping of the playback (for example, updating the time from which the sample should be played, or the sample name), you need to force update the sound thread after stopping the playback:


```cpp
// check if the sound sample is playing
if (sound.isPlaying())
{
	// stop playing the sample
	sound.stop();
	// force updating of the sound thread
	engine.sound.renderWorld(1);
	// update time
	sound.setTime(0.0f);
	// play the sample
	sound.play();
}

```


### See Also


- *[Controlling Sound Sources Globally](../../../code/usage/controlling_sound_sources_globally/index.md)* article to learn how to toggle all sounds at the same time
- C# Component sample
- [Sound](../../../sdk/api_samples/cs/sounds.md) samples in *C# Component Samples* suite
- UnigineScript samples:

  -
  -
  -
  -


## AmbientSource Class

### Members

## int isStopped () const

Returns the current value indicating if playback is stopped.
### Return value

Current the sample is stopped
## int isPlaying () const

Returns the current value indicating if the sample is being played.
### Return value

Current the sample is being played
## void setTime ( float time )

Sets a new time from the beginning of the sample. You can't set time if the sample is already playing: [stop](#stop_void) the playback, set the time, and [resume](#play_void) the playback.
### Arguments

- *float* **time** - The time from the beginning of the sample, in seconds.

## float getTime () const

Returns the current time from the beginning of the sample. You can't set time if the sample is already playing: [stop](#stop_void) the playback, set the time, and [resume](#play_void) the playback.
### Return value

Current time from the beginning of the sample, in seconds.
## void setSourceMask ( int mask )

Sets a new bit mask that determines to what [sound channels](../../../api/library/engine/class.sound_usc.md#setSourceVolume_int_float_void) the source belongs to. For a sound source to be heard, its mask should match the [player's sound mask](../../../api/library/players/class.player_usc.md#setSourceMask_int_void) in one bit at least.
### Arguments

- *int* **mask** - The integer each bit of which specifies a sound channel.

## int getSourceMask () const

Returns the current bit mask that determines to what [sound channels](../../../api/library/engine/class.sound_usc.md#setSourceVolume_int_float_void) the source belongs to. For a sound source to be heard, its mask should match the [player's sound mask](../../../api/library/players/class.player_usc.md#setSourceMask_int_void) in one bit at least.
### Return value

Current integer each bit of which specifies a sound channel.
## void setSampleName ( string name )

Sets a new
### Arguments

- *string* **name** - The path to the sound file.

## const char * getSampleName () const

Returns the current
### Return value

Current path to the sound file.
## void setPitch ( float pitch )

Sets a new sound pitch.
### Arguments

- *float* **pitch** - The factor by which the current pitch will be multiplied.

## float getPitch () const

Returns the current sound pitch.
### Return value

Current factor by which the current pitch will be multiplied.
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

Sets a new volume of the sound.
### Arguments

- *float* **gain** - The volume in range [0, 1] where **0** means muted, **1** means maximum volume.

## float getGain () const

Returns the current volume of the sound.
### Return value

Current volume in range [0, 1] where **0** means muted, **1** means maximum volume.
## void setPitchShift ( float shift )

Sets a new pitch shift of the played sample in semitones, clamped to the [-12; 12] range (one octave down to one octave up), with the default of 0 (no shift). Unlike the **[getPitch()()](../../...md#getPitch_float)** property, it changes the tone without changing the playback speed. The effect requires pitch-shifter support in the sound device; otherwise the value has no audible effect.
### Arguments

- *float* **shift** - The pitch shift of the played sample, in semitones

## float getPitchShift () const

Returns the current pitch shift of the played sample in semitones, clamped to the [-12; 12] range (one octave down to one octave up), with the default of 0 (no shift). Unlike the **[getPitch()()](../../...md#getPitch_float)** property, it changes the tone without changing the playback speed. The effect requires pitch-shifter support in the sound device; otherwise the value has no audible effect.
### Return value

Current pitch shift of the played sample, in semitones
---

## static AmbientSource ( string name , int stream = 0 )

Constructor. Creates a new ambient sound source using a given sound file.
### Arguments

- *string* **name** - Path to the sound file.
- *int* **stream** - Positive value to create a streaming source, **0** to create a static source. If the flag is set, the sample will not be fully loaded into memory. Instead, its successive parts will be read one by one into a memory buffer.

## void play ( )

Starts playing the sample.
## void stop ( )

Stops playback. This function saves the playback position so that playing of the file can be resumed from the same point.
> **Notice:** The playback won't stop immediately, as the sound thread is updated at 30 FPS. So, when you need to perform operations that require stopping of the playback (for example, updating the time, from which the sample should be played), you need to [force update](../../../api/library/engine/class.sound_usc.md#renderWorld_int_void) the sound thread after stopping the playback.
