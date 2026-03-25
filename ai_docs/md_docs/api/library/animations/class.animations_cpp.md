# Unigine::Animations Class (CPP)

**Header:** #include <UnigineAnimation.h>

> **Notice:** This class is a singleton.


This class is the central manager for the animation system. It provides functionality for two animation subsystems:


- **Timeline Animation** - managing [animation tracks](../../../principles/animations/index.md#animation_track) (`.utrack`) and [animation playbacks](../../../principles/animations/index.md#animation_playback) (`.uplay`), querying animatable classes and their parameters, and converting legacy animation formats.
- **Animation Scripts** - working with [animation scripts](../../../api/library/animations/skeletal/class.animscript_cpp.md) (compiled animation graphs that can be interacted with via code), querying graph types, and monitoring the build process.


## Animations Class

### Enums

## RESULT

| Name | Description |
|---|---|
| **RESULT_TRACK_ERROR** = 0 | A track-related error has occurred. |
| **RESULT_NEW_TRACK_LOADED** = 1 | A new [animation track](../../../principles/animations/index.md#animation_track) is loaded. |
| **RESULT_TRACK_IS_ALREADY_LOADED** = 2 | The [animation track](../../../principles/animations/index.md#animation_track) is already loaded. |
| **RESULT_TRACK_RELOADED** = 3 | The [animation track](../../../principles/animations/index.md#animation_track) is reloaded. |
| **RESULT_TRACK_SAVED** = 4 | The [animation track](../../../principles/animations/index.md#animation_track) is saved. |
| **RESULT_TRACK_UNLOADED** = 5 | The [animation track](../../../principles/animations/index.md#animation_track) is unloaded. |
| **RESULT_PLAYBACK_ERROR** = 6 | A playback-related error has occurred. |
| **RESULT_NEW_PLAYBACK_LOADED** = 7 | A new [animation playback](../../../principles/animations/index.md#animation_playback) is loaded. |
| **RESULT_PLAYBACK_IS_ALREADY_LOADED** = 8 | The [animation playback](../../../principles/animations/index.md#animation_playback) is already loaded. |
| **RESULT_PLAYBACK_SAVED** = 9 | The [animation playback](../../../principles/animations/index.md#animation_playback) is saved. |

### Members

## getNumObjects () const

Returns the current total number of animated objects.
### Return value

Current number of [animated objects](../../../principles/animations/index.md#animation_object).
## getNumTracks () const

Returns the current total number of [animation tracks](../../../principles/animations/index.md#animation_track).
### Return value

Current number of animation tracks.
## getNumPlaybacks () const

Returns the current total number of [animation playbacks](../../../principles/animations/index.md#animation_playback).
### Return value

Current number of animation playbacks.
## static Event<const Ptr < AnimationTrack > &> getEventTrackRemoved () const

Event triggered when an [animation track](../../../principles/animations/index.md#animation_track) is removed. You can subscribe to events via *connect()* and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<AnimationTrack> & **anim_track**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the TrackRemoved event handler
void trackremoved_event_handler(const Ptr<AnimationTrack> & anim_track)
{
	Log::message("\Handling TrackRemoved event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections trackremoved_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Animations::getEventTrackRemoved().connect(trackremoved_event_connections, trackremoved_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Animations::getEventTrackRemoved().connect(trackremoved_event_connections, [](const Ptr<AnimationTrack> & anim_track) {
		Log::message("\Handling TrackRemoved event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
trackremoved_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection trackremoved_event_connection;

// subscribe to the TrackRemoved event with a handler function keeping the connection
Animations::getEventTrackRemoved().connect(trackremoved_event_connection, trackremoved_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
trackremoved_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
trackremoved_event_connection.setEnabled(true);

// ...

// remove subscription to the TrackRemoved event via the connection
trackremoved_event_connection.disconnect();

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

	// A TrackRemoved event handler implemented as a class member
	void event_handler(const Ptr<AnimationTrack> & anim_track)
	{
		Log::message("\Handling TrackRemoved event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Animations::getEventTrackRemoved().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId trackremoved_handler_id;

// subscribe to the TrackRemoved event with a lambda handler function and keeping connection ID
trackremoved_handler_id = Animations::getEventTrackRemoved().connect(e_connections, [](const Ptr<AnimationTrack> & anim_track) {
		Log::message("\Handling TrackRemoved event (lambda).\n");
	}
);

// remove the subscription later using the ID
Animations::getEventTrackRemoved().disconnect(trackremoved_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all TrackRemoved events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Animations::getEventTrackRemoved().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Animations::getEventTrackRemoved().setEnabled(true);

```

</details>

### Return value

Event reference.
## static Event<const Ptr < AnimationTrack > &> getEventTrackAdded () const

Event triggered when a new [animation track](../../../principles/animations/index.md#animation_track) is added. You can subscribe to events via *connect()* and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<AnimationTrack> & **anim_track**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the TrackAdded event handler
void trackadded_event_handler(const Ptr<AnimationTrack> & anim_track)
{
	Log::message("\Handling TrackAdded event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections trackadded_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Animations::getEventTrackAdded().connect(trackadded_event_connections, trackadded_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Animations::getEventTrackAdded().connect(trackadded_event_connections, [](const Ptr<AnimationTrack> & anim_track) {
		Log::message("\Handling TrackAdded event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
trackadded_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection trackadded_event_connection;

// subscribe to the TrackAdded event with a handler function keeping the connection
Animations::getEventTrackAdded().connect(trackadded_event_connection, trackadded_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
trackadded_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
trackadded_event_connection.setEnabled(true);

// ...

// remove subscription to the TrackAdded event via the connection
trackadded_event_connection.disconnect();

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

	// A TrackAdded event handler implemented as a class member
	void event_handler(const Ptr<AnimationTrack> & anim_track)
	{
		Log::message("\Handling TrackAdded event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Animations::getEventTrackAdded().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId trackadded_handler_id;

// subscribe to the TrackAdded event with a lambda handler function and keeping connection ID
trackadded_handler_id = Animations::getEventTrackAdded().connect(e_connections, [](const Ptr<AnimationTrack> & anim_track) {
		Log::message("\Handling TrackAdded event (lambda).\n");
	}
);

// remove the subscription later using the ID
Animations::getEventTrackAdded().disconnect(trackadded_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all TrackAdded events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Animations::getEventTrackAdded().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Animations::getEventTrackAdded().setEnabled(true);

```

</details>

### Return value

Event reference.
## static Event<const Ptr < AnimationObject > &> getEventObjectRemoved () const

Event triggered when an [animation object](../../../principles/animations/index.md#animation_object) is removed. You can subscribe to events via *connect()* and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<AnimationObject> & **anim_object**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the ObjectRemoved event handler
void objectremoved_event_handler(const Ptr<AnimationObject> & anim_object)
{
	Log::message("\Handling ObjectRemoved event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections objectremoved_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Animations::getEventObjectRemoved().connect(objectremoved_event_connections, objectremoved_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Animations::getEventObjectRemoved().connect(objectremoved_event_connections, [](const Ptr<AnimationObject> & anim_object) {
		Log::message("\Handling ObjectRemoved event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
objectremoved_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection objectremoved_event_connection;

// subscribe to the ObjectRemoved event with a handler function keeping the connection
Animations::getEventObjectRemoved().connect(objectremoved_event_connection, objectremoved_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
objectremoved_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
objectremoved_event_connection.setEnabled(true);

// ...

// remove subscription to the ObjectRemoved event via the connection
objectremoved_event_connection.disconnect();

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

	// A ObjectRemoved event handler implemented as a class member
	void event_handler(const Ptr<AnimationObject> & anim_object)
	{
		Log::message("\Handling ObjectRemoved event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Animations::getEventObjectRemoved().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId objectremoved_handler_id;

// subscribe to the ObjectRemoved event with a lambda handler function and keeping connection ID
objectremoved_handler_id = Animations::getEventObjectRemoved().connect(e_connections, [](const Ptr<AnimationObject> & anim_object) {
		Log::message("\Handling ObjectRemoved event (lambda).\n");
	}
);

// remove the subscription later using the ID
Animations::getEventObjectRemoved().disconnect(objectremoved_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all ObjectRemoved events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Animations::getEventObjectRemoved().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Animations::getEventObjectRemoved().setEnabled(true);

```

</details>

### Return value

Event reference.
## static Event<const Ptr < AnimationObject > &> getEventObjectAdded () const

Event triggered when a new [animation object](../../../principles/animations/index.md#animation_object) is added. You can subscribe to events via *connect()* and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<AnimationObject> & **anim_object**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the ObjectAdded event handler
void objectadded_event_handler(const Ptr<AnimationObject> & anim_object)
{
	Log::message("\Handling ObjectAdded event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections objectadded_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Animations::getEventObjectAdded().connect(objectadded_event_connections, objectadded_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Animations::getEventObjectAdded().connect(objectadded_event_connections, [](const Ptr<AnimationObject> & anim_object) {
		Log::message("\Handling ObjectAdded event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
objectadded_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection objectadded_event_connection;

// subscribe to the ObjectAdded event with a handler function keeping the connection
Animations::getEventObjectAdded().connect(objectadded_event_connection, objectadded_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
objectadded_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
objectadded_event_connection.setEnabled(true);

// ...

// remove subscription to the ObjectAdded event via the connection
objectadded_event_connection.disconnect();

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

	// A ObjectAdded event handler implemented as a class member
	void event_handler(const Ptr<AnimationObject> & anim_object)
	{
		Log::message("\Handling ObjectAdded event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Animations::getEventObjectAdded().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId objectadded_handler_id;

// subscribe to the ObjectAdded event with a lambda handler function and keeping connection ID
objectadded_handler_id = Animations::getEventObjectAdded().connect(e_connections, [](const Ptr<AnimationObject> & anim_object) {
		Log::message("\Handling ObjectAdded event (lambda).\n");
	}
);

// remove the subscription later using the ID
Animations::getEventObjectAdded().disconnect(objectadded_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all ObjectAdded events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Animations::getEventObjectAdded().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Animations::getEventObjectAdded().setEnabled(true);

```

</details>

### Return value

Event reference.
## Event<string, string, string> getEventCustomLibBuild () const

Event triggered when a custom animation script library build is performed. The handler receives paths to the generated C++ source file, the compiled library, and the build log. You can subscribe to events via *connect()* and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const char * **cpp_path**, const char * **lib_path**, const char * **log_path**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the CustomLibBuild event handler
void customlibbuild_event_handler(const char * cpp_path,  const char * lib_path,  const char * log_path)
{
	Log::message("\Handling CustomLibBuild event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections customlibbuild_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventCustomLibBuild().connect(customlibbuild_event_connections, customlibbuild_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventCustomLibBuild().connect(customlibbuild_event_connections, [](const char * cpp_path,  const char * lib_path,  const char * log_path) {
		Log::message("\Handling CustomLibBuild event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
customlibbuild_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection customlibbuild_event_connection;

// subscribe to the CustomLibBuild event with a handler function keeping the connection
publisher->getEventCustomLibBuild().connect(customlibbuild_event_connection, customlibbuild_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
customlibbuild_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
customlibbuild_event_connection.setEnabled(true);

// ...

// remove subscription to the CustomLibBuild event via the connection
customlibbuild_event_connection.disconnect();

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

	// A CustomLibBuild event handler implemented as a class member
	void event_handler(const char * cpp_path,  const char * lib_path,  const char * log_path)
	{
		Log::message("\Handling CustomLibBuild event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventCustomLibBuild().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId customlibbuild_handler_id;

// subscribe to the CustomLibBuild event with a lambda handler function and keeping connection ID
customlibbuild_handler_id = publisher->getEventCustomLibBuild().connect(e_connections, [](const char * cpp_path,  const char * lib_path,  const char * log_path) {
		Log::message("\Handling CustomLibBuild event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventCustomLibBuild().disconnect(customlibbuild_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all CustomLibBuild events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventCustomLibBuild().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventCustomLibBuild().setEnabled(true);

```

</details>

### Return value

Event reference.
## int getNumAnimScriptTypes () const

Returns the current total number of registered [animation script](../../../api/library/animations/skeletal/class.animscript_cpp.md) types.
### Return value

Current number of registered animation script types.
## bool isAnimScriptsSuccessBuild () const

Returns the current Returns a value indicating if the last [animation script](../../../api/library/animations/skeletal/class.animscript_cpp.md) build completed successfully.
### Return value

**true** if the last animation script build completed successfully; otherwise **false**.
## bool isAnimScriptsRebuilding () const

Returns the current Returns a value indicating if [animation scripts](../../../api/library/animations/skeletal/class.animscript_cpp.md) are currently being rebuilt.
### Return value

**true** if animation scripts are currently being rebuilt; otherwise **false**.
## bool isAnimScriptsLoaded () const

Returns the current Returns a value indicating if [animation scripts](../../../api/library/animations/skeletal/class.animscript_cpp.md) are loaded.
### Return value

**true** if animation scripts are loaded; otherwise **false**.
---

## Ptr < AnimationObject > getObjectByIndex ( int index ) const

Returns an [animation object](../../../principles/animations/index.md#animation_object) by its index in the common list of animation objects.
### Arguments

- *int* **index** - Animation object index.

### Return value

Animation object with the specified index
## Ptr < AnimationObject > getObjectByID ( int id ) const

Returns an [animation object](../../../principles/animations/index.md#animation_object) by its ID.
### Arguments

- *int* **id** - Animation object ID.

### Return value

Animation object with the specified ID.
## bool containsObject ( int id ) const

Returns a value indicating if an [animation object](../../../principles/animations/index.md#animation_object) with the specified ID exists.
### Arguments

- *int* **id** - Animation object ID.

### Return value

true if the animation object with the specified ID exists; otherwise, false.
## int getObjectIndex ( const Ptr < AnimationObject > & obj ) const

Returns an index of the specified [animation object](../../../principles/animations/index.md#animation_object) in the common list.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[AnimationObject](../../../api/library/animations/timeline/class.animationobject_cpp.md)> &* **obj** - Animation object for which an index is to be found.

### Return value

Animation object index in the common list of animation objects if it is found; otherwise, -1.
## void loadTracks ( )

Loads all [animation tracks](../../../principles/animations/index.md#animation_track).
## void unloadTracks ( )

Unloads all [animation tracks](../../../principles/animations/index.md#animation_track).
## void reloadTracks ( )

Reloads all [animation tracks](../../../principles/animations/index.md#animation_track).
## Animations::RESULT loadTrack ( const char * path )

Loads an [animation track](../../../principles/animations/index.md#animation_track) from the specified file path.
### Arguments

- *const char ** **path** - Path to the source track file (`.utrack`).

### Return value

Result of loading operation.
## Animations::RESULT reloadTrack ( const char * path )

Reloads an [animation track](../../../principles/animations/index.md#animation_track) from the specified file path.
### Arguments

- *const char ** **path** - Path to the source track file (`.utrack`).

### Return value

Result of reloading operation.
## Animations::RESULT saveTrack ( const Ptr < AnimationTrack > & track , const char * path )

Saves the specified [animation track](../../../principles/animations/index.md#animation_track) to the specified file path.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[AnimationTrack](../../../api/library/animations/timeline/class.animationtrack_cpp.md)> &* **track** - Animation track to be saved.
- *const char ** **path** - Path to which the specified animation track is to be saved.

### Return value

Result of saving operation.
## Animations::RESULT saveTrackPrecomputed ( const Ptr < AnimationTrack > & track , int num_frames , bool is_looped_frames , const char * path )

Saves the precomputed version of the specified [animation track](../../../principles/animations/index.md#animation_track) to the specified file path.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[AnimationTrack](../../../api/library/animations/timeline/class.animationtrack_cpp.md)> &* **track** - Animation track to be saved.
- *int* **num_frames** - Number of frames to be saved.
- *bool* **is_looped_frames** - Set true if the animation track should be looped; otherwise, false.
- *const char ** **path** - Path to which the specified animation track is to be saved.

### Return value

Result of saving operation.
## Ptr < AnimationTrack > getTrackByIndex ( int index )

Returns an [animation track](../../../principles/animations/index.md#animation_track) by its index in the common list of tracks.
### Arguments

- *int* **index** - Animation track index in the common list of tracks.

### Return value

Animation track with the specified index.
## Ptr < AnimationTrack > getTrackByGUID ( const UGUID & guid )

Returns an [animation track](../../../principles/animations/index.md#animation_track) by its GUID.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - GUID of the animation track.

### Return value

Animation track with the specified GUID.
## Ptr < AnimationTrack > getTrackByFileGUID ( const UGUID & guid )

Returns an [animation track](../../../principles/animations/index.md#animation_track) by the GUID of the animation track file (`.utrack`).
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - GUID of the animation track file (`.utrack`).

### Return value

Animation track with the specified file GUID.
## Ptr < AnimationTrack > getTrackByPath ( const char * path )

Returns an [animation track](../../../principles/animations/index.md#animation_track) by the path to the animation track file (`.utrack`).
### Arguments

- *const char ** **path** - Path to the animation track file (`.utrack`).

### Return value

Animation track with the specified file GUID.
## bool containsTrack ( const UGUID & guid )

Returns a value indicating if an [animation track](../../../principles/animations/index.md#animation_track) with the specified GUID exists.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - GUID of the animation track.

### Return value

true if the animation track with the specified GUID exists; otherwise, false.
## int getTrackIndex ( const Ptr < AnimationTrack > & track )

Returns an index of the specified [animation track](../../../principles/animations/index.md#animation_track) in the common list.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[AnimationTrack](../../../api/library/animations/timeline/class.animationtrack_cpp.md)> &* **track** - Animation track for which an index is to be found.

### Return value

Animation track index in the common list of animation tracks if it is found; otherwise, -1.
## void loadPlaybacks ( )

Loads all [animation playbacks](../../../principles/animations/index.md#animation_playback).
## Animations::RESULT loadPlayback ( const char * path )

Loads an [animation playback](../../../principles/animations/index.md#animation_playback) from the specified file path.
### Arguments

- *const char ** **path** - Path to the source animation playback file (`.uplay`).

### Return value

Result of loading operation.
## Animations::RESULT savePlayback ( const Ptr < AnimationPlayback > & playback , const char * path )

Saves the specified [animation playback](../../../principles/animations/index.md#animation_playback) to the specified file path.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[AnimationPlayback](../../../api/library/animations/timeline/class.animationplayback_cpp.md)> &* **playback** - Animation playback to be saved.
- *const char ** **path** - Path to which the specified animation playback is to be saved.

### Return value

Result of saving operation.
## Ptr < AnimationPlayback > getPlaybackByIndex ( int index ) const

Returns an [animation playback](../../../principles/animations/index.md#animation_playback) by its index in the common list of tracks.
### Arguments

- *int* **index** - Animation playback index in the common list of playbacks.

### Return value

Animation playback with the specified index.
## Ptr < AnimationPlayback > getPlaybackByGUID ( const UGUID & guid ) const

Returns an [animation playback](../../../principles/animations/index.md#animation_playback) by its GUID.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - GUID of the animation playback.

### Return value

Animation playback with the specified GUID.
## Ptr < AnimationPlayback > getPlaybackByFileGUID ( const UGUID & guid ) const

Returns an [animation playback](../../../principles/animations/index.md#animation_playback) by the GUID of the animation track file (`.uplay`).
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - GUID of the animation playback file (`.uplay`).

### Return value

Animation track with the specified file GUID.
## Ptr < AnimationPlayback > getPlaybackByPath ( const char * path ) const

Returns an [animation playback](../../../principles/animations/index.md#animation_playback) by the path to the animation track file (`.uplay`).
### Arguments

- *const char ** **path** - Path to the animation playback file (`.uplay`).

### Return value

Animation playback with the specified path.
## bool containsPlayback ( const UGUID & guid ) const

Returns a value indicating if an [animation playback](../../../principles/animations/index.md#animation_playback) with the specified GUID exists.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - GUID of the animation playback.

### Return value

true if the animation playback with the specified GUID exists; otherwise, false.
## int getPlaybackIndex ( const Ptr < AnimationPlayback > & playback ) const

Returns an index of the specified [animation playback](../../../principles/animations/index.md#animation_playback) in the common list.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[AnimationPlayback](../../../api/library/animations/timeline/class.animationplayback_cpp.md)> &* **playback** - Animation playback for which an index is to be found.

### Return value

Animation track index in the common list of animation tracks if it is found; otherwise, -1.
## int getClasses ( Vector < String > & OUT_out_classes )

Obtains the list of names of all available classes that can be animated and puts it to the specified output buffer.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[String](../../../api/library/common/class.string_cpp.md)> &* **OUT_out_classes** - Output buffer for the list of the Engine's classes that can be animated. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of the Engine's classes that can be animated.
## int getSingletonClasses ( Vector < String > & OUT_out_classes )

Obtains the list of names of all Engine's singleton-classes and puts it to the specified output buffer.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[String](../../../api/library/common/class.string_cpp.md)> &* **OUT_out_classes** - Output buffer for the list of the Engine's singleton-classes. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of the Engine's singleton-classes.
## const char * getParentClass ( const char * class_name ) const

Returns the name of the parent class for the specified class.
### Arguments

- *const char ** **class_name** - Name of the class for which the parent class is to be found.

### Return value

Name of the parent class.
## int getDerivedClasses ( const char * class_name , Vector < String > & OUT_out_classes ) const

Obtains the list of all classes derived from the specified one and puts it to the specified output buffer.
### Arguments

- *const char ** **class_name** - Name of the class for which derived classes are to be found.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[String](../../../api/library/common/class.string_cpp.md)> &* **OUT_out_classes** - Output buffer for the list of classes derived from the specified class. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of derived classes.
## int getClassParameters ( const char * class_name , Vector <int> & OUT_out_parameters ) const

Obtains the list of all [animation parameter](../../../principles/animations/index.md#animation_parameters) for the specified class and puts it to the specified output buffer.
### Arguments

- *const char ** **class_name** - Name of the class for which the list of animation parameters is to be found.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<int> &* **OUT_out_parameters** - Output buffer for the list of parameters of the specified class. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of animation parameters for the specified class.
## const char * getParameterName ( AnimParams::PARAM param ) const

Returns the name of the specified the specified [animation parameter](../../../principles/animations/index.md#animation_parameters).
### Arguments

- *AnimParams::PARAM* **param** - Animation parameter.

### Return value

Animation parameter name.
## AnimationModifier::TYPE getParameterModifierType ( AnimParams::PARAM param ) const

Returns the type of modifier used for the specified [animation parameter](../../../principles/animations/index.md#animation_parameters).
### Arguments

- *AnimParams::PARAM* **param** - Animation parameter.

### Return value

Modifier type for the specified parameter.
## AnimParams::PARAM getParameterByName ( const char * param_name ) const

Returns an [animation parameter](../../../principles/animations/index.md#animation_parameters) by its name.
### Arguments

- *const char ** **param_name** - Animation parameter name.

### Return value

Animation parameter with the specified name.
## void convertToUanims ( const char * folder_path , const Vector < String > & playbacks )

Converts all track-files in the old *Tracker* format ( `.track`) from the specfied folder to the new animation formats (`.utrack` / `.uplay`).
### Arguments

- *const char ** **folder_path** - Path to the folder containing track-files in the old *Tracker* format ( `.track`) to be converted to the new track format (`.utrack`).
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[String](../../../api/library/common/class.string_cpp.md)> &* **playbacks** - List of *Tracker* animation tracks in old format ( `.track`) to be converted to the new playback format(`.uplay`).

## void convertToUanims ( const Vector < String > & tracks , const Vector < String > & playbacks )

Converts the specified lists of tracks in the old *Tracker* format ( `.track`) to the new animation formats (`.utrack` / `.uplay`).
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[String](../../../api/library/common/class.string_cpp.md)> &* **tracks** - List of *Tracker* animation tracks in old format ( `.track`) to be converted to the new track format (`.utrack`).
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[String](../../../api/library/common/class.string_cpp.md)> &* **playbacks** - List of *Tracker* animation tracks in old format ( `.track`) to be converted to the new playback format(`.uplay`).

## void checkUtrackTypes ( )

Checks all old-style animation parameter types (used in the *Tracker* tool) versus their equivalents in the new Animation System and outputs them to the console. In case of unknown parameter types the corresponding message is displayed.
## bool animToBonesModifier ( const char * anim_path , const Ptr < AnimationModifierBones > & out_modifier , float duration ) const

Converts the specified mesh animation file (`.anim`) to a [modifier](../../../principles/animations/index.md#animation_modifier) for [ObjectMeshSkinnedLegacy](../../../api/library/objects/class.objectmeshskinnedlegacy_cpp.md) bones ( *AnimationModifierBones*) and puts it to the specified *AnimationModifierBones* instance.
### Arguments

- *const char ** **anim_path** - Path to the mesh animation file (`.anim`) to be converted.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[AnimationModifierBones](../../../api/library/animations/timeline/class.animationmodifierbones_cpp.md)> &* **out_modifier** - Resulting animation modifier.
- *float* **duration** - Target animation duration, in seconds.

### Return value

true if the specified mesh animation file was successfully converted; otherwise, false.
## void rebuildAnimScripts ( )

Triggers a rebuild of all [animation scripts](../../../api/library/animations/skeletal/class.animscript_cpp.md). This recompiles the animation graph source files into a runtime library. Use  to check if the rebuild process is still in progress, and  to check if it completed successfully.
## const char * getAnimScriptTypeName ( int type_index ) const

Returns the name of the [animation script](../../../api/library/animations/skeletal/class.animscript_cpp.md) type by its index.
### Arguments

- *int* **type_index** - Index of the animation script type in the range from 0 to the  of types.

### Return value

Name of the animation script type.
## static void waitAnimScriptsRebuilding ( )

Blocks execution until the current animation scripts rebuild is complete. If a rebuild is in progress, this method waits for the background build task to finish and then loads the updated library. If no rebuild is in progress, returns immediately.
