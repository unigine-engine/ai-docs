# Unigine.ObjectCloudLayer Class (CPP)

**Header:** #include <UnigineObjects.h>

**Inherits from:** Object


This class is used to create cloud layers.


## ObjectCloudLayer Class

### Members

## void setAnimationNoiseOffset ( const Math:: vec4 & offset )

Sets a new noise animation offset value (a [vec4](../../../api/library/math/class.vec4_cpp.md) value, where **X**, **Y**, and **Z** components represent 3D noise texture offsets along the X-axis, Y-axis, and Z-axis respectively).
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **offset** - The noise animation offset value

## Math:: vec4 getAnimationNoiseOffset () const

Returns the current noise animation offset value (a [vec4](../../../api/library/math/class.vec4_cpp.md) value, where **X**, **Y**, and **Z** components represent 3D noise texture offsets along the X-axis, Y-axis, and Z-axis respectively).
### Return value

Current noise animation offset value
## void setAnimationCoverageOffset ( const Math:: vec4 & offset )

Sets a new coverage animation offset value (a [vec4](../../../api/library/math/class.vec4_cpp.md) value, where **X** and **Y** components represent coverage texture offsets along the X-axis and Y-axis respectively, both **Z** and **W** components are 0).
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **offset** - The coverage animation offset value

## Math:: vec4 getAnimationCoverageOffset () const

Returns the current coverage animation offset value (a [vec4](../../../api/library/math/class.vec4_cpp.md) value, where **X** and **Y** components represent coverage texture offsets along the X-axis and Y-axis respectively, both **Z** and **W** components are 0).
### Return value

Current coverage animation offset value
## void setIntersectionAccuracy ( float accuracy )

Sets a new intersection accuracy value.
### Arguments

- *float* **accuracy** - The intersection accuracy value

## float getIntersectionAccuracy () const

Returns the current intersection accuracy value.
### Return value

Current intersection accuracy value
## void setIntersectionThreshold ( float threshold )

Sets a new intersection threshold value.
### Arguments

- *float* **threshold** - The intersection threshold value

## float getIntersectionThreshold () const

Returns the current intersection threshold value.
### Return value

Current intersection threshold value
## void setCloudspaceTransform ( const Math:: Mat4 & transform )

Sets a new transformation matrix mapping world space into the cloud layer's own coordinate frame, in which the volumetric clouds are positioned, rendered, and intersected. Setting a non-identity matrix reorients or offsets the whole cloud layer space (for example, to anchor the clouds for a round-planet setup).
### Arguments

- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md)&* **transform** - The transformation of the cloud layer space

## Math:: Mat4 getCloudspaceTransform () const

Returns the current transformation matrix mapping world space into the cloud layer's own coordinate frame, in which the volumetric clouds are positioned, rendered, and intersected. Setting a non-identity matrix reorients or offsets the whole cloud layer space (for example, to anchor the clouds for a round-planet setup).
### Return value

Current transformation of the cloud layer space
---

## static ObjectCloudLayerPtr create ( )

Constructor. Creates a new empty cloud layer object with default properties.
## static int type ( )

Returns the type of the object.
### Return value

Object Cloud Layer type identifier.
## void refreshCloudsRegionMask ( )

Refreshes the clouds region mask. The method should be called after changing the mask to apply it.
## float getDensity ( const Math::Vec3& world_point ) const

Returns the current density of clouds at the given point.
### Arguments

- *const  Math::Vec3&* **world_point** - Point coordinates in world space.

### Return value

Clouds density.
