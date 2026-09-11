# VRMeshSkinnedHandMapper Component


VRMeshSkinnedHandMapper maps [*OpenXR* hand joint data](../../../../../vr_development/vr_hand_tracking.md#hand_hierarchy) to skinned hand meshes. Used together with **[VRHandTrackingControllerOpenXR](../../../../../api/modules/vr/components/players/class.vrhandtrackingcontrolleropenxr.md)** to animate hand models based on hand tracking input.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| hand_left | *Hand* (struct) | Left hand mapping configuration. |
| hand_right | *Hand* (struct) | Right hand mapping configuration. |


Each *Hand* struct contains:


| Name | Type | Description |
|---|---|---|
| object | *Node* | Reference to the skinned mesh node representing the hand. |
| use_openxr_names | *Toggle* | When enabled, bone names are resolved automatically using the OpenXR naming convention. When disabled, bone names are set manually via the *bone_names* struct. |
| bone_names | *HandBones* (struct) | Manual bone name mapping for each finger joint (tip, distal, intermediate, proximal, metacarpal) and the wrist. Only used when *use_openxr_names* is disabled. |
