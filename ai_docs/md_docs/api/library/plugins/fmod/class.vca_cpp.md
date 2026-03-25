# Unigine::Plugins::FMOD::VCA Class (CPP)

**Header:** #include <plugins/Unigine/FMOD/UnigineFMOD.h>


> **Notice:** This set of functions is available when the [FMOD](../../../../code/plugins/fmod/index.md) plugin is loaded.


Represents a global mixer VCA.


## VCA Class

### Members

## void setVolume ( float volume )

Sets a new volume level. Negative level inverts the signal. Range: [-inf, -inf]. Default: 1.
### Arguments

- *float* **volume** - The volume level. Negative level inverts the signal. Range: [-inf, -inf]. Default: 1.

## float getVolume () const

Returns the current volume level. Negative level inverts the signal. Range: [-inf, -inf]. Default: 1.
### Return value

Current volume level. Negative level inverts the signal. Range: [-inf, -inf]. Default: 1.
## bool isValid () const

Returns the current value indicating if VCA reference is valid.
### Return value

**true** if VCA reference is valid; otherwise **false**.
---

## void release ( )

Releases the VCA object.
## void releaseFromStudio ( )

Auxiliary function, not to be used.
## String getPath ( ) const

Returns the VCA object's path.
### Return value

Object's path.
