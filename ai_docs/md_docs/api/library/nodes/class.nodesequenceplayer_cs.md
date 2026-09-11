# NodeSequencePlayer Class (CS)

**Inherits from:** Node


This node plays a `*.seq` animation authored in the [Sequencer](../../../editor2/tools/sequencer/index.md). Assign a sequence to it, and the node runs it in your application the same way it ran in the editor: transport, time region, speed and looping are node parameters, saved to the `*.world` file and carried onto clones.


Under the hood the node keeps an [AnimationSequencePlayer](../../../api/library/animations/timeline/class.animationsequenceplayer_cs.md) and ticks it itself. Reach that player through the Player property when you need per-instance retargeting, event subscription or anything else the node does not expose.


Assigning a sequence rebuilds the player from scratch. A sequence that cannot be resolved leaves the node with no player at all and writes a warning to the log, so a broken path shows up as an animation that never starts.


## NodeSequencePlayer Class

### Properties

## 🔒︎ bool Playing

The value indicating if the sequence is being played.
## float Time

The position of the playhead, in seconds. The value is clamped to the time region of the node.
## 🔒︎ float Duration

The duration of the sequence assigned to the node, in seconds. A node with no sequence reports zero.
## float TimeFrom

The start of the played time region, in seconds. A negative value means the beginning of the sequence.
## float TimeTo

The end of the played time region, in seconds. A negative value means the end of the sequence.
## bool Loop

The value indicating if the node starts the sequence over when it reaches the end of the time region.
## float Speed

The speed the sequence is played at. A negative value plays it backwards, so a value of -1.0f runs the animation in reverse at its normal pace.
## UGUID SequenceFileGUID

The GUID of the sequence asset assigned to the node. Assigning another GUID rebuilds the player, so the playhead returns to the beginning.
## string SequencePath

The path to the sequence file assigned to the node. The path is only a way to name the asset: it is resolved to a GUID at once, and the node keeps the GUID.
## 🔒︎ AnimationSequencePlayer Player

The player that runs the sequence of this node. Use it to reach what the node does not expose, such as per-instance bindings, playback weight and the event stream. A node with no sequence assigned has no player.
## bool PlayOnEnable

The value indicating if the sequence starts as soon as the node is enabled.
## bool RestartOnEnable

The value indicating if the playhead returns to the beginning every time the node is enabled. With it switched off a disabled node resumes from the moment it was paused at.
## bool UseCustomOriginalsRestoreMode

The value indicating if the node applies a restore mode of its own instead of the one saved in the sequence.
## AnimationSequence.ORIGINALS_RESTORE_MODE OriginalsRestoreMode

The restore mode for the original values of the animated parameters. It reaches the player only while the node is set to use a mode of its own.
### Members

---

## NodeSequencePlayer ( )

Constructor. Creates a sequence player node with no sequence assigned.
## static int type ( )

Returns the type of the node.
### Return value

[NodeSequencePlayer](../../../api/library/nodes/class.node_cs.md#NODE_SEQUENCE_PLAYER) type identifier.
## void Play ( )

Starts playing the sequence, or resumes it after a pause.
## void Pause ( )

Pauses the playback, keeping the animated values as they are.
## void Stop ( )

Ends the take: the animated parameters are handed back according to the restore mode, and the playhead returns to the start of the time region.
## void SetTimeRegion ( float from , float to )

Sets both ends of the played time region at once.
### Arguments

- *float* **from** - Start of the region, in seconds. A negative value means the beginning of the sequence.
- *float* **to** - End of the region, in seconds. A negative value means the end of the sequence.
