# Unigine::Plugins::FMOD::VCA Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


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
## int isValid () const

Returns the current value indicating if VCA reference is valid.
### Return value

Current VCA reference is valid
---

## void release ( )

Releases the VCA object.
## void releaseFromStudio ( )

Auxiliary function, not to be used.
## String getPath ( )

Returns the VCA object's path.
### Return value

Object's path.
