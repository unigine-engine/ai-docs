# Clips


A **Clip** is a window onto a piece of content, placed on the timeline. It says where the content starts, how long it runs, how far into the content playback begins, and how much of it reaches the result.


![](clips.png)


Where a key pins one value at one moment, a clip covers a span: a key holds a value, a clip holds a source that is read through time.


**A clip over a source.** The content has a length and a clock of its own - an audio file, a character animation, a nested sequence - so the clip has an inside. It can be trimmed into, played at its own pace, and stretched past the end of the content.


**A clip as a span.** The content is simply switched on for as long as the clip lasts - a camera made active, an event held open. There is nothing inside to address, so trimming, speed and looping do not apply to it.


> **Notice:** Past these two kinds, a clip is its channel's own business: the curves it carries and the way overlapping clips are settled differ from one channel to the next. Each is covered in the [Channel Reference](../../../../editor2/tools/sequencer/channel_reference/index.md).


## Adding Clips


There are three ways to put a clip on a channel:


- **Double-click empty row space, or choose *Add Clip* in the right-click menu.** ![](adding_a_clip_menu.png) Both create a clip at the point you clicked, empty and waiting for its content. On a Sub-Sequence channel they create a nested sequence instead, ready to drill into.
- **Add Clip on the channel row.** ![](adding_a_clip.png) Inserts one at the playhead.
- **Drop an asset on the timeline.** A sound, an `*.anim` or a `*.seq` builds the channel and its first clip in one step.


How long the new clip comes out depends on what it holds. A clip pointing at a sequence takes that sequence's playback range, one holding an asset takes the asset's own length, and an empty one stretches to the next clip in its row, up to two seconds.


## Clip Properties


Besides the field naming its content, every clip carries the same set of settings.


Two clocks are involved, and telling them apart makes the rest easy:


- **Start** is a moment on the sequence timeline.
- **Clip In** and **Clip Out** are moments inside the content, counted from the content's own beginning.


![](camera_clip_properties.png)


| Enabled | Turns the clip off without deleting it. It is drawn dimmed and skipped during playback. |
|---|---|
| Start | Where the clip begins on the timeline. |
| Clip In | The moment inside the content that playback starts from. A value of 0 plays the content from its very beginning, and a larger one cuts off the head. Dragging the clip's left edge sets it. |
| Clip Out | The moment inside the content that playback stops at. Dragging the clip's right edge sets it. Where a clip runs the content more than once, the count carries straight on instead of starting over, so the number can read past the end of the content. |
| Clip Length | Read-only. How much room the clip takes on the timeline, which follows from the two trims and the speed. |
| Color | A tint for the clip on the timeline, to tell clips apart. A new clip is given a random one. |


> **Notice:** Every channel that takes clips adds settings of its own on top of these. They are covered in [Channel Reference](../../../../editor2/tools/sequencer/channel_reference/index.md).


## Editing Clips


Clips are selected, moved and box-selected like keys. Right-clicking one opens a menu of its own:


![](clip_menu.png)


- *Copy*, *Paste*, *Duplicate*, *Delete* - a pasted clip lands where the cursor is, not where it was copied from.
- *Split* - cut the clip in two at the cursor.
- *Move Up*, *Move Down* - shift it between rows, keeping its position in time.
- *Enabled* - the same switch as the clip property.
- *Expand* / *Collapse* - show or hide its [sub-tracks](#sub_tracks).


Right-clicking empty row space offers *Add Clip* and *Paste* instead.


## Sub-Tracks


A clip can carry curves of its own. They control how that content plays over the clip's length, and each one is edited in the clip's own time rather than the sequence's.

  ![](subtracks_collapsed.png)  ![](subtracks_expanded.png)
Click the arrow on the clip to open them, or use *Expand* in its right-click menu. Each curve appears as an extra row under the channel.

  ![](subtracks_collapsed_arrow.png)  ![](subtracks_expanded_arrow.png)
Which curves a clip carries, and what each of them does, follows from its channel and is covered in that channel's own article.


## Trimming and Retiming


Drag an edge of the clip and you **trim** it. The content keeps its own pace, and the clip simply shows less or more of it.

   Sorry, your browser does not support embedded videos.
A clip over a source can also be **retimed**. Hold ***Alt*** while dragging an edge: the same part of the content plays, squeezed or stretched to fit the new length.

   Sorry, your browser does not support embedded videos.
Three things describe the result:


- **Start** and **Clip Length** - the room the clip takes on the timeline.
- **Clip In** and **Clip Out** - the part of the content that plays.
- **Speed** - how fast that part is played.


Clip Length = (Clip Out - Clip In) / Speed


Speed is a curve rather than a single number, so one clip can slow down and speed up over its own length: a walk that starts brisk and settles, a shot that drifts into slow motion. It is edited on a [sub-track](#sub_tracks), and the length above is worked out from the speed the clip starts at.


Both trim fields have a button that puts the edge back on the content. **Reset Clip In** returns to its beginning, **Fit Clip Out to source** to its end. For a clip holding a sequence these are the ends of that sequence's playback range, so the edge lands where a freshly inserted clip would have put it.


## Running Past the Content


A clip can be made longer than the content it holds. The stretch beyond the end of that content is drawn ghosted on the timeline, so it is plain where the file runs out and the filling begins.


![](repeating_content.png)


What plays there is set on the clip itself, by **Pre Infinity** and **Post Infinity**, one for each side:


| Constant | Holds the first or the last frame of the content for the rest of the clip. |
|---|---|
| Cycle | Repeats the content from its beginning, as many times over as the clip is long. |
| Ping-Pong | Repeats it forward and backward in turn. Audio cannot play in reverse, so audio clips are not offered this one. |


> **Notice:** Only a clip over a source reaches this point. A clip that is just a span has no content length to run past, so it carries no infinity settings and is never ghosted.


## Rows and Overlap


A channel holding clips has several rows of them. Clips in one row follow one another, and clips in different rows can cover the same moment.


Where clips do cover the same moment, they are put in order the same way on every channel: the higher row comes first, and between clips sharing a row the later start comes first.


That order decides who is served first, not who wins outright. Whether the first clip takes the moment whole or leaves something for the one below it depends on what is being driven - a camera cannot be shared, a character animation can. The cases are covered in the [Channel Reference](../../../../editor2/tools/sequencer/channel_reference/index.md).


## See Also


- [Sub-Sequence](../../../../editor2/tools/sequencer/channel_reference/sub_sequence/index.md)
- [Keys and Curves](../../../../editor2/tools/sequencer/keys/index.md)
- [Channels](../../../../editor2/tools/sequencer/channels/index.md)
