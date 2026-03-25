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

---

## UltraleapFinger::TYPE getType ( ) const

Returns the type of the finger.
### Return value

The finger type. One of the [UltraleapFinger::TYPE_*](#TYPE_THUMB) values.
## bool isExtended ( ) const

Returns a value indicating if the finger is extended.
### Return value

true if the finger is extended; otherwise, false.
## double getLength ( ) const

Returns the length of the finger, in meters.
### Return value

The length of the finger, in meters.
## UltraleapHand * getHand ( ) const

Returns the object for the hand.
### Return value

The object for the hand.
## UltraleapBone * getBoneMetacarpal ( ) const

Returns the object for the metacarpal bone.
### Return value

The object for the metacarpal bone.
## UltraleapBone * getBoneProximal ( ) const

Returns the object for the proximal phalange bone.
### Return value

The object for the proximal phalange bone.
## UltraleapBone * getBoneIntermediate ( ) const

Returns the object for the intermediate phalange bone.
### Return value

The object for the intermediate phalange bone.
## UltraleapBone * getBoneDistal ( ) const

Returns the object for the distal phalange bone.
### Return value

The object for the distal phalange bone.
