# Converting Legacy Tracks


Animation in UNIGINE used to be authored in the **[Tracker](../../../../editor2/tools/tracker/index.md)**, and its work is kept in `*.track` files. The Sequencer converts those into sequences: point it at a `*.track` and it writes a `*.seq` beside it, under the same name.


This is a one-way conversion done once per file. The result is an ordinary sequence with nothing legacy about it - the same channels, targets and keys you would have authored by hand.


## Converting a Track


The two commands sit in the menu next to *Save* on the toolbar:


| Command | What it does |
|---|---|
| **Import Legacy .track�** | Converts the track. If the `*.seq` already exists, it is kept and nothing is written. |
| **Reimport Legacy .track (overwrite)�** | Converts it again, replacing the existing file. |


A track that plays other tracks inside itself is converted whole: every nested track becomes a sequence file of its own, and the parent gets a [Sub-Sequence](../../../../editor2/tools/sequencer/channel_reference/sub_sequence/index.md) channel whose clips point at them.


The same conversion runs from code as , which takes the `*.track` path, an output path that may be left empty, and an overwrite flag, and returns the path it wrote.


> **Notice:** **Reimport** rebuilds the whole tree, not only the file you picked. Nested sequences you have since edited by hand are replaced along with it; each one is named in the console as it goes.


## What the Sequence Looks Like


Most tracks become the channel you would expect - a position track becomes **Node � Position**, a light color becomes that light's color. A few take a shape worth recognizing:


| In the Tracker | In the sequence |
|---|---|
| Position with **follow X / Y / Z** | A **[Follow Path](../../../../editor2/tools/sequencer/channel_reference/follow_path/index.md)** channel. One channel now carries both the trajectory and the direction the node faces, and the axis it turns is a field on it. |
| **Const velocity** | The **[Constant Speed](../../../../editor2/tools/sequencer/channels/index.md#constant_speed)** option on the channel. |
| A node track aimed at the player | A **[Camera Cuts](../../../../editor2/tools/sequencer/channel_reference/camera_cuts/index.md)** channel, holding clips rather than keys. |
| A nested track | A [Sub-Sequence](../../../../editor2/tools/sequencer/channel_reference/sub_sequence/index.md) clip, with its own `*.seq` beside the parent. |
| The track's **unit_time** | The sequence's **Speed**, as its reciprocal: a **unit_time** of 2 arrives as a speed of 0.5. Key times are kept exactly as they were authored. |


Every converted channel keeps the name of the tracker parameter it came from in its **Custom Name**, so a row can be traced back to the track it was built from.


Row order arrives reversed. Where two tracker parameters wrote to the same target the last one won, while in a sequence the top row wins, so the converter lays the rows out back to front and the parameter that was in charge stays in charge. The rule itself is described in the [Channel Priority](../../../../editor2/tools/sequencer/channels/index.md#multiple_channels) section.


> **Notice:** A follow track's **look-ahead** is carried across, and three values behave differently from the way they did in the Tracker. Each is named in the console.
>
>
> - A row that named no look-ahead at all was refused by the Tracker outright. The sequence takes it and follows the path with the default step.
> - A look-ahead of 0 left the node unturned in the Tracker. In a sequence 0 means the smallest step the curve can tell apart, so the node is aimed along the instant tangent and every wobble in the trajectory reaches its rotation.
> - A negative look-ahead made the Tracker look behind. The sequence looks ahead by that much instead.


## Checking the Result


The console is the report of the conversion. It is worth reading once through, because everything the converter could not carry over is named there, one line per parameter, with the reason. The messages fall into three groups.


### Parameters That Were Not Carried Over


These produce no channel at all. The usual reasons:


- **The track did nothing in the Tracker either.** A handful of parameters stopped working there long ago - a few light textures, a particle setting, a couple of render ones. There is no behaviour to migrate, and the sequence is not missing anything the track actually did.
- **The track named no surface, or no parameter.** A material or property track has to say both which object and which parameter on it. The Tracker refused such tracks outright, and so does the conversion, rather than producing a channel that reaches nothing.
- **The parameter is not a known tracker parameter.** Hand-edited or third-party tracks can name something outside the catalogue.


### Channels Left Without a Target


Here nothing is lost - the channel and its keys are in the sequence, but the object it used to write into is not in this project, so the target field is empty and waiting. Point it at the right object in the [Targets](../../../../editor2/tools/sequencer/targets/index.md) section and the channel works.


This is also what happens to a track that was bound from game code: no file can carry that target, so the channel arrives unbound by design and the code supplies its object at runtime, as described in [Runtime Playback](../../../../editor2/tools/sequencer/runtime/index_cpp.md).


### Notes on the Result


The rest of the messages are about keys and timing, and are worth a look before playing the sequence:


- Keys that sat past the track's end are kept, and the sequence is stretched to cover them: its duration runs to the last key rather than to the end the track declared.
- A parameter that had no keys at all gets a single key holding that parameter's neutral value - 1 for a scale, 0 for an offset. A keyless track held 0 in the Tracker, and a channel with no keys would be dropped from evaluation altogether.
- If one node was driven both by a follow track and by a plain position or rotation track, the **Follow Path** channel takes it over - it writes both the position and the rotation, so the plain one has no effect.
- A smooth key whose two handles were not mirrors of each other becomes a **Break** key. The curve through it is unchanged; the key type simply names what the handles already do.
- Two nested rows that overlapped in time were averaged by the Tracker where they wrote to a shared target. A sequence layers them top-down instead, so the upper clip wins outright for the length of the overlap.
- Nesting is followed 32 levels deep, and a clip below that is skipped, as is one whose nested track cannot be found. A nested row carrying no weight keys produces no clips at all.
- Key times that were negative or not finite are clamped to 0, and key values that were NaN or infinite are replaced with 0. A track starting before 0 is clamped to it, and one ending before it starts is imported empty.


## See Also


- [Sequence Channels](../../../../editor2/tools/sequencer/channels/index.md)
- [Targets and Bindings](../../../../editor2/tools/sequencer/targets/index.md)
- [Sub-Sequence](../../../../editor2/tools/sequencer/channel_reference/sub_sequence/index.md)
- [Camera Cuts](../../../../editor2/tools/sequencer/channel_reference/camera_cuts/index.md)
