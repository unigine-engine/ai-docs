# Unigine.VRHand Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


## VRHand Class

### Members

## int getType () const

Returns the current type of the hand: left or right.
### Return value

Current type of the hand: left or right.
## VRBone getRootBone () const

Returns the current root bone of the hand � the corresponding [wrist](../../../api/library/vr/class.vrbone_usc.md#TYPE_WRIST) bone.
### Return value

Current root bone of the hand � the corresponding [wrist](../../../api/library/vr/class.vrbone_usc.md#TYPE_WRIST) bone.
## int isHoldingController () const

Returns the current value indicating if the controller is held in the hand. Not supported by Varjo.
### Return value

Current the controller is held in the hand
## int isTracking () const

Returns the current value indicating if the controller is active.
### Return value

Current the controller is active
---

## VRBone getBone ( int type )

Returns the bone of the specified type for the current hand.
### Arguments

- *int* **type** - Hand bone type, one of the [VR_BONE_TYPE_*](../../../api/library/vr/class.vrbone_usc.md#TYPE_PALM) values.

### Return value

Bone of the specified type.
## void renderVisualizer ( )

Renders the visualizer.
