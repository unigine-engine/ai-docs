# Unigine::Plugins::UltraleapArm Class (CPP)

**Header:** #include <plugins/Unigine/Ultraleap/UnigineUltraleap.h>


This structure represents a [forearm](../../../../code/plugins/ultraleap/index_cpp.md#arms).


> **Notice:** [Ultraleap](../../../../code/plugins/ultraleap/index_cpp.md) plugin must be loaded.


## UltraleapArm Class

### Members

## double getWidth () const

Returns the current width of the forearm, in meters.
### Return value

Current width of the forearm, in meters
## Math:: vec3 getDirection () const

Returns the current normalized direction in which the arm is pointing (from elbow to wrist).
### Return value

Current normalized direction in which the arm is pointing (from elbow to wrist)
## Math:: Vec3 getPositionElbow () const

Returns the current coordinates of the elbow position.
### Return value

Current coordinates of the elbow position
## Math:: Vec3 getPositionWrist () const

Returns the current coordinates of the wrist position.
### Return value

Current coordinates of the wrist position
## Math:: Vec3 getCenter () const

Returns the current coordinates of the center of the forearm.
### Return value

Current coordinates of the center of the forearm
## UltraleapHand * getHand () const

Returns the current object for the hand.
### Return value

Current object for the hand
