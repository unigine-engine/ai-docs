# Unigine::Plugins::FMOD::Bank Class (CPP)

**Header:** #include <plugins/Unigine/FMOD/UnigineFMOD.h>


> **Notice:** This set of functions is available when the [FMOD](../../../../code/plugins/fmod/index.md) plugin is loaded.


FMOD Studio banks contain the metadata and audio sample data required for runtime mixing and playback. Audio sample data may be packed into the same bank as the events which reference it, or it may be packed into separate banks.


## Bank Class

### Members

## bool isUnloading () const

Returns the current value indicating if the bank is unloading.
### Return value

**true** if bank is unloading; otherwise **false**.
## bool isUnloaded () const

Returns the current value indicating if the bank is unloaded.
### Return value

**true** if bank is unloaded; otherwise **false**.
## bool isLoading () const

Returns the current value indicating if the bank is loading.
### Return value

**true** if bank is loading; otherwise **false**.
## bool isLoaded () const

Returns the current value indicating if the bank is loaded.
### Return value

**true** if bank is loaded; otherwise **false**.
## bool isError () const

Returns the current value indicating if an error has occurred.
### Return value

**true** if error has occurred; otherwise **false**.
## bool isValid () const

Returns the current value indicating if the bank reference is valid.
### Return value

**true** if bank reference is valid; otherwise **false**.
---

## EventDescription * getEventDescription ( int index )

Returns the event description for the given index. Auxiliary function, should not be used.
### Arguments

- *int* **index** - Index of the event.

### Return value

Event description for the given index.
## Bus * getBus ( int index )

Returns a bus by its index. Auxiliary function, should not be used.
### Arguments

- *int* **index** - Index of the bus.

### Return value

Bus object.
## VCA * getVCA ( int index )

Returns a VCA by its index. Auxiliary function, should not be used.
### Arguments

- *int* **index** - Index of the VCA.

### Return value

VCA object.
## int getEventDescriptionCount ( )

Returns the number of event descriptions.
### Return value

Number of event descriptions.
## int getBusCount ( )

Returns the number of buses.
### Return value

Number of buses.
## int getVCACount ( )

Returns the number of VCAs.
### Return value

Number of VCAs.
## void loadSampleData ( )

Loads non-streaming sample data for all events in the bank.
## void unloadSampleData ( )

Unloads non-streaming sample data for all events in the bank.
## void release ( )

Cleans up used resources.
## String getPath ( ) const

Returns the object's path.
### Return value

Object's path.
