# Sound


A **Sound** channel plays a sound file from a place in the world - a voice line at a character, an explosion at a spot, a machine humming in the corner of a room. Use it whenever a sound belongs to a location rather than to the scene as a whole.


![](sound_channel.png)


## What It Drives


A Sound channel is **3D sound**: it is louder when the camera is near and quieter when far, so it needs a place to come from. Drop a **SoundSource** node into its target field and that node becomes the spot the sound is heard from. Binding in general is covered in the [Targets and Binding](../../../../../editor2/tools/sequencer/targets/index.md) article.


![](sound_target.png)


For background music that sounds the same everywhere, use the [Music](../../../../../editor2/tools/sequencer/channel_reference/music/index.md) channel instead. It is 2D and needs no node at all.


## Filling the Clip


Sound is a clip channel: you place audio files as clips on the timeline rather than keys. Double-click an empty spot on the row to create a clip, then pick its audio file in the clip's properties (`*.wav`, `*.ogg`, `*.mp3`). Each clip plays while the playhead is over it.


![](choosing_sound.png)


Timing, trimming and looping past the end of the file work the same as on any clip, described in the [Clips](../../../../../editor2/tools/sequencer/clips/index.md) article.


## Volume and Pitch


An audio clip carries two curves of its own, both keyed on the clip's [sub-tracks](../../../../../editor2/tools/sequencer/clips/index.md#sub_tracks):


- **Volume** - the clip's gain, running from 0 to 1, for fades and for ducking one sound under another. Values outside that range are clipped to it. This is the sound's own loudness control, and it stands in for the Weight row other clips carry.
- **Pitch** - a tone shift in semitones. It changes the tone and leaves the length alone.


A SoundSource node can play only one sound at a time, so where clips overlap the one with the higher **Volume** at that moment is the one heard, and the other is silent.


Both curves are written straight onto the node while the clip plays, into its **Gain** and its **Pitch Shift**. A channel with no Pitch keys leaves the node's own setting alone rather than overwriting it with zero, and the values the node held before playback are put back when the player stops.


> **Notice:** The **Speed** curve every clip carries does not make a positional sound play faster or slower. Audio runs on its own clock, and speed only moves the position the channel asks for, which the node follows by jumping. To play the sound itself faster or slower, animate the **Pitch** parameter of the SoundSource node on a channel of its own. That one shifts rate and tone together, the way a tape does.


## See Also


- [Clips](../../../../../editor2/tools/sequencer/clips/index.md)
- [Targets](../../../../../editor2/tools/sequencer/targets/index.md)
