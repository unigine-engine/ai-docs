# Unigine::SoundReverb Class (CS)

**Inherits from:** Node


This class is used to create [reverberation zones](../../../objects/sounds/sound_reverb.md) for [sound sources](../../../api/library/sounds/class.soundsource_cs.md) with [reverberation flag](../../../api/library/sounds/class.soundsource_cs.md#setReverbMask_int_void). Such sound will have initial [reflections](../../../objects/sounds/sound_reverb.md#reflections), [reverberation](../../../objects/sounds/sound_reverb.md#reverb) and [echo](../../../objects/sounds/sound_reverb.md#echo). It can have [modified pitch](../../../objects/sounds/sound_reverb.md#pitch).


If the sound passes through two reverberation zones (for example, one reverberation zone around the player and another one around the sound source), the heard sound reverberation effect will be twice as strong.


### Creating a Reverberation Zone


To create a reverberation zone, first, create a [sound source](../../../api/library/sounds/class.soundsource_cs.md#create) that will reverberate, then create an instance of the SoundReverb class and specify all required settings:


```csharp
// create a sound source
SoundSource sound = new SoundSource("static_mono_00.oga");
sound.WorldTransform = MathLib.Translate(new Vec3(10.0f));
// disable sound muffling when being occluded
sound.Occlusion = 0;
// set the distance at which the sound gets clear
sound.MinDistance = 1.0f;
// set the distance at which the sound becomes out of audible range
sound.MaxDistance =10.0f;
// set the gain that result in attenuation of 6 dB
sound.Gain = 0.5f;
// loop the sound
sound.Loop = 1;
// start playing the sound sample
sound.Play();

// create a reverberation zone
SoundReverb reverb = new SoundReverb(new vec3(10.0f));
// set transformation
reverb.WorldTransform = MathLib.Translate(new Vec3(10.0f));
// set the threshold size that determines the distance of changing from partial to full reverberation audibility
reverb.Threshold = (new vec3(1.0f, 1.0f, 1.0f));
// set the other settings for the reverberation zone
reverb.Density = 0.2f;
reverb.Diffusion = 0.5f;
reverb.DecayTime = 1.0f;
reverb.ReflectionGain = 2.0f;
reverb.LateReverbGain = 8.0f;


```


To update the settings of the created reverberation zone, you can simply call the corresponding methods when necessary.


### See Also


- C# Component sample
- UnigineScript samples:

  -
  -


## SoundReverb Class

### Properties

## vec3 Threshold

The threshold size values along the coordinates axes relative to the [reverberation zone size](#getSize_vec3). It determines the distance of changing from partial to full reverberation audibility.
## vec3 Size

The size of the reverberation zone.
## float ReflectionGain

The gain controlling the amount of initial reflections relative to the general [reverberation gain](#getGain_float). If set to **0.0**, the sound has no initial reflections at all.
## float ReflectionDelay

The initial reflection delay determining the begin time of the first reflection from the source relative to the arrival time of the original sound.
## float ModulationTime

The time for repeating the pitch modulation in the reverberation sound.
## float ModulationDepth

The modulation depth determining the amount of pitch change.
## float LateReverbGain

The gain controlling the amount of later reverberation relative to the general [reverberation gain](#getGain_float). If set to **0.0**, the sound has no late reverberation at all.
## float LateReverbDelay

The late reverberation delay determining the begin time of the late reverberation relative to the time of the initial reflection (the first of the early reflections).
## float GainLF

The gain filter value for attenuating the reverberation sound at low frequencies. If set to **1.0**, no filter is applied.
## float GainHF

The gain filter value for attenuating the reverberation sound at high frequencies. If set to **1.0**, no filter is applied.
## float Gain

The gain controlling the overall amount of the initial reflections and later reverberations. If set to **0.0**, the reverberation sound is muted.
## float EchoTime

The time period for cyclic echo to repeat itself along the reverberation decay.
## float EchoDepth

The depth value determining how long the cyclic echo persists along the reverberation decay.
## float Diffusion

The diffusion determining the rate at which the reverberation resonances increase in density after the original sound.
## float Density

The density of the resonances making up the reverberation sound.
## float DecayTime

The reverberation decay time.
## float DecayLFRatio

The ratio of low-frequency decay time relative to the time set by general reverberation [decay time](#getDecayTime_float). The value **1.0** is neutral.
## float DecayHFRatio

The ratio of high-frequency decay time relative to the time set by general reverberation [decay time](#getDecayTime_float). The value **1.0** is neutral.
## float AirAbsorption

The air absorption value determining the distance-dependent attenuation at high frequencies caused by the propagation medium.
## float RoomRolloff

The scaling room rolloff factor determining attenuation of the reflected sound (containing both reflections and reverberation) over distance.
## int ReverbMask

The bit mask that determines what [reverberation zones](../../../api/library/sounds/class.soundreverb_cs.md) can be heard. For sound to reverberate, at least one bit of this mask should match with the [player's reverberation mask](../../../api/library/players/class.player_cs.md#setReverbMask_int_void). At the same time, [reverb mask of the sound source](../../../api/library/sounds/class.soundsource_cs.md#setReverbMask_int_void) should also match with the player's one (but not necessarily in the same bit as this mask matches it).
### Members

---

## SoundReverb ( vec3 size )

Constructor. Creates a new reverberation zone of specified size.
### Arguments

- *vec3* **size** - Size of the reverberation zone in units.

## static int type ( )

Returns the type of the node.
### Return value

[Sound](../../../api/library/engine/class.sound_cs.md) type identifier.
