# Tracker: Legacy Animation Tool


> **Warning:** *Tracker* is a legacy tool, kept for projects that already use it. New animation is authored in the [Sequencer](../../../editor2/tools/sequencer/index.md), which can also [convert existing `*.track` files](../../../editor2/tools/sequencer/track_import/index.md) into sequences.


*Tracker* is a keyframe-based tool for creating sequences animated over time, which allows for adding dynamic gameplay elements or making in-game cinematic cutscenes. It gives developers the ability to:


- Easily create key frames for all nodes in the world, as well as in-game cameras and render settings.
- Set up day-night shift and weather conditions change.
- Switch between the cameras, change field-of-view on the fly and play sounds for creating stunning cinematics.
- Animate interactive objects in the game, for example, lights, doors, and platforms.
- Apply post-processing effects such as DOF, Motion blur, SSR, etc. All these effects can be fine-tuned for each camera view.
- And much more.


Moreover, the *Tracker* interface supports saving and loading of the created tracks, custom loop ranges, key cloning and snapping, as well as playback speed control.


> **Notice:** To open the *Tracker* tool, choose *Tools -> Tracker* in the Menu Bar.


![](tracker.png)

*Tracker Tool*


By using the *Tracker* tool, the following elements of the virtual world can be animated:


- [Nodes](../../../editor2/tools/tracker/parameters/index.md#node), including [light sources](../../../editor2/tools/tracker/parameters/index.md#node_light), [objects](../../../editor2/tools/tracker/parameters/index.md#node_obj), [fields](../../../editor2/tools/tracker/parameters/index.md#node_field), [players](../../../editor2/tools/tracker/parameters/index.md#node_player), [sound sources](../../../editor2/tools/tracker/parameters/index.md#node_sound), and others
- [Node References](../../../editor2/tools/tracker/parameters/index.md#node_reference)
- [Materials](../../../editor2/tools/tracker/parameters/index.md#material)
- [Properties](../../../editor2/tools/tracker/parameters/index.md#property)
- [Render Settings](../../../editor2/tools/tracker/parameters/index.md#render)
- [Sound Settings](../../../editor2/tools/tracker/parameters/index.md#sound)
- [Game Settings](../../../editor2/tools/tracker/parameters/index.md#game)
- Several [tracks](../../../editor2/tools/tracker/parameters/index.md#track)


### See Also


- - C# Component Sample demonstrating how to change the object's position, rotation, and scale using Tracker
- - CPP sample demonstrating how to change the object's position, rotation, and scale using Tracker


## Key Frame Animation


### Tracks


*Tracker* animations consist of a number of tracks and each track indicates how some parameter changes over the specified time. It can control some render effect or it can be bound to a node in the world. If more properties need to be animated for one node at the same time, simply a number of tracks are created for it. For example, with tracks, you can create animations that:


- Move nodes, toggle skinned animation, control emission of particles, etc.
- Change any of material settings and modify properties for various changeable effects. For example, you can change the texture and material reflectivity to create the effect of rain.
- Alter rendering settings: change the background color, apply post-process effects, control stereo and much more.
- Set up cameras.


### Key Frames


A track is composed of **key frames**, which are snapshots of the parameter at a certain time during the animation. Each key frame stores a time and the parameter change (new value for the parameter or whether is enabled or disabled). For example, for node position track, a key frame sets a new position of the node along one of the axes; for the node enabling track, a key can indicate that a node is disabled for rendering.


This parameter value set in the key frame is applied between the current keyframe and the next one. Depending on the transition mode, the key frame values can be switched abruptly or smoothly interpolated:


- Linear interpolation can be used, for instance, for a node scale track.
- Bezier interpolation will provide a smooth curve for a node position track.


## Tracker Settings


### Track Settings


![](track_settings.png)


| ![](line_add.png) | Add an animation track. In case of a simple track (for example, the track that toggles a node on and off), only a track line will be available. If the track controls parameter with values, key frames will also be present in the graph. |
|---|---|
| ![](line_remove.png) | Remove the selected animation track. |
| ![](line_clone.png) | Clone the selected animation track. |
| ![](line_up.png) | Move the selected animation track up the list. |
| ![](line_down.png) | Move the selected animation track down the list. |
| ![](line_save.png) | Save the parameter value from the Editor into the track. It is available only when the track is [disabled](#enable_track). See [details](../../../editor2/tools/tracker/basics/index.md#approach_2). |
| ![](enable_track.png) | Toggles the track on and off (turns its animation on and off). |
| ![](enable_track_graph.png) | Toggles displaying a track graph on and off (not available for simple tracks). |
| Load | Load the `*.track` file. Tracks from the loaded file will be displayed on the tracks list. > **Notice:** If you have some tracks in the list, you should save them before loading the track file. Otherwise, they will be lost as the loaded tracks will be displayed instead of the current ones. The ![](load_track.png) button can be found in the upper right corner of the *Tracker*. |
| Save | Save all current tracks into the `*.track` file. The ![](save_track.png) button can be found in the upper right corner of the *Tracker*. |
| Clear | Delete all tracks from the tracks list. The ![](clear_tracks.png) button can be found in the upper right corner of the *Tracker*. |


*Tracker* also displays information on the animating objects and allows specifying additional animation settings for each track. For example, you can change a node or a material to which the track is bound.


### Graph Arrange Modes


![](graph_arrange_modes.png)


| ![](track_arrange_x.png) | Scale the graph horizontally in such way that the whole animation line fits into view. ![](arrange_x_before.png) ![](arrange_x_after.png) |
|---|---|
| ![](track_arrange_y.png) | Scale the graph vertically in such way that the lowest and the highest key frames fit into view. ![](arrange_y_before.png) ![](arrange_y_after.png) |
| ![](track_arrange_xy.png) | Scale the graph so that all key frames fit into view. ![](arrange_xy_before.png) ![](arrange_xy_after.png) |


### Key Frames and Transition Modes


![](key_frame_transition_modes.png)


| ![](key_constant.png) | Constant mode (no transition). Key frame value remains constant up to the next key frame, where it abruptly changes. ![](transition_constant.png) |
|---|---|
| ![](key_linear.png) | Linear interpolation. Key frame value is linearly interpolated between neighboring key frames. ![](transition_linear.png) |
| ![](key_smooth.png) | Smooth interpolation by Bezier spline. There are two control points available for each keyframe. ![](transition_smooth.png) |
| ![](key_break.png) | Interpolation by Bezier triangle. The sharp transition between key frame values can be created. There are two control points available for each keyframe. ![](transition_break.png) |
| ![](key_auto.png) | Automatic interpolation by Bezier spline. No control points are available as the curve is smoothed automatically. ![](transition_auto.png) |
| ![](key_remove.png) | Remove selected key frames. |
| ![](key_snap.png) | Snapping mode for key frames. When a key frame is dragged along the track line, this mode pulls a keyframe into alignment with other key frames (on the same or other tracks). It can also be enabled by holding **ALT**. |
| Time | Time of the selected key frame. It controls when the key is used during track animation. |
| Value | Parameter value in the selected key frame. It controls when the key is played during track animation. |


### Playback Settings


![](playback_settings.png)


| ![](time_settings.png) | Duration and playback speed for all tracks. If you click the icon, the *Track Settings* window will open: ![](time_settings_window.png) \| Min Time \| Lower limit of the playback range. \| \|---\|---\| \| Max Time \| Upper limit of the playback range. For example, setting **Min Time** to 0 and **Max Time** to 2 means that tracks playback will last 2 units. \| \| Unit Time \| Playback speed. It sets the duration of one unit in seconds. For example, if **Unit Time** is set to 1, track animation will last 2 seconds; if set to 2, for 4 seconds. \| | Min Time | Lower limit of the playback range. | Max Time | Upper limit of the playback range. For example, setting **Min Time** to 0 and **Max Time** to 2 means that tracks playback will last 2 units. | Unit Time | Playback speed. It sets the duration of one unit in seconds. For example, if **Unit Time** is set to 1, track animation will last 2 seconds; if set to 2, for 4 seconds. |
|---|---|---|---|---|---|---|---|
| Min Time | Lower limit of the playback range. |  |  |  |  |  |  |
| Max Time | Upper limit of the playback range. For example, setting **Min Time** to 0 and **Max Time** to 2 means that tracks playback will last 2 units. |  |  |  |  |  |  |
| Unit Time | Playback speed. It sets the duration of one unit in seconds. For example, if **Unit Time** is set to 1, track animation will last 2 seconds; if set to 2, for 4 seconds. |  |  |  |  |  |  |
| From | The time to start tracks playback from. It is used to limit the playback to a specified range. |  |  |  |  |  |  |
| To | The time to stop tracks playback on. It is used to limit the playback to a specified range. |  |  |  |  |  |  |
| Time | The current animation track time. |  |  |  |  |  |  |
| ![](time_prev.png) | Go to the previous key frame. |  |  |  |  |  |  |
| ![](time_play.png) | Play all enabled tracks once. |  |  |  |  |  |  |
| ![](time_loop.png) | Play all enabled tracks in a loop. |  |  |  |  |  |  |
| ![](time_next.png) | Go to the next key frame. |  |  |  |  |  |  |


## Video Tutorial: Tracker Tool
