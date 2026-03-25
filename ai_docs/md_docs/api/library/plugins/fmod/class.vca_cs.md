# Unigine::Plugins::FMOD::VCA Class (CS)


> **Notice:** This set of functions is available when the [FMOD](../../../../code/plugins/fmod/index.md) plugin is loaded.


Represents a global mixer VCA.


## VCA Class

### Properties

## float Volume

The volume level. Negative level inverts the signal. Range: [-inf, -inf]. Default: 1.
## 🔒︎ bool IsValid

The value indicating if VCA reference is valid.
### Members

---

## void Release ( )

Releases the VCA object.
## void ReleaseFromStudio ( )

Auxiliary function, not to be used.
## string GetPath ( )

Returns the VCA object's path.
### Return value

Object's path.
