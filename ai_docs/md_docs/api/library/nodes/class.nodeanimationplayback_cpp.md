# NodeAnimationPlayback Class (CPP)

**Header:** #include <UnigineNodes.h>

**Inherits from:** Node


This class is used to play animation [tracks](../../../principles/animations/index.md#animation_track) (`.utrack`). It enables you to clone animated objects in the hierarchy, as well as to convert prepared animations and objects into *NodeReferences*. Each *AnimationPlayback* node adds overrides for its internal [playback](../../../principles/animations/index.md#animation_playback) to [animation objects](../../../principles/animations/index.md#animation_object) (animation tracks are not copied).


## NodeAnimationPlayback Class

### Members

## bool isPlaying () const

Returns the current value indicating if the playback is currently being played.
### Return value

**true** if the playback is currently being played; otherwise **false**.
## void setLoop ( bool loop )

Sets a new value indicating if the playback is looped.
### Arguments

- *bool* **loop** - Set **true** to enable the playback is looped; **false** - to disable it.

## bool isLoop () const

Returns the current value indicating if the playback is looped.
### Return value

**true** if the playback is looped; otherwise **false**.
## void setSpeed ( float speed )

Sets a new speed factor for the animation playback. This parameter enables you to control how fast the particular playback should be played giving you more flexibility and control (for example, you can use it for slow-motion effect).
### Arguments

- *float* **speed** - The playback speed factor (the value of 2 means that the track is played 2 times faster, while 0.5f will slow it down 2 times).

## float getSpeed () const

Returns the current speed factor for the animation playback. This parameter enables you to control how fast the particular playback should be played giving you more flexibility and control (for example, you can use it for slow-motion effect).
### Return value

Current playback speed factor (the value of 2 means that the track is played 2 times faster, while 0.5f will slow it down 2 times).
## void setTrackFileGUID ( const UGUID & guid )

Sets a new GUID of the `.utrack` file.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - The GUID of the `.utrack` file.

## const UGUID & getTrackFileGUID () const

Returns the current GUID of the `.utrack` file.
### Return value

Current GUID of the `.utrack` file.
## void setTrackPath ( const char * path )

Sets a new path to the `.utrack` file.
### Arguments

- *const char ** **path** - The path to the `.utrack` file.

## const char * getTrackPath () const

Returns the current path to the `.utrack` file.
### Return value

Current path to the `.utrack` file.
## void setPlayOnEnable ( bool enable )

Sets a new value indicating if the playback is started on enabling the node.
### Arguments

- *bool* **enable** - Set **true** to enable the playback is resumed on enabling the node; **false** - to disable it.

## bool isPlayOnEnable () const

Returns the current value indicating if the playback is started on enabling the node.
### Return value

**true** if the playback is resumed on enabling the node; otherwise **false**.
## void setRestartOnEnable ( bool enable )

Sets a new value indicating if the playback is restarted on enabling the node.
### Arguments

- *bool* **enable** - Set **true** to enable the playback is restarted on enabling the node; **false** - to disable it.

## bool isRestartOnEnable () const

Returns the current value indicating if the playback is restarted on enabling the node.
### Return value

**true** if the playback is restarted on enabling the node; otherwise **false**.
## void setTimeFrom ( float from )

Sets a new playback start time, in seconds.
### Arguments

- *float* **from** - The playback start time, in seconds.

## float getTimeFrom () const

Returns the current playback start time, in seconds.
### Return value

Current playback start time, in seconds.
## void setTimeTo ( float to )

Sets a new playback end time, in seconds.
### Arguments

- *float* **to** - The playback end time, in seconds.

## float getTimeTo () const

Returns the current playback end time, in seconds.
### Return value

Current playback end time, in seconds.
---

## static NodeAnimationPlaybackPtr create ( )

Constructor. Creates an instance of the class with default parameters.
## static int type ( )

Returns the type of the node.
### Return value

[NodeAnimationPlayback](../../../api/library/nodes/class.node_cpp.md#NODE_ANIMATION_PLAYBACK) type identifier.
## void play ( )

Plays the animation playback either from the start or from the moment when the playback was paused (see *[pause()](../../...md#pause_void)*).
## void pause ( )

Pauses the animation playback, so the playback can be resumed from this moment upon calling *[play()](../../...md#play_void)*.
## void stop ( )

Stops the animation playback.
## void setTime ( float time , float from = -1.0f , float to = -1.0f )

Sets the current playback time, and optional from and to limits.
### Arguments

- *float* **time** - Current playback time to be set, in seconds.
- *float* **from** - Start time to be set, in seconds.
- *float* **to** - End time to be set, in seconds.

## float getTime ( ) const

Returns the current playback time, in seconds.
### Return value

Current playback time, in seconds.
