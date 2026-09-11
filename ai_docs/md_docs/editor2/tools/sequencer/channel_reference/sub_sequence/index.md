# Sub-Sequence


A **Sub-Sequence** channel plays whole sequences inside this one. Each clip holds a `*.seq` that runs for the span of the clip, so a long cutscene can be assembled from short pieces made separately: a door opening, a character gesture, a lamp flickering.


![Sub-Sequence channel](sub_sequence.png)

*A Sub-Sequence channel with one clip and its sub-tracks open. The clip is drawn to itsWeightcurve, so the fade in and out can be read off the timeline itself*


The channel has no target field. What a clip does is decided by the sequence inside it, which carries its own channels and its own targets.


## Filling the Channel


Double-click an empty spot on the row to create a clip, or drop a `*.seq` asset onto the timeline. A drop where no channel exists yet builds the channel too.


![Adding a clip](add_sub_sequence.png)

*Right-clicking empty row space offersAdd Clipas well*


A clip keeps its sequence in one of two ways, shown by its **Type** field. A clip made by double-clicking starts out **Embedded**, one made by dropping an asset starts out **Reference**:


![Clip type](sub_sequence_types.png)

*Typedecides where the clip keeps its sequence*


- **Embedded** - the sequence is stored inside this `*.seq` and belongs to its clip alone. Use it for a piece that exists only in this cutscene and would clutter the asset browser as a file of its own.
- **Reference** - the sequence is a separate `*.seq` asset, chosen in the clip's **Sequence Asset** field. One asset can be used from many places at once, and editing it changes all of them. Use it for anything reused across shots.


## Editing an Embedded Sequence


![Edit Inside](sub_sequence_edit_inside.png)

*Edit Insideopens the nested sequence, the same as double-clicking the clip*


Double-click an embedded clip to open it, or press *Edit Inside* in its properties. The Sequencer then shows the nested sequence and the breadcrumb bar in the toolbar shows how deep you are, with arrows to step back and forward. The clip's **Name** is what the breadcrumb shows, so it is worth setting once a composition has a few levels.


> **Notice:** Pressing play inside a nested clip runs the whole sequence starting from the root.


## Timing


When the nested sequence starts, where in it playback begins and how fast it runs are all decided by the clip, through **Start**, **Clip In**, **Clip Out** and its **Speed** curve, as described in the [Clips](../../../../../editor2/tools/sequencer/clips/index.md) article.


> **Notice:** A clip inserted from an asset arrives trimmed to that sequence's playback range. Drag an edge afterwards and the clip runs against the full length instead.


## Overlapping Clips


A nested sequence can animate the same parameters of the same objects as the channels beside it. It is worked out on its own first and joins the parent in one piece, so the clip's **Weight** covers everything inside it at once - and for a number or a vector, what comes out depends on that weight:


| **Full Weight** | The clip takes the parameter whole. Nothing is left over, and the rows below it are not reached at all. |
|---|---|
| Between **0** and **1**, with a channel below | The result lands between the two: a clip at 0.5 comes out halfway toward whatever the row below holds. |
| Between **0** and **1**, with nothing below | The value passes through whole. There is nothing to blend toward, so the weight changes nothing at all. |
| **0 Weight** | The clip is skipped, and whatever is below takes over. |


The weight is a share rather than a strength: it decides how much of the result is the clip's, not how far the value travels.


What counts as below is the order of the list - the higher row comes first, and the parent's own channels rank among the clips by their own row. An ordinary channel carries no weight, so wherever it falls in that order it takes the parameter whole and ends the queue: one sitting above a Sub-Sequence clip hides it completely.


> **Notice:** Sound and skeletal animation scale by the weight instead, and weights nested inside multiply with it, so a sound clip at a volume of 0.8 within a sub-sequence clip at 0.5 comes out at 0.4.


## Sequences Inside Sequences


A nested sequence may hold sub-sequences of its own. Each level is settled first and reaches the level above as a single piece, and for sound and skeletal animation the weights of every level multiply, so a clip at 0.5 inside another at 0.5 delivers a quarter.


> **Notice:** A sequence cannot contain itself, directly or through a chain of others. The Sequencer refuses both the asset and the drop.


## See Also


- [Clips](../../../../../editor2/tools/sequencer/clips/index.md)
- [Runtime Playback](../../../../../editor2/tools/sequencer/runtime/index_cpp.md)
