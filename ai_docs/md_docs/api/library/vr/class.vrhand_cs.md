# Unigine.VRHand Class (CS)


## VRHand Class

### Enums

## TYPE

| Name | Description |
|---|---|
| **LEFT** = 0 | Left hand. |
| **RIGHT** = 1 | Right hand. |
| **NUM_TYPES** = 2 | Total number of hand types. |

### Properties

## 🔒︎ VRHand.TYPE Type

The type of the hand: left or right.
## 🔒︎ VRBone RootBone

The root bone of the hand � the corresponding [wrist](../../../api/library/vr/class.vrbone_cs.md#TYPE_WRIST) bone.
## 🔒︎ bool IsHoldingController

The value indicating if the controller is held in the hand. Not supported by Varjo.
## 🔒︎ bool IsTracking

The value indicating if the controller is active.
### Members

---

## VRBone GetBone ( VRBone.TYPE type )

Returns the bone of the specified type for the current hand.
### Arguments

- *[VRBone.TYPE](../../../api/library/vr/class.vrbone_cs.md#TYPE)* **type** - Hand bone type, one of the [VRBone.TYPE](../../../api/library/vr/class.vrbone_cs.md#TYPE) values.

### Return value

Bone of the specified type.
## void RenderVisualizer ( )

Renders the visualizer.
