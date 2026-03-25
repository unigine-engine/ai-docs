# Animation Playback


An **Animation Playback** node plays back an animation track (`.utrack`) that can animate arbitrary node properties over time. Unlike [Skeleton Pose](../../../objects/animations/nodeskeletonpose/index.md), which is focused on skeletal animation, Animation Playback works with general property animation — transforms, material parameters, and other node properties.


The node binds to objects in the scene and drives their properties according to the keyframes recorded in the track file.


> **Notice:** This feature is currently **experimental**.


### See Also


- The *[NodeAnimationPlayback](../../../api/library/nodes/class.nodeanimationplayback_cpp.md)* class API reference
- The *[Skeleton Pose](../../../objects/animations/nodeskeletonpose/index.md)* node


## Adding an Animation Playback


To add an *Animation Playback* node to the scene via UnigineEditor:


1. On the Menu bar, click *Create -> Animation -> Animation Playback (EXPERIMENTAL)*.
2. Place the node in the world.
3. Assign a `.utrack` track file in the node parameters.


![](creating_animation_playback.png)


## Animation Track


Animation tracks are created in the [Tracker](../../../editor2/tools/tracker/basics/index.md) tool and stored as `.utrack` files containing keyframed curves for the properties of one or more scene objects. Before playback, a `.utrack` file is compiled into a `.uplay` runtime format.


## Animation Playback Parameters


![](animation_playback_parameters.png)


| Parameter | Description |
|---|---|
| Track File (.utrack) | The animation track file to be played. |
| Play / Pause / Stop | Playback controls. **Play** starts or resumes playback, **Pause** pauses at the current time, **Stop** stops and resets time to zero. |
| Loop | When enabled, the animation restarts from the beginning after reaching the end. |
| Play On Enable | Automatically start playback each time the node is enabled (from the moment it was paused). |
| Restart On Enable | Start playing from the beginning each time the node is enabled. |
| Time | Current playback time in seconds. |
| Speed | Playback speed multiplier (0.5 — 2× slower, 2.0 — 2× faster). |
| Time From | Start time of the playback range. Allows playing only a portion of the track. |
| Time To | End time of the playback range. |


## Converter


The *Converter* section provides tools for migrating legacy `.track` files to the new format.


| Parameter | Description |
|---|---|
| Tracks folder path | Path to a folder containing `.track` files to be converted into the `.utrack` format (relative to the `data` folder). If left blank, all track files in the `data` folder will be converted. |
| Track for playback | A specific `.track` file to be converted into the `.uplay` runtime format. The intermediate `.utrack` file is also created next to the original. |
| Convert | Start the conversion process. |
