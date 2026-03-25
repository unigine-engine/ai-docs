# Unigine::InputVRTracker Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** InputVRDevice


The class handles VR tracker input.


> **Notice:** The VR tracker needs to have a [world transformation](../../../api/library/controls/class.inputvrdevice_usc.md#getWorldTransform_int_Mat4). So that you can, for example, pin the tracker to a camera or player for tracking its position in the virtual world.


> **Notice:** UNIGINE supports base stations that are compatible with OpenVR and Varjo devices only.


## InputVRTracker Class

### Members

---

## int getModelType ( )

Returns the model type of the VR tracker.
### Return value

Tracker model type.
