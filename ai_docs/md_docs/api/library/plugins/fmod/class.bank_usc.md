# Unigine::Plugins::FMOD::Bank Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


> **Notice:** This set of functions is available when the [FMOD](../../../../code/plugins/fmod/index.md) plugin is loaded.


FMOD Studio banks contain the metadata and audio sample data required for runtime mixing and playback. Audio sample data may be packed into the same bank as the events which reference it, or it may be packed into separate banks.


## Bank Class

### Members

## int isUnloading () const

Returns the current value indicating if the bank is unloading.
### Return value

Current bank is unloading
## int isUnloaded () const

Returns the current value indicating if the bank is unloaded.
### Return value

Current bank is unloaded
## int isLoading () const

Returns the current value indicating if the bank is loading.
### Return value

Current bank is loading
## int isLoaded () const

Returns the current value indicating if the bank is loaded.
### Return value

Current bank is loaded
## int isError () const

Returns the current value indicating if an error has occurred.
### Return value

Current error has occurred
## int isValid () const

Returns the current value indicating if the bank reference is valid.
### Return value

Current bank reference is valid
---

## EventDescription getEventDescription ( int index )

Returns the event description for the given index. Auxiliary function, should not be used.
### Arguments

- *int* **index** - Index of the event.

### Return value

Event description for the given index.
## Bus getBus ( int index )

Returns a bus by its index. Auxiliary function, should not be used.
### Arguments

- *int* **index** - Index of the bus.

### Return value

Bus object.
## VCA getVCA ( int index )

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
## String getPath ( )

Returns the object's path.
### Return value

Object's path.
