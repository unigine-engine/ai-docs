# Unigine::SoundReverb Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Node


This class is used to create [reverberation zones](../../../objects/sounds/sound_reverb.md) for [sound sources](../../../api/library/sounds/class.soundsource_usc.md) with [reverberation flag](../../../api/library/sounds/class.soundsource_usc.md#setReverbMask_int_void). Such sound will have initial [reflections](../../../objects/sounds/sound_reverb.md#reflections), [reverberation](../../../objects/sounds/sound_reverb.md#reverb) and [echo](../../../objects/sounds/sound_reverb.md#echo). It can have [modified pitch](../../../objects/sounds/sound_reverb.md#pitch).


If the sound passes through two reverberation zones (for example, one reverberation zone around the player and another one around the sound source), the heard sound reverberation effect will be twice as strong.


### Creating a Reverberation Zone


To create a reverberation zone, first, create a [sound source](../../../api/library/sounds/class.soundsource_usc.md#create) that will reverberate, then create an instance of the SoundReverb class and specify all required settings:


```cpp
// create a sound source
SoundSource sound = new SoundSource("static_mono_00.oga");
sound.setWorldTransform(translate(Vec3(10.0f)));
// disable sound muffling when being occluded
sound.setOcclusion(0);
// set the distance at which the sound gets clear
sound.setMinDistance(1.0f);
// set the distance at which the sound becomes out of audible range
sound.setMaxDistance(10.0f);
// set the gain that result in attenuation of 6 dB
sound.setGain(0.5f);
// loop the sound
sound.setLoop(1);
// start playing the sound sample
sound.play();

// create a reverberation zone
SoundReverb reverb = new SoundReverb(vec3(10.0f));
// set transformation
reverb.setWorldTransform(translate(Vec3(10.0f)));
// set the threshold size that determines the distance of changing from partial to full reverberation audibility
reverb.setThreshold(vec3(1.0f, 1.0f, 1.0f));
// set the other settings for the reverberation zone
reverb.setDensity(0.2f);
reverb.setDiffusion(0.5f);
reverb.setDecayTime(1.0f);
reverb.setReflectionGain(2.0f);
reverb.setLateReverbGain(8.0f);

```


To update the settings of the created reverberation zone, you can simply call the corresponding methods when necessary.


### See Also


- C# Component sample
- UnigineScript samples:

  -
  -


## SoundReverb Class

### Members

## void setThreshold ( vec3 threshold )

Sets a new threshold size values along the coordinates axes relative to the [reverberation zone size](#getSize_vec3). It determines the distance of changing from partial to full reverberation audibility.
### Arguments

- *vec3* **threshold** - The threshold size in units.

## vec3 getThreshold () const

Returns the current threshold size values along the coordinates axes relative to the [reverberation zone size](#getSize_vec3). It determines the distance of changing from partial to full reverberation audibility.
### Return value

Current threshold size in units.
## void setSize ( vec3 size )

Sets a new size of the reverberation zone.
### Arguments

- *vec3* **size** - The size of the reverberation zone in units.

## vec3 getSize () const

Returns the current size of the reverberation zone.
### Return value

Current size of the reverberation zone in units.
## void setReflectionGain ( float gain )

Sets a new gain controlling the amount of initial reflections relative to the general [reverberation gain](#getGain_float). If set to **0.0**, the sound has no initial reflections at all.
### Arguments

- *float* **gain** - The initial reflections gain value in range **[0.0;3.1]**.

## float getReflectionGain () const

Returns the current gain controlling the amount of initial reflections relative to the general [reverberation gain](#getGain_float). If set to **0.0**, the sound has no initial reflections at all.
### Return value

Current initial reflections gain value in range **[0.0;3.1]**.
## void setReflectionDelay ( float delay )

Sets a new initial reflection delay determining the begin time of the first reflection from the source relative to the arrival time of the original sound.
### Arguments

- *float* **delay** - The initial reflection delay in range **[0.0;0.3]**, in seconds.

## float getReflectionDelay () const

Returns the current initial reflection delay determining the begin time of the first reflection from the source relative to the arrival time of the original sound.
### Return value

Current initial reflection delay in range **[0.0;0.3]**, in seconds.
## void setModulationTime ( float time )

Sets a new time for repeating the pitch modulation in the reverberation sound.
### Arguments

- *float* **time** - The modulation repeating time in range **[0.0;1.0]**, in seconds.

## float getModulationTime () const

Returns the current time for repeating the pitch modulation in the reverberation sound.
### Return value

Current modulation repeating time in range **[0.0;1.0]**, in seconds.
## void setModulationDepth ( float depth )

Sets a new modulation depth determining the amount of pitch change.
### Arguments

- *float* **depth** - The modulation depth value in range **[0.0;1.0]**.

## float getModulationDepth () const

Returns the current modulation depth determining the amount of pitch change.
### Return value

Current modulation depth value in range **[0.0;1.0]**.
## void setLateReverbGain ( float gain )

Sets a new gain controlling the amount of later reverberation relative to the general [reverberation gain](#getGain_float). If set to **0.0**, the sound has no late reverberation at all.
### Arguments

- *float* **gain** - The late reverberation gain value in range **[0.0;10.0]**.

## float getLateReverbGain () const

Returns the current gain controlling the amount of later reverberation relative to the general [reverberation gain](#getGain_float). If set to **0.0**, the sound has no late reverberation at all.
### Return value

Current late reverberation gain value in range **[0.0;10.0]**.
## void setLateReverbDelay ( float delay )

Sets a new late reverberation delay determining the begin time of the late reverberation relative to the time of the initial reflection (the first of the early reflections).
### Arguments

- *float* **delay** - The late reverberation delay in range **[0.0;0.1]** seconds.

## float getLateReverbDelay () const

Returns the current late reverberation delay determining the begin time of the late reverberation relative to the time of the initial reflection (the first of the early reflections).
### Return value

Current late reverberation delay in range **[0.0;0.1]** seconds.
## void setGainLF ( float lf )

Sets a new gain filter value for attenuating the reverberation sound at low frequencies. If set to **1.0**, no filter is applied.
### Arguments

- *float* **lf** - The low frequencies gain value in range **[0.0;1.0]**.

## float getGainLF () const

Returns the current gain filter value for attenuating the reverberation sound at low frequencies. If set to **1.0**, no filter is applied.
### Return value

Current low frequencies gain value in range **[0.0;1.0]**.
## void setGainHF ( float hf )

Sets a new gain filter value for attenuating the reverberation sound at high frequencies. If set to **1.0**, no filter is applied.
### Arguments

- *float* **hf** - The high frequencies gain value in range **[0.0;1.0]**.

## float getGainHF () const

Returns the current gain filter value for attenuating the reverberation sound at high frequencies. If set to **1.0**, no filter is applied.
### Return value

Current high frequencies gain value in range **[0.0;1.0]**.
## void setGain ( float gain )

Sets a new gain controlling the overall amount of the initial reflections and later reverberations. If set to **0.0**, the reverberation sound is muted.
### Arguments

- *float* **gain** - The gain value in range **[0.0;1.0]**.

## float getGain () const

Returns the current gain controlling the overall amount of the initial reflections and later reverberations. If set to **0.0**, the reverberation sound is muted.
### Return value

Current gain value in range **[0.0;1.0]**.
## void setEchoTime ( float time )

Sets a new time period for cyclic echo to repeat itself along the reverberation decay.
### Arguments

- *float* **time** - The echo repeating time in range **[0.075,0.25]** seconds.

## float getEchoTime () const

Returns the current time period for cyclic echo to repeat itself along the reverberation decay.
### Return value

Current echo repeating time in range **[0.075,0.25]** seconds.
## void setEchoDepth ( float depth )

Sets a new depth value determining how long the cyclic echo persists along the reverberation decay.
### Arguments

- *float* **depth** - The echo depth value in range **[0.0;1.0]**.

## float getEchoDepth () const

Returns the current depth value determining how long the cyclic echo persists along the reverberation decay.
### Return value

Current echo depth value in range **[0.0;1.0]**.
## void setDiffusion ( float diffusion )

Sets a new diffusion determining the rate at which the reverberation resonances increase in density after the original sound.
### Arguments

- *float* **diffusion** - The diffusion value in range **[0.0;1.0]**.

## float getDiffusion () const

Returns the current diffusion determining the rate at which the reverberation resonances increase in density after the original sound.
### Return value

Current diffusion value in range **[0.0;1.0]**.
## void setDensity ( float density )

Sets a new density of the resonances making up the reverberation sound.
### Arguments

- *float* **density** - The density value in range **[0.0;1.0]**.

## float getDensity () const

Returns the current density of the resonances making up the reverberation sound.
### Return value

Current density value in range **[0.0;1.0]**.
## void setDecayTime ( float time )

Sets a new reverberation decay time.
### Arguments

- *float* **time** - The decay time in range **[0.1;20.0]** seconds.

## float getDecayTime () const

Returns the current reverberation decay time.
### Return value

Current decay time in range **[0.1;20.0]** seconds.
## void setDecayLFRatio ( float lfratio )

Sets a new ratio of low-frequency decay time relative to the time set by general reverberation [decay time](#getDecayTime_float). The value **1.0** is neutral.
### Arguments

- *float* **lfratio** - The low-frequency decay ratio in range **[0.1;2.0]**.

## float getDecayLFRatio () const

Returns the current ratio of low-frequency decay time relative to the time set by general reverberation [decay time](#getDecayTime_float). The value **1.0** is neutral.
### Return value

Current low-frequency decay ratio in range **[0.1;2.0]**.
## void setDecayHFRatio ( float hfratio )

Sets a new ratio of high-frequency decay time relative to the time set by general reverberation [decay time](#getDecayTime_float). The value **1.0** is neutral.
### Arguments

- *float* **hfratio** - The high-frequency decay ratio in range **[0.1;2.0]**.

## float getDecayHFRatio () const

Returns the current ratio of high-frequency decay time relative to the time set by general reverberation [decay time](#getDecayTime_float). The value **1.0** is neutral.
### Return value

Current high-frequency decay ratio in range **[0.1;2.0]**.
## void setAirAbsorption ( float absorption )

Sets a new air absorption value determining the distance-dependent attenuation at high frequencies caused by the propagation medium.
### Arguments

- *float* **absorption** - The air absorption value in range **[0.892;1.0]**. The value of **0.994** per unit represents normal atmospheric humidity and temperature.

## float getAirAbsorption () const

Returns the current air absorption value determining the distance-dependent attenuation at high frequencies caused by the propagation medium.
### Return value

Current air absorption value in range **[0.892;1.0]**. The value of **0.994** per unit represents normal atmospheric humidity and temperature.
## void setRoomRolloff ( float rolloff )

Sets a new scaling room rolloff factor determining attenuation of the reflected sound (containing both reflections and reverberation) over distance.
### Arguments

- *float* **rolloff** - The room rolloff factor in range **[0.0;10.0]**.

## float getRoomRolloff () const

Returns the current scaling room rolloff factor determining attenuation of the reflected sound (containing both reflections and reverberation) over distance.
### Return value

Current room rolloff factor in range **[0.0;10.0]**.
## void setReverbMask ( int mask )

Sets a new bit mask that determines what [reverberation zones](../../../api/library/sounds/class.soundreverb_usc.md) can be heard. For sound to reverberate, at least one bit of this mask should match with the [player's reverberation mask](../../../api/library/players/class.player_usc.md#setReverbMask_int_void). At the same time, [reverb mask of the sound source](../../../api/library/sounds/class.soundsource_usc.md#setReverbMask_int_void) should also match with the player's one (but not necessarily in the same bit as this mask matches it).
### Arguments

- *int* **mask** - The integer each bit of which is a mask for reverberating sound sources and reverberation zones.

## int getReverbMask () const

Returns the current bit mask that determines what [reverberation zones](../../../api/library/sounds/class.soundreverb_usc.md) can be heard. For sound to reverberate, at least one bit of this mask should match with the [player's reverberation mask](../../../api/library/players/class.player_usc.md#setReverbMask_int_void). At the same time, [reverb mask of the sound source](../../../api/library/sounds/class.soundsource_usc.md#setReverbMask_int_void) should also match with the player's one (but not necessarily in the same bit as this mask matches it).
### Return value

Current integer each bit of which is a mask for reverberating sound sources and reverberation zones.
---

## static SoundReverb ( vec3 size )

Constructor. Creates a new reverberation zone of specified size.
### Arguments

- *vec3* **size** - Size of the reverberation zone in units.

## static int type ( )

Returns the type of the node.
### Return value

[Sound](../../../api/library/engine/class.sound_usc.md) type identifier.
