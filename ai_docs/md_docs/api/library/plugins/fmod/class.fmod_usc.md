# Unigine::Plugins::FMOD::FMOD Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


> **Notice:** This set of functions is available when the [FMOD](../../../../code/plugins/fmod/index.md) plugin is loaded.


This class is intened to work with FMODCore and FMODStudio objects.


## FMOD Class

### Members

## FMODCore getCore () const

Returns the current FMOD Core System object. The Core System object can be retrieved before initializing the Studio System object to call additional core configuration functions.
### Return value

Current FMOD Core System object.
## FMODStudio getStudio () const

Returns the current FMOD Studio System object.
### Return value

Current FMOD Studio System object.
---

## void update ( )

Calls update of FMOD Studio and Core.
## bool hasErrors ( int & error_type )

Checks for errors and returns error code. To interpret the error, see [ERROR_TYPE](../../../../api/library/plugins/fmod/class.fmodenums_usc.md#ERROR_TYPE) enum.
### Arguments

- *int &* **error_type** - Variable to store error code.

### Return value

true if an eror has orrurred, otherwise, false.
## void loadOutputPlugin ( string path )

Loads an *FMOD* output plugin library from the given file and makes it the active audio output of the *FMOD* system. Failures (for example, a missing file) are reported to the log.
### Arguments

- *string* **path** - Path to the plugin dynamic library.
