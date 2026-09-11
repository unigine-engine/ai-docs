# Music


A **Music** channel plays background music for the whole scene.


![](music_channel.png)


## What It Drives


A Music channel is **2D sound**: it plays for the scene as a whole, not from any object, and its volume does not change with camera distance. It has no target field, since there is nothing to point it at.


For a sound that comes from a place in the world - an explosion at a spot, a character speaking to a specific node in the world - use the [Sound](../../../../../editor2/tools/sequencer/channel_reference/sound/index.md) channel instead, which is 3D.


## Filling the Clip


Music is a clip channel: you place audio files as clips on the timeline rather than keys. Double-click an empty spot on the row to create a clip, then pick its audio file in the clip's properties (`*.wav`, `*.ogg`, `*.mp3`). Each clip plays while the playhead is over it.


![](choosing_music.png)


Timing, trimming and looping past the end of the file work the same as on any clip, described in the [Clips](../../../../../editor2/tools/sequencer/clips/index.md) article.


> **Notice:** Past the end of its file a music clip cannot hold the last moment the way a picture does. Set to repeat, it plays the track again from the top for as long as the clip lasts. Left on Constant, it falls silent once the track runs out.


## Volume, Pitch and Speed


A music clip carries three curves of its own, all keyed on the clip's [sub-tracks](../../../../../editor2/tools/sequencer/clips/index.md#sub_tracks):


- **Volume** - the clip's gain, running from 0 to 1, for fades and for ducking the music under dialogue. Values outside that range are clipped to it. This is the track's own loudness control, and it stands in for the Weight row other clips carry.
- **Pitch** - a tone shift in semitones. It changes the tone and leaves the pace alone.
- **Speed** - how fast the track is played. Tone follows the pace here, so a track sped up plays higher and a slowed one plays lower, the way a tape does. Past four times the normal pace the track stops keeping up.


![](overlapping_music.png)


Every clip on the channel is given a voice of its own, so overlapping clips are heard together, each at its own volume. That is how one track crosses into another: fade the outgoing clip down across the overlap while the incoming one comes up, and both are audible through it.


## See Also


- [Clips](../../../../../editor2/tools/sequencer/clips/index.md)
- [Sound](../../../../../editor2/tools/sequencer/channel_reference/sound/index.md)
