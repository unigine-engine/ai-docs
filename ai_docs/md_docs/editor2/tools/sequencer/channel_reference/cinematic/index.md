# Cinematic Channels


The *CINEMATIC* half of the channel picker holds ready-made channels for the things a cutscene is assembled from. They are not plain engine parameters: each was built for one job and carries the settings that job needs.


![](cinematic_channels.png)


| **[Camera Cuts](../../../../../editor2/tools/sequencer/channel_reference/camera_cuts/index.md)** | Switches which camera the shot is seen through. |
|---|---|
| **[Skeletal Animation](../../../../../editor2/tools/sequencer/channel_reference/skeletal_animation/index.md)** | Plays `*.anim` clips on a character. |
| **[Sound](../../../../../editor2/tools/sequencer/channel_reference/sound/index.md)** | Plays audio from a place in the world. |
| **[Music](../../../../../editor2/tools/sequencer/channel_reference/music/index.md)** | Plays audio for the whole scene, with no place of its own. |
| **[Sub-Sequence](../../../../../editor2/tools/sequencer/channel_reference/sub_sequence/index.md)** | Plays whole sequences nested inside this one. |
| **[Follow Path](../../../../../editor2/tools/sequencer/channel_reference/follow_path/index.md)** | Moves a node along a keyed trajectory and turns it to face the way it travels. |
| **[Events](../../../../../editor2/tools/sequencer/channel_reference/events/index_cpp.md)** | Sends named signals to your game code, at a moment or across a span. |
| **[Material](../../../../../editor2/tools/sequencer/channel_reference/material/index.md)** | Animates a parameter, state or texture of a material. |
| **[Component](../../../../../editor2/tools/sequencer/channel_reference/component/index.md)** | Animates a field of your own C++ or C# component. |
| **[Console Command](../../../../../editor2/tools/sequencer/channel_reference/console/index.md)** | Animates an engine console variable. |


The first five hold [clips](../../../../../editor2/tools/sequencer/clips/index.md) rather than keys, and so does the Event Range half of **Events**. The rest take keys like any other channel, and what makes them special is how the thing they drive is chosen.
