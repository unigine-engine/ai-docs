# AnimationSequencePlayer Class (CS)


A sequence player runs an [AnimationSequence](../../../../api/library/animations/timeline/class.animationsequence_cs.md) and writes its values into the scene. It is the playback machine of the [Sequencer](../../../../editor2/tools/sequencer/index.md): the transport controls, the time region, the per-instance retargeting and the event stream all live here. The [NodeSequencePlayer](../../../../api/library/nodes/class.nodesequenceplayer_cs.md) node is a thin wrapper over this class, and it hands out its player through the Player property.


One file is loaded once and shared by all players that use it, so a hundred lightweight players can run the same animation over different objects. A player is created from a path, from an asset GUID, or from a sequence built in memory, and it is reference counted, so it lives while anything holds it.


The bindings authored in the file work as they are. A player can also override them per instance: the bind table has one slot per bindable channel of the whole composition, nested sequences included, and a slot is addressed either by index or by the stable key of its channel. Look the index up by the channel name rather than counting slots. See the [Runtime Playback](../../../../editor2/tools/sequencer/runtime/index_cs.md) article for the whole picture.


## AnimationSequencePlayer Class

### Properties

## 🔒︎ bool Playing

The value indicating if the player is running its sequence.
## float Time

The position of the playhead, in seconds. The value is clamped to the time region, so setting a moment outside it parks the playhead on the nearest end.
## float TimeFrom

The start of the time region played by this player, in seconds. A negative value means the beginning of the sequence.
## float TimeTo

The end of the time region played by this player, in seconds. A negative value means the end of the sequence.
## float Speed

The speed the sequence is played at. A negative value plays it backwards, and a non-finite value is ignored. Until a speed is set here, the player follows the one saved in the sequence; [resetSpeed()](#resetSpeed_void) drops the override and hands the sequence its say back.
## 🔒︎ bool IsSpeedCustom

The value indicating if the playback speed is overridden on this player rather than taken from the sequence.
## bool Loop

The value indicating if the player starts the sequence over when it reaches the end of the time region. Until the flag is set here, the player follows the one saved in the sequence; [resetLoop()](#resetLoop_void) drops the override and hands the sequence its say back.
## 🔒︎ bool IsLoopCustom

The value indicating if the looping flag is overridden on this player rather than taken from the sequence.
## 🔒︎ float Duration

The duration of the sequence assigned to the player, in seconds. A player with no sequence reports zero.
## float Weight

The contribution of the whole sequence, clamped to the [0.0f, 1.0f] range. At one the sequence drives its targets as usual, below one the values are mixed back toward what they were before it took over, and at zero the targets are released to the gameplay logic underneath. Mixing values back needs a captured snapshot. Events keep firing at any weight, so a faded out sequence still drives game logic.
## bool AutoTick

The value indicating if the player is advanced by the engine every frame. With it switched off the player stands still until it is advanced by hand.
## AnimationSequence.ORIGINALS_RESTORE_MODE OriginalsRestoreMode

The restore mode for the original values of the animated parameters. Until a mode is set here, the player follows the one saved in the sequence.
## bool ProceduralMode

The value indicating if the player samples a sequence held in memory instead of the one loaded from an asset. Switching the mode off drops the sequence that was applied procedurally.
## 🔒︎ int BindCount

The number of slots in the bind table of the player. There is one slot per bindable channel of the whole composition, including the channels of nested sequences.
## 🔒︎ uint SequenceBindRevision

The stamp of the bindings authored in the root sequence, which changes whenever those bindings do. Code that caches slot indices can compare it against the value it saw last to tell whether the indices still hold. Overrides made on the player and edits inside nested sequences are not counted, and a player with no sequence reports zero.
## 🔒︎ Event<string, int, int, string> EventTriggered

The event triggered when the playhead reaches an event key of the sequence. The handler receives the name of the event, its payload, the phase it stands for (see [EVENT_PHASE](../../../../api/library/animations/timeline/class.animationchannel_cs.md#EVENT_PHASE_POINT)), and the placement path of the nested sequence the event came from. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience.
> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(string **name**, int **payload**, int **phase**, string **placement**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Triggered event handler
void triggered_event_handler(string name, int payload, int phase, string placement)
{
	Log.Message("\Handling Triggered event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections triggered_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventTriggered.Connect(triggered_event_connections, triggered_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventTriggered.Connect(triggered_event_connections, (string name, int payload, int phase, string placement) => {
		Log.Message("Handling Triggered event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
triggered_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Triggered event with a handler function
publisher.EventTriggered.Connect(triggered_event_handler);

// remove subscription to the Triggered event later by the handler function
publisher.EventTriggered.Disconnect(triggered_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection triggered_event_connection;

// subscribe to the Triggered event with a lambda handler function and keeping the connection
triggered_event_connection = publisher.EventTriggered.Connect((string name, int payload, int phase, string placement) => {
		Log.Message("Handling Triggered event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
triggered_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
triggered_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
triggered_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Triggered events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventTriggered.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventTriggered.Enabled = true;

```

</details>

## 🔒︎ Event<> EventFinished

The event triggered once when the player finishes a take, both when the sequence runs out and when it is stopped by hand. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience.
> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Finished event handler
void finished_event_handler()
{
	Log.Message("\Handling Finished event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections finished_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventFinished.Connect(finished_event_connections, finished_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventFinished.Connect(finished_event_connections, () => {
		Log.Message("Handling Finished event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
finished_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Finished event with a handler function
publisher.EventFinished.Connect(finished_event_handler);

// remove subscription to the Finished event later by the handler function
publisher.EventFinished.Disconnect(finished_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection finished_event_connection;

// subscribe to the Finished event with a lambda handler function and keeping the connection
finished_event_connection = publisher.EventFinished.Connect(() => {
		Log.Message("Handling Finished event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
finished_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
finished_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
finished_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Finished events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventFinished.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventFinished.Enabled = true;

```

</details>

### Members

---

## AnimationSequencePlayer ( string path )

Constructor. Creates a player for the sequence stored in the specified file.
### Arguments

- *string* **path** - Path to the `*.seq` file to be played.

## AnimationSequencePlayer ( UGUID file_guid )

Constructor. Creates a player for the sequence stored in the asset with the specified GUID.
### Arguments

- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **file_guid** - GUID of the `*.seq` asset to be played.

## AnimationSequencePlayer ( AnimationSequence seq )

Constructor. Creates a player that samples the specified sequence directly, with no file behind it. This is the procedural way of playing an animation built in memory.
### Arguments

- *[AnimationSequence](../../../../api/library/animations/timeline/class.animationsequence_cs.md)* **seq** - Sequence to be played.

## void Play ( )

Starts playing the sequence, or resumes it after a pause. A player parked on the end of its time region starts over from the opposite end, so a take always plays in full. A player with no sequence writes a warning to the log and stays idle.
## void Pause ( )

Pauses the playback, keeping the animated values as they are. The scene is not handed back, which is what tells a pause from a stop.
## void Stop ( )

Ends the take: the targets are handed back according to the restore mode, the events that are still open are closed, and the playhead returns to the start of the time region.
## void SetTimeRegion ( float from , float to )

Sets both ends of the played time region at once. The region is clamped to the duration of the sequence, and an end that comes before the start collapses the region to a single moment.
### Arguments

- *float* **from** - Start of the region, in seconds. A negative value means the beginning of the sequence.
- *float* **to** - End of the region, in seconds. A negative value means the end of the sequence.

## void ApplyCurrentFrame ( )

Writes the values of the current moment into the scene at once, without waiting for the next frame. This is the scrubbing path: set the time, apply, and the scene shows that moment.
## void Update ( float dt )

Advances the player by the specified time step. Use it when automatic ticking is switched off and the pace is driven by your own code.
### Arguments

- *float* **dt** - Time to advance the playhead by, in seconds.

## void ResetOriginalsRestoreMode ( )

Drops the restore mode set on the player, so that it follows the one saved in the sequence again.
## void ResetSpeed ( )

Drops the playback speed set on the player, so that it follows the one saved in the sequence again. A player handed another sequence then picks up the speed of the new file.
## void ResetLoop ( )

Drops the looping flag set on the player, so that it follows the one saved in the sequence again. A player handed another sequence then picks up the flag of the new file.
## bool HasSnapshot ( )

Returns a value indicating if the player holds a snapshot of the values the animated parameters had before it took them over.
### Return value

true if the player holds a snapshot of the original values; otherwise, false.
## void CaptureOriginals ( )

Captures the current values of every parameter the sequence can animate, so that they can be put back later. The snapshot covers the whole sequence rather than the current moment, and a second call is ignored while a snapshot is already held.
## void RestoreOriginals ( )

Puts the captured original values back into the scene.
## void ClearSnapshot ( )

Drops the captured snapshot without restoring anything, so the values the sequence applied last stay in the scene.
## void ApplySequenceProcedural ( AnimationSequence seq )

Hands the player a sequence held in memory and switches it to procedural mode. The bind table is rebuilt, as the new sequence brings its own channels.
### Arguments

- *[AnimationSequence](../../../../api/library/animations/timeline/class.animationsequence_cs.md)* **seq** - Sequence to be sampled by the player.

## bool HasSequence ( )

Returns a value indicating if the player has a sequence to play, either loaded from an asset or applied procedurally.
### Return value

true if the player has a sequence to play; otherwise, false.
## int GetBindChannelID ( int index )

Returns the channel the specified bind slot belongs to. Together with the sequence ID it forms the key that addresses the slot no matter how the table is renumbered.
### Arguments

- *int* **index** - Bind slot number.

### Return value

ID of the channel the slot belongs to.
## ulong GetBindSequenceID ( int index )

Returns the sequence placement the specified bind slot belongs to. Two placements of one nested sequence have IDs of their own, which is what keeps their bindings apart.
### Arguments

- *int* **index** - Bind slot number.

### Return value

ID of the sequence placement the slot belongs to. The root sequence has the ID of 0.
## string GetBindChannelName ( int index )

Returns the custom name of the channel the specified bind slot belongs to. This is the name the search by name works with.
### Arguments

- *int* **index** - Bind slot number.

### Return value

Custom name of the channel the slot belongs to.
## string GetBindPlacementPath ( int index )

Returns the placement path of the specified bind slot, which tells apart two instances of one sequence nested in the composition.
### Arguments

- *int* **index** - Bind slot number.

### Return value

Placement path of the slot.
## AnimationBind.TYPE GetBindType ( int index )

Returns the kind of binding the specified slot expects, which tells which [AnimationBind](../../../../api/library/animations/timeline/class.animationbind_cs.md) subclass fits it.
### Arguments

- *int* **index** - Bind slot number.

### Return value

Type of the binding the slot expects.
## int FindBind ( string placement_path , string name )

Searches the bind table for a slot by the channel name inside a certain placement. Use it when one name occurs in several instances of a nested sequence.
### Arguments

- *string* **placement_path** - Placement path of the nested sequence to search in.
- *string* **name** - Custom name of the channel.

### Return value

Bind slot number, or -1 if there is no such slot.
## int FindBindByName ( string name )

Searches the bind table for a slot by the custom name of its channel. This is the usual way to reach a slot, as counting slots by hand breaks as soon as the sequence is edited.
### Arguments

- *string* **name** - Custom name of the channel.

### Return value

Bind slot number, or -1 if there is no such slot.
## int FindBindByChannelID ( ulong seq_id , int channel_id )

Searches the bind table for a slot by the stable key of its channel.
### Arguments

- *ulong* **seq_id** - ID of the sequence placement. The root sequence has the ID of 0.
- *int* **channel_id** - Channel ID.

### Return value

Bind slot number, or -1 if there is no such slot.
## void InvalidateBinds ( )

Marks the bind table and the resolved targets as out of date, so that both are built anew before the next frame is applied.
## bool SetBind ( int index , AnimationBind bind )

Overrides the binding of the specified slot for this player alone. The asset is not touched, so the same file can drive different objects in different players.
### Arguments

- *int* **index** - Bind slot number.
- *[AnimationBind](../../../../api/library/animations/timeline/class.animationbind_cs.md)* **bind** - Binding to be used by this player.

### Return value

true if the binding was set; otherwise, false.
## void ResetBind ( int index )

Drops the override of the specified slot, so that the binding authored in the sequence takes over again.
### Arguments

- *int* **index** - Bind slot number.

## void ClearBinds ( )

Drops all bind overrides of the player at once.
## bool SetBindComponent ( int index , Node node , Property property )

Points the specified slot at a component of a node, which saves building an [AnimationBindComponent](../../../../api/library/animations/timeline/class.animationbindcomponent_cs.md) by hand for the common case.
### Arguments

- *int* **index** - Bind slot number.
- *[Node](../../../../api/library/nodes/class.node_cs.md)* **node** - Node the component is assigned to.
- *[Property](../../../../api/library/common/class.property_cs.md)* **property** - Property of the component.

### Return value

true if the binding was set; otherwise, false.
## AnimationBind GetActiveBind ( int index )

Returns the binding the specified slot works by: the override when there is one, and the binding authored in the sequence otherwise.
### Arguments

- *int* **index** - Bind slot number.

### Return value

Copy of the binding the slot works by.
## AnimationBind GetDefaultBind ( int index )

Returns the binding authored in the sequence for the specified slot, whether or not this player overrides it.
### Arguments

- *int* **index** - Bind slot number.

### Return value

Copy of the binding authored in the sequence.
## bool SetBindByKey ( ulong seq_id , int channel_id , AnimationBind bind )

Overrides a binding addressed by the stable key of its channel rather than by the slot number.
### Arguments

- *ulong* **seq_id** - ID of the sequence placement. The root sequence has the ID of 0.
- *int* **channel_id** - Channel ID.
- *[AnimationBind](../../../../api/library/animations/timeline/class.animationbind_cs.md)* **bind** - Binding to be used by this player.

### Return value

true if the binding was set; otherwise, false.
## void ResetBindByKey ( ulong seq_id , int channel_id )

Drops the override of the binding addressed by the stable key of its channel.
### Arguments

- *ulong* **seq_id** - ID of the sequence placement. The root sequence has the ID of 0.
- *int* **channel_id** - Channel ID.

## AnimationBind GetActiveBindByKey ( ulong seq_id , int channel_id )

Returns the binding the specified channel works by, addressed by its stable key.
### Arguments

- *ulong* **seq_id** - ID of the sequence placement. The root sequence has the ID of 0.
- *int* **channel_id** - Channel ID.

### Return value

Copy of the binding the channel works by.
## AnimationBind GetDefaultBindByKey ( ulong seq_id , int channel_id )

Returns the binding authored in the sequence for the specified channel, addressed by its stable key.
### Arguments

- *ulong* **seq_id** - ID of the sequence placement. The root sequence has the ID of 0.
- *int* **channel_id** - Channel ID.

### Return value

Copy of the binding authored in the sequence.
## int QueryActiveEventIntervals ( float time )

Collects the event intervals that are open at the specified moment and reports how many were found. It answers the question an event stream cannot: which states hold right now, for a player that joined the take in the middle. The collected intervals are then read one by one by their number.
### Arguments

- *float* **time** - Moment to be looked at, in seconds.

### Return value

Number of event intervals that cover the specified moment.
## string GetActiveEventIntervalName ( int i )

Returns the name of the event the collected interval belongs to.
### Arguments

- *int* **i** - Interval number in the list collected by the last query.

### Return value

Name of the event.
## int GetActiveEventIntervalPayload ( int i )

Returns the payload carried by the event the collected interval belongs to.
### Arguments

- *int* **i** - Interval number in the list collected by the last query.

### Return value

Payload of the event.
## string GetActiveEventIntervalPlacement ( int i )

Returns the placement path of the nested sequence the collected interval came from.
### Arguments

- *int* **i** - Interval number in the list collected by the last query.

### Return value

Placement path of the sequence the event came from.
## float GetActiveEventIntervalStart ( int i )

Returns the moment the collected interval opens at.
### Arguments

- *int* **i** - Interval number in the list collected by the last query.

### Return value

Moment the interval opens at, in seconds.
## float GetActiveEventIntervalEnd ( int i )

Returns the moment the collected interval closes at.
### Arguments

- *int* **i** - Interval number in the list collected by the last query.

### Return value

Moment the interval closes at, in seconds.
