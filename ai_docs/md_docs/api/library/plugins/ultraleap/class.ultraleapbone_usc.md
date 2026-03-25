# Unigine::Plugins::UltraleapBone Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class represents a [bone](../../../../code/plugins/ultraleap/index_usc.md#bones) of a [finger](../../../../api/library/plugins/ultraleap/class.ultraleapfinger_usc.md).


> **Notice:** [Ultraleap](../../../../code/plugins/ultraleap/index_usc.md) plugin must be loaded.


## UltraleapBone Class

### Members

---

## UltraleapFinger getFinger ( )

Returns the object for the finger.
### Return value

The object for the finger.
## int getType ( )

Returns the type of the bone.
### Return value

The bone type. One of the [ULTRALEAP_BONE_TYPE_*](#TYPE_METACARPAL) values.
## double getLength ( )

Returns the length of the bone.
### Return value

The length of the bone, in meters.
## double getWidth ( )

Returns the width of the bone, in meters.
### Return value

The width of the bone, in meters.
## Vec3 getJointBeginPosition ( )

Returns the coordinates of the end of the bone closest to the wrist (proximal).
### Return value

The coordinates of the end of the bone closest to the wrist (proximal).
## Vec3 getJointEndPosition ( )

Returns the coordinates of the end of the bone closest to the finger tip (distal).
### Return value

The coordinates of the end of the bone closest to the finger tip (distal).
## Vec3 getCenter ( )

Returns the coordinates of the center of the bone.
### Return value

The coordinates of the center of the bone.
## vec3 getDirection ( )

Returns the normalized direction of the bone from wrist to tip.
### Return value

The normalized direction of the bone from wrist to tip.
