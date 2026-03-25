# Unigine::InputVRBaseStation Class (CPP)

**Header:** #include <UnigineInput.h>

**Inherits from:** InputVRDevice


The class handles VR base station input.


> **Notice:** UNIGINE supports base stations that are compatible with OpenVR and Varjo devices only.


## InputVRBaseStation Class

### Enums

## MODEL_TYPE

| Name | Description |
|---|---|
| **MODEL_TYPE_UNKNOWN** = 0 | Unknown base station |
| **MODEL_TYPE_HTC_VIVE** = 1 | HTC Vive |
| **MODEL_TYPE_VALVE** = 2 | Valve Index |
| **NUM_MODEL_TYPES** = 3 | Total number of VR base station models. |

### Members

---

## InputVRBaseStation::MODEL_TYPE getModelType ( ) const

Returns the model type of the VR base station.
### Return value

Base station model type.
