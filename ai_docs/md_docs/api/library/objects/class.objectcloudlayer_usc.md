# Unigine.ObjectCloudLayer Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Object


This class is used to create cloud layers.


## ObjectCloudLayer Class

### Members

---

## static ObjectCloudLayer ( )

Constructor. Creates a new empty cloud layer object with default properties.
## static int type ( )

Returns the type of the object.
### Return value

Object Cloud Layer type identifier.
## float getIntersectionThreshold ( )

Returns current intersection threshold value.
### Return value

Intersection threshold value.
## void setAnimationNoiseOffset ( vec4 offset )

Sets a given noise animation offset value.
### Arguments

- *vec4* **offset** - Noise animation offset (a [vec4](../../../api/library/math/class.vec4_usc.md) value, where **X**, **Y**, and **Z** components represent 3D noise texture offsets along the X-axis, Y-axis, and Z-axis respectively).

## void setAnimationCoverageOffset ( vec4 offset )

Sets a given coverage animation offset value.
### Arguments

- *vec4* **offset** - Coverage animation offset (a [vec4](../../../api/library/math/class.vec4_usc.md) value, where **X** and **Y** components represent coverage texture offsets along the X-axis and Y-axis respectively).

## vec4 getAnimationNoiseOffset ( )

Returns current noise animation offset value.
### Return value

Noise animation offset (a [vec4](../../../api/library/math/class.vec4_usc.md) value, where **X**, **Y**, and **Z** components represent 3D noise texture offsets along the X-axis, Y-axis, and Z-axis respectively).
## float getIntersectionAccuracy ( )

Returns current intersection accuracy value.
### Return value

Intersection accuracy value.
## void setIntersectionAccuracy ( float accuracy )

Sets a given intersection accuracy value.
### Arguments

- *float* **accuracy** - Intersection accuracy value.

## void setIntersectionThreshold ( float threshold )

Sets a given intersection threshold value.
### Arguments

- *float* **threshold** - Intersection threshold value.

## vec4 getAnimationCoverageOffset ( )

Returns current coverage animation offset value.
### Return value

Coverage animation offset (a [vec4](../../../api/library/math/class.vec4_usc.md) value, where **X** and **Y** components represent coverage texture offsets along the X-axis and Y-axis respectively, both **Z** and **W** components are 0).
## void refreshCloudsRegionMask ( )

Refreshes the clouds region mask. The method should be called after changing the mask to apply it.
## float getDensity ( Vec3 world_point )

Returns the current density of clouds at the given point.
### Arguments

- *Vec3* **world_point** - Point coordinates in world space.

### Return value

Clouds density.
