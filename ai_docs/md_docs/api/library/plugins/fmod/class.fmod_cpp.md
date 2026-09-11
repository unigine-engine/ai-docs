# Unigine::Plugins::FMOD::FMOD Class (CPP)

**Header:** #include <plugins/Unigine/FMOD/UnigineFMOD.h>

> **Notice:** This class is a singleton.


> **Notice:** This set of functions is available when the [FMOD](../../../../code/plugins/fmod/index.md) plugin is loaded.


This class is intened to work with FMODCore and FMODStudio objects.


## FMOD Class

### Members

## FMODCore * getCore () const

Returns the current FMOD Core System object. The Core System object can be retrieved before initializing the Studio System object to call additional core configuration functions.
### Return value

Current FMOD Core System object.
## FMODStudio * getStudio () const

Returns the current FMOD Studio System object.
### Return value

Current FMOD Studio System object.
---

## void update ( )

Calls update of FMOD Studio and Core.
## bool hasErrors ( int & error_type )

Checks for errors and returns error code. To interpret the error, see [ERROR_TYPE](../../../../api/library/plugins/fmod/class.fmodenums_cpp.md#ERROR_TYPE) enum.
### Arguments

- *int &* **error_type** - Variable to store error code.

### Return value

true if an eror has orrurred, otherwise, false.
## void loadOutputPlugin ( const char * path ) const

Loads an *FMOD* output plugin library from the given file and makes it the active audio output of the *FMOD* system. Failures (for example, a missing file) are reported to the log.
### Arguments

- *const char ** **path** - Path to the plugin dynamic library.
