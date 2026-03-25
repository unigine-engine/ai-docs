# Unigine::Plugins::UltraleapArm Class (CPP)

**Header:** #include <plugins/Unigine/Ultraleap/UnigineUltraleap.h>


This structure represents a [forearm](../../../../code/plugins/ultraleap/index_cpp.md#arms).


> **Notice:** [Ultraleap](../../../../code/plugins/ultraleap/index_cpp.md) plugin must be loaded.


## UltraleapArm Class

### Members

---

## double getWidth ( ) const

Returns the width of the forearm, in meters.
### Return value

The width of the forearm, in meters.
## Math:: vec3 getDirection ( ) const

Returns the normalized direction in which the arm is pointing (from elbow to wrist).
### Return value

The normalized direction in which the arm is pointing (from elbow to wrist).
## Math:: Vec3 getPositionElbow ( ) const

Returns the coordinates of the elbow position.
### Return value

The coordinates of the elbow position.
## Math:: Vec3 getPositionWrist ( ) const

Returns the coordinates of the end of the bone, closest to the finger tip (distal).
### Return value

The coordinates of the wrist position.
## Math:: Vec3 getCenter ( ) const

Returns the coordinates of the center of the forearm.
### Return value

The coordinates of the center of the forearm.
## UltraleapHand * getHand ( ) const

Returns the object for the hand.
### Return value

The object for the hand.
