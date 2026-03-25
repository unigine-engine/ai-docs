# Unigine.ObjectCloudLayer Class (CPP)

**Header:** #include <UnigineObjects.h>

**Inherits from:** Object


This class is used to create cloud layers.


## ObjectCloudLayer Class

### Members

---

## static ObjectCloudLayerPtr create ( )

Constructor. Creates a new empty cloud layer object with default properties.
## static int type ( )

Returns the type of the object.
### Return value

Object Cloud Layer type identifier.
## float getIntersectionThreshold ( ) const

Returns current intersection threshold value.
### Return value

Intersection threshold value.
## void setAnimationNoiseOffset ( const Math:: vec4 & offset )

Sets a given noise animation offset value.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **offset** - Noise animation offset (a [vec4](../../../api/library/math/class.vec4_cpp.md) value, where **X**, **Y**, and **Z** components represent 3D noise texture offsets along the X-axis, Y-axis, and Z-axis respectively).

## void setAnimationCoverageOffset ( const Math:: vec4 & offset )

Sets a given coverage animation offset value.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **offset** - Coverage animation offset (a [vec4](../../../api/library/math/class.vec4_cpp.md) value, where **X** and **Y** components represent coverage texture offsets along the X-axis and Y-axis respectively).

## Math:: vec4 getAnimationNoiseOffset ( ) const

Returns current noise animation offset value.
### Return value

Noise animation offset (a [vec4](../../../api/library/math/class.vec4_cpp.md) value, where **X**, **Y**, and **Z** components represent 3D noise texture offsets along the X-axis, Y-axis, and Z-axis respectively).
## float getIntersectionAccuracy ( ) const

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

## Math:: vec4 getAnimationCoverageOffset ( ) const

Returns current coverage animation offset value.
### Return value

Coverage animation offset (a [vec4](../../../api/library/math/class.vec4_cpp.md) value, where **X** and **Y** components represent coverage texture offsets along the X-axis and Y-axis respectively, both **Z** and **W** components are 0).
## void refreshCloudsRegionMask ( )

Refreshes the clouds region mask. The method should be called after changing the mask to apply it.
## float getDensity ( const Math::Vec3& world_point ) const

Returns the current density of clouds at the given point.
### Arguments

- *const  Math::Vec3&* **world_point** - Point coordinates in world space.

### Return value

Clouds density.
