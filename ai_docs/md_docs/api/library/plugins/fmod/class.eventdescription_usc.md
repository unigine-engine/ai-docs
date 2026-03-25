# Unigine::Plugins::FMOD::EventDescription Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


> **Notice:** This set of functions is available when the [FMOD](../../../../code/plugins/fmod/index.md) plugin is loaded.


The description for an FMOD Studio Event.


Event descriptions belong to banks and can be queried after the relevant bank has been loaded. Event descriptions may be retrieved via path or GUID lookup, or by enumerating all descriptions in a bank.


## EventDescription Class

### Members

## int isSampleUnloading () const

Returns the current sample data unloading state.
### Return value

Current sample is unloading
## int isSampleUnloaded () const

Returns the current sample data unloaded state.
### Return value

Current sample is unloaded
## int isSampleLoading () const

Returns the current sample data loading state.
### Return value

Current sample is loading
## int isSampleLoaded () const

Returns the current sample data loaded state.
### Return value

Current sample is loaded
## int isSampleError () const

Returns the current value indicating if the sample has failed to load.
### Return value

Current sample has failed to load
## int isValid () const

Returns the current value indicating if the event description is valid.
### Return value

Current event description is valid
## int getLength () const

Returns the current length of the timeline.
### Return value

Current timeline length.
## int isDopplerEnabled () const

Returns the current value indicating if the doppler effect is enabled.
### Return value

Current doppler effect
## int isOneShot () const

Returns the current value indicating if the event is a oneshot event.
### Return value

Current event is a oneshot event
---

## EventInstance createEvent ( )

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
## String getPath ( )

Returns the path to the event description.
### Return value

Path.
