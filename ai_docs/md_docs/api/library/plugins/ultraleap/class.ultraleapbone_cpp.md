# Unigine::Plugins::UltraleapBone Class (CPP)

**Header:** #include <plugins/Unigine/Ultraleap/UnigineUltraleap.h>


This class represents a [bone](../../../../code/plugins/ultraleap/index_cpp.md#bones) of a [finger](../../../../api/library/plugins/ultraleap/class.ultraleapfinger_cpp.md).


> **Notice:** [Ultraleap](../../../../code/plugins/ultraleap/index_cpp.md) plugin must be loaded.


## UltraleapBone Class

### Enums

## TYPE

| Name | Description |
|---|---|
| **TYPE_METACARPAL** = 0 | Metacarpal [bone](../../../../code/plugins/ultraleap/index_cpp.md#bones). |
| **TYPE_PROXIMAL** = 1 | Proximal phalange [bone](../../../../code/plugins/ultraleap/index_cpp.md#bones). |
| **TYPE_INTERMEDIATE** = 2 | Intermediate phalange [bone](../../../../code/plugins/ultraleap/index_cpp.md#bones). |
| **TYPE_DISTAL** = 3 | Distal phalange [bone](../../../../code/plugins/ultraleap/index_cpp.md#bones). A bone at the tip of the finger. |
| **NUM_TYPES** = 4 | Total number of bone types. |

### Members

---

## UltraleapFinger * getFinger ( ) const

Returns the object for the finger.
### Return value

The object for the finger.
## UltraleapBone::TYPE getType ( ) const

Returns the type of the bone.
### Return value

The bone type. One of the [Bone::TYPE_*](#TYPE_METACARPAL) values.
## double getLength ( ) const

Returns the length of the bone.
### Return value

The length of the bone, in meters.
## double getWidth ( ) const

Returns the width of the bone, in meters.
### Return value

The width of the bone, in meters.
## Math:: Vec3 getJointBeginPosition ( ) const

Returns the coordinates of the end of the bone closest to the wrist (proximal).
### Return value

The coordinates of the end of the bone closest to the wrist (proximal).
## Math:: Vec3 getJointEndPosition ( ) const

Returns the coordinates of the end of the bone closest to the finger tip (distal).
### Return value

The coordinates of the end of the bone closest to the finger tip (distal).
## Math:: Vec3 getCenter ( ) const

Returns the coordinates of the center of the bone.
### Return value

The coordinates of the center of the bone.
## Math:: vec3 getDirection ( ) const

Returns the normalized direction of the bone from wrist to tip.
### Return value

The normalized direction of the bone from wrist to tip.
