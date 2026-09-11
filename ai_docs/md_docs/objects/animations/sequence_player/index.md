# Sequence Player


A **Sequence Player** ![](sequence_player.png)� node plays a Sequencer animation (a `.seq` file) in the scene at runtime. It is the simplest way to run a sequence: add the node, point it at an animation, and it drives the animated targets - object transforms, materials, cameras, sounds, events - as the timeline plays.


The node is a thin wrapper over the playback machine described in the [Sequencer](../../../editor2/tools/sequencer/index.md) section: it exposes the transport and the per-instance target bindings in the node inspector, so you set up and preview a sequence entirely in the editor, without code. For running a sequence without a node, see [Runtime Playback](../../../editor2/tools/sequencer/runtime/index_cpp.md).


### See Also


- The *[Sequencer Tool](../../../editor2/tools/sequencer/index.md)* article series - authoring the animations this node plays


## Adding a Sequence Player


To add a *Sequence Player* node to the scene via UnigineEditor:


1. On the Menu bar, click *Create -> Animation -> Sequence Player*.
2. Place the node in the world.
3. Assign a `.seq` file in the node parameters.


![Create Menu](creating_sequence_player.png)


The sequence itself is authored in the [Sequencer Editor](../../../editor2/tools/sequencer/editor/index.md). Once assigned, use the transport buttons in the inspector to play and preview it.


## Sequence Player Parameters


![Sequence Player Settings](sequence_player_settings.png)


| Parameter | Description |
|---|---|
| Sequence File (.seq) | The Sequencer animation file to play. |
| Play / Pause / Stop | Playback controls: - **Play** - start or resume playback. - **Pause** - stop at the current time, keeping the playhead there. - **Stop** - end playback and return the playhead to the start of the playback range: **Time From**, or the beginning of the sequence when no range is set. |
| Loop | When enabled, the sequence restarts from the beginning after reaching the end. |
| Play On Enable | Automatically start playback each time the node is enabled. Playback picks up at the current time rather than at the beginning; to always start over, use **Restart On Enable**. |
| Restart On Enable | Rewind the sequence to the beginning each time the node is enabled. It only rewinds: playback starts from there if **Play On Enable** is on, or if the node was already playing when it was disabled. |
| Originals Restore Mode | Per-instance override of what happens to the animated values when playback stops. See [Originals Restore Mode](#originals_restore) below. |
| Time | Current playback time in seconds. Editing it scrubs the sequence and shows that frame in the viewport right away, as long as the node is enabled and not already playing. |
| Speed | Playback speed multiplier (0.5 - 2x slower, 2.0 - 2x faster). |
| Time From | Start time of the playback range. Allows playing only a portion of the sequence. |
| Time To | End time of the playback range. |


Disabling a Sequence Player node pauses its sequence. Enabling it again resumes from the same time if the node was playing when it was disabled, or if **Play On Enable** is set; otherwise the sequence stays paused.


## Originals Restore Mode


A sequence overwrites the parameters it animates while it plays. What becomes of those parameters afterwards is set in the sequence itself, and this node can override it for its own instance. There is no separate toggle for the override: picking a mode in the combo box is what turns it on, and the field's reset button turns it back off. While the override is active the parameter label is highlighted.


![Restore Mode Settings](originals_restore_mode.png)


The modes are:


| Mode | Behavior |
|---|---|
| Never | The sequence owns the scene and leaves the last animated values in place. |
| On Stop | Snapshots the original values on the first apply and restores them when playback stops. |
| Each Frame | Treats the animation as an overlay, restoring the original at the start of each frame so game logic keeps reading the original value. |


With no override set, the node uses the default saved with the sequence. The modes are described in full, with examples of when to use each, in the [Sequencer Editor](../../../editor2/tools/sequencer/editor/index.md#restore_mode) article.


## Bindings (Per-Instance)


A sequence stores a default target for each channel it animates, so it plays out of the box. The **Bindings (per-instance)** section retargets those channels for this node alone, leaving the shared asset untouched - which is how one animation drives different objects in several places in the scene. Targets and bindings themselves are covered in the [Targets and Binding](../../../editor2/tools/sequencer/targets/index.md) article.


The section lists one row per bindable channel of the sequence, nested sub-sequences included. A row is labeled with the channel name and, where the same sequence is nested more than once, with the placement it belongs to. Each row holds:


| Control | What it does |
|---|---|
| Targets | The objects this channel drives. It is a list rather than a single field: add more entries to drive several objects from one channel at once. The label under the list reports how many targets there are, and for a query how many objects it currently matches. |
| Match by | How an entry finds its object - **Direct** for one specific node or asset, or a query that resolves to a whole set at playback time: by name pattern, by property, by component, or by node type. An asset entry instead offers **By Inheritance** from a root asset. |
| Scope | Where a query searches: **World**, **Subtree** under a chosen root node, or **From Node Reference** - every instance loaded from a chosen `.node` file. |
| Source | Shown for material and property channels: whether the driven value comes from the **Asset**, from a **Node**, or from an object's **Surface**. |


Overrides are undone with the reset buttons: the one on the row returns the whole channel to the target authored in the sequence, the one on a single entry returns that entry to its authored value, or removes it when it was added on top of the authored list.


A channel bound to a runtime target has nothing to pick here, since its object is handed to the player by game code. Such a row reads "runtime target - set by game code" and cannot be edited; see the [Runtime Playback](../../../editor2/tools/sequencer/runtime/index_cpp.md) article.


> **Notice:** Bindings are editable for one node at a time. With several nodes selected the section shows a hint in place of the rows, while the transport buttons above keep acting on the whole selection.
