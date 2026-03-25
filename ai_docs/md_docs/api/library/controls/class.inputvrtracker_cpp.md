# Unigine::InputVRTracker Class (CPP)

**Header:** #include <UnigineInput.h>

**Inherits from:** InputVRDevice


The class handles VR tracker input.


> **Notice:** The VR tracker needs to have a [world transformation](../../../api/library/controls/class.inputvrdevice_cpp.md#getWorldTransform_int_Mat4). So that you can, for example, pin the tracker to a camera or player for tracking its position in the virtual world.


> **Notice:** UNIGINE supports base stations that are compatible with OpenVR and Varjo devices only.


## InputVRTracker Class

### Enums

## MODEL_TYPE

| Name | Description |
|---|---|
| **MODEL_TYPE_UNKNOWN** = 0 | Unknown VR tracker. |
| **MODEL_TYPE_HTC_VIVE** = 1 | HTC Vive |
| **NUM_MODEL_TYPES** = 2 | Total number of VR tracker models. |

### Members

---

## InputVRTracker::MODEL_TYPE getModelType ( ) const

Returns the model type of the VR tracker.
### Return value

Tracker model type.
