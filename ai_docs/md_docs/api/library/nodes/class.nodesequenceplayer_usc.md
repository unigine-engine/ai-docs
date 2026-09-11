# NodeSequencePlayer Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Node


This node plays a `*.seq` animation authored in the [Sequencer](../../../editor2/tools/sequencer/index.md). Assign a sequence to it, and the node runs it in your application the same way it ran in the editor: transport, time region, speed and looping are node parameters, saved to the `*.world` file and carried onto clones.


Under the hood the node keeps an [AnimationSequencePlayer](../../../api/library/animations/timeline/class.animationsequenceplayer_usc.md) and ticks it itself. Reach that player through the Player property when you need per-instance retargeting, event subscription or anything else the node does not expose.


Assigning a sequence rebuilds the player from scratch. A sequence that cannot be resolved leaves the node with no player at all and writes a warning to the log, so a broken path shows up as an animation that never starts.


## NodeSequencePlayer Class

### Members

## int isPlaying () const

Returns the current value indicating if the sequence is being played.
### Return value

Current the sequence is being played
## void setTime ( float time )

Sets a new position of the playhead, in seconds. The value is clamped to the time region of the node.
### Arguments

- *float* **time** - The position of the playhead, in seconds

## float getTime () const

Returns the current position of the playhead, in seconds. The value is clamped to the time region of the node.
### Return value

Current position of the playhead, in seconds
## float getDuration () const

Returns the current duration of the sequence assigned to the node, in seconds. A node with no sequence reports zero.
### Return value

Current duration of the assigned sequence, in seconds
## void setTimeFrom ( float from )

Sets a new start of the played time region, in seconds. A negative value means the beginning of the sequence.
### Arguments

- *float* **from** - The start of the played time region, in seconds

## float getTimeFrom () const

Returns the current start of the played time region, in seconds. A negative value means the beginning of the sequence.
### Return value

Current start of the played time region, in seconds
## void setTimeTo ( float to )

Sets a new end of the played time region, in seconds. A negative value means the end of the sequence.
### Arguments

- *float* **to** - The end of the played time region, in seconds

## float getTimeTo () const

Returns the current end of the played time region, in seconds. A negative value means the end of the sequence.
### Return value

Current end of the played time region, in seconds
## void setLoop ( int loop )

Sets a new value indicating if the node starts the sequence over when it reaches the end of the time region.
### Arguments

- *int* **loop** - The looping

## int isLoop () const

Returns the current value indicating if the node starts the sequence over when it reaches the end of the time region.
### Return value

Current looping
## void setSpeed ( float speed )

Sets a new speed the sequence is played at. A negative value plays it backwards, so a value of -1.0f runs the animation in reverse at its normal pace.
### Arguments

- *float* **speed** - The playback speed multiplier

## float getSpeed () const

Returns the current speed the sequence is played at. A negative value plays it backwards, so a value of -1.0f runs the animation in reverse at its normal pace.
### Return value

Current playback speed multiplier
## void setSequenceFileGUID ( UGUID guid )

Sets a new GUID of the sequence asset assigned to the node. Assigning another GUID rebuilds the player, so the playhead returns to the beginning.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **guid** - The GUID of the assigned sequence asset

## UGUID getSequenceFileGUID () const

Returns the current GUID of the sequence asset assigned to the node. Assigning another GUID rebuilds the player, so the playhead returns to the beginning.
### Return value

Current GUID of the assigned sequence asset
## void setSequencePath ( string path )

Sets a new path to the sequence file assigned to the node. The path is only a way to name the asset: it is resolved to a GUID at once, and the node keeps the GUID.
### Arguments

- *string* **path** - The path to the assigned sequence file

## const char * getSequencePath () const

Returns the current path to the sequence file assigned to the node. The path is only a way to name the asset: it is resolved to a GUID at once, and the node keeps the GUID.
### Return value

Current path to the assigned sequence file
## getPlayer () const

Returns the current player that runs the sequence of this node. Use it to reach what the node does not expose, such as per-instance bindings, playback weight and the event stream. A node with no sequence assigned has no player.
### Return value

Current player that runs the sequence of this node
## void setPlayOnEnable ( int enable )

Sets a new value indicating if the sequence starts as soon as the node is enabled.
### Arguments

- *int* **enable** - The the sequence starts as soon as the node is enabled

## int isPlayOnEnable () const

Returns the current value indicating if the sequence starts as soon as the node is enabled.
### Return value

Current the sequence starts as soon as the node is enabled
## void setRestartOnEnable ( int enable )

Sets a new value indicating if the playhead returns to the beginning every time the node is enabled. With it switched off a disabled node resumes from the moment it was paused at.
### Arguments

- *int* **enable** - The the playhead returns to the beginning every time the node is enabled

## int isRestartOnEnable () const

Returns the current value indicating if the playhead returns to the beginning every time the node is enabled. With it switched off a disabled node resumes from the moment it was paused at.
### Return value

Current the playhead returns to the beginning every time the node is enabled
## void setUseCustomOriginalsRestoreMode ( int mode )

Sets a new value indicating if the node applies a restore mode of its own instead of the one saved in the sequence.
### Arguments

- *int* **mode** - The the restore mode of the node

## int isUseCustomOriginalsRestoreMode () const

Returns the current value indicating if the node applies a restore mode of its own instead of the one saved in the sequence.
### Return value

Current the restore mode of the node
## void setOriginalsRestoreMode ( int mode )

Sets a new restore mode for the original values of the animated parameters. It reaches the player only while the node is set to use a mode of its own.
### Arguments

- *int* **mode** - The restore mode for the original values

## int getOriginalsRestoreMode () const

Returns the current restore mode for the original values of the animated parameters. It reaches the player only while the node is set to use a mode of its own.
### Return value

Current restore mode for the original values
---

## static NodeSequencePlayer ( )

Constructor. Creates a sequence player node with no sequence assigned.
## static int type ( )

Returns the type of the node.
### Return value

[NodeSequencePlayer](../../../api/library/nodes/class.node_usc.md#NODE_SEQUENCE_PLAYER) type identifier.
## void play ( )

Starts playing the sequence, or resumes it after a pause.
## void pause ( )

Pauses the playback, keeping the animated values as they are.
## void stop ( )

Ends the take: the animated parameters are handed back according to the restore mode, and the playhead returns to the start of the time region.
## void setTimeRegion ( float from , float to )

Sets both ends of the played time region at once.
### Arguments

- *float* **from** - Start of the region, in seconds. A negative value means the beginning of the sequence.
- *float* **to** - End of the region, in seconds. A negative value means the end of the sequence.
