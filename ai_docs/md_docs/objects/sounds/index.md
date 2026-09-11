# Sound


Next to the graphical component, sound is a very important domain of real-time technologies. Sound is the key resource for creating the proper feeling of immersion in the virtual world. It gives the user an audible characteristics of the surroundings and allows to differentiate between locations. While simple 2D ambient sound can create the overall atmosphere, it is still not enough for conveying dynamically changing environment. With 3D sound effects brought into action, the listener can subliminally estimate the distance to the sound source and pinpoint its location, thus experiencing the scene within grasp. Moreover, UNIGINE supports virtually the unlimited number of sound sources. You can let the whole ocean of sound waves speak for the reality called into being by the artist's hand.


There is an immense potential for sound application. Sound can serve for indicating a certain architectural feature. For example, the rolling echo cues us to anticipate a scene to take place in a lofty dome. The soft tapping of the stone hit by an incautious foot or a car whooshing by with lightning speed � all of that can be modelled aurally. UNIGINE makes it possible to assign a sound that will be played by contact of the objects simulating their physical properties on the level of sound. For the moving sources, like a car, the Doppler effect is applied so that the movement of the sound source relative to the listener is authentically imitated. All these changes in the sound environment provides the brain with more specific information about in what direction and exactly how the objects move. With the help of sound one can not only construct the scene in the head, but sense it.


The expressiveness and quality of the audio material substantially adds to the virtual world, so it is only logical the developers, just like movie creators, want to have full control of this tool which they use in their work. UNIGINE provides the following objects for positioning the sound in 3D environment:


- [![](sound.png)](../../objects/sounds/sound_source.md) **[Sound Source](../../objects/sounds/sound_source.md)** represents a directional or omnidirectional sound source.
- [![](reverb.png)](../../objects/sounds/sound_reverb.md) **[Sound Reverb](../../objects/sounds/sound_reverb.md)** represents a reverberation zone.


3D effects can be created on a common set of two speakers as well as on multi-channel audio systems.


## Loading Audio


The first question raised when adding audio material to their work, is how the sounds are going to be loaded, if they are not synthesized on the fly. Basically, there are two ways to load sounds in a game:


- Sounds can be loaded from files in their entirety. This is a more traditional approach, resulting in having all necessary audio resources at hand, with no lags at uploading. But it is suitable only for short sounds because it costs higher memory consumption than the second approach.
- Sounds can be streamed from some location, for example, from a remote machine. In this case, audio data is read chunk by chunk into a special buffer, from which it is played to the user. During the playback, the buffer is progressively updated. Though this approach increases disk throughput or general network loading, it is an apt solution for long tracks.


UNIGINE supports the following sound file formats:


- WAV (mono and stereo)
- Ogg Vorbis (or oga, Ogg Audio Profile)
- MP3


> **Notice:** In order to play `*.ogg` audio files in UNIGINE, change their filename extension to `*.oga` (files of both format use the same codecs, the only difference is their filename extension).


## Audio API


UNIGINE is compatible with sound cards produced by Creative Labs that provide a technology using their environmental audio extensions (EAX). EAX represents a number of presets for audio, which allow simulating audio environment faster and more accurately. With its help, the sound designer can describe the environment, the sources, and the listener with multiple parameters either using presets or by creating their own presets. When the environment changes, presets also change, and to perform smooth transition, their stored values are interpolated.


To manipulate these parameters and presets and to performs all necessary calculations like distance attenuation, Doppler effect, and so on, the following API is used: OpenAL, a cross-platform open source 3D audio library. It also supports non-EAX audio technologies.
