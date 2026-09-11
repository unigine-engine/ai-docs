# AnimationSequencePlayer Class (CPP)

**Header:** #include <UnigineAnimation.h>


A sequence player runs an [AnimationSequence](../../../../api/library/animations/timeline/class.animationsequence_cpp.md) and writes its values into the scene. It is the playback machine of the [Sequencer](../../../../editor2/tools/sequencer/index.md): the transport controls, the time region, the per-instance retargeting and the event stream all live here. The [NodeSequencePlayer](../../../../api/library/nodes/class.nodesequenceplayer_cpp.md) node is a thin wrapper over this class, and it hands out its player through the Player property.


One file is loaded once and shared by all players that use it, so a hundred lightweight players can run the same animation over different objects. A player is created from a path, from an asset GUID, or from a sequence built in memory, and it is reference counted, so it lives while anything holds it.


The bindings authored in the file work as they are. A player can also override them per instance: the bind table has one slot per bindable channel of the whole composition, nested sequences included, and a slot is addressed either by index or by the stable key of its channel. Look the index up by the channel name rather than counting slots. See the [Runtime Playback](../../../../editor2/tools/sequencer/runtime/index_cpp.md) article for the whole picture.


## AnimationSequencePlayer Class

### Members

## bool isPlaying () const

Returns the current value indicating if the player is running its sequence.
### Return value

**true** if the player is running its sequence; otherwise **false**.
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
## bool isSpeedCustom () const

Returns the current value indicating if the playback speed is overridden on this player rather than taken from the sequence.
### Return value

**true** if the playback speed is overridden on this player; otherwise **false**.
## void setLoop ( bool loop )

Sets a new value indicating if the player starts the sequence over when it reaches the end of the time region. Until the flag is set here, the player follows the one saved in the sequence; [resetLoop()](#resetLoop_void) drops the override and hands the sequence its say back.
### Arguments

- *bool* **loop** - Set **true** to enable looping; **false** - to disable it.

## bool isLoop () const

Returns the current value indicating if the player starts the sequence over when it reaches the end of the time region. Until the flag is set here, the player follows the one saved in the sequence; [resetLoop()](#resetLoop_void) drops the override and hands the sequence its say back.
### Return value

**true** if looping is enabled ; otherwise **false**.
## bool isLoopCustom () const

Returns the current value indicating if the looping flag is overridden on this player rather than taken from the sequence.
### Return value

**true** if the looping flag is overridden on this player; otherwise **false**.
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
## void setAutoTick ( bool tick )

Sets a new value indicating if the player is advanced by the engine every frame. With it switched off the player stands still until it is advanced by hand.
### Arguments

- *bool* **tick** - Set **true** to enable automatic ticking; **false** - to disable it.

## bool isAutoTick () const

Returns the current value indicating if the player is advanced by the engine every frame. With it switched off the player stands still until it is advanced by hand.
### Return value

**true** if automatic ticking is enabled ; otherwise **false**.
## void setOriginalsRestoreMode ( AnimationSequence::ORIGINALS_RESTORE_MODE mode )

Sets a new restore mode for the original values of the animated parameters. Until a mode is set here, the player follows the one saved in the sequence.
### Arguments

- *[AnimationSequence::ORIGINALS_RESTORE_MODE](../../../../api/library/animations/timeline/class.animationsequence_cpp.md#ORIGINALS_RESTORE_MODE)* **mode** - The restore mode for the original values

## AnimationSequence::ORIGINALS_RESTORE_MODE getOriginalsRestoreMode () const

Returns the current restore mode for the original values of the animated parameters. Until a mode is set here, the player follows the one saved in the sequence.
### Return value

Current restore mode for the original values
## void setProceduralMode ( bool mode )

Sets a new value indicating if the player samples a sequence held in memory instead of the one loaded from an asset. Switching the mode off drops the sequence that was applied procedurally.
### Arguments

- *bool* **mode** - Set **true** to enable procedural mode; **false** - to disable it.

## bool isProceduralMode () const

Returns the current value indicating if the player samples a sequence held in memory instead of the one loaded from an asset. Switching the mode off drops the sequence that was applied procedurally.
### Return value

**true** if procedural mode is enabled ; otherwise **false**.
## int getBindCount () const

Returns the current number of slots in the bind table of the player. There is one slot per bindable channel of the whole composition, including the channels of nested sequences.
### Return value

Current number of slots in the bind table
## unsigned int getSequenceBindRevision () const

Returns the current stamp of the bindings authored in the root sequence, which changes whenever those bindings do. Code that caches slot indices can compare it against the value it saw last to tell whether the indices still hold. Overrides made on the player and edits inside nested sequences are not counted, and a player with no sequence reports zero.
### Return value

Current stamp of the bindings authored in the root sequence
## Event<const char *, int, int, const char *> getEventTriggered () const

event triggered when the playhead reaches an event key of the sequence. The handler receives the name of the event, its payload, the phase it stands for (see [EVENT_PHASE](../../../../api/library/animations/timeline/class.animationchannel_cpp.md#EVENT_PHASE_POINT)), and the placement path of the nested sequence the event came from. You can subscribe to events via *connect()* and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cpp.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cpp.md)* classes for convenience.
> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const char * **name**, int **payload**, int **phase**, const char * **placement**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Triggered event handler
void triggered_event_handler(const char * name, int payload, int phase, const char * placement)
{
	Log::message("\Handling Triggered event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections triggered_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventTriggered().connect(triggered_event_connections, triggered_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventTriggered().connect(triggered_event_connections, [](const char * name, int payload, int phase, const char * placement) {
		Log::message("\Handling Triggered event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
triggered_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection triggered_event_connection;

// subscribe to the Triggered event with a handler function keeping the connection
publisher->getEventTriggered().connect(triggered_event_connection, triggered_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
triggered_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
triggered_event_connection.setEnabled(true);

// ...

// remove subscription to the Triggered event via the connection
triggered_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A Triggered event handler implemented as a class member
	void event_handler(const char * name, int payload, int phase, const char * placement)
	{
		Log::message("\Handling Triggered event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventTriggered().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId triggered_handler_id;

// subscribe to the Triggered event with a lambda handler function and keeping connection ID
triggered_handler_id = publisher->getEventTriggered().connect(e_connections, [](const char * name, int payload, int phase, const char * placement) {
		Log::message("\Handling Triggered event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventTriggered().disconnect(triggered_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Triggered events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventTriggered().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventTriggered().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventFinished () const

event triggered once when the player finishes a take, both when the sequence runs out and when it is stopped by hand. You can subscribe to events via *connect()* and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cpp.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cpp.md)* classes for convenience.
> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Finished event handler
void finished_event_handler()
{
	Log::message("\Handling Finished event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections finished_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventFinished().connect(finished_event_connections, finished_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventFinished().connect(finished_event_connections, []() {
		Log::message("\Handling Finished event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
finished_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection finished_event_connection;

// subscribe to the Finished event with a handler function keeping the connection
publisher->getEventFinished().connect(finished_event_connection, finished_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
finished_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
finished_event_connection.setEnabled(true);

// ...

// remove subscription to the Finished event via the connection
finished_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A Finished event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling Finished event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventFinished().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId finished_handler_id;

// subscribe to the Finished event with a lambda handler function and keeping connection ID
finished_handler_id = publisher->getEventFinished().connect(e_connections, []() {
		Log::message("\Handling Finished event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventFinished().disconnect(finished_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Finished events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventFinished().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventFinished().setEnabled(true);

```

</details>

### Return value

Event instance.
---

## AnimationSequencePlayer ( const char * path )

Constructor. Creates a player for the sequence stored in the specified file.
### Arguments

- *const char ** **path** - Path to the `*.seq` file to be played.

## AnimationSequencePlayer ( const UGUID & file_guid )

Constructor. Creates a player for the sequence stored in the asset with the specified GUID.
### Arguments

- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **file_guid** - GUID of the `*.seq` asset to be played.

## AnimationSequencePlayer ( const Ptr < AnimationSequence > & seq )

Constructor. Creates a player that samples the specified sequence directly, with no file behind it. This is the procedural way of playing an animation built in memory.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationSequence](../../../../api/library/animations/timeline/class.animationsequence_cpp.md)> &* **seq** - Sequence to be played.

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
## bool hasSnapshot ( ) const

Returns a value indicating if the player holds a snapshot of the values the animated parameters had before it took them over.
### Return value

true if the player holds a snapshot of the original values; otherwise, false.
## void captureOriginals ( )

Captures the current values of every parameter the sequence can animate, so that they can be put back later. The snapshot covers the whole sequence rather than the current moment, and a second call is ignored while a snapshot is already held.
## void restoreOriginals ( )

Puts the captured original values back into the scene.
## void clearSnapshot ( )

Drops the captured snapshot without restoring anything, so the values the sequence applied last stay in the scene.
## void applySequenceProcedural ( const Ptr < AnimationSequence > & seq )

Hands the player a sequence held in memory and switches it to procedural mode. The bind table is rebuilt, as the new sequence brings its own channels.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationSequence](../../../../api/library/animations/timeline/class.animationsequence_cpp.md)> &* **seq** - Sequence to be sampled by the player.

## bool hasSequence ( ) const

Returns a value indicating if the player has a sequence to play, either loaded from an asset or applied procedurally.
### Return value

true if the player has a sequence to play; otherwise, false.
## int getBindChannelID ( int index ) const

Returns the channel the specified bind slot belongs to. Together with the sequence ID it forms the key that addresses the slot no matter how the table is renumbered.
### Arguments

- *int* **index** - Bind slot number.

### Return value

ID of the channel the slot belongs to.
## unsigned long long getBindSequenceID ( int index ) const

Returns the sequence placement the specified bind slot belongs to. Two placements of one nested sequence have IDs of their own, which is what keeps their bindings apart.
### Arguments

- *int* **index** - Bind slot number.

### Return value

ID of the sequence placement the slot belongs to. The root sequence has the ID of 0.
## const char * getBindChannelName ( int index ) const

Returns the custom name of the channel the specified bind slot belongs to. This is the name the search by name works with.
### Arguments

- *int* **index** - Bind slot number.

### Return value

Custom name of the channel the slot belongs to.
## const char * getBindPlacementPath ( int index ) const

Returns the placement path of the specified bind slot, which tells apart two instances of one sequence nested in the composition.
### Arguments

- *int* **index** - Bind slot number.

### Return value

Placement path of the slot.
## AnimationBind::TYPE getBindType ( int index ) const

Returns the kind of binding the specified slot expects, which tells which [AnimationBind](../../../../api/library/animations/timeline/class.animationbind_cpp.md) subclass fits it.
### Arguments

- *int* **index** - Bind slot number.

### Return value

Type of the binding the slot expects.
## int findBind ( const char * placement_path , const char * name ) const

Searches the bind table for a slot by the channel name inside a certain placement. Use it when one name occurs in several instances of a nested sequence.
### Arguments

- *const char ** **placement_path** - Placement path of the nested sequence to search in.
- *const char ** **name** - Custom name of the channel.

### Return value

Bind slot number, or -1 if there is no such slot.
## int findBindByName ( const char * name ) const

Searches the bind table for a slot by the custom name of its channel. This is the usual way to reach a slot, as counting slots by hand breaks as soon as the sequence is edited.
### Arguments

- *const char ** **name** - Custom name of the channel.

### Return value

Bind slot number, or -1 if there is no such slot.
## int findBindByChannelID ( unsigned long long seq_id , int channel_id ) const

Searches the bind table for a slot by the stable key of its channel.
### Arguments

- *unsigned long long* **seq_id** - ID of the sequence placement. The root sequence has the ID of 0.
- *int* **channel_id** - Channel ID.

### Return value

Bind slot number, or -1 if there is no such slot.
## void invalidateBinds ( )

Marks the bind table and the resolved targets as out of date, so that both are built anew before the next frame is applied.
## bool setBind ( int index , const Ptr < AnimationBind > & bind )

Overrides the binding of the specified slot for this player alone. The asset is not touched, so the same file can drive different objects in different players.
### Arguments

- *int* **index** - Bind slot number.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationBind](../../../../api/library/animations/timeline/class.animationbind_cpp.md)> &* **bind** - Binding to be used by this player.

### Return value

true if the binding was set; otherwise, false.
## void resetBind ( int index )

Drops the override of the specified slot, so that the binding authored in the sequence takes over again.
### Arguments

- *int* **index** - Bind slot number.

## void clearBinds ( )

Drops all bind overrides of the player at once.
## bool setBindComponent ( int index , const Ptr < Node > & node , const Ptr < Property > & property )

Points the specified slot at a component of a node, which saves building an [AnimationBindComponent](../../../../api/library/animations/timeline/class.animationbindcomponent_cpp.md) by hand for the common case.
### Arguments

- *int* **index** - Bind slot number.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Node](../../../../api/library/nodes/class.node_cpp.md)> &* **node** - Node the component is assigned to.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Property](../../../../api/library/common/class.property_cpp.md)> &* **property** - Property of the component.

### Return value

true if the binding was set; otherwise, false.
## Ptr < AnimationBind > getActiveBind ( int index ) const

Returns the binding the specified slot works by: the override when there is one, and the binding authored in the sequence otherwise.
### Arguments

- *int* **index** - Bind slot number.

### Return value

Copy of the binding the slot works by.
## Ptr < AnimationBind > getDefaultBind ( int index ) const

Returns the binding authored in the sequence for the specified slot, whether or not this player overrides it.
### Arguments

- *int* **index** - Bind slot number.

### Return value

Copy of the binding authored in the sequence.
## bool setBindByKey ( unsigned long long seq_id , int channel_id , const Ptr < AnimationBind > & bind )

Overrides a binding addressed by the stable key of its channel rather than by the slot number.
### Arguments

- *unsigned long long* **seq_id** - ID of the sequence placement. The root sequence has the ID of 0.
- *int* **channel_id** - Channel ID.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationBind](../../../../api/library/animations/timeline/class.animationbind_cpp.md)> &* **bind** - Binding to be used by this player.

### Return value

true if the binding was set; otherwise, false.
## void resetBindByKey ( unsigned long long seq_id , int channel_id )

Drops the override of the binding addressed by the stable key of its channel.
### Arguments

- *unsigned long long* **seq_id** - ID of the sequence placement. The root sequence has the ID of 0.
- *int* **channel_id** - Channel ID.

## Ptr < AnimationBind > getActiveBindByKey ( unsigned long long seq_id , int channel_id ) const

Returns the binding the specified channel works by, addressed by its stable key.
### Arguments

- *unsigned long long* **seq_id** - ID of the sequence placement. The root sequence has the ID of 0.
- *int* **channel_id** - Channel ID.

### Return value

Copy of the binding the channel works by.
## Ptr < AnimationBind > getDefaultBindByKey ( unsigned long long seq_id , int channel_id ) const

Returns the binding authored in the sequence for the specified channel, addressed by its stable key.
### Arguments

- *unsigned long long* **seq_id** - ID of the sequence placement. The root sequence has the ID of 0.
- *int* **channel_id** - Channel ID.

### Return value

Copy of the binding authored in the sequence.
## int queryActiveEventIntervals ( float time )

Collects the event intervals that are open at the specified moment and reports how many were found. It answers the question an event stream cannot: which states hold right now, for a player that joined the take in the middle. The collected intervals are then read one by one by their number.
### Arguments

- *float* **time** - Moment to be looked at, in seconds.

### Return value

Number of event intervals that cover the specified moment.
## const char * getActiveEventIntervalName ( int i ) const

Returns the name of the event the collected interval belongs to.
### Arguments

- *int* **i** - Interval number in the list collected by the last query.

### Return value

Name of the event.
## int getActiveEventIntervalPayload ( int i ) const

Returns the payload carried by the event the collected interval belongs to.
### Arguments

- *int* **i** - Interval number in the list collected by the last query.

### Return value

Payload of the event.
## const char * getActiveEventIntervalPlacement ( int i ) const

Returns the placement path of the nested sequence the collected interval came from.
### Arguments

- *int* **i** - Interval number in the list collected by the last query.

### Return value

Placement path of the sequence the event came from.
## float getActiveEventIntervalStart ( int i ) const

Returns the moment the collected interval opens at.
### Arguments

- *int* **i** - Interval number in the list collected by the last query.

### Return value

Moment the interval opens at, in seconds.
## float getActiveEventIntervalEnd ( int i ) const

Returns the moment the collected interval closes at.
### Arguments

- *int* **i** - Interval number in the list collected by the last query.

### Return value

Moment the interval closes at, in seconds.
