# Unigine::Plugins::UltraleapFinger Class (CPP)

**Header:** #include <plugins/Unigine/Ultraleap/UnigineUltraleap.h>


This structure represents a [finger](../../../../code/plugins/ultraleap/index_cpp.md#fingers) of a [hand](../../../../api/library/plugins/ultraleap/class.ultraleaphand_cpp.md).


> **Notice:** [Ultraleap](../../../../code/plugins/ultraleap/index_cpp.md) plugin must be loaded.


## UltraleapFinger Class

### Enums

## TYPE

| Name | Description |
|---|---|
| **TYPE_THUMB** = 0 | Thumb. |
| **TYPE_INDEX** = 1 | Index finger. |
| **TYPE_MIDDLE** = 2 | Middle finger. |
| **TYPE_RING** = 3 | Ring finger. |
| **TYPE_PINKY** = 4 | Pinky finger. |
| **NUM_TYPES** = 5 | Total number of finger types. |

### Members

## UltraleapFinger::TYPE getType () const

Returns the current type of the finger. One of the [TYPE_*](#TYPE_THUMB) values.
### Return value

Current type of the finger
## bool isExtended () const

Returns the current value indicating if the finger is extended.
### Return value

**true** if the finger is extended; otherwise **false**.
## double getLength () const

Returns the current length of the finger, in meters.
### Return value

Current length of the finger, in meters
## UltraleapHand * getHand () const

Returns the current object for the hand.
### Return value

Current object for the hand
## UltraleapBone * getBoneMetacarpal () const

Returns the current object for the metacarpal bone.
### Return value

Current object for the metacarpal bone
## UltraleapBone * getBoneProximal () const

Returns the current object for the proximal phalange bone.
### Return value

Current object for the proximal phalange bone
## UltraleapBone * getBoneIntermediate () const

Returns the current object for the intermediate phalange bone.
### Return value

Current object for the intermediate phalange bone
## UltraleapBone * getBoneDistal () const

Returns the current object for the distal phalange bone.
### Return value

Current object for the distal phalange bone
