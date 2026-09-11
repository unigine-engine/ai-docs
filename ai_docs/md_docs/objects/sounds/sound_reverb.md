# Sound Reverb


The famous koan goes: "Two hands clap and there is a sound; what is the sound of one hand?" The same way the sound and its reflections are physically interconnected and constitute the same sonic phenomenon for the listener. After the sound is emitted, there begins a long and multifarious interaction of the dispersing sound waves with the environment. Contribution of naturally emulated reflections cannot be diminished: they are necessary to give a sound a sense of place and reality, and fool the ear into believing in authenticity of the auditory experience.


[![Sound reverb](sound_reverb_sm.png)](sound_reverb.png)


The sound reverberation zone correctly reproduces the way the sound is reflected from surfaces, forming three main components:


- Early reflections
- Late reverberation
- Echo


Besides that, a number of parameters can be changed to alter the type of environment being simulated.


## Creating a Sound Reverberation Zone


To create a sound reverberation zone via UnigineEditor:


1. In the [Menu bar](../../editor2/interface/index.md#menu_bar), click *Create -> Sound -> Reverberation Zone*. ![](sound_reverb_create.png)
2. Place the sound reverberation zone somewhere in the world.


## Reverberation Zone Size


The reverberation zone represents a separate acoustic enclosure in the virtual world. It limits the perimeter in which reverberation will be added to the sound. Outside this zone, the sound emitted by sources will not undergo reverberation modification. If two zones overlap, their parameters are interpolated linearly for proper physical simulation of the mixed characteristics.


The size of the zone (in units) is set along three coordinates axes: X, Y, and Z.


### Threshold


For comfortable concentration on the displayed image, sound snapping is strongly undesirable. *Threshold* enables smooth sound transition when the listener moves from the outside area into the reverberation zone. Its values are set as an offset inside the zone along X, Y, and Z axes relative to the zone perimeter.


![Reverberation zone threshold](sound_reverb_threshold.png)


## Reflections


When a sound wave reaches an obstacle, a smaller part of it is absorbed by the material depending on its rigidity and density characteristics. But the most part bounces off and then reaches the listener's ears. It can also continue to the next obstacle to be bounced off for the second time. This sounds are called the first-order and second-order reflections. Though being perceived a split second later than the original sound, they are still interpreted by the brain as one integrated sound because of their similarity and closeness in time. The integrated sound not only seems to be louder, but it may take some tone coloration.


Even in complete darkness, the listener can orient basing on the sound environment cues. Of course, it is not possible to reproduce the exact location geometry, but the character of the reflections gives some indication of the immediate surroundings. For example, a strong and immediate primary reflection tells that the walls are close. The change in tonal coloration indicates the reflective quality of the wall � whether it is highly reflective or somewhat absorptive that mutes reflections.


### Reflection Gain


The overall amount of initial reflections can be adjusted independently from other reverberation parameters. Reflection Gain represents linear gain, corrected by the general reverberation sound *[Gain](#gain)* parameter, with the following values available:


- A maximum of 3.16 equals +10 dB for reflections.
- A minimum of 0 equals -100 dB and results in having no initial reflections at all.


### Reflection Delay


The amount of delay between the arrival time of the direct emitted sound to the first reflection from the source that helps to estimate subconsciously the location size. The corresponding *Reflection Delay* parameter ranges from 0 to 0.3 seconds.


- Reducing the value simulates close and small locations.
- Increasing the value means that reflective surfaces are located farther.


## Reverberation


With the first and secondary reflections, the path of the sound wave does not end. These reflections originate further reflections that in their turn induce more reflections, until totally losing specularity and becoming inaudible. All these reflections become merged into an overall sonic wash called reverberation. Reflections and reverberation tend to be perceived as one combined and very prolonged sound wave. The reverberation tail provides yet another environmental audio cue depending on its length and loudness. The more reflective the walls are and the larger the room, the longer the reverberation lasts. The more reflective the walls are and the smaller the room, the louder the reverberation is.


### Reverberation Decay Time


The decay time defining the character of the reverberation tail can also be tweaked independently for accurate acoustic simulation. It represents the interval between the onset of late reverberation and the time when its intensity has been reduced by 60 dB. The parameter has the following values:


- A minimum of 0.1 seconds is typically appropriate for the small rooms with dead surfaces.
- A maximum of 20.0 seconds is typically appropriate for a large room with very live surfaces.


#### Decay LF Ratio


To fine-tune the decay time of low frequencies, the *Decay LF Ratio* parameter can be used. It is the ratio of low-frequency decay time relative to the time set by *[Decay Time](#reverb_decay)*.


- For the decay time to be equal at all frequencies, neutral value 1.0 is used.
- Increasing the value above the neutral one results in having a longer decay time at low frequencies than at medium ones. Reverberation acquires the booming character with long low frequencies tail.
- Decreasing the value below 1.0 shortens the low frequencies decay time relative to the medium ones. The final reverberation sounds more tinny.


#### Decay HF Ratio


*Decay HF Ratio* also adjusts the spectral quality of the *Decay Time* parameter. It represents a linear multiplier value for the *[Decay Time](#reverb_decay)* parameter.


- For decay time to be equal at all frequencies, neutral value 1.0 is used.
- Increasing the value above the neutral one results in having a longer decay time at high frequencies than at mid ones. The reverberation is more brilliant with long high frequencies tail.
- Decreasing the value below 1.0 shortens the high frequencies decay time relative to the mid ones. The final reverberation sounds more naturally.


### Late Reverb Gain


To define the total intensity of the reverberation sound (the averaged square of its amplitude), adjusting the *Reverberation Decay* is not enough. *Late Reverb Gain* controls the overall amount of later reverberation relative to the general *[Gain](#gain)* parameter.


- A maximum of 10.0 equals +20 dB for the reverberation.
- A minimum of 0 equals -100 dB and results in having no reverberation at all.


### Late Reverb Delay


Besides the time of the sounding, the begin time of reverberation relative to the time of the initial reflection (the first of the early reflections) can be set. The Late reverb delay ranges from 0 to 0.1 seconds.


## Echo


If the reflector is located on the considerable distance from the sound source, it takes some time for the sound wave to reach the listener. Since perception of a sound usually endures in memory for only 0.1 second, there will be a small time delay between perception of the original sound and perception of the reflected sound. Such discrete perception of the reflected sound wave is called an echo. The following parameters allow the veridical imitation of this phenomenon:


### Echo Depth


The *Echo Depth* parameter modulates a cyclic echo in the reverberation decay, which is especially noticeable with transient or percussive sounds. It is a linear multiplier value that determines how long the echo will persist along the reverberation decay. The larger the value, the more prominent the echo effect is.


Combined with the *[Diffusion](#diffusion)* parameter, echo depth introduces a more diffuse environment, where the echo wash dies more quickly, or a less diffuse one with a large number of echo repetitions. If Diffusion is set to 0 and Echo Depth is set to 1.0, the echo will persist distinctly until the end of the reverberation decay.


### Echo Time


The *Echo Time* parameter controls the time period for cyclic echo to repeat itself along the reverberation decay. For example, if the time is set to 0.250 seconds, the echo occurs 4 times per second. Therefore, on beating the drum in such reverberation zone, the listener will hear four repetitions of a beat per second.


## Gain


To control the maximum amount of reflections and reverberation added to the final sound perceived by the listener, the gain parameter is used. It affects all sound sources placed in the reverberation zone. *Gain* is a scalar multiplier for the amplitude of the produced reverberation sound.


- The Gain value of 1.0 (0 dB) equals the maximum amount of a reflected sound.
- The Gain value of 0 (-100 dB) results in having no reflected sound at all.


### Gain at Low Frequencies


For further fine-tuning adjustment there is the *Gain LF* parameter. It is a multiplier allowing to attenuate the reflected sound generated in the zone at low frequencies.


- If the *Gain LF* value is set to 1.0 (0 dB), no filter is applied.
- The *Gain LF* value of 0 (-100 dB) results in having virtually no reflected sound.


### Gain at High Frequencies


The high frequencies are attenuated the same way, as the [low ones](#gain_lf).


## Pitch Modulation


The pitch modulation effect is not usually encountered in the real life, but it can be used to carry the emotional load and add additional expression to the established sound environment. For example, with its help, the feeling of dizziness or intoxication is aurally rendered, especially when set to extreme together with other parameters values. This effect will be most noticeable when applied to the reverberation zone with sources that have tonal color or pitch.


### Modulation Time


*Modulation Time* stands for the speed of the vibrato (rate of periodic changes in pitch). The available range is from 0.04 to 4.0 seconds. The default is 0.25 seconds.


### Modulation Depth


*Modulation Depth* is a linear multiplier value that controls the amount of pitch change. Combined with low *[Diffusion](#diffusion)* values, mixing of overlapping reflections in the reverberation decay is reduced, and the perceived effect is reinforced. By default, modulation depth is set to 0.


## Room Rolloff


Not only the sound emitted by the source becomes fuzzy and indistinct as the listener withdraws from it. The same is valid for its reflections and reverberations. The *Room Rolloff* factor defines the rate at which the reflected sound is attenuated with a distance. It is concurrent with the corresponding [parameter](../../objects/sounds/sound_source.md#rolloff) of the sound source, except being set for the whole reverberation zone.


- By default, the value is set to 0 because the natural rolloff of a reflected sound is automatically simulated for each sound source.
- Setting the factor to 1.0 will result in the reflected sound decay by 6 dB every time the distance doubles.
- Any other value will be equivalent to scaling factor for the reference source-listener distance.


## Air Absorption


Similar to the corresponding parameter of the [sound source](../../objects/sounds/sound_source.md#air), the transition of the reflected sound through the specific medium, such as fumes or, on the contrary, dry heated air, can be simulated. The present parameter is applied to the reflected sound in the reverberation zone. The air absorption controls the distant-depending attenuation at high frequencies based on the propagation medium properties. The reason for such filtering is the following: all materials in the sound environment are more efficient at reflecting specific sound frequencies, but in most cases high frequencies tend to be absorbed more readily than low frequencies. As a result, reverberation time of low frequencies turns out to be longer. In very large spaces, the effect of the air absorbing high frequencies may exaggerate this tendency, giving the reverb tail a rolling or thunder-like quality.


- The default value of 0.994 (-0.05 dB) per unit approximates normal atmospheric humidity and temperature.
- Lower values correspond to a more humid medium.
- Higher values correspond to a less absorbent medium.


## Reverberation Density


Density defines the coloration of the late reverberation sound. As the density increases, individual resonances making up the reverb component of the sound are interlaid more tightly.


- The default value of 1.0 provides the highest density of reverberation, which tends to sound more natural on drums and percussion.
- Lowering the value can produce coarse-sounding reverberation for percussive sounds while often embellishing non-percussive ones and adding more coloration.


## Reverberation Diffusion


Closely related to density is diffusion, which determines the rate at which resonances increase in density after the original sound during the reverberation decay. A square room with flat surfaces might exhibit a relatively low diffusion rate compared with a similarly sized room covered in irregularly shaped surfaces, which is one reason for concert halls being built with pillars and ornate alcoves.


- The default 1.0 provides the highest increase in density.
- By reducing density, reverberation acquires more granularity in sounding, especially noticeable with percussive sound sources.
- If set to 0, the reverberation decay sounds like a succession of distinct and individual echoes.


## See also


- The *[SoundReverb](../../api/library/sounds/class.soundreverb_cpp.md)* class to manage reverberation zones via API
- *[Sound](../../sdk/api_samples/cs/sounds.md)* samples in *C# Component Samples* suite
