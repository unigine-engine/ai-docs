# Unigine.VRHand Class (CPP)

**Header:** #include <UnigineVRHandTracking.h>


## VRHand Class

### Enums

## TYPE

| Name | Description |
|---|---|
| **TYPE_LEFT** = 0 | Left hand. |
| **TYPE_RIGHT** = 1 | Right hand. |
| **NUM_TYPES** = 2 | Total number of hand types. |

### Members

## VRHand::TYPE getType () const

Returns the current type of the hand: left or right.
### Return value

Current type of the hand: left or right.
## Ptr < VRBone > getRootBone () const

Returns the current root bone of the hand � the corresponding [wrist](../../../api/library/vr/class.vrbone_cpp.md#TYPE_WRIST) bone.
### Return value

Current root bone of the hand � the corresponding [wrist](../../../api/library/vr/class.vrbone_cpp.md#TYPE_WRIST) bone.
## bool isHoldingController () const

Returns the current value indicating if the controller is held in the hand. Not supported by Varjo.
### Return value

**true** if the controller is held in the hand; otherwise **false**.
## bool isTracking () const

Returns the current value indicating if the controller is active.
### Return value

**true** if the controller is active; otherwise **false**.
---

## Ptr < VRBone > getBone ( VRBone::TYPE type )

Returns the bone of the specified type for the current hand.
### Arguments

- *[VRBone::TYPE](../../../api/library/vr/class.vrbone_cpp.md#TYPE)* **type** - Hand bone type, one of the [VRBone::TYPE](../../../api/library/vr/class.vrbone_cpp.md#TYPE_PALM) values.

### Return value

Bone of the specified type.
## void renderVisualizer ( ) const

Renders the visualizer.
