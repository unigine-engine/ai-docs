# Unigine::Plugins::FMOD::FMOD Class (CS)

> **Notice:** This class is a singleton.


> **Notice:** This set of functions is available when the [FMOD](../../../../code/plugins/fmod/index.md) plugin is loaded.


This class is intened to work with FMODCore and FMODStudio objects.


## FMOD Class

### Properties

## 🔒︎ FMODCore Core

The FMOD Core System object. The Core System object can be retrieved before initializing the Studio System object to call additional core configuration functions.
## 🔒︎ FMODStudio Studio

The FMOD Studio System object.
### Members

---

## void Update ( )

Calls update of FMOD Studio and Core.
## bool HasErrors ( out int error_type )

Checks for errors and returns error code. To interpret the error, see [ERROR_TYPE](../../../../api/library/plugins/fmod/class.fmodenums_cs.md#ERROR_TYPE) enum.
### Arguments

- *out int* **error_type** - Variable to store error code.

### Return value

true if an eror has orrurred, otherwise, false.
## void LoadOutputPlugin ( string path )

Loads an *FMOD* output plugin library from the given file and makes it the active audio output of the *FMOD* system. Failures (for example, a missing file) are reported to the log.
### Arguments

- *string* **path** - Path to the plugin dynamic library.
