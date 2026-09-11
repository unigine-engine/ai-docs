# Unigine::Plugins::UltraleapFinger Class (CS)


This structure represents a [finger](../../../../code/plugins/ultraleap/index_cs.md#fingers) of a [hand](../../../../api/library/plugins/ultraleap/class.ultraleaphand_cs.md).


> **Notice:** [Ultraleap](../../../../code/plugins/ultraleap/index_cs.md) plugin must be loaded.


## UltraleapFinger Class

### Enums

## TYPE

| Name | Description |
|---|---|
| **THUMB** = 0 | Thumb. |
| **INDEX** = 1 | Index finger. |
| **MIDDLE** = 2 | Middle finger. |
| **RING** = 3 | Ring finger. |
| **PINKY** = 4 | Pinky finger. |
| **NUM_TYPES** = 5 | Total number of finger types. |

### Properties

## 🔒︎ UltraleapFinger.TYPE Type

The type of the finger. One of the [TYPE_*](#TYPE_THUMB) values.
## 🔒︎ bool IsExtended

The value indicating if the finger is extended.
## 🔒︎ double Length

The length of the finger, in meters.
## 🔒︎ UltraleapHand Hand

The object for the hand.
## 🔒︎ UltraleapBone BoneMetacarpal

The object for the metacarpal bone.
## 🔒︎ UltraleapBone BoneProximal

The object for the proximal phalange bone.
## 🔒︎ UltraleapBone BoneIntermediate

The object for the intermediate phalange bone.
## 🔒︎ UltraleapBone BoneDistal

The object for the distal phalange bone.
