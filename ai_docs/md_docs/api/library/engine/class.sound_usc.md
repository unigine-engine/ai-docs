# Unigine::Sound Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

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


The following example shows how to load sound settings from the `*.world` file, change them and then save back to the sound settings file. Settings are loaded at startup. While the sound source (*[AmbientSource](../../../api/library/sounds/class.ambientsource_usc.md)*) is playing, you can use keyboard to change sound volume, toggle sounds on and off, and display current velocity. On shutdown the current sound settings are saved.


```cpp
#include <core/unigine.h>

AmbientSource source;

int init() {

	// load sound settings from a file
	engine.sound.loadSettings("sound_settings.sound");

	// create a sound source that plays a sample
	source = new AmbientSource("ambient_source.oga",1);
	source.setLoop(1);
	source.play();

	return 1;
}

int update() {

	// enable/disable sounds in the scene
	if (engine.app.clearKeyState('z')) {
		engine.sound.setEnabled(!engine.sound.isEnabled());
		log.message("The enabled flag is %d\n", engine.sound.isEnabled());
	}

	// print the current speed of sound
	if (engine.app.clearKeyState('c')) {
		log.message("Sound velocity: %f\n", engine.sound.getVelocity());
	}

	// make the sound louder
	if (engine.app.clearKeyState('n')) {
		if (engine.sound.getVolume() != 1.0f) engine.sound.setVolume(engine.sound.getVolume() + 0.1f);
		log.message("The sound is louder %f\n", engine.sound.getVolume());
	}

	// make the sound quieter
	if (engine.app.getKeyState('m')) {
		if (engine.sound.getVolume() > 0.0f) engine.sound.setVolume(engine.sound.getVolume() - 0.1f);
		log.message("The sound is quieter %f\n", engine.sound.getVolume());
	}

	return 1;
}

int shutdown() {

	// save the sound settings into the file
	engine.sound.saveSettings("sound_settings.sound",1);
	source.clearPtr();

	return 1;
}

```


## Sound Class

### Members

## void setSourceOcclusion ( int occlusion )

Sets a new value indicating if occlusion for sounds is enabled. When enabled, the sound will be occluded when there are other nodes between the listener and the sound source.
### Arguments

- *int* **occlusion** - The occlusion for sounds is enabled

## int isSourceOcclusion () const

Returns the current value indicating if occlusion for sounds is enabled. When enabled, the sound will be occluded when there are other nodes between the listener and the sound source.
### Return value

Current occlusion for sounds is enabled
## void setSourceReverbMode ( int mode )

Sets a new sound reverberation mode. One of the [REVERB_*](#REVERB_DISABLED) values. The default value is [REVERB_MULTIPLE](#REVERB_MULTIPLE).
### Arguments

- *int* **mode** - The sound reverberation mode

## int getSourceReverbMode () const

Returns the current sound reverberation mode. One of the [REVERB_*](#REVERB_DISABLED) values. The default value is [REVERB_MULTIPLE](#REVERB_MULTIPLE).
### Return value

Current sound reverberation mode
## void setHRTF ( int hrtf )

Sets a new value indicating if the binaural HRTF (head related transfer function) sound is enabled. HRTF provides imitation of the surround sound for the stereo wired headset.
### Arguments

- *int* **hrtf** - The the binaural HRTF (head related transfer function) sound is enabled

## int isHRTF () const

Returns the current value indicating if the binaural HRTF (head related transfer function) sound is enabled. HRTF provides imitation of the surround sound for the stereo wired headset.
### Return value

Current the binaural HRTF (head related transfer function) sound is enabled
## void setAttenuation ( int attenuation )

Sets a new sound attenuation mode. Attenuation is the ability of a sound to lower in volume as the player moves away from it. One of the [ATTENUATION_*](#ATTENUATION_EXPONENT) values. The default value is [ATTENUATION_LINEAR_CLAMPED](#ATTENUATION_LINEAR_CLAMPED).
### Arguments

- *int* **attenuation** - The sound attenuation mode

## int getAttenuation () const

Returns the current sound attenuation mode. Attenuation is the ability of a sound to lower in volume as the player moves away from it. One of the [ATTENUATION_*](#ATTENUATION_EXPONENT) values. The default value is [ATTENUATION_LINEAR_CLAMPED](#ATTENUATION_LINEAR_CLAMPED).
### Return value

Current sound attenuation mode
## void setScale ( float scale )

Sets a new time scale for the sound playing. The provided value is clamped in the range **[0; 2]**.
### Arguments

- *float* **scale** - The time scale for the sound playing

## float getScale () const

Returns the current time scale for the sound playing. The provided value is clamped in the range **[0; 2]**.
### Return value

Current time scale for the sound playing
## void setDoppler ( float doppler )

Sets a new Doppler factor. This parameter allows you to exaggerate or tone-down the Doppler shift effect. The default value is 1.0f.
### Arguments

- *float* **doppler** - The Doppler factor

## float getDoppler () const

Returns the current Doppler factor. This parameter allows you to exaggerate or tone-down the Doppler shift effect. The default value is 1.0f.
### Return value

Current Doppler factor
## void setAdaptation ( float adaptation )

Sets a new time set for sound adaptation, that is used when the sound source becomes occluded or other way round.
### Arguments

- *float* **adaptation** - The time set for sound adaptation

## float getAdaptation () const

Returns the current time set for sound adaptation, that is used when the sound source becomes occluded or other way round.
### Return value

Current time set for sound adaptation
## void setVelocity ( float velocity )

Sets a new velocity value the Doppler shift calculation is based upon. By default, it is set to 343.3f. If you have players moving really fast, then you may want to adjust this to prevent the Doppler shift from distorting the sound too much.
### Arguments

- *float* **velocity** - The velocity value the Doppler shift calculation is based upon

## float getVelocity () const

Returns the current velocity value the Doppler shift calculation is based upon. By default, it is set to 343.3f. If you have players moving really fast, then you may want to adjust this to prevent the Doppler shift from distorting the sound too much.
### Return value

Current velocity value the Doppler shift calculation is based upon
## void setVolume ( float volume )

Sets a new sound volume. 0 means the muted sound, 1 means the maximum volume. The default value is 1.0f.
### Arguments

- *float* **volume** - The sound volume

## float getVolume () const

Returns the current sound volume. 0 means the muted sound, 1 means the maximum volume. The default value is 1.0f.
### Return value

Current sound volume
## float getTotalTime () const

Returns the current total time of asynchronous loading sounds.
### Return value

Current total time of asynchronous loading sounds
## void setData ( string data )

Sets a new user string data associated with the world. This string is written directly into the data tag of the `*.world` file, into the *data* child tag of the *sound* tag, for example:
```xml
<world version="2.16.0.2">

	<sound>
		<data>User data</data>
	</sound>

</world>


```


### Arguments

- *string* **data** - The user string data associated with the world

## const char * getData () const

Returns the current user string data associated with the world. This string is written directly into the data tag of the `*.world` file, into the *data* child tag of the *sound* tag, for example:
```xml
<world version="2.16.0.2">

	<sound>
		<data>User data</data>
	</sound>

</world>


```


### Return value

Current user string data associated with the world
## void setEnabled ( int enabled )

Sets a new value indicating if sounds in the scene are enabled.
### Arguments

- *int* **enabled** - The sounds in the scene are enabled

## int isEnabled () const

Returns the current value indicating if sounds in the scene are enabled.
### Return value

Current sounds in the scene are enabled
---

## void engine.sound. setSourceLimit ( int source , int limit )

Limits the number of simultaneously played sound sources per one mixer channel. This setting is also available in the Editor global [sound settings](../../../editor2/settings/sound_global/index.md#volume_channels).
### Arguments

- *int* **source** - Number of the mixer [channel](../../../principles/bit_masking/index.md#source_mask) (from **0** to **31**).
- *int* **limit** - The maximum number of sound sources that can be played simultaneously.

## int engine.sound. getSourceLimit ( int source )

Returns the current number of simultaneously played sound sources per one mixer channel.
### Arguments

- *int* **source** - Number of the mixer channel (from **0** to **31**).

### Return value

The maximum number of sound sources that can be played simultaneously.
## void engine.sound. setSourceVolume ( int source , float volume )

Sets the volume of the specified mixer channel.
### Arguments

- *int* **source** - Number of the mixer channel (from **0** to **31**).
- *float* **volume** - Channel volume. The provided value is clamped within [0;1] range, where 0 means muted sound and 1 is the maximum volume.

## float engine.sound. getSourceVolume ( int source )

Returns the current volume of the specified mixer channel.
### Arguments

- *int* **source** - Number of the mixer channel (from **0** to **31**).

### Return value

Volume of the specified mixer channel. The returning value is in range [0;1], where 0 means muted sound and 1 is the maximum volume.
## int engine.sound. loadSettings ( string name , int clear = false )

Loads the sound settings from the given file.
### Arguments

- *string* **name** - Path to a sound settings file (`*.sound`).
- *int* **clear** - Clear flag. Set **1** to clear settings before loading (new settings shall be applied right after loading them), or **0** not to clear.

### Return value

**1** if the sound settings are loaded successfully; otherwise, **0**.
## int engine.sound. loadWorld ( Xml xml )

Loads a sound state from the Xml. The sound state includes such settings as the volume, velocity, adaptation, Doppler factor, time scale and number of sound sources and their volumes.
### Arguments

- *[Xml](../../../api/library/common/class.xml_usc.md)* **xml** - Xml node.

### Return value

**1** if the sound state is loaded successfully; otherwise, **0**.
## void engine.sound. renderWorld ( int force )


Forces update of the sound system: all sound changes (such as *[play()](../../../api/library/sounds/class.ambientsource_usc.md#play_void)* or *[stop()](../../../api/library/sounds/class.ambientsource_usc.md#stop_void)* events and change of parameters) will be applied at once. The sound thread is updated at 30 FPS. Imagine, you have a [sound sample](../../../api/library/sounds/class.ambientsource_usc.md) playing and you want to update the time, from which the sample should be played. But playback won't stop immediately, so the a new time value won't be set. You need force updating of the sound thread after stopping it:


```cpp
AmbientSource sound = new AmbientSource("ambient_sample.oga");;
// ...
// check if the sound sample is playing
if(sound.isPlaying()) {
	// stop playing the sample
	sound.stop();
	// force updating of the sound thread
	engine.sound.renderWorld(1);
	// update time
	sound.setTime(45.0f);
	// continue playing the sample
	sound.play();
}

```


### Arguments

- *int* **force** - **1** to force update of the sound system; otherwise, **0**.

## int engine.sound. saveSettings ( string name , int force = 0 )

Saves the current sound settings to the given file.
### Arguments

- *string* **name** - Path to a sound settings file (`*.sound`).
- *int* **force** - Force flag indcating if forced saving of sound settings is enabled.

### Return value

**1** if the sound settings are saved successfully; otherwise, **0**.
## int engine.sound. saveState ( Stream stream )

Saves a sound state into the stream. The sound state includes such settings as the volume, velocity, adaptation, Doppler factor, time scale and number of sound sources and their volumes.


**Example** using saveState() and [restoreState()](#restoreState_Stream_int) methods:


```cpp
// create a sound source that plays a sample and set its state
source = new AmbientSource("ambient_source.oga",1);
source.setScale(0.75f);

// save state
Blob blob_state = new Blob();
source.saveState(blob_state);

// change state
source.setScale(1.25f);

// restore state
blob_state.seekSet(0); // returning the carriage to the start of the blob
source.restoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - Stream to save the state into.

### Return value

**1** if the sound state is saved successfully; otherwise, **0**.
## int engine.sound. restoreState ( Stream stream )

Restores a sound state from the stream. The sound state includes such settings as the volume, velocity, adaptation, Doppler factor, time scale and number of sound sources and their volumes.


**Example** using [saveState()](#saveState_Stream_int) and restoreState() methods:


```cpp
// create a sound source that plays a sample and set its state
source = new AmbientSource("ambient_source.oga",1);
source.setScale(0.75f);

// save state
Blob blob_state = new Blob();
source.saveState(blob_state);

// change state
source.setScale(1.25f);

// restore state
blob_state.seekSet(0); // returning the carriage to the start of the blob
source.restoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - Stream to restore the state from.

### Return value

**1** if the sound state is restored successfully; otherwise, **0**.
## int engine.sound. saveWorld ( Xml xml , int force = 0 )

Saves a sound state into the given Xml node. The sound state includes such settings as the volume, velocity, adaptation, Doppler factor, time scale and number of sound sources and their volumes.
### Arguments

- *[Xml](../../../api/library/common/class.xml_usc.md)* **xml** - Xml node.
- *int* **force** - Force flag indicating if forced saving of the sound state is enabled.

### Return value

**1** if the sound state is saved successfully; otherwise, **0**.
