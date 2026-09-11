# Unigine::Plugins::UltraleapArm Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This structure represents a [forearm](../../../../code/plugins/ultraleap/index_usc.md#arms).


> **Notice:** [Ultraleap](../../../../code/plugins/ultraleap/index_usc.md) plugin must be loaded.


## UltraleapArm Class

### Members

## double getWidth () const

Returns the current width of the forearm, in meters.
### Return value

Current width of the forearm, in meters
## vec3 getDirection () const

Returns the current normalized direction in which the arm is pointing (from elbow to wrist).
### Return value

Current normalized direction in which the arm is pointing (from elbow to wrist)
## Vec3 getPositionElbow () const

Returns the current coordinates of the elbow position.
### Return value

Current coordinates of the elbow position
## Vec3 getPositionWrist () const

Returns the current coordinates of the wrist position.
### Return value

Current coordinates of the wrist position
## Vec3 getCenter () const

Returns the current coordinates of the center of the forearm.
### Return value

Current coordinates of the center of the forearm
## UltraleapHand getHand () const

Returns the current object for the hand.
### Return value

Current object for the hand
