# NodeAnimationPlayback Class (CS)

**Inherits from:** Node


This class is used to play animation [tracks](../../../principles/animations/index.md#animation_track) (`.utrack`). It enables you to clone animated objects in the hierarchy, as well as to convert prepared animations and objects into *NodeReferences*. Each *AnimationPlayback* node adds overrides for its internal [playback](../../../principles/animations/index.md#animation_playback) to [animation objects](../../../principles/animations/index.md#animation_object) (animation tracks are not copied).


## NodeAnimationPlayback Class

### Properties

## 🔒︎ bool IsPlaying

The value indicating if the playback is currently being played.
## bool Loop

The value indicating if the playback is looped.
## float Speed

The speed factor for the animation playback. This parameter enables you to control how fast the particular playback should be played giving you more flexibility and control (for example, you can use it for slow-motion effect).
## UGUID TrackFileGUID

The GUID of the `.utrack` file.
## string TrackPath

The path to the `.utrack` file.
## bool PlayOnEnable

The value indicating if the playback is started on enabling the node.
## bool RestartOnEnable

The value indicating if the playback is restarted on enabling the node.
## float TimeFrom

The playback start time, in seconds.
## float TimeTo

The playback end time, in seconds.
### Members

---

## NodeAnimationPlayback ( )

Constructor. Creates an instance of the class with default parameters.
## static int type ( )

Returns the type of the node.
### Return value

[NodeAnimationPlayback](../../../api/library/nodes/class.node_cs.md#NODE_ANIMATION_PLAYBACK) type identifier.
## void Play ( )

Plays the animation playback either from the start or from the moment when the playback was paused (see *[Pause()](../../...md#pause_void)*).
## void Pause ( )

Pauses the animation playback, so the playback can be resumed from this moment upon calling *[Play()](../../...md#play_void)*.
## void Stop ( )

Stops the animation playback.
## void SetTime ( float time , float from = -1.0f , float to = -1.0f )

Sets the current playback time, and optional from and to limits.
### Arguments

- *float* **time** - Current playback time to be set, in seconds.
- *float* **from** - Start time to be set, in seconds.
- *float* **to** - End time to be set, in seconds.

## float GetTime ( )

Returns the current playback time, in seconds.
### Return value

Current playback time, in seconds.
