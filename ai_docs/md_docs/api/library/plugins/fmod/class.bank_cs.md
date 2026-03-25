# Unigine::Plugins::FMOD::Bank Class (CS)


> **Notice:** This set of functions is available when the [FMOD](../../../../code/plugins/fmod/index.md) plugin is loaded.


FMOD Studio banks contain the metadata and audio sample data required for runtime mixing and playback. Audio sample data may be packed into the same bank as the events which reference it, or it may be packed into separate banks.


## Bank Class

### Properties

## 🔒︎ bool IsUnloading

The value indicating if the bank is unloading.
## 🔒︎ bool IsUnloaded

The value indicating if the bank is unloaded.
## 🔒︎ bool IsLoading

The value indicating if the bank is loading.
## 🔒︎ bool IsLoaded

The value indicating if the bank is loaded.
## 🔒︎ bool IsError

The value indicating if an error has occurred.
## 🔒︎ bool IsValid

The value indicating if the bank reference is valid.
### Members

---

## EventDescription GetEventDescription ( int index )

Returns the event description for the given index. Auxiliary function, should not be used.
### Arguments

- *int* **index** - Index of the event.

### Return value

Event description for the given index.
## Bus GetBus ( int index )

Returns a bus by its index. Auxiliary function, should not be used.
### Arguments

- *int* **index** - Index of the bus.

### Return value

Bus object.
## VCA GetVCA ( int index )

Returns a VCA by its index. Auxiliary function, should not be used.
### Arguments

- *int* **index** - Index of the VCA.

### Return value

VCA object.
## int GetEventDescriptionCount ( )

Returns the number of event descriptions.
### Return value

Number of event descriptions.
## int GetBusCount ( )

Returns the number of buses.
### Return value

Number of buses.
## int GetVCACount ( )

Returns the number of VCAs.
### Return value

Number of VCAs.
## void LoadSampleData ( )

Loads non-streaming sample data for all events in the bank.
## void UnloadSampleData ( )

Unloads non-streaming sample data for all events in the bank.
## void Release ( )

Cleans up used resources.
## string GetPath ( )

Returns the object's path.
### Return value

Object's path.
