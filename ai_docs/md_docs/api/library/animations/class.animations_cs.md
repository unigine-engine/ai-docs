# Unigine::Animations Class (CS)

> **Notice:** This class is a singleton.


This class is the central manager for the animation system. It provides functionality for two animation subsystems:


- **Timeline Animation** - managing [animation tracks](../../../principles/animations/index.md#animation_track) (`.utrack`) and [animation playbacks](../../../principles/animations/index.md#animation_playback) (`.uplay`), querying animatable classes and their parameters, and converting legacy animation formats.
- **Animation Scripts** - working with [animation scripts](../../../api/library/animations/skeletal/class.animscript_cs.md) (compiled animation graphs that can be interacted with via code), querying graph types, and monitoring the build process.


## Animations Class

### Enums

## RESULT

| Name | Description |
|---|---|
| **TRACK_ERROR** = 0 | A track-related error has occurred. |
| **NEW_TRACK_LOADED** = 1 | A new [animation track](../../../principles/animations/index.md#animation_track) is loaded. |
| **TRACK_IS_ALREADY_LOADED** = 2 | The [animation track](../../../principles/animations/index.md#animation_track) is already loaded. |
| **TRACK_RELOADED** = 3 | The [animation track](../../../principles/animations/index.md#animation_track) is reloaded. |
| **TRACK_SAVED** = 4 | The [animation track](../../../principles/animations/index.md#animation_track) is saved. |
| **TRACK_UNLOADED** = 5 | The [animation track](../../../principles/animations/index.md#animation_track) is unloaded. |
| **PLAYBACK_ERROR** = 6 | A playback-related error has occurred. |
| **NEW_PLAYBACK_LOADED** = 7 | A new [animation playback](../../../principles/animations/index.md#animation_playback) is loaded. |
| **PLAYBACK_IS_ALREADY_LOADED** = 8 | The [animation playback](../../../principles/animations/index.md#animation_playback) is already loaded. |
| **PLAYBACK_SAVED** = 9 | The [animation playback](../../../principles/animations/index.md#animation_playback) is saved. |

### Properties

## 🔒︎ int NumObjects

The total number of animated objects.
## 🔒︎ int NumTracks

The total number of [animation tracks](../../../principles/animations/index.md#animation_track).
## 🔒︎ int NumPlaybacks

The total number of [animation playbacks](../../../principles/animations/index.md#animation_playback).
## 🔒︎ Event< AnimationTrack > EventTrackRemoved

The Event triggered when an [animation track](../../../principles/animations/index.md#animation_track) is removed. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(AnimationTrack **anim_track**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the TrackRemoved event handler
void trackremoved_event_handler(AnimationTrack anim_track)
{
	Log.Message("\Handling TrackRemoved event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections trackremoved_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Animations.EventTrackRemoved.Connect(trackremoved_event_connections, trackremoved_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Animations.EventTrackRemoved.Connect(trackremoved_event_connections, (AnimationTrack anim_track) => {
		Log.Message("Handling TrackRemoved event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
trackremoved_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the TrackRemoved event with a handler function
Animations.EventTrackRemoved.Connect(trackremoved_event_handler);

// remove subscription to the TrackRemoved event later by the handler function
Animations.EventTrackRemoved.Disconnect(trackremoved_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection trackremoved_event_connection;

// subscribe to the TrackRemoved event with a lambda handler function and keeping the connection
trackremoved_event_connection = Animations.EventTrackRemoved.Connect((AnimationTrack anim_track) => {
		Log.Message("Handling TrackRemoved event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
trackremoved_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
trackremoved_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
trackremoved_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring TrackRemoved events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Animations.EventTrackRemoved.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Animations.EventTrackRemoved.Enabled = true;

```

</details>

## 🔒︎ Event< AnimationTrack > EventTrackAdded

The Event triggered when a new [animation track](../../../principles/animations/index.md#animation_track) is added. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(AnimationTrack **anim_track**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the TrackAdded event handler
void trackadded_event_handler(AnimationTrack anim_track)
{
	Log.Message("\Handling TrackAdded event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections trackadded_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Animations.EventTrackAdded.Connect(trackadded_event_connections, trackadded_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Animations.EventTrackAdded.Connect(trackadded_event_connections, (AnimationTrack anim_track) => {
		Log.Message("Handling TrackAdded event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
trackadded_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the TrackAdded event with a handler function
Animations.EventTrackAdded.Connect(trackadded_event_handler);

// remove subscription to the TrackAdded event later by the handler function
Animations.EventTrackAdded.Disconnect(trackadded_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection trackadded_event_connection;

// subscribe to the TrackAdded event with a lambda handler function and keeping the connection
trackadded_event_connection = Animations.EventTrackAdded.Connect((AnimationTrack anim_track) => {
		Log.Message("Handling TrackAdded event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
trackadded_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
trackadded_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
trackadded_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring TrackAdded events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Animations.EventTrackAdded.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Animations.EventTrackAdded.Enabled = true;

```

</details>

## 🔒︎ Event< AnimationObject > EventObjectRemoved

The Event triggered when an [animation object](../../../principles/animations/index.md#animation_object) is removed. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(AnimationObject **anim_object**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the ObjectRemoved event handler
void objectremoved_event_handler(AnimationObject anim_object)
{
	Log.Message("\Handling ObjectRemoved event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections objectremoved_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Animations.EventObjectRemoved.Connect(objectremoved_event_connections, objectremoved_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Animations.EventObjectRemoved.Connect(objectremoved_event_connections, (AnimationObject anim_object) => {
		Log.Message("Handling ObjectRemoved event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
objectremoved_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the ObjectRemoved event with a handler function
Animations.EventObjectRemoved.Connect(objectremoved_event_handler);

// remove subscription to the ObjectRemoved event later by the handler function
Animations.EventObjectRemoved.Disconnect(objectremoved_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection objectremoved_event_connection;

// subscribe to the ObjectRemoved event with a lambda handler function and keeping the connection
objectremoved_event_connection = Animations.EventObjectRemoved.Connect((AnimationObject anim_object) => {
		Log.Message("Handling ObjectRemoved event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
objectremoved_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
objectremoved_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
objectremoved_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring ObjectRemoved events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Animations.EventObjectRemoved.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Animations.EventObjectRemoved.Enabled = true;

```

</details>

## 🔒︎ Event< AnimationObject > EventObjectAdded

The Event triggered when a new [animation object](../../../principles/animations/index.md#animation_object) is added. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(AnimationObject **anim_object**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the ObjectAdded event handler
void objectadded_event_handler(AnimationObject anim_object)
{
	Log.Message("\Handling ObjectAdded event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections objectadded_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Animations.EventObjectAdded.Connect(objectadded_event_connections, objectadded_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Animations.EventObjectAdded.Connect(objectadded_event_connections, (AnimationObject anim_object) => {
		Log.Message("Handling ObjectAdded event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
objectadded_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the ObjectAdded event with a handler function
Animations.EventObjectAdded.Connect(objectadded_event_handler);

// remove subscription to the ObjectAdded event later by the handler function
Animations.EventObjectAdded.Disconnect(objectadded_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection objectadded_event_connection;

// subscribe to the ObjectAdded event with a lambda handler function and keeping the connection
objectadded_event_connection = Animations.EventObjectAdded.Connect((AnimationObject anim_object) => {
		Log.Message("Handling ObjectAdded event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
objectadded_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
objectadded_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
objectadded_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring ObjectAdded events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Animations.EventObjectAdded.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Animations.EventObjectAdded.Enabled = true;

```

</details>

## 🔒︎ Event<string, string, string> EventCustomLibBuild

The Event triggered when a custom animation script library build is performed. The handler receives paths to the generated C++ source file, the compiled library, and the build log. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(string **cpp_path**, string **lib_path**, string **log_path**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the CustomLibBuild event handler
void customlibbuild_event_handler(string cpp_path,  string lib_path,  string log_path)
{
	Log.Message("\Handling CustomLibBuild event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections customlibbuild_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventCustomLibBuild.Connect(customlibbuild_event_connections, customlibbuild_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventCustomLibBuild.Connect(customlibbuild_event_connections, (string cpp_path,  string lib_path,  string log_path) => {
		Log.Message("Handling CustomLibBuild event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
customlibbuild_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the CustomLibBuild event with a handler function
publisher.EventCustomLibBuild.Connect(customlibbuild_event_handler);

// remove subscription to the CustomLibBuild event later by the handler function
publisher.EventCustomLibBuild.Disconnect(customlibbuild_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection customlibbuild_event_connection;

// subscribe to the CustomLibBuild event with a lambda handler function and keeping the connection
customlibbuild_event_connection = publisher.EventCustomLibBuild.Connect((string cpp_path,  string lib_path,  string log_path) => {
		Log.Message("Handling CustomLibBuild event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
customlibbuild_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
customlibbuild_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
customlibbuild_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring CustomLibBuild events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventCustomLibBuild.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventCustomLibBuild.Enabled = true;

```

</details>

## 🔒︎ int NumAnimScriptTypes

The total number of registered [animation script](../../../api/library/animations/skeletal/class.animscript_cs.md) types.
## 🔒︎ bool IsAnimScriptsSuccessBuild

The Returns a value indicating if the last [animation script](../../../api/library/animations/skeletal/class.animscript_cs.md) build completed successfully.
## 🔒︎ bool IsAnimScriptsRebuilding

The Returns a value indicating if [animation scripts](../../../api/library/animations/skeletal/class.animscript_cs.md) are currently being rebuilt.
## 🔒︎ bool IsAnimScriptsLoaded

The Returns a value indicating if [animation scripts](../../../api/library/animations/skeletal/class.animscript_cs.md) are loaded.
### Members

---

## AnimationObject GetObjectByIndex ( int index )

Returns an [animation object](../../../principles/animations/index.md#animation_object) by its index in the common list of animation objects.
### Arguments

- *int* **index** - Animation object index.

### Return value

Animation object with the specified index
## AnimationObject GetObjectByID ( int id )

Returns an [animation object](../../../principles/animations/index.md#animation_object) by its ID.
### Arguments

- *int* **id** - Animation object ID.

### Return value

Animation object with the specified ID.
## bool ContainsObject ( int id )

Returns a value indicating if an [animation object](../../../principles/animations/index.md#animation_object) with the specified ID exists.
### Arguments

- *int* **id** - Animation object ID.

### Return value

true if the animation object with the specified ID exists; otherwise, false.
## int GetObjectIndex ( AnimationObject obj )

Returns an index of the specified [animation object](../../../principles/animations/index.md#animation_object) in the common list.
### Arguments

- *[AnimationObject](../../../api/library/animations/timeline/class.animationobject_cs.md)* **obj** - Animation object for which an index is to be found.

### Return value

Animation object index in the common list of animation objects if it is found; otherwise, -1.
## void LoadTracks ( )

Loads all [animation tracks](../../../principles/animations/index.md#animation_track).
## void UnloadTracks ( )

Unloads all [animation tracks](../../../principles/animations/index.md#animation_track).
## void ReloadTracks ( )

Reloads all [animation tracks](../../../principles/animations/index.md#animation_track).
## Animations.RESULT LoadTrack ( string path )

Loads an [animation track](../../../principles/animations/index.md#animation_track) from the specified file path.
### Arguments

- *string* **path** - Path to the source track file (`.utrack`).

### Return value

Result of loading operation.
## Animations.RESULT ReloadTrack ( string path )

Reloads an [animation track](../../../principles/animations/index.md#animation_track) from the specified file path.
### Arguments

- *string* **path** - Path to the source track file (`.utrack`).

### Return value

Result of reloading operation.
## Animations.RESULT SaveTrack ( AnimationTrack track , string path )

Saves the specified [animation track](../../../principles/animations/index.md#animation_track) to the specified file path.
### Arguments

- *[AnimationTrack](../../../api/library/animations/timeline/class.animationtrack_cs.md)* **track** - Animation track to be saved.
- *string* **path** - Path to which the specified animation track is to be saved.

### Return value

Result of saving operation.
## Animations.RESULT SaveTrackPrecomputed ( AnimationTrack track , int num_frames , bool is_looped_frames , string path )

Saves the precomputed version of the specified [animation track](../../../principles/animations/index.md#animation_track) to the specified file path.
### Arguments

- *[AnimationTrack](../../../api/library/animations/timeline/class.animationtrack_cs.md)* **track** - Animation track to be saved.
- *int* **num_frames** - Number of frames to be saved.
- *bool* **is_looped_frames** - Set true if the animation track should be looped; otherwise, false.
- *string* **path** - Path to which the specified animation track is to be saved.

### Return value

Result of saving operation.
## AnimationTrack GetTrackByIndex ( int index )

Returns an [animation track](../../../principles/animations/index.md#animation_track) by its index in the common list of tracks.
### Arguments

- *int* **index** - Animation track index in the common list of tracks.

### Return value

Animation track with the specified index.
## AnimationTrack GetTrackByGUID ( UGUID guid )

Returns an [animation track](../../../principles/animations/index.md#animation_track) by its GUID.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - GUID of the animation track.

### Return value

Animation track with the specified GUID.
## AnimationTrack GetTrackByFileGUID ( UGUID guid )

Returns an [animation track](../../../principles/animations/index.md#animation_track) by the GUID of the animation track file (`.utrack`).
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - GUID of the animation track file (`.utrack`).

### Return value

Animation track with the specified file GUID.
## AnimationTrack GetTrackByPath ( string path )

Returns an [animation track](../../../principles/animations/index.md#animation_track) by the path to the animation track file (`.utrack`).
### Arguments

- *string* **path** - Path to the animation track file (`.utrack`).

### Return value

Animation track with the specified file GUID.
## bool ContainsTrack ( UGUID guid )

Returns a value indicating if an [animation track](../../../principles/animations/index.md#animation_track) with the specified GUID exists.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - GUID of the animation track.

### Return value

true if the animation track with the specified GUID exists; otherwise, false.
## int GetTrackIndex ( AnimationTrack track )

Returns an index of the specified [animation track](../../../principles/animations/index.md#animation_track) in the common list.
### Arguments

- *[AnimationTrack](../../../api/library/animations/timeline/class.animationtrack_cs.md)* **track** - Animation track for which an index is to be found.

### Return value

Animation track index in the common list of animation tracks if it is found; otherwise, -1.
## void LoadPlaybacks ( )

Loads all [animation playbacks](../../../principles/animations/index.md#animation_playback).
## Animations.RESULT LoadPlayback ( string path )

Loads an [animation playback](../../../principles/animations/index.md#animation_playback) from the specified file path.
### Arguments

- *string* **path** - Path to the source animation playback file (`.uplay`).

### Return value

Result of loading operation.
## Animations.RESULT SavePlayback ( AnimationPlayback playback , string path )

Saves the specified [animation playback](../../../principles/animations/index.md#animation_playback) to the specified file path.
### Arguments

- *[AnimationPlayback](../../../api/library/animations/timeline/class.animationplayback_cs.md)* **playback** - Animation playback to be saved.
- *string* **path** - Path to which the specified animation playback is to be saved.

### Return value

Result of saving operation.
## AnimationPlayback GetPlaybackByIndex ( int index )

Returns an [animation playback](../../../principles/animations/index.md#animation_playback) by its index in the common list of tracks.
### Arguments

- *int* **index** - Animation playback index in the common list of playbacks.

### Return value

Animation playback with the specified index.
## AnimationPlayback GetPlaybackByGUID ( UGUID guid )

Returns an [animation playback](../../../principles/animations/index.md#animation_playback) by its GUID.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - GUID of the animation playback.

### Return value

Animation playback with the specified GUID.
## AnimationPlayback GetPlaybackByFileGUID ( UGUID guid )

Returns an [animation playback](../../../principles/animations/index.md#animation_playback) by the GUID of the animation track file (`.uplay`).
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - GUID of the animation playback file (`.uplay`).

### Return value

Animation track with the specified file GUID.
## AnimationPlayback GetPlaybackByPath ( string path )

Returns an [animation playback](../../../principles/animations/index.md#animation_playback) by the path to the animation track file (`.uplay`).
### Arguments

- *string* **path** - Path to the animation playback file (`.uplay`).

### Return value

Animation playback with the specified path.
## bool ContainsPlayback ( UGUID guid )

Returns a value indicating if an [animation playback](../../../principles/animations/index.md#animation_playback) with the specified GUID exists.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - GUID of the animation playback.

### Return value

true if the animation playback with the specified GUID exists; otherwise, false.
## int GetPlaybackIndex ( AnimationPlayback playback )

Returns an index of the specified [animation playback](../../../principles/animations/index.md#animation_playback) in the common list.
### Arguments

- *[AnimationPlayback](../../../api/library/animations/timeline/class.animationplayback_cs.md)* **playback** - Animation playback for which an index is to be found.

### Return value

Animation track index in the common list of animation tracks if it is found; otherwise, -1.
## int GetClasses ( string[] OUT_out_classes )

Obtains the list of names of all available classes that can be animated and puts it to the specified output buffer.
### Arguments

- *string[]* **OUT_out_classes** - Output buffer for the list of the Engine's classes that can be animated. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of the Engine's classes that can be animated.
## int GetSingletonClasses ( string[] OUT_out_classes )

Obtains the list of names of all Engine's singleton-classes and puts it to the specified output buffer.
### Arguments

- *string[]* **OUT_out_classes** - Output buffer for the list of the Engine's singleton-classes. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of the Engine's singleton-classes.
## string GetParentClass ( string class_name )

Returns the name of the parent class for the specified class.
### Arguments

- *string* **class_name** - Name of the class for which the parent class is to be found.

### Return value

Name of the parent class.
## int GetDerivedClasses ( string class_name , string[] OUT_out_classes )

Obtains the list of all classes derived from the specified one and puts it to the specified output buffer.
### Arguments

- *string* **class_name** - Name of the class for which derived classes are to be found.
- *string[]* **OUT_out_classes** - Output buffer for the list of classes derived from the specified class. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of derived classes.
## int GetClassParameters ( string class_name , int[] OUT_out_parameters )

Obtains the list of all [animation parameter](../../../principles/animations/index.md#animation_parameters) for the specified class and puts it to the specified output buffer.
### Arguments

- *string* **class_name** - Name of the class for which the list of animation parameters is to be found.
- *int[]* **OUT_out_parameters** - Output buffer for the list of parameters of the specified class. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of animation parameters for the specified class.
## string GetParameterName ( AnimParams.PARAM param )

Returns the name of the specified the specified [animation parameter](../../../principles/animations/index.md#animation_parameters).
### Arguments

- *AnimParams.PARAM* **param** - Animation parameter.

### Return value

Animation parameter name.
## AnimationModifier.TYPE GetParameterModifierType ( AnimParams.PARAM param )

Returns the type of modifier used for the specified [animation parameter](../../../principles/animations/index.md#animation_parameters).
### Arguments

- *AnimParams.PARAM* **param** - Animation parameter.

### Return value

Modifier type for the specified parameter.
## AnimParams.PARAM GetParameterByName ( string param_name )

Returns an [animation parameter](../../../principles/animations/index.md#animation_parameters) by its name.
### Arguments

- *string* **param_name** - Animation parameter name.

### Return value

Animation parameter with the specified name.
## void ConvertToUanims ( string folder_path , string[] playbacks )

Converts all track-files in the old *Tracker* format ( `.track`) from the specfied folder to the new animation formats (`.utrack` / `.uplay`).
### Arguments

- *string* **folder_path** - Path to the folder containing track-files in the old *Tracker* format ( `.track`) to be converted to the new track format (`.utrack`).
- *string[]* **playbacks** - List of *Tracker* animation tracks in old format ( `.track`) to be converted to the new playback format(`.uplay`).

## void ConvertToUanims ( string[] tracks , string[] playbacks )

Converts the specified lists of tracks in the old *Tracker* format ( `.track`) to the new animation formats (`.utrack` / `.uplay`).
### Arguments

- *string[]* **tracks** - List of *Tracker* animation tracks in old format ( `.track`) to be converted to the new track format (`.utrack`).
- *string[]* **playbacks** - List of *Tracker* animation tracks in old format ( `.track`) to be converted to the new playback format(`.uplay`).

## void CheckUtrackTypes ( )

Checks all old-style animation parameter types (used in the *Tracker* tool) versus their equivalents in the new Animation System and outputs them to the console. In case of unknown parameter types the corresponding message is displayed.
## bool AnimToBonesModifier ( string anim_path , AnimationModifierBones out_modifier , float duration )

Converts the specified mesh animation file (`.anim`) to a [modifier](../../../principles/animations/index.md#animation_modifier) for [ObjectMeshSkinnedLegacy](../../../api/library/objects/class.objectmeshskinnedlegacy_cs.md) bones ( *AnimationModifierBones*) and puts it to the specified *AnimationModifierBones* instance.
### Arguments

- *string* **anim_path** - Path to the mesh animation file (`.anim`) to be converted.
- *[AnimationModifierBones](../../../api/library/animations/timeline/class.animationmodifierbones_cs.md)* **out_modifier** - Resulting animation modifier.
- *float* **duration** - Target animation duration, in seconds.

### Return value

true if the specified mesh animation file was successfully converted; otherwise, false.
## void RebuildAnimScripts ( )

Triggers a rebuild of all [animation scripts](../../../api/library/animations/skeletal/class.animscript_cs.md). This recompiles the animation graph source files into a runtime library. Use  to check if the rebuild process is still in progress, and  to check if it completed successfully.
## string GetAnimScriptTypeName ( int type_index )

Returns the name of the [animation script](../../../api/library/animations/skeletal/class.animscript_cs.md) type by its index.
### Arguments

- *int* **type_index** - Index of the animation script type in the range from 0 to the  of types.

### Return value

Name of the animation script type.
## static void WaitAnimScriptsRebuilding ( )

Blocks execution until the current animation scripts rebuild is complete. If a rebuild is in progress, this method waits for the background build task to finish and then loads the updated library. If no rebuild is in progress, returns immediately.
