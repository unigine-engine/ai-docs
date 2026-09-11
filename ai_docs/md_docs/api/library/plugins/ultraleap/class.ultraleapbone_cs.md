# Unigine::Plugins::UltraleapBone Class (CS)


This class represents a [bone](../../../../code/plugins/ultraleap/index_cs.md#bones) of a [finger](../../../../api/library/plugins/ultraleap/class.ultraleapfinger_cs.md).


> **Notice:** [Ultraleap](../../../../code/plugins/ultraleap/index_cs.md) plugin must be loaded.


## UltraleapBone Class

### Enums

## TYPE

| Name | Description |
|---|---|
| **METACARPAL** = 0 | Metacarpal [bone](../../../../code/plugins/ultraleap/index_cs.md#bones). |
| **PROXIMAL** = 1 | Proximal phalange [bone](../../../../code/plugins/ultraleap/index_cs.md#bones). |
| **INTERMEDIATE** = 2 | Intermediate phalange [bone](../../../../code/plugins/ultraleap/index_cs.md#bones). |
| **DISTAL** = 3 | Distal phalange [bone](../../../../code/plugins/ultraleap/index_cs.md#bones). A bone at the tip of the finger. |
| **NUM_TYPES** = 4 | Total number of bone types. |

### Properties

## 🔒︎ UltraleapFinger Finger

The object for the finger.
## 🔒︎ UltraleapBone.TYPE Type

The type of the bone. One of the [TYPE_*](#TYPE_METACARPAL) values.
## 🔒︎ double Length

The length of the bone, in meters.
## 🔒︎ double Width

The width of the bone, in meters.
## 🔒︎ vec3 JointBeginPosition

The coordinates of the end of the bone closest to the wrist (proximal).
## 🔒︎ vec3 JointEndPosition

The coordinates of the end of the bone closest to the finger tip (distal).
## 🔒︎ vec3 Center

The coordinates of the center of the bone.
## 🔒︎ vec3 Direction

The normalized direction of the bone from wrist to tip.
