# Unigine::Sound Class (CS)

> **Notice:** This class is a singleton.


Controls the general sound settings, such as volume, speed of sound, the Doppler factor, sound adaptation and sound mixer channels. Settings can be loaded from a `*.sound` file or changed by the corresponding functions below.


In the `*.sound` file, the sound settings are stored in the *<sound>* section, for example:


```xml
<?xml version="1.0" encoding="utf-8"?>
<settings version="2.16.0.2">
	<sound>
		<enabled>1</enabled>
		<sound_manager_load_samples>0</sound_manager_load_samples>
		<sound_manager_sample_static_memory>64</sound_manager_sample_static_memory>
		<sound_manager_sample_stream_memory>16</sound_manager_sample_stream_memory>
		<sound_reverb>2</sound_reverb>
		<sound_occlusion>1</sound_occlusion>
		<al_sound_skip_errors>0</al_sound_skip_errors>
		<scale>1</scale>
		<volume>1</volume>
		<doppler>1</doppler>
		<velocity>343.299988</velocity>
		<adaptation>1</adaptation>
		<attenuation>3</attenuation>
		<hrtf>0</hrtf>
		<source source="0" limit="2"/>
		<source source="1" limit="4"/>
		<source source="2" limit="4"/>
		<source source="4" volume="0.4"/>
	</sound>
</settings>

```


### Usage Example


The following example shows how to load sound settings from the `*.world` file, change them and then save back to the sound settings file. Settings are loaded at startup. While the sound source (*[AmbientSource](../../../api/library/sounds/class.ambientsource_cs.md)*) is playing, you can use keyboard to change sound volume, toggle sounds on and off, and display current velocity. On shutdown the current sound settings are saved.


`AppWorldLogic.cs`


```csharp
AmbientSource source;

private void Init()
{
	 // load sound settings from a file
	Sound.LoadSettings("sound_settings.sound");

	// create a sound source that plays a sample
	source = new AmbientSource("ambient_source.oga",1);
	source.Loop = 1;
	source.Play();
}

private void Update()
{
	// enable/disable sounds in the scene
	if (Input.IsKeyPressed(Input.KEY.Z)) {

		Sound.Enabled = !Sound.Enabled;
		Log.Message("The enabled flag is {0}\n", Sound.Enabled);
	}

	// print the current speed of sound
	if (Input.IsKeyPressed(Input.KEY.C)) {
		Log.Message("Sound velocity: {0}\n", Sound.Velocity);
	}

	// make the sound louder
	if (Input.IsKeyPressed(Input.KEY.N)) {
		if (Sound.Volume != 1.0f) Sound.Volume += 0.1f;
		Log.Message("The sound is louder {0}\n", Sound.Volume);
	}

	// make the sound lower
	if (Input.IsKeyPressed(Input.KEY.M)) {
		if (Sound.Volume > 0.0f) Sound.Volume -= 0.1f;
		Log.Message("The sound is quieter {0}\n", Sound.Volume);
	}

}

private void Shutdown()
{
	// save the sound settings into the file
	Sound.SaveSettings("sound_settings.sound",1);
}


```


## Sound Class

### Properties

## bool SourceOcclusion

The value indicating if occlusion for sounds is enabled. When enabled, the sound will be occluded when there are other nodes between the listener and the sound source.
## int SourceReverbMode

The sound reverberation mode. One of the [REVERB_*](#REVERB_DISABLED) values. The default value is [REVERB_MULTIPLE](#REVERB_MULTIPLE).
## bool HRTF

The value indicating if the binaural HRTF (head related transfer function) sound is enabled. HRTF provides imitation of the surround sound for the stereo wired headset.
## int Attenuation

The sound attenuation mode. Attenuation is the ability of a sound to lower in volume as the player moves away from it. One of the [ATTENUATION_*](#ATTENUATION_EXPONENT) values. The default value is [ATTENUATION_LINEAR_CLAMPED](#ATTENUATION_LINEAR_CLAMPED).
## float Scale

The time scale for the sound playing. The provided value is clamped in the range **[0; 2]**.
## float Doppler

The Doppler factor. This parameter allows you to exaggerate or tone-down the Doppler shift effect. The default value is 1.0f.
## float Adaptation

The time set for sound adaptation, that is used when the sound source becomes occluded or other way round.
## float Velocity

The velocity value the Doppler shift calculation is based upon. By default, it is set to 343.3f. If you have players moving really fast, then you may want to adjust this to prevent the Doppler shift from distorting the sound too much.
## float Volume

The sound volume. 0 means the muted sound, 1 means the maximum volume. The default value is 1.0f.
## 🔒︎ float TotalTime

The total time of asynchronous loading sounds.
## string Data

The user string data associated with the world. This string is written directly into the data tag of the `*.world` file, into the *data* child tag of the *sound* tag, for example:
```xml
<world version="2.16.0.2">

	<sound>
		<data>User data</data>
	</sound>

</world>


```


## bool Enabled

The value indicating if sounds in the scene are enabled.
### Members

---

## void SetSourceLimit ( int source , int limit )

Limits the number of simultaneously played sound sources per one mixer channel. This setting is also available in the Editor global [sound settings](../../../editor2/settings/sound_global/index.md#volume_channels).
### Arguments

- *int* **source** - Number of the mixer [channel](../../../principles/bit_masking/index.md#source_mask) (from **0** to **31**).
- *int* **limit** - The maximum number of sound sources that can be played simultaneously.

## int GetSourceLimit ( int source )

Returns the current number of simultaneously played sound sources per one mixer channel.
### Arguments

- *int* **source** - Number of the mixer channel (from **0** to **31**).

### Return value

The maximum number of sound sources that can be played simultaneously.
## void SetSourceVolume ( int source , float volume )

Sets the volume of the specified mixer channel.
### Arguments

- *int* **source** - Number of the mixer channel (from **0** to **31**).
- *float* **volume** - Channel volume. The provided value is clamped within [0;1] range, where 0 means muted sound and 1 is the maximum volume.

## float GetSourceVolume ( int source )

Returns the current volume of the specified mixer channel.
### Arguments

- *int* **source** - Number of the mixer channel (from **0** to **31**).

### Return value

Volume of the specified mixer channel. The returning value is in range [0;1], where 0 means muted sound and 1 is the maximum volume.
## bool LoadSettings ( string name , bool clear = false )

Loads the sound settings from the given file.
### Arguments

- *string* **name** - Path to a sound settings file (`*.sound`).
- *bool* **clear** - Clear flag. Set true to clear settings before loading (new settings shall be applied right after loading them), or false not to clear.

### Return value

true if the sound settings are loaded successfully; otherwise, false.
## bool LoadWorld ( Xml xml )

Loads a sound state from the Xml. The sound state includes such settings as the volume, velocity, adaptation, Doppler factor, time scale and number of sound sources and their volumes.
### Arguments

- *[Xml](../../../api/library/common/class.xml_cs.md)* **xml** - Xml node.

### Return value

true if the sound state is loaded successfully; otherwise, false.
## void RenderWorld ( int force )

Forces update of the sound system: all sound changes (such as *[play()](../../../api/library/sounds/class.ambientsource_cs.md#play_void)* or *[stop()](../../../api/library/sounds/class.ambientsource_cs.md#stop_void)* events and change of parameters) will be applied at once. The sound thread is updated at 30 FPS. Imagine, you have a [sound sample](../../../api/library/sounds/class.ambientsource_cs.md) playing and you want to update the time, from which the sample should be played. But playback won't stop immediately, so the a new time value won't be set. You need force updating of the sound thread after stopping it:


```csharp
AmbientSource sound = new AmbientSource("ambient_sample.oga");
// ...
// check if the sound sample is playing
if (sound.IsPlaying)
{
	// stop playing the sample
	sound.Stop();
	// force updating of the sound thread
	Sound.RenderWorld(1);
	// update time
	sound.Time = 45.0f;
	// continue playing the sample
	sound.Play();
}


```


### Arguments

- *int* **force** - true to force update of the sound system; otherwise, false.

## bool SaveSettings ( string name , int force = 0 )

Saves the current sound settings to the given file.
### Arguments

- *string* **name** - Path to a sound settings file (`*.sound`).
- *int* **force** - Force flag indcating if forced saving of sound settings is enabled.

### Return value

true if the sound settings are saved successfully; otherwise, false.
## bool SaveState ( Stream stream )

Saves a sound state into the stream. The sound state includes such settings as the volume, velocity, adaptation, Doppler factor, time scale and number of sound sources and their volumes.


**Example** using saveState() and [restoreState()](#restoreState_Stream_int) methods:


```csharp
// create a sound source that plays a sample and set its state
source = new AmbientSource("ambient_source.oga",1);
Sound.Scale = 0.75f;

// save state
Blob blob_state = new Blob();
Sound.SaveState(blob_state);

// change the node state
Sound.Scale = 1.25f;

// restore state
blob_state.SeekSet(0);	// returning the carriage to the start of the blob
Sound.RestoreState(blob_state);


```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream to save the state into.

### Return value

true if the sound state is saved successfully; otherwise, false.
## bool RestoreState ( Stream stream )

Restores a sound state from the stream. The sound state includes such settings as the volume, velocity, adaptation, Doppler factor, time scale and number of sound sources and their volumes.


**Example** using [saveState()](#saveState_Stream_int) and restoreState() methods:


```csharp
// create a sound source that plays a sample and set its state
source = new AmbientSource("ambient_source.oga",1);
Sound.Scale = 0.75f;

// save state
Blob blob_state = new Blob();
Sound.SaveState(blob_state);

// change the node state
Sound.Scale = 1.25f;

// restore state
blob_state.SeekSet(0);	// returning the carriage to the start of the blob
Sound.RestoreState(blob_state);


```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream to restore the state from.

### Return value

true if the sound state is restored successfully; otherwise, false.
## bool SaveWorld ( Xml xml , int force = 0 )

Saves a sound state into the given Xml node. The sound state includes such settings as the volume, velocity, adaptation, Doppler factor, time scale and number of sound sources and their volumes.
### Arguments

- *[Xml](../../../api/library/common/class.xml_cs.md)* **xml** - Xml node.
- *int* **force** - Force flag indicating if forced saving of the sound state is enabled.

### Return value

true if the sound state is saved successfully; otherwise, false.
