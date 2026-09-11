# AnimationSequencePlayer Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


A sequence player runs an [AnimationSequence](../../../../api/library/animations/timeline/class.animationsequence_usc.md) and writes its values into the scene. It is the playback machine of the [Sequencer](../../../../editor2/tools/sequencer/index.md): the transport controls, the time region, the per-instance retargeting and the event stream all live here. The [NodeSequencePlayer](../../../../api/library/nodes/class.nodesequenceplayer_usc.md) node is a thin wrapper over this class, and it hands out its player through the Player property.


One file is loaded once and shared by all players that use it, so a hundred lightweight players can run the same animation over different objects. A player is created from a path, from an asset GUID, or from a sequence built in memory, and it is reference counted, so it lives while anything holds it.


The bindings authored in the file work as they are. A player can also override them per instance: the bind table has one slot per bindable channel of the whole composition, nested sequences included, and a slot is addressed either by index or by the stable key of its channel. Look the index up by the channel name rather than counting slots. See the [Runtime Playback](../../../../editor2/tools/sequencer/runtime/index.md) article for the whole picture.


## AnimationSequencePlayer Class

### Members

## int isPlaying () const

Returns the current value indicating if the player is running its sequence.
### Return value

Current the player is running its sequence
## void setTime ( float time )

Sets a new position of the playhead, in seconds. The value is clamped to the time region, so setting a moment outside it parks the playhead on the nearest end.
### Arguments

- *float* **time** - The position of the playhead, in seconds

## float getTime () const

Returns the current position of the playhead, in seconds. The value is clamped to the time region, so setting a moment outside it parks the playhead on the nearest end.
### Return value

Current position of the playhead, in seconds
## void setTimeFrom ( float from )

Sets a new start of the time region played by this player, in seconds. A negative value means the beginning of the sequence.
### Arguments

- *float* **from** - The start of the time region, in seconds

## float getTimeFrom () const

Returns the current start of the time region played by this player, in seconds. A negative value means the beginning of the sequence.
### Return value

Current start of the time region, in seconds
## void setTimeTo ( float to )

Sets a new end of the time region played by this player, in seconds. A negative value means the end of the sequence.
### Arguments

- *float* **to** - The end of the time region, in seconds

## float getTimeTo () const

Returns the current end of the time region played by this player, in seconds. A negative value means the end of the sequence.
### Return value

Current end of the time region, in seconds
## void setSpeed ( float speed )

Sets a new speed the sequence is played at. A negative value plays it backwards, and a non-finite value is ignored. Until a speed is set here, the player follows the one saved in the sequence; [resetSpeed()](#resetSpeed_void) drops the override and hands the sequence its say back.
### Arguments

- *float* **speed** - The playback speed multiplier

## float getSpeed () const

Returns the current speed the sequence is played at. A negative value plays it backwards, and a non-finite value is ignored. Until a speed is set here, the player follows the one saved in the sequence; [resetSpeed()](#resetSpeed_void) drops the override and hands the sequence its say back.
### Return value

Current playback speed multiplier
## int isSpeedCustom () const

Returns the current value indicating if the playback speed is overridden on this player rather than taken from the sequence.
### Return value

Current the playback speed is overridden on this player
## void setLoop ( int loop )

Sets a new value indicating if the player starts the sequence over when it reaches the end of the time region. Until the flag is set here, the player follows the one saved in the sequence; [resetLoop()](#resetLoop_void) drops the override and hands the sequence its say back.
### Arguments

- *int* **loop** - The looping

## int isLoop () const

Returns the current value indicating if the player starts the sequence over when it reaches the end of the time region. Until the flag is set here, the player follows the one saved in the sequence; [resetLoop()](#resetLoop_void) drops the override and hands the sequence its say back.
### Return value

Current looping
## int isLoopCustom () const

Returns the current value indicating if the looping flag is overridden on this player rather than taken from the sequence.
### Return value

Current the looping flag is overridden on this player
## float getDuration () const

Returns the current duration of the sequence assigned to the player, in seconds. A player with no sequence reports zero.
### Return value

Current duration of the sequence, in seconds
## void setWeight ( float weight )

Sets a new contribution of the whole sequence, clamped to the [0.0f, 1.0f] range. At one the sequence drives its targets as usual, below one the values are mixed back toward what they were before it took over, and at zero the targets are released to the gameplay logic underneath. Mixing values back needs a captured snapshot. Events keep firing at any weight, so a faded out sequence still drives game logic.
### Arguments

- *float* **weight** - The contribution of the whole sequence, in the [0.0f, 1.0f] range

## float getWeight () const

Returns the current contribution of the whole sequence, clamped to the [0.0f, 1.0f] range. At one the sequence drives its targets as usual, below one the values are mixed back toward what they were before it took over, and at zero the targets are released to the gameplay logic underneath. Mixing values back needs a captured snapshot. Events keep firing at any weight, so a faded out sequence still drives game logic.
### Return value

Current contribution of the whole sequence, in the [0.0f, 1.0f] range
## void setAutoTick ( int tick )

Sets a new value indicating if the player is advanced by the engine every frame. With it switched off the player stands still until it is advanced by hand.
### Arguments

- *int* **tick** - The automatic ticking

## int isAutoTick () const

Returns the current value indicating if the player is advanced by the engine every frame. With it switched off the player stands still until it is advanced by hand.
### Return value

Current automatic ticking
## void setOriginalsRestoreMode ( int mode )

Sets a new restore mode for the original values of the animated parameters. Until a mode is set here, the player follows the one saved in the sequence.
### Arguments

- *int* **mode** - The restore mode for the original values

## int getOriginalsRestoreMode () const

Returns the current restore mode for the original values of the animated parameters. Until a mode is set here, the player follows the one saved in the sequence.
### Return value

Current restore mode for the original values
## void setProceduralMode ( int mode )

Sets a new value indicating if the player samples a sequence held in memory instead of the one loaded from an asset. Switching the mode off drops the sequence that was applied procedurally.
### Arguments

- *int* **mode** - The procedural mode

## int isProceduralMode () const

Returns the current value indicating if the player samples a sequence held in memory instead of the one loaded from an asset. Switching the mode off drops the sequence that was applied procedurally.
### Return value

Current procedural mode
## int getBindCount () const

Returns the current number of slots in the bind table of the player. There is one slot per bindable channel of the whole composition, including the channels of nested sequences.
### Return value

Current number of slots in the bind table
## int getSequenceBindRevision () const

Returns the current stamp of the bindings authored in the root sequence, which changes whenever those bindings do. Code that caches slot indices can compare it against the value it saw last to tell whether the indices still hold. Overrides made on the player and edits inside nested sequences are not counted, and a player with no sequence reports zero.
### Return value

Current stamp of the bindings authored in the root sequence
## getEventTriggered () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## Event<> getEventFinished () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
---

## AnimationSequencePlayer ( string path )

Constructor. Creates a player for the sequence stored in the specified file.
### Arguments

- *string* **path** - Path to the `*.seq` file to be played.

## void play ( )

Starts playing the sequence, or resumes it after a pause. A player parked on the end of its time region starts over from the opposite end, so a take always plays in full. A player with no sequence writes a warning to the log and stays idle.
## void pause ( )

Pauses the playback, keeping the animated values as they are. The scene is not handed back, which is what tells a pause from a stop.
## void stop ( )

Ends the take: the targets are handed back according to the restore mode, the events that are still open are closed, and the playhead returns to the start of the time region.
## void setTimeRegion ( float from , float to )

Sets both ends of the played time region at once. The region is clamped to the duration of the sequence, and an end that comes before the start collapses the region to a single moment.
### Arguments

- *float* **from** - Start of the region, in seconds. A negative value means the beginning of the sequence.
- *float* **to** - End of the region, in seconds. A negative value means the end of the sequence.

## void applyCurrentFrame ( )

Writes the values of the current moment into the scene at once, without waiting for the next frame. This is the scrubbing path: set the time, apply, and the scene shows that moment.
## void update ( float dt )

Advances the player by the specified time step. Use it when automatic ticking is switched off and the pace is driven by your own code.
### Arguments

- *float* **dt** - Time to advance the playhead by, in seconds.

## void resetOriginalsRestoreMode ( )

Drops the restore mode set on the player, so that it follows the one saved in the sequence again.
## void resetSpeed ( )

Drops the playback speed set on the player, so that it follows the one saved in the sequence again. A player handed another sequence then picks up the speed of the new file.
## void resetLoop ( )

Drops the looping flag set on the player, so that it follows the one saved in the sequence again. A player handed another sequence then picks up the flag of the new file.
## int hasSnapshot ( )

Returns a value indicating if the player holds a snapshot of the values the animated parameters had before it took them over.
### Return value

**1** if the player holds a snapshot of the original values; otherwise, **0**.
## void captureOriginals ( )

Captures the current values of every parameter the sequence can animate, so that they can be put back later. The snapshot covers the whole sequence rather than the current moment, and a second call is ignored while a snapshot is already held.
## void restoreOriginals ( )

Puts the captured original values back into the scene.
## void clearSnapshot ( )

Drops the captured snapshot without restoring anything, so the values the sequence applied last stay in the scene.
## void applySequenceProcedural ( AnimationSequence seq )

Hands the player a sequence held in memory and switches it to procedural mode. The bind table is rebuilt, as the new sequence brings its own channels.
### Arguments

- *AnimationSequence* **seq** - Sequence to be sampled by the player.

## int hasSequence ( )

Returns a value indicating if the player has a sequence to play, either loaded from an asset or applied procedurally.
### Return value

**1** if the player has a sequence to play; otherwise, **0**.
## int getBindChannelID ( int index )

Returns the channel the specified bind slot belongs to. Together with the sequence ID it forms the key that addresses the slot no matter how the table is renumbered.
### Arguments

- *int* **index** - Bind slot number.

### Return value

ID of the channel the slot belongs to.
## long getBindSequenceID ( int index )

Returns the sequence placement the specified bind slot belongs to. Two placements of one nested sequence have IDs of their own, which is what keeps their bindings apart.
### Arguments

- *int* **index** - Bind slot number.

### Return value

ID of the sequence placement the slot belongs to. The root sequence has the ID of 0.
## string getBindChannelName ( int index )

Returns the custom name of the channel the specified bind slot belongs to. This is the name the search by name works with.
### Arguments

- *int* **index** - Bind slot number.

### Return value

Custom name of the channel the slot belongs to.
## string getBindPlacementPath ( int index )

Returns the placement path of the specified bind slot, which tells apart two instances of one sequence nested in the composition.
### Arguments

- *int* **index** - Bind slot number.

### Return value

Placement path of the slot.
## int getBindType ( int index )

Returns the kind of binding the specified slot expects, which tells which [AnimationBind](../../../../api/library/animations/timeline/class.animationbind_usc.md) subclass fits it.
### Arguments

- *int* **index** - Bind slot number.

### Return value

Type of the binding the slot expects.
## int findBind ( string placement_path , string name )

Searches the bind table for a slot by the channel name inside a certain placement. Use it when one name occurs in several instances of a nested sequence.
### Arguments

- *string* **placement_path** - Placement path of the nested sequence to search in.
- *string* **name** - Custom name of the channel.

### Return value

Bind slot number, or -1 if there is no such slot.
## int findBindByName ( string name )

Searches the bind table for a slot by the custom name of its channel. This is the usual way to reach a slot, as counting slots by hand breaks as soon as the sequence is edited.
### Arguments

- *string* **name** - Custom name of the channel.

### Return value

Bind slot number, or -1 if there is no such slot.
## int findBindByChannelID ( long seq_id , int channel_id )

Searches the bind table for a slot by the stable key of its channel.
### Arguments

- *long* **seq_id** - ID of the sequence placement. The root sequence has the ID of 0.
- *int* **channel_id** - Channel ID.

### Return value

Bind slot number, or -1 if there is no such slot.
## void invalidateBinds ( )

Marks the bind table and the resolved targets as out of date, so that both are built anew before the next frame is applied.
## int setBind ( int index , AnimationBind bind )

Overrides the binding of the specified slot for this player alone. The asset is not touched, so the same file can drive different objects in different players.
### Arguments

- *int* **index** - Bind slot number.
- *AnimationBind* **bind** - Binding to be used by this player.

### Return value

**1** if the binding was set; otherwise, **0**.
## void resetBind ( int index )

Drops the override of the specified slot, so that the binding authored in the sequence takes over again.
### Arguments

- *int* **index** - Bind slot number.

## void clearBinds ( )

Drops all bind overrides of the player at once.
## int setBindComponent ( int index , Node node , Property property )

Points the specified slot at a component of a node, which saves building an [AnimationBindComponent](../../../../api/library/animations/timeline/class.animationbindcomponent_usc.md) by hand for the common case.
### Arguments

- *int* **index** - Bind slot number.
- *[Node](../../../../api/library/nodes/class.node_usc.md)* **node** - Node the component is assigned to.
- *[Property](../../../../api/library/common/class.property_usc.md)* **property** - Property of the component.

### Return value

**1** if the binding was set; otherwise, **0**.
## AnimationBind getActiveBind ( int index )

Returns the binding the specified slot works by: the override when there is one, and the binding authored in the sequence otherwise.
### Arguments

- *int* **index** - Bind slot number.

### Return value

Copy of the binding the slot works by.
## AnimationBind getDefaultBind ( int index )

Returns the binding authored in the sequence for the specified slot, whether or not this player overrides it.
### Arguments

- *int* **index** - Bind slot number.

### Return value

Copy of the binding authored in the sequence.
## int setBindByKey ( long seq_id , int channel_id , AnimationBind bind )

Overrides a binding addressed by the stable key of its channel rather than by the slot number.
### Arguments

- *long* **seq_id** - ID of the sequence placement. The root sequence has the ID of 0.
- *int* **channel_id** - Channel ID.
- *AnimationBind* **bind** - Binding to be used by this player.

### Return value

**1** if the binding was set; otherwise, **0**.
## void resetBindByKey ( long seq_id , int channel_id )

Drops the override of the binding addressed by the stable key of its channel.
### Arguments

- *long* **seq_id** - ID of the sequence placement. The root sequence has the ID of 0.
- *int* **channel_id** - Channel ID.

## AnimationBind getActiveBindByKey ( long seq_id , int channel_id )

Returns the binding the specified channel works by, addressed by its stable key.
### Arguments

- *long* **seq_id** - ID of the sequence placement. The root sequence has the ID of 0.
- *int* **channel_id** - Channel ID.

### Return value

Copy of the binding the channel works by.
## AnimationBind getDefaultBindByKey ( long seq_id , int channel_id )

Returns the binding authored in the sequence for the specified channel, addressed by its stable key.
### Arguments

- *long* **seq_id** - ID of the sequence placement. The root sequence has the ID of 0.
- *int* **channel_id** - Channel ID.

### Return value

Copy of the binding authored in the sequence.
## int queryActiveEventIntervals ( float time )

Collects the event intervals that are open at the specified moment and reports how many were found. It answers the question an event stream cannot: which states hold right now, for a player that joined the take in the middle. The collected intervals are then read one by one by their number.
### Arguments

- *float* **time** - Moment to be looked at, in seconds.

### Return value

Number of event intervals that cover the specified moment.
## string getActiveEventIntervalName ( int i )

Returns the name of the event the collected interval belongs to.
### Arguments

- *int* **i** - Interval number in the list collected by the last query.

### Return value

Name of the event.
## int getActiveEventIntervalPayload ( int i )

Returns the payload carried by the event the collected interval belongs to.
### Arguments

- *int* **i** - Interval number in the list collected by the last query.

### Return value

Payload of the event.
## string getActiveEventIntervalPlacement ( int i )

Returns the placement path of the nested sequence the collected interval came from.
### Arguments

- *int* **i** - Interval number in the list collected by the last query.

### Return value

Placement path of the sequence the event came from.
## float getActiveEventIntervalStart ( int i )

Returns the moment the collected interval opens at.
### Arguments

- *int* **i** - Interval number in the list collected by the last query.

### Return value

Moment the interval opens at, in seconds.
## float getActiveEventIntervalEnd ( int i )

Returns the moment the collected interval closes at.
### Arguments

- *int* **i** - Interval number in the list collected by the last query.

### Return value

Moment the interval closes at, in seconds.
