# Unigine::Plugins::UltraleapArm Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This structure represents a [forearm](../../../../code/plugins/ultraleap/index_usc.md#arms).


> **Notice:** [Ultraleap](../../../../code/plugins/ultraleap/index_usc.md) plugin must be loaded.


## UltraleapArm Class

### Members

---

## double getWidth ( )

Returns the width of the forearm, in meters.
### Return value

The width of the forearm, in meters.
## vec3 getDirection ( )

Returns the normalized direction in which the arm is pointing (from elbow to wrist).
### Return value

The normalized direction in which the arm is pointing (from elbow to wrist).
## Vec3 getPositionElbow ( )

Returns the coordinates of the elbow position.
### Return value

The coordinates of the elbow position.
## Vec3 getPositionWrist ( )

Returns the coordinates of the end of the bone, closest to the finger tip (distal).
### Return value

The coordinates of the wrist position.
## Vec3 getCenter ( )

Returns the coordinates of the center of the forearm.
### Return value

The coordinates of the center of the forearm.
## UltraleapHand getHand ( )

Returns the object for the hand.
### Return value

The object for the hand.
