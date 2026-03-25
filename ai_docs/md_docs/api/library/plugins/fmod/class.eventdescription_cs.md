# Unigine::Plugins::FMOD::EventDescription Class (CS)


> **Notice:** This set of functions is available when the [FMOD](../../../../code/plugins/fmod/index.md) plugin is loaded.


The description for an FMOD Studio Event.


Event descriptions belong to banks and can be queried after the relevant bank has been loaded. Event descriptions may be retrieved via path or GUID lookup, or by enumerating all descriptions in a bank.


## EventDescription Class

### Properties

## 🔒︎ bool IsSampleUnloading

The sample data unloading state.
## 🔒︎ bool IsSampleUnloaded

The sample data unloaded state.
## 🔒︎ bool IsSampleLoading

The sample data loading state.
## 🔒︎ bool IsSampleLoaded

The sample data loaded state.
## 🔒︎ bool IsSampleError

The value indicating if the sample has failed to load.
## 🔒︎ bool IsValid

The value indicating if the event description is valid.
## 🔒︎ int Length

The length of the timeline.
## 🔒︎ bool IsDopplerEnabled

The value indicating if the doppler effect is enabled.
## 🔒︎ bool IsOneShot

The value indicating if the event is a oneshot event.
### Members

---

## EventInstance CreateEvent ( )

Creates a playable instance.
### Return value

EventInstance object.
## void ReleaseAllEvents ( )

Releases all instances.
## void LoadSampleData ( )

Loads all non-streaming sample data.
## void UnloadSampleData ( )

Unloads all non-streaming sample data. Sample data will not be unloaded until all instances of the event are released.
## void Release ( )

Marks the event instance for release. Event instances marked for release are destroyed by the asynchronous update when they are in the stopped state.
## void ReleaseFromStudio ( )

Auxiliary function, should not be used.
## void Update ( )

Updates the position of the event instance in world space.
## string GetPath ( )

Returns the path to the event description.
### Return value

Path.
