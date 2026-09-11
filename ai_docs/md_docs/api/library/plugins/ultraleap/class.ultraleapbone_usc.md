# Unigine::Plugins::UltraleapBone Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class represents a [bone](../../../../code/plugins/ultraleap/index_usc.md#bones) of a [finger](../../../../api/library/plugins/ultraleap/class.ultraleapfinger_usc.md).


> **Notice:** [Ultraleap](../../../../code/plugins/ultraleap/index_usc.md) plugin must be loaded.


## UltraleapBone Class

### Members

## UltraleapFinger getFinger () const

Returns the current object for the finger.
### Return value

Current object for the finger
## int getType () const

Returns the current type of the bone. One of the [TYPE_*](#TYPE_METACARPAL) values.
### Return value

Current type of the bone
## double getLength () const

Returns the current length of the bone, in meters.
### Return value

Current length of the bone, in meters
## double getWidth () const

Returns the current width of the bone, in meters.
### Return value

Current width of the bone, in meters
## Vec3 getJointBeginPosition () const

Returns the current coordinates of the end of the bone closest to the wrist (proximal).
### Return value

Current coordinates of the end of the bone closest to the wrist (proximal)
## Vec3 getJointEndPosition () const

Returns the current coordinates of the end of the bone closest to the finger tip (distal).
### Return value

Current coordinates of the end of the bone closest to the finger tip (distal)
## Vec3 getCenter () const

Returns the current coordinates of the center of the bone.
### Return value

Current coordinates of the center of the bone
## vec3 getDirection () const

Returns the current normalized direction of the bone from wrist to tip.
### Return value

Current normalized direction of the bone from wrist to tip
