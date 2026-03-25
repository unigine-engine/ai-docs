# Global Sound Settings


The *Sound* section of the *Settings* window allows you to adjust *global sound-related settings*: values set here will be applied to all [sounds](../../../objects/sounds/index.md) in the scene.


> **Notice:** To configure sound settings, open the *Settings* window by choosing *Window -> Settings* in the main menu and select *Runtime -> World -> Sound* section.


![Sound Settings](sound_settings.png)

*Global Sound Settings Window*


The following settings are available:


| Scale | Scale factor to speed up or slow down the sound play. |
|---|---|
| Volume | Volume for all sounds in the scene. - The value can be in range [**0** ;**1** ]. - The higher the value (up to the maximum **1**), the louder the sounds. |
| Doppler | Doppler effect intensity. The default is 1. |
| Velocity | Speed of sound. It is used to control sound propagation. |
| Adaptation | Controls the time of sound adaptation to a filter. The parameter is used when the sound source becomes occluded (an obstacle appears between it and the player). - By the minimum value of **0**, the sound changes from clear to muffled one (and vice versa) instantly. - By the maximum value of **1**, the sound changes gradually over time. |
| Source Occlusion | Toggles sound occlusion on and off. When enabled, sounds will be occluded when there are other nodes between the listener and the sound source. |
| Source Reverb Mode | Reverberation mode to be used for sound sources. The following modes are available: - *Disabled* - *Single* - *Multiple* |
| Attenuation | Model used to calculate sound attenuation. Attenuation is a reduction of the sound volume as the player moves away from the sound source. The following models are available: - *Inverse* - *Inverse Clamped* - *Linear* - *Linear Clamped* - *Exponent* - *Exponent Clamped* |
| HRTF | Toggles the binaural HRTF (Head Related Transfer Function) mode on and off. This mode provides imitation of the surround sound for the stereo wired headset. |
| Volume 0 - Volume 31 | Volume of the specified mixer channel. - By the minimum value of 0, the sound is muted. - By the maximum value of 1, the sound is played with the maximum volume. The number of simultaneously played sound sources per one mixer channel is specified in the **Limit** field. To what channel the sound belongs is set in the *[Source mask](../../../principles/bit_masking/index.md#source_mask)* per sound source. For example, let's assume that we have 10 sound sources with the Source mask 0 enabled, and the Limit is set to 3. In this case, when the camera is within the reach of the sound sources, only 3 closest sources are heard on Channel 0. |
