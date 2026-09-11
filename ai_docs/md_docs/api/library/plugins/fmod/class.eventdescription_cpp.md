# Unigine::Plugins::FMOD::EventDescription Class (CPP)

**Header:** #include <plugins/Unigine/FMOD/UnigineFMOD.h>


> **Notice:** This set of functions is available when the [FMOD](../../../../code/plugins/fmod/index.md) plugin is loaded.


The description for an FMOD Studio Event.


Event descriptions belong to banks and can be queried after the relevant bank has been loaded. Event descriptions may be retrieved via path or GUID lookup, or by enumerating all descriptions in a bank.


## EventDescription Class

### Members

## bool isSampleUnloading () const

Returns the current sample data unloading state.
### Return value

**true** if sample is unloading; otherwise **false**.
## bool isSampleUnloaded () const

Returns the current sample data unloaded state.
### Return value

**true** if sample is unloaded; otherwise **false**.
## bool isSampleLoading () const

Returns the current sample data loading state.
### Return value

**true** if sample is loading; otherwise **false**.
## bool isSampleLoaded () const

Returns the current sample data loaded state.
### Return value

**true** if sample is loaded; otherwise **false**.
## bool isSampleError () const

Returns the current value indicating if the sample has failed to load.
### Return value

**true** if sample has failed to load; otherwise **false**.
## bool isValid () const

Returns the current value indicating if the event description is valid.
### Return value

**true** if event description is valid; otherwise **false**.
## int getLength () const

Returns the current length of the timeline.
### Return value

Current timeline length.
## bool isDopplerEnabled () const

Returns the current value indicating if the doppler effect is enabled.
### Return value

**true** if doppler effect is enabled ; otherwise **false**.
## bool isOneShot () const

Returns the current value indicating if the event is a oneshot event.
### Return value

**true** if event is a oneshot event; otherwise **false**.
---

## EventInstance * createEvent ( )

Creates a playable instance.
### Return value

EventInstance object.
## void releaseAllEvents ( )

Releases all instances.
## void loadSampleData ( )

Loads all non-streaming sample data.
## void unloadSampleData ( )

Unloads all non-streaming sample data. Sample data will not be unloaded until all instances of the event are released.
## void release ( )

Marks the event instance for release. Event instances marked for release are destroyed by the asynchronous update when they are in the stopped state.
## void releaseFromStudio ( )

Auxiliary function, should not be used.
## void update ( )

Updates the position of the event instance in world space.
## String getPath ( ) const

Returns the path to the event description.
### Return value

Path.
